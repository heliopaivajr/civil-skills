---
name: orcamento-obra
description: >
  Elabora orçamentos analíticos de obras de construção civil com múltiplas bases de
  referência: SINAPI (CEF/IBGE), TCPO (PINI), composição própria de mercado ou estrutura
  BIM (ABNT NBR 15965). Use quando o usuário pedir para "fazer um orçamento de obra",
  "orçar um serviço", "montar uma planilha orçamentária", "calcular custo de construção",
  "levantar quantitativos", "compor preço unitário", "verificar custo SINAPI", "usar TCPO",
  "elaborar BDI", "fazer curva ABC de obra", "orçar reforma", "orçar edificação",
  "orçamento BIM", "precificar serviço de engenharia" ou qualquer variação dessas
  expressões em português. Não usar para cronogramas físico-financeiros (use a skill
  cronograma-obra) nem para memoriais descritivos (use memorial-descritivo-obra).
license: MIT
compatibility:
  - claude-code
  - openclaw
  - claude
  - cursor
  - copilot
---

# Orçamento de Obra — Construção Civil

## Visão Geral

Esta skill transforma o agente em um **orçamentista sênior de obras**, dominando múltiplas
bases de referência de custos — SINAPI, TCPO, composição própria de mercado e estruturação
BIM (ABNT NBR 15965) — além de BDI, composições de preços unitários (CPU), curva ABC e
legislação vigente (Lei 14.133/2021 e Decreto 7.983/2013).

O orçamento produzido segue o padrão **analítico** — o mais preciso e exigido em obras
públicas e privadas de médio/grande porte — estruturado em macroetapas, etapas e serviços
com código de referência, descrição, unidade, quantidade, custo unitário e custo total.

A **base de referência** é escolhida pelo usuário na Etapa 0, e toda a estrutura subsequente
se adapta automaticamente à escolha feita.

---

## Quando Usar Esta Skill

**Acione automaticamente quando o usuário mencionar:**
- Orçar / orçamento / orçamentação de obra, serviço, reforma ou construção
- Planilha orçamentária / planilha de custos / planilha de quantitativos
- SINAPI / TCPO / composição de preços / CPU / custo unitário
- BDI / taxa de administração / lucro / custo indireto
- Levantamento de quantitativos / levantamento de serviços
- Curva ABC de insumos ou serviços
- Desoneração / encargos sociais / mão de obra
- Custo m² de construção / custo global de obra
- Cotação de insumos / pesquisa de preços
- Orçamento BIM / classificação ABNT NBR 15965 / Uniclass / Omniclass
- Orçamento paramétrico / estimativa de custo por sistema

**Não acionar quando:**
- O usuário pedir cronograma físico-financeiro → use `cronograma-obra`
- O usuário pedir memorial descritivo → use `memorial-descritivo-obra`
- Perguntas conceituais gerais sem intenção de produzir documento

---

## Etapa 0 — Seleção da Base de Referência

**Esta é a primeira pergunta a fazer.** A escolha da base define códigos, formato de
planilha, nível de detalhe e compatibilidade legal do orçamento.

Apresentar ao usuário as opções abaixo e aguardar resposta antes de prosseguir:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 BASE DE REFERÊNCIA — Qual deseja usar neste orçamento?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 [1] SINAPI      — Padrão CEF/IBGE, obrigatório em obras federais
 [2] TCPO        — Padrão PINI, referência privada de mercado
 [3] Própria     — Composições próprias com cotação de mercado
 [4] BIM/ABNT    — Estrutura paramétrica ABNT NBR 15965
 [5] Mista       — SINAPI como base + complemento TCPO ou cotação
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

> Se o usuário não souber escolher, recomendar:
> - Obra pública / licitação → **[1] SINAPI**
> - Obra privada com projeto executivo completo → **[2] TCPO** ou **[5] Mista**
> - Orçamento rápido / sem tabela de referência → **[3] Própria**
> - Projeto em BIM (Revit, Archicad, etc.) → **[4] BIM/ABNT**

