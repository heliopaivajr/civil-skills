# Changelog — civil-skills

Todas as mudanças relevantes deste repositório são documentadas aqui.
Formato baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.0.0/).

---

## [v0.3.0] — 2026-04-05

### Adicionado
- ✅ Skill `cronograma-obra` v1.0 — Suite completa de planejamento PMI/PMBOK
  - Etapa 0: seleção do nível (Gantt / Físico-Financeiro / CPM / EVM / Plano Completo)
  - Etapa 1: coleta em blocos A/B — identificação e dados técnicos
  - Etapa 2: EAP (WBS) hierárquica padrão para edificações
  - Etapa 3: Cronograma Físico (Gantt) com predecessoras e pesos
  - Etapa 4: CPM/PERT com passagem direta/inversa, folgas e caminho crítico
  - Etapa 5: Cronograma Financeiro + Curva S com padrão esperado por fase
  - Etapa 6: Histograma de MO e equipamentos + nivelamento + índice de irregularidade
  - Etapa 7: EVM completo — VP, VA, CR, IDC, IDP, EAC, VAC, IDCN, relatório de medição
  - Etapa 8: Marcos do projeto (milestones) — padrão e obras públicas
  - Etapa 9: Cronograma de suprimentos e contratações com lead times
  - Etapa 10: Análise de riscos do cronograma (PMBOK) + buffer de contingência
  - Etapa 11: Checklist de validação e alertas automáticos
  - Etapa 12: Formatos de saída e softwares do mercado
  - Etapa 13: 7 prompts profissionais prontos para uso
- 📄 README.md atualizado com fluxo e prompts da skill `cronograma-obra`
- 📄 CHANGELOG.md v0.3.0

---

## [v0.2.0] — 2026-04-05

### Adicionado
- ✅ Skill `memorial-descritivo-obra` v1.0
  - 8 tipos de memorial, diagnóstico DEFINIDO/PARCIAL/OMISSO/CONTRADITÓRIO
  - Modelo completo 18 seções + tabela de acabamentos por ambiente
  - 7 prompts profissionais prontos para uso

---

## [v0.1.0] — 2026-04-05

### Adicionado
- 🎉 Criação do repositório `civil-skills`
- ✅ Skill `orcamento-obra` v1.0
  - SINAPI, TCPO, BIM/ABNT, Própria, Mista — 12 etapas completas

---

## [v1.0.0 — previsto]

Suite completa das 3 skills integradas + publicação no agentskill.sh

---

## [v0.3.1] — 2026-04-06

### Atualizado
- ✅ Skill `cronograma-obra` → v1.1
  - Etapa 14: Leitura e análise de cronograma existente (XLS/CSV do MS Project, Primavera P6)
    - Como exportar de cada ferramenta
    - Extração automática: caminho crítico, predecessoras, % avanço, desvios
    - 5 tipos de simulação de cenário (atraso, nova frente, antecipação, chuvas, redução equipe)
    - Formato padronizado de resposta para análise de impacto
  - Etapa 15: Geração de relatórios automatizados por público-alvo
    - Público 1 (cliente) → Word/.docx narrativo com KPIs e linguagem acessível
    - Público 2 (diretoria) → PowerPoint/.pptx executivo, 8 slides, Gantt + Curva S
    - Público 3 (campo) → Dashboard HTML interativo com filtros e status por atividade
    - Distribuição simultânea para múltiplos públicos a partir de um único arquivo
  - Prompts 8, 9 e 10 adicionados (leitura, simulação, relatório multi-público)
  - description do frontmatter atualizado com novos gatilhos
- 📄 README.md atualizado com exemplos v1.1
