---
name: memorial-descritivo-obra
description: >
  Elabora memoriais descritivos técnicos completos para obras de construção civil,
  arquitetura, reforma, retrofit e instalações. Use quando o usuário pedir para
  "fazer um memorial descritivo", "escrever memorial de obra", "memorial técnico",
  "memorial de acabamentos", "memorial de instalações", "memorial de arquitetura",
  "descrever materiais e serviços da obra", "memorial para orçamento", "memorial
  para licitação", "memorial as built", "especificação técnica de obra" ou qualquer
  variação dessas expressões em português. A skill atua como especialista sênior
  fazendo perguntas técnicas antes de redigir, garantindo documento útil para
  orçamento, compras, planejamento e execução. Não usar para orçamentos
  (use orcamento-obra) nem para cronogramas (use cronograma-obra).
license: MIT
compatibility:
  - claude-code
  - openclaw
  - claude
  - cursor
  - copilot
---

# Memorial Descritivo de Obra — Construção Civil, Arquitetura e Instalações

## Visão Geral

Esta skill transforma o agente em um **especialista sênior em memoriais descritivos**,
combinando domínio técnico de construção civil, arquitetura e instalações com capacidade
de diagnóstico de lacunas, compatibilização entre disciplinas e redação objetiva.

O memorial produzido não é um "anexo decorativo". Ele funciona como:
- base técnica para orçamento e quantitativos
- referência para compras e suprimentos
- guia de execução em campo
- instrumento de compatibilização entre disciplinas
- registro do padrão construtivo adotado
- documento de apoio contratual e rastreabilidade

> **Princípio fundamental:** A IA organiza, acelera, sugere e aponta lacunas.
> O técnico valida, corrige, define e assina. Responsabilidade técnica é sempre humana.

---

## Quando Usar Esta Skill

**Acione automaticamente quando o usuário mencionar:**
- Memorial descritivo / memorial técnico / memorial de obra
- Memorial de acabamentos / memorial de instalações / memorial de arquitetura
- Especificação técnica de materiais e serviços
- Caderno de especificações / caderno técnico
- Memorial para licitação / memorial para orçamento
- Memorial as built / memorial de entrega
- Descrever materiais, acabamentos, sistemas ou soluções construtivas
- Tabela de acabamentos por ambiente

**Não acionar quando:**
- Usuário pedir orçamento → use `orcamento-obra`
- Usuário pedir cronograma → use `cronograma-obra`
- Perguntas conceituais sem intenção de produzir documento

---

## Etapa 0 — Entendimento do Tipo de Memorial

**Antes de qualquer pergunta técnica**, identificar o tipo de memorial necessário.
Se o usuário não informou, perguntar:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 TIPO DE MEMORIAL — Qual é o objetivo deste documento?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 [1] Obra nova         — edificação completa do zero
 [2] Reforma / retrofit — intervenção em edificação existente
 [3] Ampliação         — acréscimo em edificação existente
 [4] Instalações       — memorial específico de MEP (hidro/elétrico/AR)
 [5] Interiores        — acabamentos, mobiliário fixo e ambientes
 [6] As built          — registro do que foi efetivamente executado
 [7] Licitação pública — memorial no padrão exigido por editais
 [8] Orçamentação      — versão otimizada para levantamento de custos
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Etapa 1 — Coleta de Contexto (Perguntas Técnicas)

Após identificar o tipo, fazer as perguntas abaixo **em blocos**, não todas de uma vez.
Adaptar as perguntas conforme o tipo escolhido na Etapa 0.

### Bloco A — Identificação Geral (sempre perguntar)

```
1. Nome / descrição resumida da obra
2. Endereço e município (UF)
3. Nome do cliente / contratante
4. Responsável técnico (engenheiro ou arquiteto) e número do registro (ART/RRT)
5. Fase do projeto: estudo preliminar / anteprojeto / projeto básico / executivo
6. Disciplinas contempladas neste memorial:
   [ ] Arquitetura e construção civil
   [ ] Estrutura
   [ ] Instalações hidrossanitárias
   [ ] Instalações elétricas e lógica
   [ ] Climatização / exaustão / ventilação
   [ ] Incêndio e segurança
   [ ] Acessibilidade (NBR 9050)
   [ ] Áreas externas / urbanização
   [ ] Todas as anteriores
7. Qual o uso principal do memorial?
   [ ] Orçamento e compras
   [ ] Execução em campo
   [ ] Contrato com cliente
   [ ] Licitação pública
   [ ] Entrega / as built
```

