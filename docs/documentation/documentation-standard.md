# Padrão Corporativo de Documentação Técnica (BMAD)

Este guia estabelece um padrão único de documentação para equipes que utilizam o método BMAD em cenários _brownfield_ (código legado) e _greenfield_ (código novo). O objetivo é garantir rastreabilidade, consistência e clareza independentemente do estágio do sistema.

## Princípios Gerais

1. **Fonte única da verdade** – Toda decisão relevante deve estar documentada em Markdown sob `docs/`.
2. **Sincronização contínua** – Atualize documentos sempre que o código mudar. Evite acumular "atualizações futuras".
3. **Evidências objetivas** – Inclua trechos de código, resultados de testes e métricas que sustentem a narrativa.
4. **Riscos visíveis** – Registre débitos técnicos, impactos e planos de mitigação de forma explícita.
5. **Voz profissional** – Escreva de maneira direta, em português claro, com foco na equipe de engenharia.

## Estrutura de Documentos

Todo artefato segue os blocos abaixo. Use apenas as seções aplicáveis ao contexto.

```markdown
# Título do Artefato

## Contexto

Resumo do cenário, stakeholders e motivadores.

## Estado Atual

Fotografia do código/processo hoje. Referencie caminhos, módulos e serviços.

## Metas / Critérios de Sucesso

Resultado esperado, indicadores e restrições.

## Análise Técnica

- Componentes envolvidos
- Dependências e integrações
- Riscos e complexidades

## Plano ou Implementação

Passos propostos/executados, com responsáveis e datas quando aplicável.

## Evidências

Capturas de comando, hashes de commit, prints ou logs essenciais.

## Débitos & Seguimentos

Itens pendentes, riscos residuais, próximos passos.

## Histórico de Revisões

Tabela `Data | Autor | Mudança`.
```

### Convenções de Estilo

- Use listas numeradas para sequências e listas com marcadores para itens soltos.
- Sempre prefira tabelas para consolidar comparações ou deliberações.
- Trechos de código devem declarar linguagem (`ts`, `json`, etc.).
- Referencie arquivos com caminho absoluto a partir do repositório (ex.: `src/core/service.ts`).
- Evite termos vagos como "em breve" ou "resolver depois". Defina datas ou critérios claros.

## Diferenciação por Cenário

### Brownfield (código legado)

- Prioridade em **diagnóstico do estado atual**, riscos e dívidas técnicas.
- Documentos-chave: Auditoria de Legado, Plano de Refatoração, Matriz de Risco.
- Sempre registrar dependências externas, contratos herdados e limitações históricas.
- Destacar áreas críticas que exigem testes adicionais ou monitoramento.

### Greenfield (código novo)

- Foco em **decisões antecipadas**, justificativas arquiteturais e critérios de aceite.
- Documentos-chave: Blueprint de Implementação, Guia de Desenvolvedor, Catálogo de APIs.
- Registrar hipóteses de negócio e técnicas, bem como estratégia de observabilidade.
- Manter atualização incremental conforme funcionalidades são entregues.

## Pastas Recomendas

```
docs/
  documentation/
    documentation-standard.md   # este arquivo
    usage-guide.md              # fluxo operacional e comandos
    examples/
      brownfield-audit.md       # exemplo legado
      greenfield-blueprint.md   # exemplo novo
```

## Integração com os Agentes

1. **Brownfield Documentation Sentinel** – prioriza análise de risco, débitos e sincronização com código existente.
2. **Greenfield Documentation Steward** – estrutura documentação proativa, orienta decisões antes do código.

Os agentes utilizam este padrão como referência. Ajustes específicos podem ser registrados nas memórias personalizadas de cada agente.
