# 🏗️ civil-skills

> **Agent Skills para Construção Civil** — Skills profissionais para Claude Code, OpenClaw, Cursor, GitHub Copilot e demais agentes compatíveis com o formato SKILL.md.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Skills: 1](https://img.shields.io/badge/Skills-1-blue.svg)](#skills-disponíveis)
[![Versão](https://img.shields.io/badge/Versão-v0.1.0-green.svg)](#changelog)
[![Compatível com](https://img.shields.io/badge/Compatível%20com-Claude%20%7C%20OpenClaw%20%7C%20Cursor%20%7C%20Copilot-blueviolet.svg)](#compatibilidade)

---

## O que é este repositório?

Este repositório reúne **Agent Skills especializadas em construção civil** desenvolvidas por um engenheiro civil com experiência em orçamentação, projetos e gestão de obras no Brasil.

As skills seguem o **formato aberto SKILL.md** — desenvolvido pela Anthropic e adotado como padrão pelo ecossistema de agentes de IA — o que garante que funcionem em múltiplas ferramentas sem nenhuma adaptação.

Pense nelas como **receitas técnicas** que ensinam seu agente de IA a trabalhar como um profissional sênior da construção civil: orçamentista, planejador de obras, redator de memoriais.

---

## Skills Disponíveis

| # | Skill | Descrição | Status |
|---|-------|-----------|--------|
| 01 | [`orcamento-obra`](./skills/orcamento-obra/SKILL.md) | Orçamento analítico com SINAPI, TCPO, composição própria ou BIM/ABNT | ✅ v1.0 |
| 02 | [`cronograma-obra`](./skills/cronograma-obra/SKILL.md) | Cronograma físico-financeiro, CPM/PERT, Curva S, EVM/GVA, histograma de MO | ✅ v1.1 |
| 03 | [`memorial-descritivo-obra`](./skills/memorial-descritivo-obra/SKILL.md) | Memorial descritivo técnico completo — obras, arquitetura e instalações | ✅ v1.0 |

---

## Como Instalar

### Opção 1 — Via CLI do agentskill.sh (recomendado)

```bash
# Instalar uma skill específica
npx @agentskill.sh/cli@latest install @heliopaivajr/orcamento-obra

# Ou instalar todas as skills deste repositório
npx @agentskill.sh/cli@latest install @heliopaivajr/civil-skills
```

### Opção 2 — Manual para Claude Code

```bash
# No diretório raiz do seu projeto
mkdir -p .claude/skills/orcamento-obra

# Baixar o SKILL.md diretamente
curl -o .claude/skills/orcamento-obra/SKILL.md \
  https://raw.githubusercontent.com/heliopaivajr/civil-skills/main/skills/orcamento-obra/SKILL.md
```

### Opção 3 — Manual para OpenClaw

```bash
# Criar pasta de skills do OpenClaw (ajuste o caminho conforme seu sistema)
mkdir -p ~/.openclaw/skills/orcamento-obra

# Baixar o SKILL.md
curl -o ~/.openclaw/skills/orcamento-obra/SKILL.md \
  https://raw.githubusercontent.com/heliopaivajr/civil-skills/main/skills/orcamento-obra/SKILL.md
```

### Opção 4 — Clonar o repositório completo

```bash
# Clonar uma vez e usar todas as skills localmente
git clone https://github.com/heliopaivajr/civil-skills.git

# Copiar para Claude Code (projeto atual)
cp -r civil-skills/skills/orcamento-obra .claude/skills/

# Copiar para OpenClaw
cp -r civil-skills/skills/orcamento-obra ~/.openclaw/skills/
```

### Opção 5 — Windows (PowerShell)

```powershell
# Criar pasta no perfil do usuário (disponível em todos os projetos)
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills\orcamento-obra"

# Baixar o arquivo
Invoke-WebRequest `
  -Uri "https://raw.githubusercontent.com/heliopaivajr/civil-skills/main/skills/orcamento-obra/SKILL.md" `
  -OutFile "$env:USERPROFILE\.claude\skills\orcamento-obra\SKILL.md"
```

---

## Como Usar

### Invocação explícita (Claude Code / OpenClaw)

```
/orcamento-obra
```

### Invocação implícita (por linguagem natural)

Basta descrever o que você precisa — o agente ativa a skill automaticamente:

```
"Preciso orçar a construção de uma casa de 120m² em Recife, PE"

"Qual o custo de revestimento cerâmico interno pelo SINAPI de Pernambuco?"

"Monte uma planilha orçamentária para reforma de banheiro"

"Orçamento analítico para obra pública — escola em Maceió/AL"

"Quanto custa construir um galpão industrial de 500m²?"
```

### Fluxo típico de uso (skill `orcamento-obra`)

```
1. Agente pergunta: qual base de referência? (SINAPI / TCPO / Própria / BIM / Mista)
2. Agente coleta: UF, tipo de obra, mês de referência, desoneração, natureza
3. Agente estrutura: planilha por macroetapas com códigos e custos
4. Agente calcula: BDI, encargos, Administração Local
5. Agente gera: Curva ABC + Resumo Geral
6. Agente entrega: em Markdown, XLSX, DOCX ou texto estruturado
```

---

## Compatibilidade

| Ferramenta | Suporte | Invocação |
|---|---|---|
| **Claude Code** | ✅ Nativo | `/orcamento-obra` ou linguagem natural |
| **OpenClaw** | ✅ Nativo | `/orcamento-obra` ou linguagem natural |
| **GitHub Copilot** | ✅ Via `.github/skills/` | `/orcamento-obra` no chat |
| **Cursor** | ✅ Via `.cursor/skills/` | Linguagem natural |
| **Windsurf** | ✅ Compatível | Linguagem natural |
| **Codex CLI** | ✅ Compatível | `$orcamento-obra` |
| **Claude.ai** | ✅ Upload manual | Upload do SKILL.md nas configurações |

---

## Localização dos Arquivos por Ferramenta

```
Projeto (escopo local):
  Claude Code:   .claude/skills/orcamento-obra/SKILL.md
  Copilot:       .github/skills/orcamento-obra/SKILL.md
  Cursor:        .cursor/skills/orcamento-obra/SKILL.md

Usuário (disponível em todos os projetos):
  Claude Code:   ~/.claude/skills/orcamento-obra/SKILL.md
  OpenClaw:      ~/.openclaw/skills/orcamento-obra/SKILL.md
  Copilot:       ~/.copilot/skills/orcamento-obra/SKILL.md
```

---

## Estrutura do Repositório

```
civil-skills/
├── README.md                          ← Este arquivo
├── LICENSE                            ← MIT License
├── CHANGELOG.md                       ← Histórico de versões
└── skills/
    ├── orcamento-obra/
    │   └── SKILL.md                   ← Skill de orçamento (v1.0)
    ├── cronograma-obra/               ← Em desenvolvimento
    │   └── SKILL.md
    └── memorial-descritivo-obra/      ← Em desenvolvimento
        └── SKILL.md
```

---

## Base Técnica das Skills

As skills deste repositório são desenvolvidas com base em:

| Referência | Aplicação |
|---|---|
| **SINAPI** — CEF/IBGE (tabelas mensais) | Preços de insumos e composições |
| **TCPO Ed. 14** — Editora PINI | Composições de mercado privado |
| **Lei 14.133/2021** | Nova Lei de Licitações e Contratos |
| **Decreto 7.983/2013** | Uso obrigatório do SINAPI em obras federais |
| **Acórdão TCU 2622/2013** | Limites de BDI para obras públicas |
| **ABNT NBR 15965** | Classificação da Informação da Construção (BIM) |
| **Decreto 9.983/2019** | Implantação do BIM no setor público brasileiro |
| **ABNT NBR 12.721** | CUB — Custo Unitário Básico |
| **NR-18** | Segurança em obras de construção civil |

---

## Sobre o Autor

**Hélio Paiva Jr.** — Engenheiro Civil | Orçamentista | Desenvolvedor

- 🏗️ Engenheiro civil com experiência em orçamentação SINAPI e gestão de obras
- 💻 Desenvolvedor SaaS — [ObraPrice](https://github.com/heliopaivajr/SAAS_ORCA) (plataforma de orçamentação automatizada)
- 🌐 Site: [heliopaiva.com.br](https://heliopaiva.com.br)
- 📦 GitHub: [@heliopaivajr](https://github.com/heliopaivajr)

---

## Contribuição

Contribuições são bem-vindas! Se você é profissional da construção civil e quer melhorar ou adicionar skills:

1. Faça um fork do repositório
2. Crie uma branch: `git checkout -b feat/nome-da-skill`
3. Adicione ou edite o `SKILL.md` na pasta correta
4. Abra um Pull Request descrevendo a melhoria

Por favor, mantenha o padrão de qualidade: instruções claras, exemplos reais, referências técnicas brasileiras.

---

## Changelog

### v0.1.0 — Abril/2026
- 🎉 Criação do repositório `civil-skills`
- ✅ Publicação da skill `orcamento-obra` v1.0
  - Suporte a SINAPI, TCPO, Composição Própria, BIM/ABNT NBR 15965 e Base Mista
  - 12 etapas completas: contexto → entrega
  - BDI com fórmula TCU, Curva ABC, Administração Local, validações automáticas

---

## Licença

MIT License — veja o arquivo [LICENSE](./LICENSE) para detalhes.

> Skills são instruções de texto. Não contêm código executável. Podem ser usadas, modificadas e distribuídas livremente conforme os termos da licença MIT.

---

### Fluxo típico de uso (skill `memorial-descritivo-obra`)

A skill atua como especialista sênior — **faz perguntas técnicas antes de redigir**, garantindo documento útil para orçamento, compras e execução.

```
1. Agente pergunta: qual tipo de memorial? (obra nova / reforma / instalações / as built...)
2. Agente coleta: identificação, disciplinas e documentos disponíveis
3. Agente analisa arquivos enviados (plantas, PDFs, briefing)
4. Agente executa diagnóstico: DEFINIDO / PARCIAL / OMISSO / CONTRADITÓRIO
5. Agente redige: memorial por disciplina + tabela de acabamentos por ambiente
6. Agente consolida: pendências com impacto e responsável
7. Agente entrega: Markdown, DOCX ou PDF — com aviso de revisão pelo RT
```

**Prompts prontos para usar com a skill `memorial-descritivo-obra`:**

```
# Diagnóstico técnico completo (envie os projetos junto):
"Analise tecnicamente os arquivos como especialista em memorial descritivo.
Identifique por disciplina tudo que está definido, parcialmente definido, omisso
e contraditório. Destaque lacunas que afetam orçamento e execução."

# Memorial completo:
"Gere um memorial descritivo técnico e profissional. Estruture em: identificação,
objetivo, escopo contemplado e excluído, premissas, serviços preliminares,
arquitetura, estrutura, instalações, tabela de acabamentos por ambiente, pendências
e observações. Registre [PENDENTE] onde não há definição."

# Diagnóstico por ambiente:
"Faça levantamento por ambiente: piso, rodapé, paredes, teto, esquadrias, vidros,
bancadas, louças, metais, iluminação e climatização. Indique [PENDENTE] onde não
houver definição clara."

# Versão para orçamento:
"Transforme o memorial em versão para orçamento, classificando cada item em:
DEFINIDO / PARCIALMENTE DEFINIDO / PENDENTE / CONFLITANTE."

# Relatório de pendências para cliente:
"Gere relatório de pendências por disciplina para envio ao cliente/arquiteto,
destacando o impacto de cada omissão no orçamento e execução."
```

---

### Fluxo típico de uso (skill `cronograma-obra`)

A skill atua como especialista PMI — estrutura do zero ou aprimora cronogramas existentes, do físico ao controle financeiro.

```
1. Agente pergunta: o que precisa? (Gantt / Físico-Financeiro / CPM / EVM / Plano Completo)
2. Agente coleta: obra, prazo, orçamento, atividades, restrições
3. Agente monta: EAP hierárquica (WBS) como base do cronograma
4. Agente calcula: caminho crítico (CPM/PERT) com folgas e atividades críticas
5. Agente distribui: custos por período → tabela de desembolso mensal
6. Agente gera: Curva S (físico e financeiro acumulado)
7. Agente dimensiona: histograma de MO e equipamentos + nivelamento
8. Agente monitora: EVM com VP, VA, CR, IDC, IDP, EAC e diagnóstico
9. Agente entrega: relatório completo com marcos, riscos e suprimentos
```

**Prompts prontos para usar com a skill `cronograma-obra`:**

```
# Cronograma físico-financeiro completo:
"Atue como especialista em planejamento de obras. Elabore cronograma físico-financeiro
completo para [obra], prazo [X meses], orçamento R$ [valor]. Inclua EAP, Gantt com
caminho crítico, desembolso mensal, Curva S e histograma de MO. Metodologia PMI/PMBOK."

# Caminho crítico (CPM):
"Calcule o caminho crítico para as seguintes atividades: [lista com duração e
predecessoras]. Apresente passagem direta/inversa, folgas e duração mínima da obra."

# EVM — controle de obra em andamento:
"Calcule os indicadores EVM: OAC=R$[valor], % planejado=[X]%, % realizado=[Y]%,
custo real=R$[valor]. Calcule VP, VA, CR, IDC, IDP, EAC, VAC e IDCN. Diagnóstico
e recomendações."

# Histograma de mão de obra:
"Dimensione o histograma de MO para [obra]. Calcule equipe por atividade,
consolide por período, apresente o histograma e calcule o índice de irregularidade."

# Plano de recuperação de atraso:
"A obra está [X dias] atrasada. Caminho crítico: [atividades]. Analise causas,
impacto e proponha plano de recuperação com aceleração das atividades críticas."

# Cronograma de suprimentos:
"Com base no cronograma físico, elabore o cronograma de compras e contratações
considerando lead times. Identifique itens críticos e datas limite de compra."
```

---

### Novidades v1.1 — skill `cronograma-obra`

**Etapa 14 — Simulação de Cenários (XLS/CSV existente)**
Carregue o XLS exportado do MS Project e simule qualquer hipótese em linguagem natural:

```
# Ler e diagnosticar cronograma existente:
"Analise o cronograma em anexo (XLS do MS Project). Identifique caminho crítico,
atividades com folga, % de avanço abaixo do esperado para hoje [data] e diagnóstico
do status atual."

# Simular atraso e calcular impacto:
"Com base no cronograma anexado, simule: atraso de 3 semanas na concretagem do
3º pavimento. Calcule nova data de entrega, atividades impactadas no caminho crítico
e 3 alternativas de recuperação com custo incremental."
```

**Etapa 15 — Relatórios Automatizados por Público**
Do mesmo arquivo, três formatos simultâneos em minutos:

```
# Três relatórios a partir de um único XLS:
"Com base no cronograma anexado, gere:
1. Word para o cliente — resumo executivo, % avanço, previsto x realizado,
   pendências e próximas entregas. Linguagem acessível.
2. PPT para diretoria — KPIs, Gantt executivo, Curva S, alertas, decisões.
3. Dashboard HTML para o time de campo — status por atividade, filtros por
   frente, caminho crítico destacado, alertas 7 dias.
Data de referência: [data]."
```
