# Changelog — civil-skills

Todas as mudanças relevantes deste repositório são documentadas aqui.
Formato baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.0.0/).

---

## [v0.2.0] — 2026-04-05

### Adicionado
- ✅ Skill `memorial-descritivo-obra` v1.0
  - Etapa 0: seleção do tipo (obra nova / reforma / instalações / as built / licitação / orçamentação)
  - Etapa 1: coleta em blocos A/B/C/D — identificação, documentos, obra, disciplinas
  - Etapa 2: diagnóstico técnico com checklist por disciplina (A/B/C/D)
  - Etapa 3: modelo completo de memorial — 18 seções + tabela de acabamentos por ambiente
  - Etapa 4: três abordagens de estrutura (por disciplina / por ambiente / híbrido)
  - Etapa 5: 7 prompts profissionais prontos para uso
  - Etapa 6: checklist de qualidade e alertas de erros comuns
  - Etapa 7: formatos de saída (Markdown, DOCX, PDF, texto)
  - Baseada no documento técnico "Como gerar memoriais descritivos com IA"
- 📄 README.md atualizado com fluxo e prompts da skill `memorial-descritivo-obra`

---

## [v0.1.0] — 2026-04-05

### Adicionado
- 🎉 Criação do repositório `civil-skills`
- ✅ Skill `orcamento-obra` v1.0
  - Etapa 0: seleção de base de referência (SINAPI / TCPO / Própria / BIM / Mista)
  - 12 etapas completas: contexto → planilha → BDI → Curva ABC → resumo → entrega
  - BDI com fórmula TCU, Curva ABC, Administração Local, validações automáticas
- 📄 README.md, LICENSE MIT e CHANGELOG.md

---

## [Próximas versões planejadas]

### v0.3.0 — previsto
- ✅ Skill `cronograma-obra` v1.0
  - Cronograma físico-financeiro (Gantt simplificado)
  - Curva S de avanço físico e financeiro
  - Histograma de mão de obra
  - Método do caminho crítico (CPM simplificado)

### v1.0.0 — previsto
- Suite completa das 3 skills integradas
- Templates de uso combinado
- Publicação oficial no agentskill.sh
