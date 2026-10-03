# Research (Phase 0): Soluções de desgaste – Concentradora 2 (escopo P1: S1 e S2)

**Data**: 2026-10-03 | **Spec**: [spec.md](./spec.md) | **Plano**: [plan.md](./plan.md)

Neste documento, cada item marcado como NEEDS CLARIFICATION no Technical Context recebe uma decisão de engenharia ou vira uma entrada que o cliente precisa enviar, com uma premissa de projeto até lá. Os números de cálculo são estimativas de ordem de grandeza e serão confirmados no memorial de cálculo.

---

## R1. Linha de produto Haver disponível para as alternativas citadas na visita

- **Decision**: usar a linha **Rhino Hyde** da Haver & Boecker Niagara (fornecida em parceria com a Tandem Products). São revestimentos de **poliuretano termofixo** em formulação própria, com variantes "Blue" (chapa padrão), magnética, **cerâmica com base de uretano**, lâminas, belt skirting e **soldável (com base de aço)**.
- **Rationale**: a linha cobre as duas histórias P1. S1 usa a variante cerâmica + uretano e S2 usa a chapa Blue de 1", nas versões aparafusada ou soldável. Também cobre a maior parte das histórias S3 a S8, que ficaram adiadas.
- **Alternatives considered**: comprar poliuretano ou cerâmica de terceiros e montar internamente. Foi descartado nesta fase porque a linha própria já é produzida e tem formulação e processo validados (Princípio V: preferir soluções padronizadas).
- **Fonte**: [Haver & Boecker Niagara presents Rhino Hyde liners](https://www.pitandquarry.com/haver-boecker-niagara-rhino-hyde-liners/), [agg-net](https://agg-net.com/news/haver-boecker-niagara-offer-rhino-hyde-liners).

## R2. S1 – Conceito de revestimento para a calha de descarga (abrasão + impacto de bolas de 3")

**Carga de impacto de referência**:
- bola de aço de 3" (Ø 76,2 mm): massa ≈ 1,8 kg;
- energia de impacto ≈ 17,9 J por metro de queda (E = m·g·h);
- a altura de queda real depende da geometria da calha e é uma entrada que o cliente precisa enviar.

**Por que as soluções anteriores falharam**:
- *peças cerâmicas pequenas*: a área de colagem ou fixação por peça é pequena, então as peças se soltam por vibração e impacto e a junta entre elas se desgasta primeiro;
- *peças cerâmicas grandes*: a cerâmica é frágil e uma peça grande sobre base rígida concentra tensão e quebra quando uma bola de 3" bate.

- **Decision**: usar um **painel compósito de cerâmica encapsulada em poliuretano, com base de aço**. São cilindros ou pastilhas de alumina (≥ 92% Al₂O₃) moldados dentro de uma matriz de PU termofixo e ligados quimicamente a uma chapa de aço de fixação. A fixação é aparafusada e, sempre que a geometria permitir, reaproveita a furação atual.
  - O PU **amortece o impacto** e distribui a carga, o que protege a cerâmica contra a quebra.
  - A cerâmica **resiste à abrasão** da polpa.
  - O encapsulamento e a ligação à base **impedem que as peças se soltem**, mesmo quando uma pastilha se desgasta ou trinca.
  - Os painéis têm no máximo 25 kg (FR-003) e são presos por parafusos de cabeça escareada protegidos pela própria camada de PU.
- **Recurso geométrico complementar**: avaliar uma "caixa de pedra" (degrau ou prateleira que retém polpa e bolas e forma um leito de material) na zona de impacto direto das bolas. Esse leito absorve o impacto sem desgastar o revestimento. A viabilidade depende dos desenhos e das fotos.
- **Rationale**: o conceito ataca os dois modos de falha observados ao mesmo tempo, mantém a troca por parafusos sem solda ou corte (FR-002) e já existe na linha Rhino Hyde.
- **Alternatives considered**:

  | Alternativa | Motivo da rejeição / posição |
  |---|---|
  | PU puro de grande espessura | Ótimo contra impacto, mas a abrasão de polpa grossa reduz a vida útil. Fica como plano B para as zonas de baixo desgaste. |
  | Borracha + cerâmica | É equivalente técnico (o cliente testa no britador). O PU tem maior resistência à abrasão e ao rasgo. Fica como referência de comparação. |
  | Chapa com revestimento de carbonetos de cromo (CCO) | Trinca e se desprende com o impacto repetido das bolas. |
  | Ferro fundido branco alto cromo / Ni-hard | Frágil sob impacto de bolas de aço e pesado (> 25 kg por peça). |
  | Cerâmica maior aparafusada | É o modo de falha atual: quebra. |

## R3. S2 – Chapa de PU de 1" em substituição ao Hardox 5/8"

- **Decision**: fornecer a chapa **Rhino Hyde Blue de 25,4 mm** em **painéis pré-cortados** do tamanho de cada posição de teste, em duas versões conforme a fixação atual de cada posição:
  - **(a) aparafusada**: furação com bucha ou arruela de aço embutida;
  - **(b) soldável**: PU ligado a uma chapa de aço fina, que permite soldar a base ao equipamento como o cliente já faz hoje com o Hardox.
- **Rationale**:
  - O PU não pode ser cortado a maçarico nem soldado diretamente como o Hardox. Para atender o FR-201 ("cortar e fixar com os meios atuais ou instrução") é preciso a versão soldável ou painéis já cortados com instrução de corte a frio (serra ou disco para PU).
  - **Massa**: PU (densidade ≈ 1,2) com 25,4 mm pesa ≈ 30 kg/m². O Hardox de 16 mm pesa ≈ 126 kg/m². A chapa nova é cerca de 4× mais leve, o que facilita o manuseio. Painéis de ≤ 0,8 m² ficam abaixo de 25 kg.
  - **Desempenho**: o PU termofixo costuma superar o aço resistente à abrasão quando o desgaste é por deslizamento ou impacto de partículas finas a médias, com polpa ou úmido. O Hardox leva vantagem com rocha grande e cortante, com temperatura acima de ~80 °C ou com óleos e solventes. Por isso o teste lado a lado (FR-203) é necessário.
- **Alternatives considered**: Hardox 500 de maior espessura, que é solução incremental e mais pesada; borracha natural, com menor resistência ao corte; e uma chapa bimetálica com overlay, que é cara e perde da chapa de PU quando há impacto.
- **Restrição de aplicação**: o PU não deve ser usado em posições que **excedam 80 °C** em operação, que recebam **blocos com aresta viva > 150 mm** ou que tenham **contato com óleo ou solvente**. Essas posições ficam fora do teste.

## R4. Normas aplicáveis (planta no México)

- **Decision**:
  - **Segurança**: NOM-023-STPS-2012 (minas a céu aberto e subterrâneas: condições de segurança), NOM-004-STPS-1999 (proteções e dispositivos de segurança em máquinas) e NOM-006-STPS-2014 (manejo e armazenamento de materiais, incluindo levantamento manual). O procedimento de trabalho seguro do Grupo México se aplica à instalação.
  - **Referência complementar** (constituição): NR-12 e NR-22.
  - **Ensaios de material**:
    - PU: dureza Shore A (ASTM D2240), tração e alongamento (ASTM D412), rasgo (ASTM D624), abrasão (ISO 4649, perda de volume em mm³) e adesão PU-aço (ASTM D429 método B);
    - cerâmica: teor de Al₂O₃ e densidade (ASTM C373);
    - aço da base: certificado de usina (ASTM A36 ou equivalente).
- **Rationale**: as normas STPS são as exigíveis no local da instalação. Os ensaios ASTM/ISO são os usados na prática para verificar elastômeros e cerâmicas técnicas.

## R5. Medição de desgaste e projeção de vida útil (FR-104, FR-204)

- **Decision**:
  - Cada painel e cada chapa sai da fábrica com **pontos de medição marcados** (grade de 3 a 9 pontos por painel, em mapa) e espessura inicial registrada no relatório de inspeção dimensional.
  - **Instrumentos**: medidor ultrassônico de espessura calibrado para PU (velocidade do som ≈ 1.700 m/s, a confirmar com amostra) e, para conferir, um furo-testemunho de profundidade conhecida por painel (indicador de desgaste visual).
  - **No Hardox de comparação**: medidor ultrassônico padrão para aço.
  - **Inspeções**: na instalação (T0), a cada parada programada (referência mensal) e no fim do teste.
  - **Projeção de vida útil**: taxa de desgaste = perda de espessura ÷ horas de operação. Vida projetada = espessura útil inicial ÷ taxa no ponto mais desgastado. Usar sempre o ponto **mais desgastado**, nunca a média.
- **Rationale**: atende o critério de fim de teste da S2 (o Hardox atinge a espessura de troca) e dá base objetiva para a regra de 1,5× na S1.

## R6. Custo por hora de operação (FR-007, FR-202)

- **Decision**: custo/h = (preço do material + mão de obra de instalação + custo da parada atribuível à troca) ÷ horas de vida útil. A mesma fórmula vale para a solução atual e para a proposta. O preço atual do Hardox e da cerâmica é uma **entrada que o cliente precisa enviar** (FR-901). Enquanto não vier, usa-se um preço de mercado de referência, marcado como estimativa.

## R7. Entradas que o cliente precisa enviar (até lá, valem as premissas de projeto)

| Entrada | Necessária para | Premissa até recebimento |
|---|---|---|
| Desenhos e fotos da calha de descarga (geometria, furação, espessura atual, quantidade de calhas) | S1: projeto do painel e contrato de interface | Furação reaproveitada; painéis ≤ 25 kg; espessura total do revestimento ≤ espessura atual + 10 mm |
| Vazão, % de sólidos, granulometria (P80) e altura de queda das bolas | S1: dimensionamento ao impacto | Polpa de 55 a 70% de sólidos; queda de 1 a 2 m (≈ 18 a 36 J por bola) |
| Lista das posições onde hoje se usa Hardox 5/8", com dimensões, fixação e temperatura | S2: escolha das 2 a 4 posições de teste | Desgaste por deslizamento de minério britado < 150 mm; temperatura < 60 °C |
| Espessura de troca do Hardox adotada pela manutenção | S2: fim do teste | 6 mm remanescentes |
| Preços atuais (Hardox 5/8" por m² ou kg; jogo de cerâmica da calha) | Custo por hora (S1, S2) | Preço de mercado de referência, marcado como estimativa |