### Bloco B — Documentos Disponíveis

```
8. Quais projetos / documentos você possui para enviar ou descrever?
   [ ] Projeto arquitetônico (plantas, cortes, fachadas)
   [ ] Projeto de interiores / layout
   [ ] Projeto estrutural
   [ ] Projeto hidrossanitário
   [ ] Projeto elétrico
   [ ] Projeto de climatização
   [ ] Projeto de incêndio
   [ ] Projeto de SPDA
   [ ] Perspectivas / renders / imagens 3D
   [ ] Briefing ou programa do cliente
   [ ] Orçamento preliminar existente
   [ ] Nenhum — vou descrever verbalmente
9. Pode enviar os arquivos agora? (PDF, imagens, texto)
```

> Se o usuário enviar arquivos, executar diagnóstico técnico antes de redigir
> (ver Etapa 2). Se descrever verbalmente, prosseguir para Bloco C.

### Bloco C — Caracterização da Obra

```
10. Tipo de edificação: residencial / comercial / industrial / institucional / misto
11. Área total construída (m²) — aproximada se não souber
12. Número de pavimentos
13. Padrão construtivo: popular / econômico / médio / alto / luxo
14. Sistema estrutural: concreto armado / metálica / alvenaria estrutural / madeira / misto
15. Já existe definição de acabamentos? (sim / parcialmente / não)
16. Há ambientes ou disciplinas com especificação já fechada?
```

### Bloco D — Perguntas por Disciplina (conforme escopo marcado no Bloco A)

Fazer apenas as perguntas das disciplinas selecionadas:

**Arquitetura e Construção Civil:**
```
- Sistema de vedação: tijolo / bloco de concreto / drywall / misto?
- Revestimento interno de parede: reboco + pintura / gesso / cerâmica / outro?
- Revestimento externo: textura / ACM / pastilha / pintura / outro?
- Tipologia de piso por ambiente (se souber)
- Forro: laje aparente / gesso / drywall / PVC / madeira / nenhum?
- Esquadrias: alumínio / ferro / madeira / PVC / misto?
- Vidros: comum / temperado / laminado / insulado / especificação aberta?
- Cobertura: telha cerâmica / metálica / fibrocimento / shingle / laje impermeabilizada?
```

**Estrutura:**
```
- Fundação prevista: direta (sapata/radier/baldrame) ou profunda (estaca/tubulão)?
- Laje: maciça / nervurada / treliçada / pré-moldada / steel deck?
- Há contenções, muros de arrimo ou estruturas especiais?
```

**Instalações Hidrossanitárias:**
```
- Água fria: ramal da rua ou poço?
- Água quente: chuveiro elétrico / aquecedor a gás / solar / bomba de calor?
- Esgoto: rede pública ou fossa/sumidouro?
- Louças e metais: padrão popular / médio / alto — ou marca/linha já definida?
- Caixa d'água: fibra / concreto / aço inox — capacidade prevista?
```

**Instalações Elétricas:**
```
- Tensão: monofásica / bifásica / trifásica?
- Entrada: aérea ou subterrânea?
- Há gerador, nobreak ou energia solar fotovoltaica?
- Automação residencial / predial prevista?
- Rede de dados, CFTV ou controle de acesso?
- Cargas especiais: elevador, ar condicionado central, cozinha industrial?
```

**Climatização:**
```
- Sistema: split convencional / VRF / central / janela / sem definição?
- Há exaustão mecânica em banheiros, cozinha, área técnica?
- Renovação de ar prevista (ambientes com ocupação intensa)?
```

**Incêndio:**
```
- Uso sujeito a aprovação no Corpo de Bombeiros? (área > 750m² ou uso específico)
- Sistemas previstos: extintores / hidrantes / sprinkler / alarme / emergência?
```

---

## Etapa 2 — Diagnóstico Técnico (quando há arquivos)

Se o usuário enviou projetos ou documentos, executar diagnóstico **antes** de redigir.
Analisar cada disciplina e classificar cada item em:

```
[A] DEFINIDO       — pode entrar direto no memorial
[B] PARCIAL        — entra com observação de complementação
[C] OMISSO         — marcar como [PENDENTE DE DEFINIÇÃO]
[D] CONTRADITÓRIO  — tratar como conflito de projeto, não apenas ausência
```

### Checklist de diagnóstico por disciplina:

**Arquitetura:**
- [ ] Identificação de todos os ambientes com nome e área
- [ ] Cotas, níveis e pé-direito definidos
- [ ] Tipologia de piso por ambiente
- [ ] Revestimento de parede por ambiente
- [ ] Forro / teto por ambiente
- [ ] Pintura (tipo, cor, marca — ou referência)
- [ ] Bancadas descritas (material, dimensões)
- [ ] Louças e metais especificados
- [ ] Esquadrias: tipologia, dimensões, material, acabamento
- [ ] Ferragens definidas (marca/padrão)
- [ ] Vidros especificados (espessura, tipo)
- [ ] Cobertura: sistema, telha, estrutura
- [ ] Impermeabilização: sistema, áreas aplicadas
- [ ] Fachadas: revestimento, pintura, elementos especiais
- [ ] Áreas externas: piso, paisagismo, muro, gradil
- [ ] Acessibilidade: rampas, piso tátil, sanitário acessível

**Estrutura:**
- [ ] Sistema estrutural definido e coerente com arquitetura
- [ ] Tipo de fundação compatível com sondagem/solo
- [ ] Lajes, pilares e vigas com especificação de concreto (fck)
- [ ] Shafts e passagens para instalações marcados
- [ ] Reservatórios estruturais descritos
- [ ] Contenções e arrimos, se aplicável

**Hidrossanitário:**
- [ ] Pontos de água fria e quente por ambiente
- [ ] Esgoto sanitário e ventilação
- [ ] Águas pluviais (calhas, condutores, destino)
- [ ] Reservação (volume, material, localização)
- [ ] Louças, cubas e metais por ambiente
- [ ] Caixas de inspeção e gordura
- [ ] Rede externa e ligação pública

**Elétrico:**
- [ ] Padrão de entrada e medição
- [ ] Quadros de distribuição (QD) localizados
- [ ] Circuitos principais descritos
- [ ] Pontos de tomada e iluminação por ambiente
- [ ] Pontos de dados, telefone, CFTV
- [ ] SPDA (para-raios): obrigatório conforme NBR 5419
- [ ] Aterramento descrito
- [ ] Cargas especiais identificadas

**Climatização:**
- [ ] Sistema definido com capacidades (BTUs/TR)
- [ ] Localização de evaporadoras e condensadoras
- [ ] Infraestrutura civil (shafts, passagens, drenos)
- [ ] Ponto elétrico para condensadoras
- [ ] Exaustão mecânica onde necessária

**Incêndio:**
- [ ] Extintores previstos e dimensionados (conforme legislação)
- [ ] Hidrantes / mangotinhos
- [ ] Sprinkler (se obrigatório)
- [ ] Alarme de incêndio
- [ ] Iluminação de emergência
- [ ] Sinalização de rotas de fuga
- [ ] Portas corta-fogo (se aplicável)

---

## Etapa 3 — Modelo de Estrutura do Memorial

Após diagnóstico e coleta, redigir o memorial na seguinte estrutura.
Adaptar conforme tipo escolhido na Etapa 0.

### Modelo Híbrido (recomendado na maioria dos casos):
Seção geral por disciplina + tabelas por ambiente + pendências no final.

---

