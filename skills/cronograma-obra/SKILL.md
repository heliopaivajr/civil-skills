---
name: cronograma-obra
description: >
  Elabora cronogramas físico-financeiros completos para obras de construção civil,
  integrando planejamento físico, financeiro e de recursos com base nas metodologias
  PMI/PMBOK, CPM, PERT, Linha de Balanço e EVM (Earned Value Management).
  Use quando o usuário pedir "cronograma de obra", "cronograma físico-financeiro",
  "planejamento de obra", "curva S", "caminho crítico", "CPM", "PERT", "diagrama de
  Gantt", "histograma de mão de obra", "histograma de equipamentos", "EAP da obra",
  "linha de base do projeto", "EVM", "valor agregado", "IDP", "IDC", "controle de
  obra", "avanço físico", "avanço financeiro", "cronograma de suprimentos",
  "cronograma de contratações" ou qualquer variação dessas expressões em português.
  Não usar para orçamentos (use orcamento-obra) nem para memoriais (use memorial-descritivo-obra).
license: MIT
compatibility:
  - claude-code
  - openclaw
  - claude
  - cursor
  - copilot
---

# Cronograma de Obra — Planejamento Físico-Financeiro Integrado

## Visão Geral

Esta skill transforma o agente em um **especialista sênior em planejamento e controle
de obras**, dominando o arsenal completo de ferramentas utilizadas pelos melhores
gestores de projetos de construção civil do Brasil:

**Ferramentas de planejamento:**
- EAP (Estrutura Analítica do Projeto) — WBS do PMBOK
- Diagrama de Gantt — visualização de atividades no tempo
- PERT/CPM — rede de precedências e caminho crítico
- Linha de Balanço (LOB) — ideal para obras repetitivas
- Lean Construction / Last Planner System (conceitos)

**Ferramentas de controle:**
- Curva S — avanço físico e financeiro acumulado
- Histograma de mão de obra e equipamentos
- EVM/GVA — Earned Value Management / Gerenciamento do Valor Agregado
- Índices de desempenho (IDP, IDC, VPr, VC)
- Previsão de término (EAC, ETC, TCPI)

**Base metodológica:**
- PMI — Project Management Institute
- PMBOK® Guide (6ª e 7ª edições)
- NBR ISO 21500 — Gerência de Projetos
- Mattos, A.D. — *Planejamento e Controle de Obras* (PINI, 2010)

> **Princípio fundamental:** Cronograma sem financeiro é incompleto.
> Físico sem controle é decorativo. Esta skill entrega os dois, integrados.

---

## Quando Usar Esta Skill

**Acione automaticamente quando o usuário mencionar:**
- Cronograma de obra / cronograma físico / cronograma financeiro
- Diagrama de Gantt / gráfico de barras de obra
- Caminho crítico / CPM / PERT / rede de precedências
- Curva S / avanço físico / avanço financeiro acumulado
- Histograma de mão de obra / histograma de equipamentos
- EAP / WBS / estrutura analítica do projeto
- EVM / valor agregado / GVA / IDP / IDC
- Planejamento de obra / plano de ataque / frentes de trabalho
- Cronograma de suprimentos / cronograma de contratações
- Linha de balanço / planejamento de obra repetitiva
- Datas marco / milestones / marcos do projeto

**Não acionar quando:**
- Usuário pedir orçamento → use `orcamento-obra`
- Usuário pedir memorial descritivo → use `memorial-descritivo-obra`
- Perguntas conceituais sem intenção de produzir documento

---

## Etapa 0 — Seleção do Nível de Planejamento

Antes de qualquer pergunta técnica, identificar **o que o usuário precisa produzir**.
Apresentar opções e aguardar escolha:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 O QUE DESEJA ELABORAR?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 [1] Cronograma Físico          — Gantt com atividades e prazos
 [2] Cronograma Físico-Financeiro — Gantt + custo por período + Curva S
 [3] Caminho Crítico (CPM/PERT)  — rede de precedências e folgas
 [4] Histograma de Recursos      — mão de obra e equipamentos
 [5] EVM / Controle de Obra      — medição de avanço e indicadores
 [6] Plano Completo de Obra      — tudo acima integrado (nível máximo)
 [7] Cronograma de Suprimentos   — compras e contratações alinhadas ao físico
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