---

### BASE [1] — SINAPI (Sistema Nacional de Pesquisa de Custos e Índices)

**Responsável:** Caixa Econômica Federal + IBGE
**Atualização:** Mensal, por UF
**Acesso:** Gratuito — https://www.caixa.gov.br/sinapi
**Obrigatoriedade:** Lei 14.133/2021 e Decreto 7.983/2013 — obras com recursos federais

**Quando usar:**
- Obras públicas federais, estaduais ou municipais (licitações)
- Obras do MCMV, PAC, convênios com União
- Quando o cliente ou edital exige referência SINAPI
- Para obras privadas que desejam respaldo técnico-legal

**Estrutura do código SINAPI:**
```
Código: NNNNN (5 dígitos numéricos)
Exemplos:
  87864 → Concreto fck=25MPa bombeado
  92793 → Alvenaria de vedação tijolo 9cm
  88262 → Pedreiro (custo horário)
  94219 → Impermeabilização com manta asfáltica
```

**Comportamento da skill com SINAPI:**
- Usar obrigatoriamente UF + mês de referência + versão (desonerado/não desonerado)
- Alertar quando o serviço não tiver código SINAPI disponível
- Calcular BDI conforme limites do Acórdão TCU 2622/2013
- Encargos sociais já inclusos nas composições (exceto Administração Local)

---

### BASE [2] — TCPO (Tabela de Composições de Preços para Orçamentos)

**Responsável:** Editora PINI (hoje integrada ao Sienge/Softplan)
**Atualização:** Edição 14 (impressa) + atualizações digitais
**Acesso:** Pago — licença PINI ou plataformas integradas (Sienge, Volare)
**Referência:** Padrão de mercado privado, amplamente usado em construtoras

**Quando usar:**
- Obras privadas (residencial, comercial, industrial) sem obrigatoriedade de SINAPI
- Projetos onde se prefere composições mais alinhadas ao mercado real
- Quando a construtora já tem licença TCPO ativa
- Orçamentos para incorporadoras e investidores privados

**Estrutura do código TCPO:**
```
Código: XX.XX.XX.XX (hierarquia por capítulos)
Exemplos:
  04.01.02.01 → Escavação manual de vala até 1,5m
  07.01.01.01 → Forma de madeira para pilares
  11.02.03.01 → Revestimento cerâmico piso 33x33cm
```

**Diferenças em relação ao SINAPI:**
- Composições refletem produtividade de mercado (nem sempre igual ao SINAPI)
- Não tem força legal para obras públicas federais
- Preços de insumos precisam ser pesquisados / atualizados regionalmente
- Mais detalhado em acabamentos e serviços especiais

**Comportamento da skill com TCPO:**
- Usar código TCPO no campo de código; registrar edição de referência
- Preços unitários devem ser informados pelo usuário ou estimados por cotação
- BDI sem limitação de TCU — usar referência de mercado regional
- Alertar que preços precisam de atualização pela variação do INCC

---

### BASE [3] — Composição Própria / Cotação de Mercado

**Quando usar:**
- Quando não há código SINAPI nem TCPO para o serviço
- Reformas simples sem necessidade de respaldo legal
- Obras com materiais ou métodos construtivos específicos / regionais
- Orçamentos rápidos para clientes privados com base em cotação real

**Estrutura do código próprio:**
```
Prefixo: COMP-NNN (composição própria numerada)
Exemplos:
  COMP-001 → Fachada ventilada com perfis especiais
  COMP-002 → Piso de pedra cariri assentado
  COMP-003 → Cobertura com telha ecológica reciclada
```

**Comportamento da skill com Composição Própria:**
- Montar a composição analítica detalhada (conforme Etapa 8)
- Registrar fonte dos preços: cotação, NF de compra, lista de fornecedor, etc.
- Calcular encargos sociais e BDI manualmente conforme regime do contratado
- Incluir memória de cálculo justificando cada coeficiente adotado