```markdown
# MEMORIAL DESCRITIVO TÉCNICO

## 1. Identificação do Empreendimento

| Campo | Dados |
|---|---|
| Obra | [nome] |
| Endereço | [logradouro, número, bairro, cidade/UF] |
| Cliente / Contratante | [nome] |
| Responsável técnico | [nome — CREA/CAU nº XXXXX] |
| Disciplina(s) | [ex: Arquitetura e Construção Civil + Instalações] |
| Tipo | [obra nova / reforma / ampliação] |
| Fase do projeto | [executivo / básico / anteprojeto] |
| Data de emissão | [DD/MM/AAAA] |
| Revisão | [00 — emissão inicial] |
| Documentos analisados | [lista de projetos utilizados como base] |

---

## 2. Objetivo

Este memorial descritivo tem por objetivo consolidar tecnicamente as soluções
construtivas, materiais, acabamentos, instalações e premissas adotadas para a
obra em referência, servindo como base para orçamento, compras, planejamento
e execução.

---

## 3. Escopo Contemplado

- Serviços preliminares e condições gerais
- Arquitetura e construção civil
- Estrutura
- Cobertura e impermeabilização
- Instalações hidrossanitárias
- Instalações elétricas e lógica
- Climatização, ventilação e exaustão
- Sistemas de incêndio e segurança
- Acessibilidade (NBR 9050)
- Áreas externas e urbanização

---

## 4. Escopo Não Contemplado

- [descrever explicitamente o que está excluído]
- Exemplo: mobiliário solto, paisagismo de manutenção, decoração, obras de arte

---

## 5. Premissas Adotadas

- As medidas deverão ser conferidas em campo antes da execução
- Divergências entre projeto e campo deverão ser validadas formalmente
- Itens sem especificação completa estão registrados como [PENDENTE DE DEFINIÇÃO]
- Nenhuma especificação ausente deve ser presumida como definida sem validação formal
- Preços e quantitativos não são objeto deste memorial

---

## 6. Condições Gerais e Serviços Preliminares

### 6.1 Canteiro e Mobilização
[descrever: instalações provisórias, tapumes, placa de obra, ligações provisórias]

### 6.2 Demolições e Remoções
[descrever: o que será demolido, forma de descarte, destinação de entulho]

### 6.3 Proteção de Áreas Existentes
[descrever proteção de pisos, esquadrias e instalações em reformas]

### 6.4 Segurança do Trabalho
[referência à NR-18: EPI, EPC, PCMAT quando aplicável]

### 6.5 Gestão de Resíduos
[referência à Resolução CONAMA 307 — classificação e destinação de resíduos]

### 6.6 Serviços Preliminares
[locação, levantamentos topográficos, conferência de medidas em campo, marcação de eixos]

---

## 7. Arquitetura e Construção Civil

### 7.1 Vedações e Alvenarias
[ex: Alvenaria de vedação interna com bloco cerâmico 9x19x19cm, assentado com
argamassa industrializada, juntas de 1cm, espessura final 10cm com revestimento]

### 7.2 Revestimentos de Parede Internos
[ex: Chapisco + emboço + gesso liso nas áreas secas; chapisco + reboco + cerâmica
até o teto nas áreas molhadas — especificar por ambiente ou usar tabela]

### 7.3 Revestimentos de Parede Externos
[ex: Chapisco + emboço + textura acrílica na cor [X] nas fachadas — ou ACM, pastilha, etc.]

### 7.4 Pisos
[especificar por ambiente ou referenciar tabela do item 16]

### 7.5 Contrapiso e Base
[ex: Lastro de concreto magro 5cm + contrapiso de argamassa nivelada com 3cm]

### 7.6 Tetos e Forros
[ex: Forro de gesso acartonado (drywall) na sala e quartos; laje aparente pintada
nos depósitos; especificar pé-direito acabado por ambiente]

### 7.7 Pintura
[ex: Látex PVA nas áreas secas internas; acrílico externo nas fachadas;
esmalte sintético em esquadrias metálicas — especificar número de demãos e preparação]

### 7.8 Bancadas e Elementos Fixos
[ex: Bancada de granito cinza andorinha esp. 3cm nas pias; bancada de inox
no tanque — dimensões, apoios, borda]

### 7.9 Esquadrias e Ferragens
[especificar por tipo: porta interna / porta externa / janela / porta de correr
— material, dimensões, acabamento, ferragem]

### 7.10 Vidros
[ex: Vidro temperado 8mm incolor nas janelas de correr; laminado 6+6mm nas portas
de entrada; especificar norma ABNT NBR 7199]

---

## 8. Estrutura

### 8.1 Fundações
[ex: Fundação em sapatas isoladas de concreto armado fck=20MPa, dimensionadas
conforme sondagem SPT — laudo nº X — profundidade mínima de 1,20m abaixo do lençol]

### 8.2 Estrutura de Concreto Armado
[ex: Pilares, vigas e lajes em concreto armado fck=25MPa, aço CA-50,
conforme projeto estrutural do Eng. [nome] — CREA nº XXXXX]

### 8.3 Lajes
[ex: Laje nervurada com EPS, h=20cm, revestimento de 3cm, conforme projeto]

### 8.4 Reservatórios
[ex: Reservatório inferior em concreto armado, cap. 10.000L, impermeabilizado
internamente com argamassa polimérica em 3 demãos]

---

## 9. Cobertura e Impermeabilização

### 9.1 Cobertura
[ex: Estrutura de madeira tratada (resinosa classe 2) + telha cerâmica tipo francesa,
inclinação mínima 30%, com manta subcobertura]

### 9.2 Impermeabilização de Laje
[ex: Manta asfáltica 4mm APP com proteção mecânica (argamassa) nas lajes de cobertura
expostas — aplicação conforme NBR 9952]

### 9.3 Impermeabilização de Áreas Molhadas
[ex: Argamassa polimérica flexível (tipo II) em 3 demãos nos boxes de banheiro,
sacadas e varandas, com virada de parede mínima de 30cm]

### 9.4 Impermeabilização de Fundações
[ex: Emulsão asfáltica em 2 demãos nas faces externas das vigas baldrame]

---

## 10. Instalações Hidrossanitárias

### 10.1 Água Fria
[ex: Tubulação em PVC rígido soldável (ABNT NBR 5648), barrilete com diâmetros
conforme projeto, ramal individual para cada unidade; caixa d'água 5.000L fibra
de vidro instalada na cobertura]

### 10.2 Água Quente
[ex: Tubulação em CPVC (ABNT NBR 15884), aquecedor a gás de passagem 35L/min
instalado na área de serviço, conforme projeto; pré-instalação para aquecimento solar]

### 10.3 Esgoto Sanitário
[ex: Tubulação em PVC série normal (ABNT NBR 5688), com inspeções e ventilação
conforme projeto; ligação à rede pública municipal — caixa de inspeção em alvenaria
com tampa de concreto armado]

### 10.4 Águas Pluviais
[ex: Calhas em alumínio 0,8mm, condutores em PVC 100mm, destinação ao sistema
municipal conforme legislação municipal]

### 10.5 Louças, Cubas e Metais
[especificar por ambiente ou referenciar tabela — marca, linha, cor]
[ex: Vaso sanitário com caixa acoplada — Deca Carrara branco; lavatório de
embutir 46x30cm — Celite branco; torneira monocomando bica alta — Docol Dot]

---

## 11. Instalações Elétricas e Lógica

### 11.1 Padrão de Entrada e Medição
[ex: Entrada aérea monofásica 220V, poste externo com medidor digital,
disjuntor de ramal 60A conforme padrão da concessionária Neoenergia/PE]

### 11.2 Quadros de Distribuição
[ex: QD geral embutido no corredor, barramento 63A, com disjuntores individuais
por circuito conforme projeto elétrico — mínimo 20% de reserva]

### 11.3 Circuitos e Pontos
[ex: Tomadas baixas (1,00m) e altas (2,00m) conforme ABNT NBR 5410;
tomadas de uso geral 10A e específicas 20A para equipamentos; iluminação em
eletroduto corrugado flexível no teto]

### 11.4 Iluminação
[ex: Pontos de luz preparados para luminária embutida — tipo e potência a definir
pelo cliente; banheiros com spot fixo IP44]

### 11.5 Rede de Dados e Lógica
[ex: Rede estruturada cat.6 em todos os ambientes, ponto CFTV na entrada,
interfone com câmera, campainha]

### 11.6 SPDA (Para-raios)
[ex: SPDA tipo Franklin conforme NBR 5419, instalado na caixa d'água,
aterramento em malha de cobre nú 50mm², resistência ≤ 10Ω]

---

## 12. Climatização, Ventilação e Exaustão

### 12.1 Ar Condicionado
[ex: Sistema split inverter, capacidade por ambiente conforme memorial de carga
térmica; ponto elétrico 220V 20A e ponto de dreno em cada evaporadora;
condensadoras na área técnica da cobertura]

### 12.2 Ventilação e Exaustão
[ex: Exaustor de teto 150mm nos banheiros sem janela; exaustor axial 200mm na
cozinha; renovação de ar natural assegurada nas demais áreas por janelas]

---

## 13. Incêndio e Segurança

### 13.1 Extintores
[ex: Extintores ABC 6kg conforme Decreto Estadual — locação e quantidade conforme
projeto de prevenção aprovado pelo CBMPE]

### 13.2 Sistemas Complementares
[ex: Iluminação de emergência autônoma com autonomia mínima 1h (NBR 10898);
sinalização de rotas de fuga e saídas de emergência (NBR 13434)]

---

## 14. Acessibilidade

[ex: Rampa de acesso com inclinação 1:12 (8,33%), largura 1,20m, corrimão
duplo conforme ABNT NBR 9050; piso tátil direcional e de alerta na entrada;
sanitário acessível conforme NBR 9050 — área mínima 1,50x1,70m]

---

## 15. Áreas Externas

### 15.1 Calçadas e Acessos
[ex: Piso intertravado de concreto 20x10x6cm natural nas calçadas externas;
rampa de acessibilidade e rebaixo de meio-fio]

### 15.2 Muro e Gradil
[ex: Muro frontal de alvenaria h=0,50m + gradil metálico h=1,50m pintado a
esmalte; portão de correr motorizado com acionamento remoto]

### 15.3 Paisagismo
[PENDENTE DE DEFINIÇÃO — aguardando projeto de paisagismo]

---

## 16. Tabela de Acabamentos por Ambiente

| Ambiente | Piso | Rodapé | Parede | Teto/Forro | Pintura | Obs. |
|---|---|---|---|---|---|---|
| Sala de estar | Porcelanato 60x60cm acetinado | Rodapé cerâmico 10cm | Gesso liso | Gesso liso | Látex branco | — |
| Cozinha | Cerâmica 45x45cm antiderrapante | Rodapé cerâmico | Cerâmica 30x60cm até teto | Gesso liso | — | Conforme layout |
| Banheiro social | Porcelanato 60x60cm | — | Porcelanato até teto | Gesso c/ pintura PVA | — | Piso aquecido? [PENDENTE] |
| Dormitório 1 | Porcelanato 60x60cm | Rodapé MDF | Gesso liso | Gesso liso | Látex branco | — |
| Área de serviço | Cerâmica 30x30cm | — | Cerâmica 20x30cm h=1,50m | Laje aparente | PVA branco | — |
| Garagem | Concreto desempenado | — | Pintura acrílica | Laje aparente | Acrílico externo | — |

> Adicionar linhas conforme ambientes do projeto. Células com [PENDENTE] indicam
> definição pendente com o cliente ou projetista.

---

## 17. Pendências Consolidadas

Todos os itens sem definição completa devem ser listados aqui, organizados por
disciplina, com indicação do impacto e responsável pela definição:

| # | Disciplina | Pendência | Impacto | Responsável | Prazo |
|---|---|---|---|---|---|
| 01 | Arquitetura | Definição de piso do banheiro social (aquecido ou não) | Orçamento e prazo | Cliente | Antes da compra |
| 02 | Elétrico | Especificação de luminária dos ambientes sociais | Compras | Cliente/Designer | Antes da execução |
| 03 | Climatização | Carga térmica formal para dimensionamento | Projeto | Eng. Elétrico | Antes do projeto |
| 04 | Paisagismo | Projeto não recebido | Escopo externo | Arquiteto | [PENDENTE] |

---

## 18. Observações Finais

- Qualquer alteração posterior deverá ser formalmente registrada com nova revisão
- Itens pendentes deverão ser definidos antes da fase de compra ou execução correspondente
- Este memorial deve ser lido em conjunto com os projetos e documentos complementares
- Em caso de divergência entre este memorial e os projetos, prevalece a versão de maior
  detalhamento técnico, devendo a divergência ser comunicada ao responsável técnico
- As especificações indicadas podem ser substituídas por similares de qualidade
  equivalente ou superior, mediante aprovação formal do responsável técnico e do cliente
```