> Se o usuário não souber escolher, recomendar:
> - Obra pública / licitação → **[2] ou [6]**
> - Controle de obra em andamento → **[5] EVM**
> - Planejamento inicial rápido → **[1] ou [2]**
> - Obra com pavimentos repetidos → **[3] Linha de Balanço**

---

## Etapa 1 — Coleta de Contexto Obrigatório

Fazer perguntas em **dois blocos**. Não perguntar tudo de uma vez.

### Bloco A — Identificação (sempre perguntar)

```
1. Nome / descrição da obra
2. Local (cidade/UF)
3. Tipo: residencial / comercial / industrial / infraestrutura / reforma
4. Área total (m²) e número de pavimentos
5. Data de início prevista
6. Prazo contratual total (em meses ou dias corridos)
7. Já existe orçamento? (sim — valor total / não — estimar)
8. Responsável pelo planejamento (nome e papel)
```

### Bloco B — Dados Técnicos (conforme nível escolhido)

```
9.  Já existe lista de atividades / EAP? (sim — enviar / não — montar aqui)
10. Qual a unidade de tempo preferida? semanas / meses / quinzenas
11. Há restrições externas de prazo? (marcos contratuais, licenças, chuvas, etc.)
12. Há frentes de trabalho simultâneas? (subempreiteiros, disciplinas paralelas)
13. Existe planilha orçamentária com custos por etapa? (integrar ao financeiro)
14. Regime de execução: empreitada global / por administração / misto
15. Será necessário controle de avanço (EVM)? sim / não
```

---

## Etapa 2 — EAP (Estrutura Analítica do Projeto)

A EAP é o alicerce de qualquer cronograma. Deve ser montada **antes** do Gantt.

### Conceito PMI/PMBOK:
A EAP decompõe o escopo total em pacotes de trabalho gerenciáveis e mensuráveis,
organizados hierarquicamente. Cada elemento deve ser:
- **Mutuamente exclusivo** — sem sobreposição entre pacotes
- **Coletivamente exaustivo** — a soma cobre 100% do escopo
- **Mensurável** — permite atribuir custo, prazo e responsável

### EAP Padrão para Obras de Edificação (adaptável):

```
OBRA [Nome]
│
├── 1. SERVIÇOS PRELIMINARES
│   ├── 1.1 Mobilização e canteiro
│   ├── 1.2 Locação e topografia
│   └── 1.3 Demolições e limpeza
│
├── 2. INFRAESTRUTURA
│   ├── 2.1 Terraplenagem
│   ├── 2.2 Fundações
│   └── 2.3 Contenções e arrimos
│
├── 3. SUPERESTRUTURA
│   ├── 3.1 Estrutura de concreto (pilares, vigas, lajes)
│   ├── 3.2 Estrutura metálica (se aplicável)
│   └── 3.3 Pré-moldados (se aplicável)
│
├── 4. VEDAÇÕES E COBERTURA
│   ├── 4.1 Alvenaria de vedação
│   ├── 4.2 Cobertura (estrutura + telhas)
│   └── 4.3 Impermeabilização
│
├── 5. INSTALAÇÕES
│   ├── 5.1 Instalações hidrossanitárias
│   ├── 5.2 Instalações elétricas e lógica
│   ├── 5.3 Climatização e exaustão
│   └── 5.4 Instalações especiais (incêndio, gás, etc.)
│
├── 6. REVESTIMENTOS E ACABAMENTOS
│   ├── 6.1 Revestimentos de parede (interno e externo)
│   ├── 6.2 Pisos e contrapiso
│   ├── 6.3 Tetos e forros
│   ├── 6.4 Pintura
│   └── 6.5 Esquadrias e vidros
│
├── 7. COMPLEMENTOS
│   ├── 7.1 Louças, metais e bancadas
│   ├── 7.2 Paisagismo e urbanização
│   └── 7.3 Limpeza final e entrega
│
└── 8. GERENCIAMENTO DO PROJETO
    ├── 8.1 Planejamento e controle
    ├── 8.2 Qualidade (inspeções, ensaios)
    └── 8.3 Segurança do trabalho (NR-18)
```

> Adaptar a EAP conforme escopo real. Cada pacote de trabalho vira uma atividade
> (ou conjunto de atividades) no cronograma Gantt.

---

## Etapa 3 — Cronograma Físico (Diagrama de Gantt)

### Formato da tabela de atividades:

```markdown
| ID | Atividade | Predecessora | Duração | Início | Término | % Peso | Responsável |
|----|-----------|-------------|---------|--------|---------|--------|-------------|
| 1  | Mobilização | —       | 10 dias | S1     | S2      | 1,5%   | Mestre |
| 2  | Locação da obra | 1   | 5 dias  | S2     | S2      | 0,5%   | Topógrafo |
| 3  | Escavação manual | 2  | 15 dias | S3     | S5      | 3,0%   | Empreiteiro A |
| 4  | Fundação (sapatas) | 3 | 20 dias | S4     | S7      | 8,0%   | Empreiteiro B |
...
```

### Relações de precedência (PMBOK):
```
TI — Término-Início:    B só inicia após A terminar (mais comum)
II — Início-Início:     B inicia junto com A (ex: escavação e locação)
TT — Término-Término:  B termina junto com A
IT — Início-Término:   raro, usado em transições de turno
```

### Regras para montagem do Gantt:
1. Listar **todas** as atividades da EAP como linhas
2. Definir **duração** com base em produtividade real (TCPO ou experiência)
3. Estabelecer **predecessoras** obrigatórias e lógicas
4. Calcular **datas** de início e fim de cada atividade
5. Atribuir **peso percentual** (% do custo total ou % do prazo)
6. Identificar o **caminho crítico** (Etapa 4)
7. Verificar **marcos contratuais** — datas que não podem ser violadas

### Representação do Gantt em Markdown:

```
PERÍODO →           S1  S2  S3  S4  S5  S6  S7  S8  S9  S10
1. Mobilização      ████
2. Locação              ██
3. Escavação               ████████████
4. Fundação                    ████████████████
5. Estrutura pav.1                          ████████████████
6. Alvenaria                                        ████████
...
```

> Legenda: `████` = execução | `----` = folga disponível | `◆` = marco

---

## Etapa 4 — Caminho Crítico (CPM/PERT)

### Conceitos fundamentais:

**CPM (Critical Path Method):**
- Identifica a sequência de atividades que determina a duração mínima da obra
- Qualquer atraso em atividade crítica = atraso direto na entrega
- Atividades não-críticas têm **folga** (podem atrasar sem impactar o prazo final)

**PERT (Program Evaluation and Review Technique):**
- Lida com incertezas nas durações
- Usa três estimativas: otimista (to), mais provável (tm), pessimista (tp)
- Duração esperada: **te = (to + 4×tm + tp) / 6**
- Desvio padrão: **σ = (tp - to) / 6**

### Cálculo CPM — Passagem Direta e Inversa:

```
PASSAGEM DIRETA (cálculo de datas mais cedo):
  IC_j = MAX(TC_i + D_ij)   para todos os predecessores i de j
  TC_i = IC_i + D_i

PASSAGEM INVERSA (cálculo de datas mais tarde):
  TT_i = MIN(IT_j - D_ij)   para todos os sucessores j de i
  IT_i = TT_i - D_i

FOLGA TOTAL:
  FT_i = IT_i - IC_i = TT_i - TC_i

ATIVIDADE CRÍTICA: FT = 0
CAMINHO CRÍTICO: sequência de atividades com FT = 0
```

### Exemplo de cálculo para apresentar ao usuário:

```
Atividade | Pred. | Dur. | IC  | TC  | IT  | TT  | FT  | Crítica?
----------|-------|------|-----|-----|-----|-----|-----|--------
A Escav.  |  —    |  10  |  0  | 10  |  0  | 10  |  0  |   SIM ★
B Fundiç. |  A    |  20  | 10  | 30  | 10  | 30  |  0  |   SIM ★
C Forma   |  B    |  15  | 30  | 45  | 32  | 47  |  2  |   não
D Armad.  |  B    |  12  | 30  | 42  | 35  | 47  |  5  |   não
E Concr.  | C,D   |  8   | 45  | 53  | 47  | 55  |  2  |   não
F Desfor. |  E    |  5   | 53  | 58  | 55  | 60  |  2  |   não
...
```

### Caminho Crítico identificado: A → B → ...
Duração mínima da obra = soma das atividades críticas

> ⚠️ **Alerta**: Monitorar semanalmente as atividades críticas.
> Uma atividade com FT = 0 que atrasa = obra atrasa na mesma proporção.

### Linha de Balanço (LOB) — obras repetitivas:

Indicada para: edifícios multipavimentos, conjuntos habitacionais, rodovias.