---

### BASE [4] — BIM / ABNT NBR 15965 (Classificação da Informação da Construção)

**Responsável:** ABNT — Associação Brasileira de Normas Técnicas
**Norma:** ABNT NBR 15965 (partes 1 a 7) — Sistema de Classificação da Informação
**Alinhamento internacional:** Omniclass (EUA) / Uniclass (Reino Unido) / IFC
**Decreto BIM:** Decreto 9.983/2019 — implantação gradual obrigatória no setor público

**Quando usar:**
- Projetos desenvolvidos em BIM (Revit, Archicad, Allplan, etc.)
- Quando o cliente exige entrega em IFC com classificação de elementos
- Projetos de maior complexidade que precisam de rastreabilidade total
- Obras públicas de grande porte com exigência de BIM Level 2+

**Estrutura de classificação NBR 15965:**
```
Parte 1 — Terminologia e estrutura geral
Parte 2 — Características dos objetos da construção
Parte 3 — Processos da construção
Parte 4 — Recursos da construção
Parte 5 — Resultados da construção (produtos/entregas)
Parte 6 — Propriedades e grandezas
Parte 7 — Informação da construção (documentação)
```

**Hierarquia de orçamento BIM (adaptada ao BR):**
```
Nível 1 — Sistema (ex: Estrutura)
  Nível 2 — Subsistema (ex: Estrutura de Concreto Armado)
    Nível 3 — Elemento (ex: Pilares)
      Nível 4 — Componente (ex: Pilar retangular 30x60cm)
        Nível 5 — Serviço (ex: Fôrma + Armação + Concretagem)
```

**Código de exemplo (Uniclass adaptado):**
```
Ss_20_10_15 → Fundações rasas (sapatas isoladas)
Ss_25_10_25 → Estrutura de concreto armado moldado in loco
Ss_35_10_10 → Alvenaria de vedação interna
En_55_10_30 → Instalações hidráulicas prediais — água fria
En_60_10_15 → Instalações elétricas — baixa tensão
```

**Comportamento da skill com BIM/ABNT:**
- Estruturar o orçamento por **sistemas construtivos** (não por etapa de execução)
- Usar códigos de classificação NBR 15965 / Uniclass no campo de código
- Os preços unitários podem vir do SINAPI, TCPO ou cotação — declarar a fonte
- Compatível com extração de quantitativos direto do modelo BIM via IFC/QTO
- Gerar tabela em formato compatível com Navisworks, Revit QTO, Dalux

---

### BASE [5] — Mista (SINAPI + Complemento TCPO ou Cotação)

**Quando usar:**
- A maioria dos serviços tem código SINAPI, mas alguns itens especiais não
- Obras públicas com itens que exigem composição complementar
- Melhor equilíbrio entre respaldo legal (SINAPI) e realidade de mercado

**Comportamento da skill com Base Mista:**
- SINAPI como base principal para todos os itens disponíveis
- Para itens sem SINAPI: usar TCPO com nota de fonte, ou composição própria justificada
- Registrar na planilha a **fonte de cada item** (coluna extra "Base")
- BDI segue regras TCU para a parcela SINAPI; justificar itens complementares
- Percentual de itens fora do SINAPI não deve ultrapassar 20% do CDT em obras públicas

**Coluna extra na planilha mista:**
```
| Cód.         | Base    | Descrição              | Und | Quant. | C.Unit.  | C.Total   |
|--------------|---------|------------------------|-----|--------|----------|-----------|
| 87864        | SINAPI  | Concreto fck=25MPa     | m³  |  42,50 |   512,34 | 21.774,45 |
| 04.01.02.01  | TCPO    | Escavação manual vala  | m³  |  18,00 |    38,20 |    687,60 |
| COMP-001     | Própria | Fachada em pedra cariri| m²  | 120,00 |   280,00 | 33.600,00 |
```