---

## Etapa 4 — Modelo de Estrutura por Abordagem

Conforme o tipo de memorial, adaptar a estrutura:

### Modelo 1 — Por Disciplina
Recomendado para: obras complexas, industriais, licitações públicas.
Estrutura: seções independentes por sistema (conforme modelo acima).

### Modelo 2 — Por Ambiente
Recomendado para: interiores, varejo, clínicas, residências de alto padrão.
Estrutura: cada ambiente como seção com todos os itens (piso, parede, teto, etc.).

### Modelo 3 — Híbrido (recomendado na maioria dos casos)
Estrutura: seção geral por disciplina + tabela de acabamentos por ambiente + pendências.
Este é o modelo padrão desta skill.

---

## Etapa 5 — Prompts para o Usuário Solicitar o Memorial

Estes prompts estão disponíveis para uso direto com esta skill ou qualquer agente.
Copie e adapte conforme sua necessidade:

---

### Prompt 1 — Diagnóstico Técnico Completo

```
Analise tecnicamente os arquivos enviados como especialista em memorial descritivo,
orçamento e execução de obras. Identifique, por disciplina, tudo o que está claramente
definido, tudo o que está parcialmente definido, tudo o que está omisso e tudo o que
está contraditório. Organize a análise em: arquitetura, construção civil, estrutura,
impermeabilização, cobertura, hidrossanitário, elétrico, climatização, incêndio,
acessibilidade e áreas externas. Destaque as lacunas que afetam orçamento, compras,
planejamento, compatibilização e execução.
```