```
Princípio: cada equipe executa o mesmo serviço em pavimentos diferentes,
em ritmo constante, sem interferência entre equipes.

Gráfico LOB:
  Eixo X = Tempo (semanas)
  Eixo Y = Pavimentos (P1, P2, P3... Pn)
  Linhas diagonais = ritmo de cada equipe/serviço

Ritmo ideal = Duração total / Número de unidades repetidas
```

---

## Etapa 5 — Cronograma Financeiro e Curva S

O cronograma financeiro distribui o **custo total da obra** ao longo do tempo,
integrando diretamente com o físico.

### Passo a passo:

**1. Distribuição de custos por atividade:**
Atribuir a cada atividade do Gantt seu custo correspondente (do orçamento).

**2. Distribuição dentro do período:**
Para cada atividade, distribuir o custo proporcionalmente à duração no período:
```
Custo no período = (Duração no período / Duração total) × Custo da atividade
```

**3. Tabela de desembolso mensal:**
```
| Etapa/Atividade      | Custo Total | M1      | M2      | M3      | M4      | ... |
|----------------------|-------------|---------|---------|---------|---------|-----|
| 1. Serv. Preliminares| R$ 45.000   |45.000   |   —     |   —     |   —     |     |
| 2. Fundações         | R$ 180.000  |30.000   |90.000   |60.000   |   —     |     |
| 3. Estrutura         | R$ 420.000  |  —      |70.000   |140.000  |140.000  | 70k |
| ...                  |             |         |         |         |         |     |
| **TOTAL MENSAL**     |             |75.000   |160.000  |200.000  |140.000  |     |
| **ACUMULADO**        |             |75.000   |235.000  |435.000  |575.000  |     |
| **% MENSAL**         |             | 5,0%    | 10,7%   | 13,4%   |  9,4%   |     |
| **% ACUMULADO**      |             | 5,0%    | 15,7%   | 29,1%   | 38,5%   |     |
```

**4. Curva S — representação gráfica:**
```
100% ┤                                              ●────●
 90% ┤                                        ●────/
 80% ┤                                   ●───/
 70% ┤                              ●───/
 60% ┤                         ●───/
 50% ┤                    ●───/
 40% ┤               ●───/
 30% ┤          ●───/
 20% ┤     ●───/
 10% ┤ ●───/
  0% ┼──────────────────────────────────────────── Tempo
     M1   M2   M3   M4   M5   M6   M7   M8   M9   M10
```

### Padrão da Curva S em obras de edificação:
```
Mobilização (0–10% do prazo):   ~5–10% do custo acumulado
Estrutura (10–40% do prazo):    ~25–45% do custo acumulado
Instalações/Reboco (40–70%):    ~60–75% do custo acumulado
Acabamentos (70–95% do prazo):  ~88–95% do custo acumulado
Entrega (95–100% do prazo):     100% do custo
```

> **Alerta de padrão anormal:** Curva muito íngreme no início pode indicar
> mobilização excessiva ou frente de trabalho superdimensionada. Curva muito
> plana no final pode sinalizar risco de paralisação por falta de recursos.

---

## Etapa 6 — Histograma de Mão de Obra e Equipamentos

O histograma mostra a **demanda de recursos** ao longo do tempo — permite planejar
contratações, evitar sobrecarga e otimizar custos de equipe.

### Como calcular o histograma de MO:

**1. Para cada atividade, dimensionar a equipe:**
```
Equipe = Quantidade de serviço / (Produtividade unitária × Duração)

Exemplo: Alvenaria de vedação — 500m²
  Produtividade: 8 m²/homem.dia (TCPO)
  Duração planejada: 25 dias úteis
  Equipe = 500 / (8 × 25) = 2,5 → arredondar para 3 pedreiros + 2 serventes
```

**2. Tabela de alocação de recursos:**
```
| Atividade         | Dur. | M1  | M2  | M3  | M4  | M5  | Tipo de MO    |
|-------------------|------|-----|-----|-----|-----|-----|---------------|
| Fundações         | 30d  |  8  |  4  |  —  |  —  |  —  | Pedreiro + AUX|
| Estrutura         | 60d  |  —  | 12  | 15  |  8  |  —  | Carpinteiro + ARM |
| Alvenaria         | 25d  |  —  |  —  |  5  |  5  |  —  | Pedreiro      |
| Instalações Hidro | 40d  |  —  |  3  |  4  |  3  |  —  | Encanador     |
| Instalações Elétr | 45d  |  —  |  2  |  4  |  4  |  2  | Eletricista   |
| Revestimentos     | 30d  |  —  |  —  |  —  |  6  |  6  | Azulejista    |
|**TOTAL OPERÁRIOS**|      |  8  | 21  | 28  | 26  |  8  |               |
```