---

## Etapa 1 — Coleta de Contexto Obrigatório

Antes de qualquer cálculo, colete estas informações. Se não forem fornecidas,
**pergunte explicitamente** na seguinte ordem:

```
1. Tipo de obra: edificação residencial / comercial / industrial / reforma / infraestrutura
2. Estado (UF): para selecionar a tabela SINAPI correta
3. Mês de referência: se não informado, usar o mês atual
4. Desoneração: com desoneração ou sem desoneração da folha de pagamento
5. Regime tributário do contratado: Simples / Lucro Presumido / Lucro Real (para BDI)
6. Natureza: obra pública (licitação) ou obra privada
7. Projeto disponível: há projetos, plantas, especificações técnicas? Quais?
8. Área construída (m²) ou escopo resumido da obra
```

> **Regra de ouro:** Nunca inicie os cálculos sem UF e tipo de obra confirmados.

---

## Etapa 2 — Estrutura do Orçamento Analítico

Organize o orçamento obrigatoriamente nas seguintes **macroetapas** (adaptáveis ao tipo
de obra). Use numeração hierárquica no formato `X.Y.Z`:

```
1.  SERVIÇOS PRELIMINARES
    1.1  Mobilização e instalação do canteiro
    1.2  Tapumes, placas e cercamentos
    1.3  Ligações provisórias (água, luz, esgoto)
    1.4  Locação da obra

2.  SERVIÇOS DE TERRAPLENAGEM E MOVIMENTO DE TERRA
    2.1  Limpeza e destocamento do terreno
    2.2  Escavação manual / mecanizada
    2.3  Aterro compactado
    2.4  Transporte de material excedente

3.  FUNDAÇÕES
    3.1  Fundação direta (radier, sapata, viga baldrame)
    3.2  Fundação profunda (estacas, tubulões)
    3.3  Impermeabilização de fundações

4.  ESTRUTURA
    4.1  Formas (madeira / metálica / plástica)
    4.2  Armadura (aço CA-50 / CA-60)
    4.3  Concreto (usinado / dosado em obra)
    4.4  Estrutura metálica / pré-moldada (se aplicável)
    4.5  Lajes (maciça / nervurada / treliçada / pré-fabricada)

5.  ALVENARIA E VEDAÇÃO
    5.1  Alvenaria de vedação (tijolo / bloco de concreto / cerâmico)
    5.2  Vergas e contravergas
    5.3  Divisórias internas (se aplicável)

6.  COBERTURA
    6.1  Estrutura de madeira / metálica para telhado
    6.2  Telhas (cerâmica / metálica / fibrocimento / shingle)
    6.3  Rufos, calhas e condutores
    6.4  Impermeabilização de laje de cobertura

7.  INSTALAÇÕES HIDROSSANITÁRIAS
    7.1  Instalação de água fria
    7.2  Instalação de água quente (se aplicável)
    7.3  Instalação de esgoto sanitário
    7.4  Instalação de águas pluviais
    7.5  Louças e metais sanitários
    7.6  Caixa d'água e reservatório

8.  INSTALAÇÕES ELÉTRICAS E DE LÓGICA
    8.1  Instalação elétrica (baixa tensão)
    8.2  Quadros de distribuição e disjuntores
    8.3  Rede de dados / lógica / CFTV (se aplicável)
    8.4  Para-raios (SPDA) (se aplicável)
    8.5  Gerador / nobreak (se aplicável)

9.  REVESTIMENTOS INTERNOS
    9.1  Chapisco e emboço (reboco)
    9.2  Gesso liso / drywall / PVC
    9.3  Azulejos e revestimentos cerâmicos
    9.4  Pintura interna

10. REVESTIMENTOS EXTERNOS
    10.1 Chapisco e emboço externo
    10.2 Revestimento externo (textura / ACM / pastilha)
    10.3 Pintura externa / selador / primer

11. PISOS E CONTRAPISO
    11.1 Lastro de concreto e contrapiso
    11.2 Piso cerâmico / porcelanato
    11.3 Piso cimentado / epóxi / taco (conforme projeto)

12. ESQUADRIAS E VIDROS
    12.1 Portas de madeira / metálicas
    12.2 Janelas de alumínio / PVC / ferro
    12.3 Vidros e espelhos
    12.4 Ferragens e fechaduras

13. INSTALAÇÕES ESPECIAIS (conforme escopo)
    13.1 Ar condicionado (previsão de infraestrutura)
    13.2 Sistema de combate a incêndio
    13.3 Elevadores (se aplicável)
    13.4 Instalações de gás

14. SERVIÇOS COMPLEMENTARES E PAISAGISMO
    14.1 Limpeza final da obra
    14.2 Calçadas, meio-fios, estacionamento
    14.3 Paisagismo e jardins (se aplicável)
    14.4 Muro de fechamento / gradil

15. BDI — BENEFÍCIOS E DESPESAS INDIRETAS
    (Item separado, incide sobre o custo direto total)
```

