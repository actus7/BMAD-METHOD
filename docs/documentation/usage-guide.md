# Guia de Uso – Agentes de Documentação BMAD

Este guia explica como o time pode executar e aproveitar os agentes especializados de documentação para projetos com código legado (_brownfield_) e código novo (_greenfield_).

## Pré-requisitos

1. Node.js 20 ou superior instalado.
2. Dependências do BMAD instaladas no repositório: `npm install`.
3. Configuração base atualizada via CLI: `npx bmad-method install` (executar uma vez por máquina).

## Executando os Agentes

Cada agente pode ser acionado pela CLI com o comando geral:

```bash
npx bmad-method run-agent <agent-id>
```

### 1. Brownfield Documentation Sentinel

- **ID:** `doc-brownfield`
- **Objetivo:** gerar diagnósticos do legado, identificar débitos técnicos e orientar refatorações.
- **Execução:**
  ```bash
  npx bmad-method run-agent doc-brownfield
  ```
- **Entradas sugeridas:** caminho do módulo legado, objetivos da manutenção, restrições de risco, horizonte de tempo.

### 2. Greenfield Documentation Steward

- **ID:** `doc-greenfield`
- **Objetivo:** orientar a criação de documentação preventiva para novos módulos, antes ou durante a implementação.
- **Execução:**
  ```bash
  npx bmad-method run-agent doc-greenfield
  ```
- **Entradas sugeridas:** visão da feature, requisitos funcionais e não funcionais, decisões arquiteturais candidatas, critérios de aceite.

## Fluxo de Trabalho Recomendado

1. **Definir objetivo do ciclo** (correção, refatoração, feature nova).
2. **Selecionar o agente** apropriado e executar via CLI.
3. **Responder às perguntas iniciais** – os agentes guiam a coleta de contexto.
4. **Gerar documento base** seguindo o [padrão corporativo](./documentation-standard.md).
5. **Validar com a equipe** – revisar riscos, plano de ação e evidências.
6. **Publicar no repositório** dentro de `docs/documentation/` com histórico de revisões.
7. **Atualizar após a implementação** – registrar resultados, métricas e débitos remanescentes.

## Integração com Processos da Equipe

- **Revisões Técnicas:** inclua o documento produzido na pauta da reunião de revisão ou _tech review_.
- **Quadro de Débitos:** extraia itens da seção “Débitos & Seguimentos” para o backlog técnico.
- **Auditorias:** utilize o Brownfield Sentinel antes de milestones críticos ou auditorias externas.
- **Onboarding:** forneça a documentação gerada pelo Greenfield Steward para novos integrantes.

## Troubleshooting

| Sintoma                             | Ação recomendada                                                                                     |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------- |
| CLI informa que o agente não existe | Rode `npx bmad-method status` para verificar instalação e reexecute `npx bmad-method install`.       |
| Arquivo de saída não é gerado       | Verifique permissões de escrita na pasta `docs/` e confirme se o agente concluiu todos os passos.    |
| Dúvidas sobre conteúdo padrão       | Consulte o [documentation-standard.md](./documentation-standard.md) e ajuste a seção correspondente. |

## Boas Práticas

- Versione todo artefato criado pelos agentes (commits pequenos e frequentes).
- Use _pull requests_ para revisão cruzada do conteúdo técnico.
- Atualize memórias personalizadas dos agentes quando surgirem padrões específicos do projeto.
- Anexe evidências (prints, logs, consultas SQL) diretamente no documento ou como anexos vinculados.

Com esses dois agentes o time mantém documentação viva, alinhada às necessidades de legado e de novas entregas.