**3. Gráfico do histograma (texto):**
```
N° de
Operários
  30 ┤          ████
  25 ┤     ████ ████ ████
  20 ┤     ████ ████ ████
  15 ┤     ████ ████ ████
  10 ┤████ ████ ████ ████
   5 ┤████ ████ ████ ████ ████
   0 ┼─────────────────────────
     M1   M2   M3   M4   M5
```

**4. Nivelamento de recursos:**
- Identificar picos excessivos → redistribuir atividades não-críticas
- Identificar vales → avaliar ociosidade e possível aceleração
- Meta: histograma com variação máxima de ±30% entre períodos adjacentes

### Índice de irregularidade (II):
```
II = Pico máximo de MO / MO média ao longo da obra
Ideal: II < 2,0 (quanto mais próximo de 1, mais nivelado)
```

### Equipes principais para obras de edificação:

| Categoria | Composição típica | Quando mobilizar |
|---|---|---|
| Infraestrutura | Escavadeirista + ajudantes | Início da obra |
| Fundações | Pedreiro sênior + armadores + aux. | Após locação |
| Estrutura | Carpinteiro + armador + concretista | Após fundação |
| Alvenaria | Pedreiro + servente (1:1,5) | Após estrutura |
| Instalações | Encanador + eletricista + aux. | Paralelo a alvenaria |
| Reboco/Gesso | Gesseiro / reboqueiro + aux. | Após instalações brutas |
| Acabamentos | Azulejista + pintor + marceneiro | Últimos 30% da obra |
| Limpeza e entrega | Equipe multifuncional | Últimas 2 semanas |

---

## Etapa 7 — EVM / Gerenciamento do Valor Agregado

O EVM integra **escopo + prazo + custo** em um único sistema de medição,
respondendo à pergunta: *"O que conseguimos com o dinheiro que gastamos?"*

### Três grandezas fundamentais (PMBOK):

```
VP  (Valor Planejado / Planned Value — PV):
    Custo orçado do trabalho planejado até a data de medição
    = % planejado × Orçamento total
    Representa a LINHA DE BASE — o que deveria ter sido feito

VA  (Valor Agregado / Earned Value — EV):
    Custo orçado do trabalho REALMENTE executado até a data
    = % real executado × Orçamento total
    Representa o PROGRESSO FÍSICO convertido em valor monetário

CR  (Custo Real / Actual Cost — AC):
    Custo efetivamente gasto até a data de medição
    = Notas fiscais + folha de pagamento + locações
    Representa o DESEMBOLSO REAL
```

### Variações e Índices de Desempenho:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 VARIAÇÕES (em R$)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 VC  = VA – CR     (Variação de Custo)
   VC > 0 → abaixo do orçamento ✅
   VC < 0 → acima do orçamento  ⚠️

 VPr = VA – VP     (Variação de Prazo)
   VPr > 0 → adiantado           ✅
   VPr < 0 → atrasado            ⚠️

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 ÍNDICES DE DESEMPENHO (adimensionais)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 IDC = VA / CR     (Índice de Desempenho de Custo — CPI)
   IDC > 1,0 → eficiente (cada R$1 gasto gera >R$1 de valor) ✅
   IDC = 1,0 → dentro do orçamento                            ✅
   IDC < 1,0 → ineficiente (cada R$1 gasto gera <R$1 de valor)⚠️

 IDP = VA / VP     (Índice de Desempenho de Prazo — SPI)
   IDP > 1,0 → adiantado em relação ao planejado              ✅
   IDP = 1,0 → no prazo                                       ✅
   IDP < 1,0 → atrasado (ritmo abaixo do planejado)           ⚠️
```

### Previsões de término (Forecasting):

```
OAC  = Orçamento na Conclusão (Budget at Completion — BAC)
       = valor total do orçamento original

EAC  = Estimativa no Término (Estimate at Completion)
       Previsão do custo total final da obra

       Fórmula 1 (desvio persistirá): EAC = OAC / IDC
       Fórmula 2 (desvio pontual):    EAC = CR + (OAC – VA)
       Fórmula 3 (novo orçamento):    EAC = CR + ETC (nova estimativa do restante)