---

## Etapa 3 — Formato da Planilha Orçamentária

Cada item deve ser apresentado em tabela com as seguintes colunas:

| Cód. SINAPI | Descrição do Serviço | Und | Quant. | Custo Unit. (R$) | Custo Total (R$) |
|:-----------:|:---------------------|:---:|-------:|----------------:|----------------:|
| 87864       | Concreto fck=25MPa lançado c/ bomba | m³ | 42,50 | 512,34 | 21.774,45 |

**Regras de preenchimento:**
- Código SINAPI no formato `NNNNN` (5 dígitos) ou `NNNNN_P` para composição principal
- Se não houver código SINAPI, usar prefixo `SIN` + código interno ou `COMP` para composição própria
- Unidade conforme padrão SINAPI: m², m³, m, kg, un, vb, h, mês
- Quantidades com 2 casas decimais
- Custos unitários com 2 casas decimais, em R$
- Custo total = Quant × Custo Unit (calculado automaticamente)

---

## Etapa 4 — Cálculo do BDI

O BDI (Benefícios e Despesas Indiretas) incide sobre o **custo direto total** e deve ser
calculado conforme a natureza da obra.

### Fórmula do BDI (Acórdão TCU 2622/2013):

```
BDI = [(1 + AC + S + R + G) × (1 + DF) × (1 + L) / (1 - I)] - 1

Onde:
  AC = Administração central (2,0% a 3,5%)
  S  = Seguros e garantias (0,3% a 0,8%)
  R  = Risco (0,5% a 1,5%)
  G  = Garantias (0,3% a 0,5%)
  DF = Despesas financeiras (0,5% a 1,3%)
  L  = Lucro (5,5% a 8,96%)
  I  = Impostos (PIS + COFINS + ISS + CPRB conforme regime)
```

### Referências de BDI por tipo de obra (TCU):

| Tipo de Obra | BDI Referencial |
|---|---|
| Edificações (obras públicas) | 24,23% (desonerado) / 22,12% (não desonerado) |
| Instalações e serviços de engenharia | 22% a 25% |
| Obras de saneamento e infraestrutura | 20% a 24% |
| Obras privadas (estimativa) | 20% a 35% |

> **Atenção:** Para obras públicas, o BDI deve seguir os limites do Acórdão TCU 2622/2013.
> O ISS é excluído do BDI quando já incluído nas composições unitárias.

### Aplicação:

```
Custo Direto Total (CDT) = soma de todos os serviços
Custo com BDI = CDT × (1 + BDI%)
Custo Global da Obra = Custo com BDI
```

---

## Etapa 5 — Encargos Sociais e Desoneração

