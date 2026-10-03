# Feature Specification: Soluções de Revestimento e Peças de Desgaste – Grupo México, Concentradora 2

**Feature Branch**: `001-visit-opportunity-tracker`

**Created**: 2026-10-03

**Status**: Draft

**Input**: User description: resumo de visita técnico-comercial "Grupo Mexico - Concentradora 2 - Resumen de visita y próximos pasos - visita 9/9/26", enviado por Laís Andrade a Isidro. Participantes: Gilberto Lopes, Ismael Burgos, Jorge, Isidro e Laís. O resumo identifica 8 oportunidades de revestimentos e peças de desgaste: britadores cônicos, peças magnéticas para reparo provisório, hidrociclones, calha de descarga do hidrociclone, tubulações revestidas, placas de desgaste, célula de flotação e belt skirting. Pede também preços de referência e, em caso de recusa, o motivo.

## Contexto

A Concentradora 2 do Grupo México é uma planta de beneficiamento de minério. Tem britagem cônica, moagem com bolas de 3", classificação em hidrociclones, flotação e transporte de polpa e de minério por tubulações e correias. Os componentes expostos a polpa e minério sofrem abrasão e, em alguns pontos, impacto. Por isso a planta substitui com frequência revestimentos e chapas de desgaste.

Esta especificação reúne, como **um programa de produtos manufaturados**, as soluções que a Haver pode fornecer para as 8 aplicações identificadas na visita de 09/09/2026. Cada aplicação é uma user story **independente**: pode ser cotada, prototipada, testada em campo e fornecida separadamente das demais. Conforme a constituição (Princípio I), toda entrega é um produto físico com sua documentação técnica. Não há software envolvido.

Conforme a constituição, materiais, processos e fornecedores **não são fixados nesta spec**. As alternativas citadas na visita (poliuretano, poliuretano + cerâmica, chapa "Rhino Hyde") ficam registradas como **alternativas de interesse do cliente**, para serem avaliadas no plano.

## Clarifications

### Session 2026-10-03

- Q: O plano e as tarefas devem cobrir as 8 aplicações ou só as P1? → A: Plano detalhado só das P1 (S1 calha de descarga + S2 placas de desgaste); S3–S8 permanecem na spec como "aguardando dados do cliente" e entram no plano quando os dados chegarem.
- Q: Qual meta de vida útil a placa alternativa (S2) deve atingir frente ao Hardox 5/8"? → A: Vida útil ≥ 1,5× a do Hardox na mesma posição **e** custo por hora de operação ≤ o do Hardox.

## User Scenarios & Testing *(mandatory)*

> Aqui "usuário" significa cliente, operador ou mantenedor da Concentradora 2. "Teste" significa inspeção, ensaio ou teste de campo.

### User Story 1 - Revestimento da calha de descarga do hidrociclone (Priority: P1)

A manutenção da Concentradora 2 precisa de um revestimento para a calha de descarga do hidrociclone que dure **mais de 12 meses**. Hoje usam peças cerâmicas padrão aparafusadas que duram cerca de **8 meses**. Já tentaram peças cerâmicas menores, mas elas **se soltam e se desgastam rápido**. As peças maiores **quebram**, porque a aplicação combina abrasão da polpa com **impacto de bolas de moinho de 3"**.

**Why this priority**: É a única aplicação com insatisfação declarada, meta de vida útil quantificada e modos de falha conhecidos. Por isso tem a maior chance de conversão e o ganho mais claro para o cliente: menos trocas por ano.

**Independent Test**: Instalar o revestimento em uma calha, em teste de campo, e medir a vida útil e o modo de falha contra a solução atual na mesma posição.

**Acceptance Scenarios**:

1. **Given** as fotos e os desenhos da calha enviados pelo cliente, **When** a Engenharia confirma as dimensões e a fixação, **Then** o revestimento encaixa na calha existente sem modificar a estrutura hospedeira.
2. **Given** o revestimento instalado e a operação normal (polpa abrasiva + bolas de 3"), **When** se completam 12 meses, **Then** nenhuma peça se soltou ou quebrou e a espessura remanescente nos pontos críticos fica acima do mínimo de troca.
3. **Given** a necessidade de troca, **When** a equipe de manutenção do cliente substitui o revestimento, **Then** a troca é feita na parada programada, com ferramentas convencionais e sem corte ou solda no equipamento.

---

### User Story 2 - Placas de desgaste em substituição ao Hardox 5/8" (Priority: P1)

A manutenção compra chapas de Hardox de 5/8" (16 mm), corta no local e instala em várias superfícies de desgaste. A Haver sugeriu testar uma chapa alternativa com 1" de espessura ("Rhino Hyde") nessas mesmas aplicações. O objetivo é aumentar a vida útil, mantendo o cliente capaz de cortar e instalar a chapa como faz hoje.

**Why this priority**: O próximo passo depende só da Haver (preparar cotação). Não há desenho pendente, e o produto é simples e aplicável em vários pontos da planta. É a oportunidade mais rápida de converter.

**Independent Test**: Instalar a chapa alternativa ao lado do Hardox em pelo menos uma superfície com desgaste equivalente e comparar a perda de espessura no mesmo período.

**Acceptance Scenarios**:

1. **Given** uma chapa fornecida em dimensões padrão, **When** a manutenção corta e fixa a chapa com os meios disponíveis no local, **Then** a instalação não precisa de ferramenta especial ou deve vir acompanhada de instrução que a dispense.
2. **Given** chapas Hardox e alternativas instaladas lado a lado, **When** termina o período de avaliação combinado, **Then** a vida útil projetada da alternativa é ≥ 1,5× a do Hardox e o custo por hora de operação é ≤ o do Hardox.
3. **Given** a aplicação de uma chapa mais espessa (1" contra 5/8"), **When** é instalada, **Then** a folga, a massa e a fixação continuam compatíveis com o equipamento hospedeiro.

---

### User Story 3 - Revestimento da célula de flotação (Priority: P2)

A planta usa revestimentos de borracha e poliuretano nas células de flotação. A Haver identificou pelo menos um modelo de célula que parece igual a um equipamento que ela já mediu. O cliente precisa de um revestimento para esse modelo que encaixe sem retrabalho.

**Why this priority**: As medições já existem, o que reduz o tempo de engenharia. Antes, porém, é preciso confirmar que os equipamentos são iguais.

**Independent Test**: Comparar as dimensões críticas da célula da Concentradora 2 com as medições existentes. Se forem iguais, fornecer um conjunto e verificar o encaixe na primeira instalação.

**Acceptance Scenarios**:

1. **Given** as medições existentes e os dados da célula da Concentradora 2 (modelo, fabricante, dimensões críticas), **When** são comparados, **Then** a equivalência é confirmada ou as diferenças são listadas antes da proposta.
2. **Given** a equivalência confirmada, **When** o revestimento é instalado, **Then** todas as peças encaixam sem corte, ajuste ou furação em campo.

---

### User Story 4 - Peças magnéticas para reparo provisório de perfurações (Priority: P2)

Quando um chute, uma calha ou uma tubulação fura por desgaste com o equipamento em operação, a manutenção precisa **cobrir o furo por fora, provisoriamente**, até a próxima parada para o reparo definitivo. Hoje já usam uma solução parecida. A Haver pode oferecer uma peça com ímãs, instalada por fora, que contenha o vazamento sem parar o equipamento.

**Why this priority**: Evita paradas não programadas, que têm alto valor para o cliente. Como ele já usa uma solução semelhante, o desempenho mínimo esperado é conhecido. Precisa de cotação.

**Independent Test**: Aplicar a peça sobre uma perfuração real ou simulada, em superfície metálica com a curvatura típica da planta, e verificar a fixação e a contenção do vazamento durante o período até a parada.

**Acceptance Scenarios**:

1. **Given** um furo de desgaste em superfície de aço com o equipamento operando, **When** um mantenedor posiciona a peça, **Then** a peça fixa e reduz o vazamento a um nível aceitável sem ferramenta especial e sem parar o equipamento.
2. **Given** a peça instalada sob vibração e fluxo de polpa, **When** passa o período até a parada programada, **Then** a peça não se desloca nem se solta.
3. **Given** a parada programada, **When** a peça é retirada, **Then** sai sem danos e pode ser reutilizada.

---

### User Story 5 - Revestimento de hidrociclones (incluindo Cavex 48) (Priority: P3)

Os hidrociclones são revestidos hoje com borracha e com cerâmica de carbeto de silício. O cliente citou o modelo **Cavex 48** e quer avaliar um revestimento alternativo (interesse declarado: poliuretano com ou sem cerâmica) que mantenha a classificação e aumente a vida útil.

**Why this priority**: Há interesse, mas a oportunidade depende de desenhos do cliente. A geometria interna afeta o desempenho da classificação, o que aumenta o risco técnico.

**Independent Test**: Instalar o revestimento em um hidrociclone em teste de campo e comparar a vida útil e a classificação com um hidrociclone igual que use a solução atual.

**Acceptance Scenarios**:

1. **Given** os desenhos do hidrociclone, **When** o revestimento é projetado, **Then** o perfil interno reproduz a geometria original dentro das tolerâncias do OEM.
2. **Given** o revestimento em operação, **When** a classificação é medida, **Then** os parâmetros do overflow e do underflow continuam equivalentes aos da solução atual.
3. **Given** o fim da vida útil, **When** comparado à solução atual, **Then** a vida útil é igual ou maior.

---

### User Story 6 - Revestimento da parte inferior dos britadores cônicos (Priority: P3)

A parte inferior dos britadores cônicos usa hoje Hardox, com vida útil **acima de 17.000 horas**. O cliente também testa borracha com cerâmica, com bons resultados, e aceita testar uma alternativa (interesse declarado: poliuretano + cerâmica).

**Why this priority**: A solução atual já tem bom desempenho, então o ganho é incremental. Além disso, a oportunidade depende de desenhos do cliente.

**Independent Test**: Instalar o revestimento em um britador, em teste de campo, e acompanhar o desgaste até completar pelo menos 17.000 horas ou até o fim da vida.

**Acceptance Scenarios**:

1. **Given** os desenhos da região inferior do britador, **When** o revestimento é projetado, **Then** encaixa na fixação existente sem modificar o britador.
2. **Given** a operação normal, **When** atinge 17.000 horas, **Then** o revestimento continua íntegro e com espessura acima do mínimo de troca.

---

### User Story 7 - Tubulações revestidas de 24" (Priority: P3)

A planta usa tubulações de **24"** revestidas com borracha, na maioria com **6 m** de comprimento. Não há reclamação, mas o cliente aceita testar uma alternativa que aumente a vida útil.

**Why this priority**: Não há uma dor declarada e a oportunidade depende de desenhos do cliente. Por outro lado, o volume pode ser grande.

**Independent Test**: Fornecer um carretel de 24" × 6 m para instalar em uma linha com desgaste conhecido e comparar a perda de espessura com o carretel de borracha da mesma linha.

**Acceptance Scenarios**:

1. **Given** os desenhos da linha (flanges, pressão, conexões), **When** o tubo é fornecido, **Then** os flanges e o comprimento são intercambiáveis com os tubos existentes.
2. **Given** o tubo em operação, **When** comparado ao tubo de borracha na mesma linha, **Then** a vida útil projetada é maior.

---

### User Story 8 - Belt skirting (vedação lateral de correia) (Priority: P3)

Depois da reunião, a equipe viu no pátio um rolo de poliuretano usado como belt skirting. O cliente precisa de um material de vedação lateral nas dimensões que já usa, com preço competitivo e vida útil igual ou maior.

**Why this priority**: É um produto de reposição simples. Para cotar, faltam apenas as dimensões e o preço atual.

**Independent Test**: Fornecer um rolo nas dimensões confirmadas e verificar a instalação nos transportadores existentes e o desgaste no mesmo período que o material atual.

**Acceptance Scenarios**:

1. **Given** as dimensões confirmadas (largura, espessura, comprimento do rolo), **When** o material é fornecido, **Then** encaixa nos fixadores de skirting existentes sem adaptação.
2. **Given** a proposta comercial, **When** comparada ao preço atual informado pelo cliente, **Then** o custo por metro instalado e por mês de vida útil é igual ou menor.

---

### Edge Cases

- **Cliente não envia desenhos ou fotos**: as stories 1, 5, 6 e 7 ficam bloqueadas na fase de proposta. A Haver pode propor levantamento dimensional em campo como alternativa.
- **Equipamento de flotação não é igual ao já medido**: a story 3 passa a exigir novo levantamento dimensional antes da proposta.
- **Teste de campo interrompido** por parada da planta, troca de minério ou mudança de regime: a vida útil é contada em horas efetivas de operação ou em toneladas processadas, e não em tempo de calendário.
- **Bolas de moinho de diâmetro maior que 3"** ou outros corpos estranhos na calha (story 1): o revestimento não pode soltar fragmentos que causem dano a jusante.
- **Peça magnética em superfície não ferromagnética** (aço inoxidável austenítico, tubo revestido de borracha por fora): a limitação deve constar na instrução de uso.
- **Chapa mais espessa (story 2)** interfere em folgas ou aumenta a massa acima do limite de manuseio manual: a espessura deve ser revista para aquele ponto.
- **Unidades mistas**: dimensões em polegadas e em milímetros. Toda documentação usa o sistema métrico, com a medida em polegadas entre parênteses quando for a referência do cliente.
- **Proposta recusada**: o motivo (preço, prazo, desempenho técnico, preferência pela solução atual, outro) é registrado e a proposta pode ser revisada.

## Requirements *(mandatory)*

### Functional Requirements

**Requisitos gerais (todas as stories)**

- **FR-001**: Cada produto MUST ser compatível com as interfaces do equipamento hospedeiro (dimensões envelope, furação, fixação, flanges), verificadas contra desenhos do cliente, documentação do OEM ou levantamento em campo.
- **FR-002**: Cada produto MUST ser instalável e substituível pela equipe de manutenção do cliente, com ferramentas convencionais e sem corte ou solda no equipamento hospedeiro, exceto quando isso já fizer parte da prática atual (story 2).
- **FR-003**: Cada peça manuseada manualmente MUST ter massa máxima de 25 kg por pessoa ou pontos de içamento identificados.
- **FR-004**: Cada produto MUST atender às normas de segurança aplicáveis à mineração no México (NOM-023-STPS e NOM-004-STPS) e aos requisitos do cliente e do OEM. As normas brasileiras citadas na constituição (NR-12, NR-22) servem de referência complementar.
- **FR-005**: Cada produto MUST ter um método de verificação física de cada requisito (inspeção dimensional, ensaio de material, teste de campo) e um critério de aceitação de primeira peça (FAI).
- **FR-006**: Cada produto MUST ter rastreabilidade de material e lote e vir com instrução de instalação e de critério de troca (espessura mínima ou sinal de fim de vida).
- **FR-007**: Cada proposta MUST trazer o custo total para o cliente (preço + frequência de troca + tempo de parada), comparado com a solução atual sempre que o preço atual ou de referência for conhecido.

**Story 1 – Calha de descarga do hidrociclone**

- **FR-101**: O revestimento MUST resistir ao mesmo tempo à abrasão da polpa e ao impacto de bolas de moinho de 3" sem desprendimento nem fratura de peças.
- **FR-102**: O revestimento MUST manter a fixação durante toda a vida útil. Peças soltas são falha.

**Story 2 – Placas de desgaste**

- **FR-201**: A chapa MUST poder ser cortada e fixada no local com os meios que o cliente já usa, ou vir com instrução de corte e fixação.
- **FR-202**: A chapa MUST ter vida útil ≥ 1,5× a do Hardox 5/8" na mesma posição e custo por hora de operação (preço da chapa + mão de obra de corte e instalação ÷ horas de vida) ≤ o do Hardox. Os dois critérios são obrigatórios.

**Story 3 – Célula de flotação**

- **FR-301**: Antes da proposta, a equivalência entre a célula da Concentradora 2 e o equipamento já medido MUST ser confirmada por modelo, fabricante e dimensões críticas.

**Story 4 – Peças magnéticas**

- **FR-401**: A peça MUST ser instalada por fora, com o equipamento em operação, por no máximo 2 mantenedores e sem ferramenta especial.
- **FR-402**: A peça MUST se manter fixa sob vibração e fluxo de polpa até a próxima parada programada, com referência de 30 dias.
- **FR-403**: A peça MUST se adaptar à curvatura das superfícies típicas (chutes planos e tubos) informadas pelo cliente.
- **FR-404**: A peça MUST poder ser removida e reutilizada.

**Story 5 – Hidrociclones**

- **FR-501**: O revestimento MUST preservar a geometria interna e o desempenho de classificação do hidrociclone original (incluindo o Cavex 48).

**Story 6 – Britadores cônicos**

- **FR-601**: O revestimento MUST encaixar na fixação existente da região inferior do britador e ter vida útil de pelo menos 17.000 horas.

**Story 7 – Tubulações**

- **FR-701**: O tubo revestido MUST ser intercambiável com os tubos existentes de 24" × 6 m (flanges, comprimento, classe de pressão).

**Story 8 – Belt skirting**

- **FR-801**: O material MUST ser fornecido nas dimensões confirmadas pelo cliente e ser compatível com os fixadores de skirting existentes.

**Requisitos comerciais**

- **FR-901**: Para cada story, a Haver MUST pedir ao cliente o preço atual ou de referência da solução em uso antes de fechar a proposta.
- **FR-902**: Toda resposta negativa a uma proposta MUST ter o motivo registrado, para tratar a objeção e revisar a proposta.

### Estrutura do Produto *(Key Entities)*

- **Revestimento da calha de descarga** (S1): conjunto de peças de desgaste com sistema de fixação para a calha de descarga do hidrociclone.
- **Placa de desgaste** (S2): chapa em dimensões padrão, para corte e fixação no local.
- **Kit de revestimento da célula de flotação** (S3): conjunto de peças por modelo de célula, com mapa de montagem.
- **Peça magnética de reparo provisório** (S4): placa de vedação com ímãs, adaptável a superfícies planas e curvas, em uma ou mais medidas.
- **Revestimento de hidrociclone** (S5): revestimento interno por seção do hidrociclone (ex.: Cavex 48).
- **Revestimento inferior do britador cônico** (S6): segmentos de revestimento com fixação na região inferior do britador.
- **Tubo revestido 24" × 6 m** (S7): carretel flangeado com revestimento interno.
- **Belt skirting** (S8): rolo de material de vedação lateral nas dimensões do cliente.

Todo item vem com desenho, especificação de material, critério de troca, instrução de instalação e rastreabilidade.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001** (S1): O revestimento da calha de descarga alcança **≥ 12 meses** de operação, contra ~8 meses hoje (+50%), sem peças soltas ou quebradas.
- **SC-002** (S2): A placa de desgaste alternativa tem vida útil pelo menos **1,5 vez** a do Hardox 5/8" na mesma posição, com **custo por hora de operação** igual ou menor.
- **SC-003** (S3): O kit da célula de flotação é instalado na primeira tentativa com **0 peças** precisando de ajuste em campo.
- **SC-004** (S4): A peça magnética é instalada em **≤ 15 minutos** por no máximo 2 pessoas, sem parar o equipamento, e fica fixa até a parada programada (referência **30 dias**).
- **SC-005** (S5): O revestimento do hidrociclone tem vida útil **≥** à da solução atual (borracha / carbeto de silício) e a classificação continua equivalente à atual.
- **SC-006** (S6): O revestimento inferior do britador alcança **≥ 17.000 horas** de operação.
- **SC-007** (S7): O tubo revestido de 24" tem vida útil projetada **≥ 1,25 vez** a do tubo de borracha da mesma linha.
- **SC-008** (S8): O belt skirting tem vida útil **≥** à do material atual e **custo por metro instalado ≤** ao preço atual informado.
- **SC-009** (comercial): **100%** das propostas têm preço de referência pedido ao cliente, e **100%** das recusas têm motivo registrado.
- **SC-010** (comercial): Pelo menos **3 das 8** oportunidades chegam a teste de campo ou pedido em até 6 meses após a visita.

## Assumptions

- **Escopo**: um único programa de produtos para a Concentradora 2, com 8 user stories independentes. **Nesta fase, o plano e as tarefas cobrem só as P1 (S1 e S2).** S3–S8 ficam com status "aguardando dados do cliente" e entram no plano (ou viram specs próprias) quando os desenhos, as dimensões ou a confirmação de equivalência chegarem.
- **Vida útil** é medida em horas efetivas de operação ou em toneladas processadas. Quando o cliente só souber em meses de calendário (story 1), vale o regime de operação atual.
- **Metas sem número no resumo** foram definidas por mim e devem ser confirmadas com o cliente: S4 15 min / 30 dias; S7 ×1,25; S10 3 de 8 em 6 meses.
- **Condições de operação** (minério, granulometria, % de sólidos, vazões, pressões, temperatura) ainda não foram informadas e dependem dos desenhos e dados que o cliente vai enviar.
- **Normas**: a planta fica no México. Valem as normas mexicanas de segurança (STPS) e os requisitos do Grupo México. As normas ABNT/NR da constituição servem de referência de boas práticas.
- **Alternativas citadas na visita** (poliuretano, poliuretano + cerâmica, chapa "Rhino Hyde" 1") são hipóteses de solução para avaliar no plano. Esta spec não as impõe.
- **A Haver tem processos** de moldagem de poliuretano e de montagem de conjuntos com insertos cerâmicos, ou pode contratá-los (a confirmar no plano).
- **Dependências do cliente** (próximos passos combinados na visita):

  | Story | Pendência | Responsável |
  |---|---|---|
  | S1 Calha de descarga | Fotos da aplicação e desenhos | Cliente → avaliação pela Engenharia Haver |
  | S2 Placas de desgaste | Cotação | Haver |
  | S3 Célula de flotação | Confirmar equivalência; proposta | Haver |
  | S4 Peças magnéticas | Cotação | Haver |
  | S5 Hidrociclones | Desenhos | Cliente |
  | S6 Britadores cônicos | Desenhos | Cliente |
  | S7 Tubulações 24" | Desenhos → cotação | Cliente → Haver |
  | S8 Belt skirting | Dimensões e preço atual | Cliente |
  | Todas | Preço atual/de referência; motivo de eventual recusa | Cliente |
