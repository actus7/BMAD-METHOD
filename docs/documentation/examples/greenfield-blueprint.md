# Blueprint Greenfield – Módulo de Assinaturas Digitais

## Contexto

- **Visão:** permitir que clientes assinem contratos online com validade jurídica.
- **Stakeholders:** Tribunais parceiros, equipe jurídica, squad Digital Onboarding.
- **Drivers:** Redução de ciclo de onboarding de 5 dias para 1 dia, aderência LGPD.

## Estado Atual

- Módulo ainda não existe; integrações planejadas:
  - BFF `bff/contracts` expõe endpoints REST
  - Serviço externo DocuSign para assinatura
  - Webhook de retorno para atualização de status no CRM
- Dependência de feature flag `ff_signature_flow`.

## Metas / Critérios de Sucesso

1. Disponibilizar MVP com assinatura simples em 30 dias.
2. Garantir rastreabilidade de consentimento (audit trail completo).
3. Atingir cobertura de testes >= 85% no módulo de front-end.

## Análise Técnica

| Dimensão          | Decisão                                   | Justificativa                                                  |
| ----------------- | ----------------------------------------- | -------------------------------------------------------------- |
| Arquitetura Front | Angular 17 + Signals                      | Integração com design system interno e granularidade de estado |
| Autenticação      | MSAL com fluxo silent refresh             | Reuso de infraestrutura existente                              |
| Persistência      | Firestore (read) + BFF para escrita       | Evita acesso direto ao legado; BFF orquestra transações        |
| Observabilidade   | Dynatrace spans `ACTION:SIGNATURE_SUBMIT` | Necessário para auditoria e SLO                                |

## Plano de Implementação

1. **Sprint 1**
   - Definir contrato de API com BFF (`docs/api/signature-v1.yaml`).
   - Criar `SignatureModule` com rota protegida `/assinaturas`.
   - Documentar fluxos de erro e fallback (timeout DocuSign).
2. **Sprint 2**
   - Implementar componente `signature-request-form` com validação reativa.
   - Integrar serviço `SignatureService` usando `HttpClient` e interceptores de trace-id.
   - Configurar logs estruturados no BFF com `traceId` e `journeyId`.
3. **Sprint 3**
   - Automatizar testes E2E com Playwright (`tests/e2e/signature-flow.spec.ts`).
   - Publicar guia de observabilidade e dashboards.
   - Revisar política de expurgo de documentos assinados (30 dias).

## Evidências Previstas

- Diagramas C4 atualizados (`docs/architecture/c4/signature-context.puml`).
- Testes unitários: `npm run test -- SignatureModule`.
- Métricas Dynatrace configuradas e documentadas em `docs/observability/signature.md`.

## Riscos & Mitigações

- **Dependência externa DocuSign:** criar ambiente de sandbox e monitorar limites de rate-limit.
- **Conformidade LGPD:** registrar consentimento explícito e permitir revogação via portal.
- **Disponibilidade:** configurar retry exponencial no BFF (3 tentativas) e fallback de suporte manual.

## Débitos & Seguimentos

- Avaliar suporte a múltiplos signatários (fase 2).
- Definir política de versionamento de contratos (metadado `contractVersion`).
- Formalizar checklist de acessibilidade para formulários.

## Histórico de Revisões

| Data       | Autor                            | Mudança                                   |
| ---------- | -------------------------------- | ----------------------------------------- |
| 2025-02-05 | Greenfield Documentation Steward | Blueprint inicial com decisões e plano    |
| 2025-02-07 | Arquiteto de Plataforma          | Inclusão de estratégia de observabilidade |