### Sem Desoneração (regime normal — INSS 20% sobre folha):
- Encargos Sociais sobre MO = ~118% a ~150% (varia por categoria)
- O SINAPI já inclui esses encargos nas composições

### Com Desoneração (Lei 12.546/2011 — CPRB):
- Substituição do INSS patronal por CPRB (4,5% sobre faturamento)
- Tabelas SINAPI disponíveis em versão desonerada e não desonerada
- Escolha conforme o regime tributário efetivo do contratado

> **Regra:** Usar a mesma versão (desonerada/não desonerada) em todo o orçamento.
> Nunca misturar as duas versões na mesma planilha.

---

## Etapa 6 — Curva ABC de Serviços e Insumos

Após estruturar o orçamento, gerar automaticamente a **Curva ABC**:

### Curva ABC de Serviços:
1. Listar todos os itens por custo total (decrescente)
2. Calcular percentual individual e acumulado sobre o custo direto total
3. Classificar:
   - **Classe A:** itens que somam até 80% do custo (normalmente 10-20% dos itens)
   - **Classe B:** itens entre 80% e 95%
   - **Classe C:** demais itens (menos críticos, mas numerosos)

### Apresentar análise:
```
Exemplo de saída:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CURVA ABC — TOP 10 SERVIÇOS (Classe A)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Concreto estrutural fck=25MPa    R$ 48.200  → 18,4% (acum: 18,4%)
2. Armadura CA-50 (corte/dobra)     R$ 32.100  → 12,3% (acum: 30,7%)
3. Alvenaria de vedação 14cm        R$ 28.900  → 11,0% (acum: 41,7%)
...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Etapa 7 — Estimativas e Tipos de Orçamento

Conforme o nível de detalhamento disponível, adotar o tipo adequado:

| Tipo | Quando Usar | Precisão | Referência |
|---|---|---|---|
| **Estimativa de Custo** | Estudo de viabilidade, sem projeto | ±30% | CUB/m² |
| **Orçamento Preliminar** | Anteprojeto / partido arquitetônico | ±20% | SINAPI paramétrico |
| **Orçamento Analítico** | Projeto básico ou executivo completo | ±5 a 10% | SINAPI composições |
| **Orçamento Executivo** | Projeto + especificações + quantitativos | ±2 a 5% | SINAPI + cotação mercado |

### CUB como estimativa rápida:
```
Custo estimado = Área construída (m²) × CUB (R$/m²) × Fator de padrão

Padrões (ABNT NBR 12.721):
  Residencial Popular (RP):    CUB × 0,80
  Residencial Baixo Padrão (R1): CUB × 0,90
  Residencial Normal (R8):    CUB × 1,00
  Residencial Alto Padrão (R16): CUB × 1,20
  Comercial / Salas e Lojas (CSL): CUB × 1,10
```

---

## Etapa 8 — Composições Próprias (Sem Código SINAPI)

Quando um serviço não possui código SINAPI, montar **composição analítica própria**:

```markdown
### COMPOSIÇÃO PRÓPRIA — [Nome do Serviço]
Código: COMP-001
Unidade: m²

| Insumo | Código SINAPI | Und | Coef. | Preço Unit. (R$) | Subtotal (R$) |
|--------|--------------|-----|------:|----------------:|-------------:|
| Mão de obra (pedreiro) | 88262 | h | 0,80 | 24,50 | 19,60 |
| Mão de obra (servente)  | 88316 | h | 0,40 | 18,30 |  7,32 |
| Material X              | XXXXX | kg | 2,50 | 12,00 | 30,00 |
| Equipamento (betoneira) | 92767 | h | 0,20 | 15,60 |  3,12 |