ETC  = Estimativa para Terminar (Estimate to Complete)
       ETC = EAC – CR

VNC  = Variação na Conclusão (Variance at Completion — VAC)
       VAC = OAC – EAC
       VAC > 0 → ficará abaixo do orçamento
       VAC < 0 → ficará acima do orçamento (risco de aditivo)

IDCN = Índice de Desempenho de Custo Necessário (TCPI)
       IDCN = (OAC – VA) / (OAC – CR)
       IDCN > 1,2 → meta praticamente inatingível (replanejar)
       IDCN ≤ 1,0 → meta confortável
```

### Relatório de Medição (modelo padrão):

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 RELATÓRIO DE AVANÇO — [OBRA] — [Período: MM/AAAA]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 Orçamento total (OAC):        R$ 1.500.000,00
 Data de medição:              [DD/MM/AAAA]

 GRANDEZAS BÁSICAS:
   Valor Planejado (VP):       R$ 600.000,00  (40,0% previsto)
   Valor Agregado (VA):        R$ 510.000,00  (34,0% realizado)
   Custo Real (CR):            R$ 540.000,00  (36,0% gasto)

 VARIAÇÕES:
   Variação de Custo (VC):     R$ -30.000,00  ⚠️ acima do orçado
   Variação de Prazo (VPr):    R$ -90.000,00  ⚠️ atrasado

 ÍNDICES:
   IDC (Custo):                0,944          ⚠️ ineficiente
   IDP (Prazo):                0,850          ⚠️ atrasado (85% do ritmo)

 PREVISÕES:
   EAC (custo final previsto): R$ 1.589.000,00
   VAC (variação final):       R$ -89.000,00  ⚠️ estouro de +5,9%
   IDCN necessário:            1,08           ⚠️ exigente mas viável

 ANÁLISE:
   A obra está 6% abaixo do avanço físico previsto e gastando mais
   por unidade produzida que o orçado. Ação recomendada: revisar
   composição das equipes na etapa de estrutura e reforçar frente
   de trabalho de alvenaria para recuperar o cronograma.

 PRÓXIMAS AÇÕES:
   [ ] Reunião de análise com equipe até [data]
   [ ] Replanejar atividades das semanas S+1 a S+4
   [ ] Verificar suprimento de materiais críticos
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Etapa 8 — Marcos do Projeto (Milestones)

Todo cronograma deve ter **marcos** — eventos pontuais (duração zero) que
representam entregas ou condições contratuais críticas.

### Marcos típicos em obras de edificação:

```
◆ M01 — Ordem de Serviço / Início oficial da obra
◆ M02 — Aprovação do Canteiro e instalações provisórias
◆ M03 — Conclusão das fundações
◆ M04 — Estrutura do último pavimento concluída (Topping Out)
◆ M05 — Cobertura impermeabilizada (obra "fechada")
◆ M06 — Instalações brutas concluídas (rough-in)
◆ M07 — Revestimentos internos concluídos
◆ M08 — Habite-se / Vistoria do Corpo de Bombeiros
◆ M09 — Comissionamento e testes de sistemas
◆ M10 — Entrega das chaves / Recebimento pelo cliente
```

### Para obras públicas (marcos contratuais adicionais):
```
◆ Medições mensais para faturamento (% do contrato)
◆ Prazo para utilização da reserva de contingência
◆ Data-limite para não incidência de multas contratuais
◆ Marco de 50% de execução (geralmente exigido em contratos)
```

---

## Etapa 9 — Cronograma de Suprimentos e Contratações

Todo cronograma físico-financeiro exige um cronograma de **aquisições integrado**,
que antecipa a necessidade de materiais e serviços com os lead times necessários.

### Lead times típicos (Brasil):

| Item | Lead time típico | Observações |
|---|---|---|
| Concreto usinado | 2–5 dias | Agendar com concreteira |
| Estrutura metálica | 30–60 dias | Após projeto aprovado |
| Esquadrias de alumínio | 20–45 dias | Após medição final |
| Esquadrias de madeira | 15–30 dias | Sob medida |
| Elevadores | 60–120 dias | Importados: até 180 dias |
| Ar condicionado VRF | 30–60 dias | Importado ou nacional |
| Porcelanato importado | 45–90 dias | Verificar estoque |
| Louças e metais premium | 15–30 dias | Verificar estoque |
| Gerador | 30–60 dias | Nacional ou importado |

### Modelo de tabela de suprimentos:

```
| Item            | Quant. | Prazo necessário | Lead time | Data de compra | Fornecedor |
|-----------------|--------|-----------------|-----------|----------------|------------|
| Concreto fck25  | 120m³  | Semana 8        | 3 dias    | Semana 7       | [a definir]|
| Estr. metálica  | 8,5t   | Semana 12       | 45 dias   | Semana 5       | [a definir]|
| Esquadrias alum | 48 un  | Semana 22       | 30 dias   | Semana 17      | [a definir]|
...
```

---

## Etapa 10 — Análise de Riscos do Cronograma (PMBOK)

Um cronograma robusto inclui identificação e mitigação de riscos de prazo.

### Riscos típicos em obras de construção civil:

```
CATEGORIA: TEMPO/CLIMA
  R01 — Chuvas intensas no período de escavação/fundações      Alto
  R02 — Períodos de estiagem no Norte/Nordeste (poeira, calor)  Médio