---

### Prompt 2 — Diagnóstico por Ambiente

```
Com base nos projetos enviados, faça um levantamento por ambiente contendo: piso,
rodapé, paredes, teto/forro, esquadrias, vidros, bancadas, louças, metais, iluminação,
climatização e observações. Tudo o que não estiver claramente definido deve ser
indicado como [PENDENTE DE DEFINIÇÃO].
```

---

### Prompt 3 — Geração do Memorial Completo

```
Gere um memorial descritivo técnico, completo e profissional com base na análise
validada. O memorial deve ser útil para orçamento, compras e execução. Estruture em:
identificação da obra, objetivo, escopo contemplado, escopo não contemplado, premissas
adotadas, serviços preliminares, arquitetura, construção civil, estrutura, cobertura,
impermeabilização, hidrossanitário, elétrico, climatização, incêndio, acessibilidade,
áreas externas, tabela de acabamentos por ambiente, lista consolidada de pendências e
observações finais. Use linguagem técnica, objetiva e verificável. Não invente
especificações ausentes — registre como [PENDENTE DE DEFINIÇÃO].
```

---

### Prompt 4 — Versão para Orçamento

```
Transforme o memorial gerado em uma versão com foco em orçamento, destacando itens
que impactam quantitativos, contratação, compra, planejamento e risco de aditivo.
Classifique cada item em: DEFINIDO / PARCIALMENTE DEFINIDO / PENDENTE / CONFLITANTE.
```