Custo Direto Unitário: R$ 60,04
```

---

## Etapa 9 — Administração Local (AL)

Calcular separadamente os custos de **Administração Local da Obra**, incluindo:

```
- Engenheiro responsável: salário + encargos + EPI
- Mestre de obras / encarregado: salário + encargos
- Técnico de segurança (NR-18): salário + encargos
- Almoxarife / apontador: salário + encargos
- Veículo de obra (combustível, manutenção)
- Energia elétrica do canteiro
- Água de consumo do canteiro
- Comunicação (telefone, internet)
- Material de escritório e informática
- Equipamentos de topografia (aluguéis)
- Equipamentos de segurança coletiva (NR-18)
- Placa de obra (conforme legislação)
```

> Os encargos sociais sobre a Administração Local são calculados à parte,
> pois não estão incluídos nas composições SINAPI de custo unitário.

---

## Etapa 10 — Resumo Geral do Orçamento

Sempre apresentar ao final um **quadro-resumo** estruturado:

```
╔══════════════════════════════════════════════════════════════╗
║                  RESUMO GERAL DO ORÇAMENTO                   ║
╠══════════════════════════════════════════════════════════════╣
║ Obra:     [Nome da obra]                                      ║
║ Local:    [Cidade / UF]                                       ║
║ Referência SINAPI: [Mês/Ano] — [Desonerado/Não Desonerado]   ║
║ Data de elaboração: [Data]                                    ║
╠══════════════════════════════════════════════════════════════╣
║ 1. SERVIÇOS PRELIMINARES             R$    XX.XXX,XX          ║
║ 2. TERRAPLENAGEM                     R$    XX.XXX,XX          ║
║ 3. FUNDAÇÕES                         R$    XX.XXX,XX          ║
║ 4. ESTRUTURA                         R$    XX.XXX,XX          ║
║ 5. ALVENARIA E VEDAÇÃO               R$    XX.XXX,XX          ║
║ 6. COBERTURA                         R$    XX.XXX,XX          ║
║ 7. INSTALAÇÕES HIDROSSANITÁRIAS      R$    XX.XXX,XX          ║
║ 8. INSTALAÇÕES ELÉTRICAS             R$    XX.XXX,XX          ║
║ 9. REVESTIMENTOS INTERNOS            R$    XX.XXX,XX          ║
║ 10. REVESTIMENTOS EXTERNOS           R$    XX.XXX,XX          ║
║ 11. PISOS E CONTRAPISO               R$    XX.XXX,XX          ║
║ 12. ESQUADRIAS E VIDROS              R$    XX.XXX,XX          ║
║ 13. INSTALAÇÕES ESPECIAIS            R$    XX.XXX,XX          ║
║ 14. SERVIÇOS COMPLEMENTARES          R$    XX.XXX,XX          ║
╠══════════════════════════════════════════════════════════════╣
║ CUSTO DIRETO TOTAL (CDT)             R$   XXX.XXX,XX          ║
║ BDI (XX%)                            R$    XX.XXX,XX          ║
╠══════════════════════════════════════════════════════════════╣
║ CUSTO GLOBAL DA OBRA                 R$   XXX.XXX,XX          ║
║ Custo por m² (área construída)       R$     X.XXX,XX/m²       ║
╚══════════════════════════════════════════════════════════════╝
```

---

## Etapa 11 — Validações e Alertas

Ao finalizar o orçamento, verificar e alertar sobre:

```
✅ VERIFICAÇÕES OBRIGATÓRIAS:
[ ] UF e mês de referência SINAPI corretos
[ ] Versão (desonerado/não desonerado) consistente em todo o orçamento
[ ] BDI dentro dos limites TCU para obras públicas
[ ] Administração local calculada separadamente
[ ] Todos os serviços têm código SINAPI ou composição própria justificada
[ ] Custo por m² está dentro da faixa aceitável para o tipo/padrão de obra
[ ] Itens Classe A da Curva ABC representam ≤ 20% dos itens e ≥ 70% do custo