CATEGORIA: SUPRIMENTOS
  R03 — Atraso na entrega de materiais críticos                Alto
  R04 — Ruptura de estoque de insumo específico                Médio
  R05 — Aumento de preço de materiais (inflação/câmbio)        Alto

CATEGORIA: MÃO DE OBRA
  R06 — Rotatividade de mão de obra especializada              Alto
  R07 — Greve ou paralisação de empreiteiros                   Baixo
  R08 — Acidentes de trabalho com impacto no cronograma        Médio

CATEGORIA: PROJETO
  R09 — Alterações de escopo pelo cliente durante a obra       Alto
  R10 — Incompatibilização tardia entre disciplinas            Médio
  R11 — Aprovações e licenças com atraso nos órgãos            Alto

CATEGORIA: FINANCEIRO
  R12 — Atraso de pagamentos do contratante                    Alto
  R13 — Necessidade de aditivo por serviços extra-contratuais  Médio
```

### Buffer de contingência (PMBOK):
```
Reserva de contingência de prazo:
  Conservadora:   10–15% da duração total
  Normal:          5–10% da duração total
  Agressiva:       3–5%  da duração total

Aplicar nas atividades críticas e nos marcos finais.
```

---

## Etapa 11 — Validações e Alertas

Ao finalizar o cronograma, verificar:

```
✅ CHECKLIST DO CRONOGRAMA:
[ ] EAP cobre 100% do escopo (nenhuma atividade "perdida")
[ ] Todas as atividades têm predecessora (exceto a primeira)
[ ] Todas as atividades têm sucessora (exceto a última)
[ ] Soma dos pesos = 100% exato
[ ] Caminho crítico identificado e documentado
[ ] Marcos contratuais respeitados (conferir datas)
[ ] Histograma nivelado (II < 2,0)
[ ] Curva S com formato em "S" (não linear, não exponencial)
[ ] Cronograma de suprimentos integrado (lead times)
[ ] Reserva de contingência de prazo incluída
[ ] Linha de base (baseline) registrada antes do início