---

### Prompt 5 — Relatório de Pendências para Cliente ou Projetista

```
Com base nas pendências identificadas, gere um relatório de pendências de especificação
em linguagem profissional, clara e direta, para envio ao cliente, arquiteto ou
projetista. Organize por disciplina e destaque o impacto de cada omissão no orçamento
e na execução.
```

---

### Prompt 6 — Memorial por Ambiente (Interiores)

```
Gere um memorial descritivo por ambiente para o projeto de interiores enviado.
Para cada ambiente liste: piso, rodapé, paredes (revestimento e pintura), teto/forro,
esquadrias, vidros, bancadas, louças e metais, iluminação e climatização.
Registre [PENDENTE] onde não há definição. Ao final, gere a tabela de acabamentos
consolidada e a lista de pendências por ambiente.
```

---

### Prompt 7 — Memorial de Instalações (MEP)

```
Elabore um memorial descritivo técnico das instalações prediais (hidrossanitário,
elétrico, climatização e incêndio) com base nos projetos enviados. Para cada
disciplina descreva: sistemas adotados, materiais e normas técnicas aplicáveis,
especificações de equipamentos, interfaces com obra civil e pendências de definição.
Use linguagem técnica e objetiva, compatível com uso em orçamento e execução.
```

---

## Etapa 6 — Validação e Entrega

Antes de entregar o memorial final, verificar:

```
✅ CHECKLIST DE QUALIDADE DO MEMORIAL:
[ ] Identificação completa (obra, cliente, RT, data, revisão)
[ ] Escopo contemplado claramente definido
[ ] Escopo excluído explicitamente registrado
[ ] Premissas declaradas (protege o técnico)
[ ] Todos os ambientes cobertos na tabela de acabamentos
[ ] Itens sem definição registrados como [PENDENTE] — nunca inventados
[ ] Pendências consolidadas com impacto e responsável
[ ] Disciplinas cruzadas (ex: ponto elétrico do ar-condicionado mencionado
    tanto em elétrico quanto em climatização)
[ ] Linguagem técnica, objetiva e verificável (não subjetiva)
[ ] Versão, data e revisão registradas no documento

⚠️ ALERTAS COMUNS:
- Memorial genérico sem especificação real → inútil para orçamento
- Esquecer escopo excluído → cria passivo contratual
- Omitir pendências → todo mundo finge que estava definido
- Misturar definição com suposição → perigoso tecnicamente
- Não cruzar disciplinas → conflitos na execução (tubulação onde havia viga, etc.)
- Confiar na IA sem revisão humana → automatizar o erro
```

---

## Etapa 7 — Formatos de Saída

| Formato | Quando usar |
|---|---|
| **Markdown** | Visualização rápida, Obsidian, Claude |
| **DOCX** | Entrega profissional ao cliente (requer skill `docx`) |
| **PDF** | Assinatura digital, entrega formal (requer skill `pdf`) |
| **Texto estruturado** | Importação em sistemas de gestão de obra |

---

## Referências Técnicas e Normativas

| Norma / Documento | Aplicação |
|---|---|
| ABNT NBR 9050:2020 | Acessibilidade a edificações |
| ABNT NBR 5410:2004 | Instalações elétricas de baixa tensão |
| ABNT NBR 5648 | Tubulações de PVC — água fria |
| ABNT NBR 5688 | Tubulações de PVC — esgoto |
| ABNT NBR 15884 | Tubulações de CPVC — água quente |
| ABNT NBR 9952 | Manta asfáltica para impermeabilização |
| ABNT NBR 7199 | Vidros na construção civil |
| ABNT NBR 5419 | SPDA — para-raios |
| ABNT NBR 10898 | Iluminação de emergência |
| ABNT NBR 13434 | Sinalização de segurança contra incêndio |
| Resolução CONAMA 307 | Gestão de resíduos da construção civil |
| NR-18 | Condições de segurança em obras |
| Lei 14.133/2021 | Nova Lei de Licitações (memoriais em licitações) |

---

## Erros que Esta Skill Evita Ativamente

1. **Memorial genérico** — nunca redigir sem especificação real por ambiente/disciplina
2. **Esquecer escopo excluído** — sempre declarar o que não está contemplado
3. **Omitir pendências** — sempre registrar [PENDENTE], nunca inventar especificação
4. **Misturar definição com suposição** — distinguir claramente o que é dado e o que é hipótese
5. **Não cruzar disciplinas** — sempre verificar interfaces (elétrico × climatização, estrutura × hidro)
6. **Confiar cegamente na IA** — sempre indicar que o documento requer revisão e assinatura do RT

---

## Exemplos de Invocação

**Explícito:**
```
/memorial-descritivo-obra
```

**Implícito (linguagem natural):**
```
"Preciso de um memorial descritivo para uma casa de 150m² em Paulista/PE"
"Faça o memorial técnico de instalações para este projeto hidráulico"
"Gere o memorial de acabamentos por ambiente para esta reforma comercial"
"Memorial descritivo para licitação pública — escola municipal"
"Preciso descrever os materiais e sistemas para orçamento desta obra"
```

---

## Notas do Criador

- Desenvolvida por **Pr. Hélio Paiva Jr.** — Engenheiro Civil
- Baseada no documento técnico *"Como gerar memoriais descritivos com IA — versão técnica, completa e aplicável"*
- Metodologia em 6 etapas: levantamento → diagnóstico → classificação → redação → validação → consolidação
- Integra com `orcamento-obra` e `cronograma-obra` para workflow completo de projetos
- Versão 1.0 — Abril/2026