⚠️ ALERTAS COMUNS:
- Custo por m² muito abaixo do CUB: possível subquantitativo
- BDI acima de 30% em obras públicas: exige justificativa técnica
- Serviços sem código SINAPI > 20% do CDT: risco de impugnação em licitação
- Mês de referência com mais de 6 meses: considerar atualização pelo INCC ou IPCA
```

---

## Etapa 12 — Saída e Formato de Entrega

### Formatos disponíveis (perguntar ao usuário):

1. **Markdown** — para visualização rápida no Claude/Obsidian
2. **XLSX** — planilha Excel com cálculos automáticos (requer skill xlsx)
3. **DOCX** — documento Word formatado (requer skill docx)
4. **Texto estruturado** — para copiar em sistema de orçamento (Sienge, Volare, OrçaFácil)

### Estrutura mínima de qualquer saída:

```
[Cabeçalho com dados da obra]
[Planilha orçamentária por macroetapas]
[Quadro de BDI]
[Curva ABC — Top 10 itens]
[Resumo Geral]
[Notas e premissas adotadas]
```

---

## Referências Técnicas e Normativas

| Documento | Aplicação |
|---|---|
| SINAPI — CEF/IBGE (tabelas mensais) | Preços de insumos e composições |
| Decreto 7.983/2013 | Uso obrigatório do SINAPI em obras federais |
| Lei 14.133/2021 | Nova Lei de Licitações e Contratos |
| Acórdão TCU 2622/2013 | Limites de BDI para obras públicas |
| ABNT NBR 12.721 | Custo unitário básico (CUB) e padrões |
| NR-18 | Condições de segurança em obras |
| Mattos, A. D. — *Como preparar orçamentos de obras* | Referência técnica nacional |
| TCPO — PINI | Tabela de Composições de Preços para Orçamentos |

---

## Exemplos de Invocação

**Explícito (Claude Code / OpenClaw):**
```
/orcamento-obra
```

**Implícito (por descrição):**
```
"Preciso orçar a construção de uma casa de 120m² em Recife, PE"
"Qual o custo de revestimento cerâmico interno pelo SINAPI de Pernambuco?"
"Monte uma planilha orçamentária para reforma de banheiro"
"Orçamento analítico para obra pública — escola em Maceió/AL"
"Quanto custa construir um galpão industrial de 500m² em Paulista/PE?"
```

---

## Notas do Criador

- Desenvolvida por **Pr. Hélio Paiva Jr.** — Engenheiro Civil, Orçamentista
- Especializada no contexto **brasileiro**, tabelas SINAPI e legislação nacional
- Integra com o projeto **ObraPrice** (SaaS de orçamentação automatizada)
- Para customização por estado ou tipo de obra, ajuste as macroetapas da Etapa 2
- Versão 1.0 — Abril/2026

---

## Como Instalar

### Via agentskill.sh (quando publicada):
```bash
npx @agentskill.sh/cli@latest install @heliopaivajr/orcamento-obra
```

### Manual — Claude Code:
```bash
# Criar pasta da skill no projeto
mkdir -p .claude/skills/orcamento-obra

# Copiar este arquivo
cp SKILL.md .claude/skills/orcamento-obra/SKILL.md
```

### Manual — OpenClaw (Logos):
```bash
# Copiar para a pasta de skills do OpenClaw
cp SKILL.md ~/openclaw/skills/orcamento-obra/SKILL.md
```

### Manual — Obsidian (MySkills):
```
Salvar em: C:\Users\helio\OneDrive\_OBISIDIAN HELIO JR\MySkills\orcamento-obra\SKILL.md
```

### Via GitHub (MySkills repo):
```bash
# No repositório heliopaivajr/MySkills
git clone https://github.com/heliopaivajr/MySkills
cp -r orcamento-obra/ MySkills/skills/
cd MySkills && git add . && git commit -m "feat: add orcamento-obra skill" && git push
```

### Invocação direta no Claude Code:
```
/learn @heliopaivajr/orcamento-obra
```
