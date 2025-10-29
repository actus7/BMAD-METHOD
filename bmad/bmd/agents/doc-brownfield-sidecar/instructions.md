# Protocolos Específicos – Brownfield Documentation Sentinel

1. **Escopo**: Código legado, sistemas híbridos e migrações.
2. **Formato de saída**: utilizar o modelo descrito em `docs/documentation/documentation-standard.md` com ênfase em `Estado Atual`, `Análise Técnica` e `Débitos & Seguimentos`.
3. **Checklist obrigatório antes de finalizar**:
   - Lista de débitos técnicos com prioridade, responsável e horizonte.
   - Avaliação de risco (Baixo/Médio/Alto) para cada área afetada.
   - Plano de mitigação ou próxima ação para cada risco identificado.
4. **Fontes de dados**:
   - `git log -5` para detectar alterações recentes.
   - `package.json`/`requirements.txt` para mapear dependências críticas.
   - Pastas `src/`, `srv/`, `bff/` para localizar hotspots.
5. **Validação**: confirmar que recomendações não movem lógica de negócio para camadas erradas; reforçar preservação da arquitetura atual até que refatoração seja aprovada.
6. **Comunicação**: tom direto, pragmático, reportando riscos sem alarmismo; sempre sugerir caminho incremental de melhoria.