⚠️ ALERTAS COMUNS:
- Atividade sem predecessora (exceto início) → erro de lógica
- Pesos que não somam 100% → rebalancear
- Curva S muito linear → distribuição irreal de custos
- Histograma com pico > 3x a média → risco de gargalo de MO
- IDC < 0,80 por mais de 2 medições → intervenção obrigatória
- IDP < 0,70 por mais de 2 medições → replanejar urgente
- IDCN > 1,20 → meta financeira provavelmente inatingível
```

---

## Etapa 12 — Formatos de Saída

| Formato | Conteúdo | Ferramenta |
|---|---|---|
| **Markdown** | Tabelas de atividades, Curva S em texto, relatório EVM | Claude direto |
| **XLSX** | Gantt com fórmulas, Curva S gráfico, histograma | Skill `xlsx` |
| **DOCX** | Relatório completo de planejamento para contrato | Skill `docx` |
| **Texto estruturado** | Para importar em MS Project, Primavera P6, GanttProject | Formato CSV/XML |

### Softwares de referência do mercado:
```
MS Project       — padrão corporativo, integra com Office
Primavera P6     — padrão industrial, obras complexas e EPC
GanttProject     — gratuito, adequado para PME
ProjectLibre     — open source, similar ao MS Project
Sienge/Prevision — integrado ao ERP de construção civil
Trello/Asana     — visual, para equipes ágeis
```

---

## Etapa 13 — Prompts para o Usuário

Prompts prontos para usar com esta skill ou qualquer agente:

---

### Prompt 1 — Cronograma Físico-Financeiro Completo

```
Atue como especialista sênior em planejamento de obras. Elabore um cronograma
físico-financeiro completo para [descrever a obra], com prazo de [X meses] e
orçamento de R$ [valor]. Inclua: EAP estruturada, diagrama de Gantt com atividades
e predecessoras, identificação do caminho crítico (CPM), tabela de desembolso
mensal, Curva S de avanço físico e financeiro, e histograma de mão de obra.
Use metodologia PMI/PMBOK.
```

---

### Prompt 2 — Caminho Crítico (CPM)

```
Calcule o caminho crítico (CPM) para as seguintes atividades: [lista de atividades
com duração e predecessoras]. Apresente: passagem direta e inversa, folgas totais
e livres, identificação das atividades críticas e duração mínima da obra.
```

---

### Prompt 3 — Curva S e Cronograma Financeiro

```
Com base nas atividades e custos abaixo, elabore o cronograma financeiro mensal,
calculando o desembolso por período e o acumulado. Apresente a Curva S em formato
de tabela com percentuais mensais e acumulados. Identifique o pico de desembolso
e o padrão da curva.
Atividades: [lista com duração, período e custo]
```

---

### Prompt 4 — Histograma de Mão de Obra

```
Dimensione o histograma de mão de obra para a obra [descrição], com base nas
atividades e produtividades abaixo. Calcule a equipe necessária por atividade,
consolide por período (mensal), apresente o histograma em formato de tabela e
calcule o índice de irregularidade. Sugira nivelamento se necessário.
```

---

### Prompt 5 — EVM (Controle de Obra em Andamento)

```
Calcule os indicadores de EVM para a obra [nome] na data de medição [data]:
- Orçamento total (OAC): R$ [valor]
- % planejado executado até hoje: [X]%
- % real executado até hoje: [Y]%
- Custo real incorrido até hoje: R$ [valor]
Calcule VP, VA, CR, VC, VPr, IDC, IDP, EAC, VAC e IDCN.
Emita diagnóstico e recomendações.
```

---

### Prompt 6 — Análise de Atraso e Recuperação

```
A obra [descrição] está [X dias/semanas] atrasada em relação ao cronograma baseline.
O caminho crítico passa pelas atividades [lista]. Analise as causas do atraso,
calcule o impacto no prazo de entrega e proponha um plano de recuperação com
aceleração das atividades críticas, remanejamento de recursos e novo cronograma
ajustado. Considere as restrições: [citar restrições].
```

---

### Prompt 7 — Cronograma de Suprimentos

```
Com base no cronograma físico abaixo, elabore o cronograma de suprimentos e
contratações, considerando os lead times dos principais insumos e serviços.
Identifique os itens críticos que precisam ser comprados antes do início da
atividade correspondente. Apresente em tabela com: item, quantidade, data de
necessidade, lead time e data limite de compra.
```

---

## Referências Técnicas e Normativas

| Referência | Aplicação |
|---|---|
| **PMBOK® Guide 7ª Ed.** — PMI | Gestão de projetos, EVM, EAP, marcos |
| **NBR ISO 21500:2021** | Gestão de projetos no contexto brasileiro |
| **Mattos, A.D. — Planejamento e Controle de Obras** (PINI, 2010) | CPM, Curva S, histograma — referência nacional |
| **TCPO Ed. 14** — PINI | Produtividades de mão de obra para dimensionamento |
| **Lei 14.133/2021** | Cronograma físico-financeiro em licitações públicas |
| **Decreto 7.983/2013** | Requisitos de cronograma em obras com recursos federais |
| **NR-18** | Segurança do trabalho — impacta mobilização e cronograma |
| **Lean Construction / Last Planner System** | Planejamento de curto prazo e fluxo contínuo |

---

## Notas do Criador

- Desenvolvida por **Pr. Hélio Paiva Jr.** — Engenheiro Civil, Especialista em Planejamento
- Metodologia baseada em PMI/PMBOK, CPM/PERT, EVM e Mattos (2010)
- Integra com `orcamento-obra` (custos) e `memorial-descritivo-obra` (especificações)
- Versão 1.0 — Abril/2026
