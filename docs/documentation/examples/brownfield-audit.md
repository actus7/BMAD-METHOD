# Auditoria Brownfield – Módulo de Faturamento

## Contexto

- **Sistema:** Plataforma de cobrança corporativa
- **Motivador:** Reincidência de erros 500 no endpoint `POST /billing/v1/invoices`
- **Stakeholders:** Squad Faturamento, SRE, Compliance

## Estado Atual

- Serviço principal localizado em `srv/billing/invoice-service.ts`
- Banco de dados legado Oracle; queries embutidas no código com `any`
- Falta de testes de regressão para cálculo de impostos estaduais
- Observabilidade inexistente: ausência de métricas Prometheus e logging estrutural

## Metas / Critérios de Sucesso

1. Estabilizar o endpoint com SLO de erro < 0,5%
2. Documentar débitos técnicos priorizados e responsáveis
3. Definir plano de refatoração incremental aprovado pela liderança técnica

## Análise Técnica

| Área                   | Risco | Complexidade | Observações                                 |
| ---------------------- | ----- | ------------ | ------------------------------------------- |
| ORM inexistente        | Alto  | Alta         | Queries duplicadas e sem tratamento de erro |
| Cálculo de impostos    | Médio | Média        | Regras dispersas em 5 funções diferentes    |
| Tratamento de exceções | Alto  | Baixa        | Exceções genéricas capturadas e engolidas   |
| Testes automatizados   | Alto  | Alta         | Cobertura < 15%, sem mocks para Oracle      |

## Plano de Refatoração

1. **Curto prazo (1 sprint)**
   - Criar middleware de logging estruturado (`pino`) – responsável: @sre-aline
   - Normalizar tratamento de erro com `InvoiceServiceError` – responsável: @dev-rodrigo
   - Adicionar teste Jest cobrindo fluxo feliz do endpoint – responsável: @qa-marcos
2. **Médio prazo (3 sprints)**
   - Extrair cálculos fiscais para `srv/billing/tax-engine.ts`
   - Introduzir camada de repositório com Knex + tipagem Zod
   - Configurar dashboards no Grafana para taxa de erro e tempo médio

## Evidências

- Execução de teste atual: `npm test -- invoice-service` → falha registrada em 2 cenários de estado `PR` (ver saída anexada ao relatório).
- Logs de produção mostram exceção `TypeError: Cannot read properties of undefined (reading 'taxCode')` capturada às 03:41 UTC (log rotation 2025-02-02).

## Débitos & Seguimentos

- Validar contratos com área fiscal antes de consolidar regras no `tax-engine`
- Criar testes de carga para volume > 5k requisições/hora
- Revisar políticas de rollback devido ao alto acoplamento com Oracle

## Histórico de Revisões

| Data       | Autor                             | Mudança                                        |
| ---------- | --------------------------------- | ---------------------------------------------- |
| 2025-02-03 | Brownfield Documentation Sentinel | Primeira versão a partir de análise automática |
| 2025-02-04 | Tech Lead Billing                 | Ajustes em priorização e responsáveis          |
