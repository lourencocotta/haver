# Feature Specification: Acompanhamento de Oportunidades de Visitas a Clientes

**Feature Branch**: `001-visit-opportunity-tracker`

**Created**: 2026-10-03

**Status**: Draft

**Input**: User description: resumo de visita enviado por Laís Andrade a Isidro: "Grupo Mexico - Concentradora 2 - Resumen de visita y próximos pasos - visita 9/9/26". O resumo lista 8 oportunidades comerciais de revestimentos e peças de desgaste, cada uma com a solução atual do cliente, a proposta e o próximo passo. Também pede preços de referência para cada oportunidade e, em caso de recusa, o motivo.

## Contexto

Depois de cada visita técnico-comercial a um cliente industrial (mineração, beneficiamento), a equipe comercial envia um e-mail com as oportunidades identificadas e os próximos passos. Hoje esse acompanhamento fica só no e-mail. Fica difícil saber quais desenhos, fotos e preços o cliente ainda deve, quais cotações a equipe precisa preparar, que proposta foi enviada e por que uma proposta foi recusada.

Esta funcionalidade organiza o resultado de uma visita em uma estrutura acompanhável. A estrutura é: **visita → oportunidades → próximos passos → proposta → resultado**. O resumo da visita à Concentradora 2 do Grupo México é o caso de referência.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Registrar visita e suas oportunidades (Priority: P1)

Depois de uma visita, a pessoa responsável pela conta (por exemplo, Laís) registra os dados da visita: cliente, unidade/planta, data e participantes. Em seguida registra cada oportunidade identificada, com:

- equipamento ou aplicação;
- solução atual do cliente (material, vida útil atual);
- solução proposta;
- dados técnicos citados (dimensões, espessuras, modelos);
- próximo passo.

**Why this priority**: Sem esse registro não existe nada para acompanhar. Mesmo isolado, ele já substitui o e-mail como fonte única e consultável do que foi combinado.

**Independent Test**: Cadastrar a visita de 9/9/2026 à Concentradora 2 com as 8 oportunidades do resumo e verificar que todas aparecem com as informações completas.

**Acceptance Scenarios**:

1. **Given** um cliente "Grupo México" com a unidade "Concentradora 2", **When** a usuária registra a visita de 09/09/2026 com os participantes Gilberto Lopes, Ismael Burgos, Jorge, Isidro e Laís, **Then** a visita fica salva e aparece no histórico do cliente.
2. **Given** a visita registrada, **When** a usuária adiciona a oportunidade "Calha de descarga do hidrociclone" com a solução atual "revestimento cerâmico padrão aparafusado", a vida útil atual de ~8 meses, a meta de >12 meses e as condições "abrasão + impacto de bolas de moinho de 3"", **Then** a oportunidade fica vinculada à visita com todos esses dados.
3. **Given** uma visita com 8 oportunidades, **When** alguém abre a visita, **Then** vê a lista das 8 com o título, o status e o próximo passo de cada uma.

---

### User Story 2 - Acompanhar próximos passos e pendências (Priority: P1)

Cada oportunidade tem um ou mais próximos passos. Cada passo tem um responsável, que pode ser **do cliente** ou **da nossa empresa**. Exemplos de passo do cliente: enviar desenhos, fotos, dimensões ou preço atual. Exemplos de passo nosso: preparar cotação, confirmar equivalência de equipamento, avaliar com a Engenharia. A equipe precisa ver rapidamente o que está esperando o cliente e o que está esperando a própria equipe.

**Why this priority**: É o motivo principal da ferramenta. No caso de referência, 4 das 8 oportunidades estão paradas esperando desenhos do cliente e 3 esperam uma cotação nossa. Sem visibilidade, isso se perde.

**Independent Test**: Com a visita de referência cadastrada, filtrar as pendências "aguardando cliente" e conferir que aparecem os desenhos de britador cônico, hidrociclone, tubulação de 24" e calha de descarga (fotos + desenhos), mais as dimensões e o preço do belt skirting.

**Acceptance Scenarios**:

1. **Given** a oportunidade "Revestimento de hidrociclones" com o passo "Enviar desenhos" atribuído ao cliente, **When** a usuária consulta as pendências do cliente, **Then** esse passo aparece na lista.
2. **Given** um passo "Preparar cotação" nosso para "Peças magnéticas para reparos provisórios", **When** o passo é marcado como concluído, **Then** ele sai da lista de pendências e a data de conclusão fica registrada.
3. **Given** um passo do cliente em aberto há mais tempo que o prazo de acompanhamento, **When** a equipe consulta as pendências, **Then** o passo aparece destacado como atrasado.

---

### User Story 3 - Registrar preço atual / de referência (Priority: P2)

Para cada oportunidade, a equipe registra, quando houver, o preço que o cliente paga hoje pela solução atual ou um preço de referência. Também registra a origem da informação (informado pelo cliente, estimativa interna, etc.). Assim a proposta pode ser comercialmente viável.

**Why this priority**: O resumo diz que esse dado é "muito importante" para todas as oportunidades. Mesmo assim, uma proposta pode ser preparada sem ele, por isso vem depois do registro e das pendências.

**Independent Test**: Registrar o preço atual do belt skirting e verificar que ele aparece na oportunidade e que as oportunidades sem preço de referência podem ser listadas.

**Acceptance Scenarios**:

1. **Given** a oportunidade "Belt skirting" sem preço de referência, **When** a usuária registra o preço informado pelo cliente, com moeda, unidade e data, **Then** o preço fica associado à oportunidade com a origem "informado pelo cliente".
2. **Given** várias oportunidades, **When** a usuária filtra "sem preço de referência", **Then** vê apenas as que ainda não têm essa informação.

---

### User Story 4 - Registrar proposta e resultado, com motivo de recusa (Priority: P2)

Quando a proposta de uma oportunidade é enviada, a equipe registra a data de envio e o valor. Depois registra o resultado: aceita, recusada, em teste ou em negociação. Se a proposta for recusada, é obrigatório registrar o motivo informado pelo cliente (preço, prazo, desempenho técnico, preferência por fornecedor atual, etc.). Assim é possível trabalhar a objeção e tentar reverter.

**Why this priority**: O resumo pede explicitamente o motivo das respostas negativas. Esse dado só existe depois que as propostas forem enviadas.

**Independent Test**: Registrar a proposta de Rhino Hyde de 1" em substituição ao Hardox de 5/8", marcá-la como recusada pelo motivo "preço" e verificar que o motivo aparece e que a oportunidade pode ser reaberta.

**Acceptance Scenarios**:

1. **Given** uma oportunidade com cotação pronta, **When** a usuária registra o envio da proposta, **Then** o status passa a "Proposta enviada" com data e valor.
2. **Given** uma proposta enviada, **When** a usuária marca o resultado como "Recusada", **Then** o sistema exige uma categoria de motivo antes de salvar, e o texto livre do cliente é opcional.
3. **Given** uma proposta recusada, **When** a equipe decide ajustar a proposta, **Then** a oportunidade pode ser reaberta e o histórico da proposta anterior e do motivo da recusa é mantido.
4. **Given** uma proposta aceita para teste (por exemplo, poliuretano + cerâmica no britador cônico), **When** o resultado é registrado como "Em teste", **Then** a oportunidade fica identificada como teste de campo, com a vida útil de referência da solução atual (>17.000 h) disponível para comparação.

---

### User Story 5 - Gerar resumo da visita para o cliente (Priority: P3)

A partir da visita registrada, a equipe gera um resumo no formato do e-mail de referência: participantes, oportunidades numeradas, situação atual, próximo passo e o pedido de preços e motivos de recusa. O resumo pode ser enviado ao contato do cliente.

**Why this priority**: Hoje esse texto é escrito à mão. Gerá-lo a partir dos dados evita divergência entre o que foi enviado e o que é acompanhado, mas é conveniência e não o núcleo da funcionalidade.

**Independent Test**: Gerar o resumo da visita de referência e comparar com o e-mail original: devem constar as 8 oportunidades, a situação atual e o próximo passo de cada uma.

**Acceptance Scenarios**:

1. **Given** uma visita com oportunidades registradas, **When** a usuária pede o resumo, **Then** recebe um texto com cabeçalho (cliente, unidade, data da visita), participantes, as oportunidades numeradas (situação atual + próximo passo) e o fechamento padrão.
2. **Given** o resumo gerado, **When** a usuária edita o texto antes de enviar, **Then** as edições não alteram os dados registrados.

---

### Edge Cases

- **Oportunidade identificada fora da reunião**: o belt skirting foi visto no pátio depois da reunião. Precisa ser possível registrá-lo na mesma visita, indicando a origem "observação em campo".
- **Equivalência de equipamento não confirmada**: na célula de flotação, a oportunidade depende de confirmar que o equipamento é igual a um já medido. O status precisa mostrar "aguardando confirmação" e permitir vincular as medições existentes.
- **Várias alternativas na mesma oportunidade**: no hidrociclone, a proposta pode ser poliuretano com ou sem cerâmica. Precisa ser possível registrar mais de uma alternativa de solução.
- **Cliente nunca envia o material pedido**: o passo continua aberto, é marcado como atrasado e pode ser encerrado como "sem retorno" sem perder o histórico.
- **Unidades mistas**: medidas em polegadas e milímetros (5/8" = 16 mm, 24", 6 m) e vida útil em horas ou meses precisam ser registradas sem perder a unidade original.
- **Participante citado só pelo primeiro nome** ("Jorge"): o registro é aceito sem sobrenome ou empresa.
- **Oportunidade sem preço de referência**: a proposta pode ser enviada mesmo assim, mas a falta do dado fica visível.
- **Visita a cliente/unidade ainda não cadastrado**: dá para cadastrar o cliente ou a unidade no momento de registrar a visita.

## Requirements *(mandatory)*

### Functional Requirements

**Visitas**

- **FR-001**: O sistema MUST permitir registrar uma visita com cliente, unidade/planta, data e lista de participantes (nome e, opcionalmente, empresa e função).
- **FR-002**: O sistema MUST manter o histórico de visitas por cliente e por unidade, da mais recente para a mais antiga.

**Oportunidades**

- **FR-003**: O sistema MUST permitir registrar várias oportunidades por visita, cada uma com: título, equipamento/aplicação, solução atual (material e fornecedor, se conhecido), vida útil atual (valor + unidade), meta de vida útil (opcional), condições de operação (texto livre) e dados técnicos (dimensões, espessuras, modelos).
- **FR-004**: O sistema MUST permitir registrar uma ou mais alternativas de solução proposta por oportunidade (por exemplo, "poliuretano + cerâmica", "poliuretano sem cerâmica", "Rhino Hyde 1"").
- **FR-005**: O sistema MUST permitir indicar a origem da oportunidade (discutida na reunião / observada em campo / outra).
- **FR-006**: Cada oportunidade MUST ter um status num ciclo definido: *Identificada → Aguardando informações do cliente → Em avaliação interna (ex.: Engenharia) → Cotação em preparação → Proposta enviada → Em teste / Em negociação → Ganha / Perdida / Sem retorno*. O status MUST poder ser reaberto a partir de Perdida ou Sem retorno.
- **FR-007**: O sistema MUST guardar o histórico de mudanças de status de cada oportunidade, com data e autor.

**Próximos passos e pendências**

- **FR-008**: O sistema MUST permitir registrar próximos passos por oportunidade, com descrição, tipo (enviar desenhos, enviar fotos, informar dimensões, informar preço atual, preparar cotação, confirmar equivalência de equipamento, avaliação técnica, outro), lado responsável (cliente ou nossa empresa), pessoa responsável (opcional), data de criação e prazo de acompanhamento.
- **FR-009**: O sistema MUST listar as pendências abertas filtradas por lado responsável (cliente / nossa empresa), por cliente e por visita.
- **FR-010**: O sistema MUST destacar como atrasados os passos abertos com prazo vencido. O prazo padrão é de 14 dias após a criação do passo, editável.
- **FR-011**: Ao concluir um passo, o sistema MUST registrar a data de conclusão e permitir anexar ou referenciar o material recebido (desenhos, fotos, medições).

**Preços de referência**

- **FR-012**: O sistema MUST permitir registrar, por oportunidade, um ou mais preços de referência, com valor, moeda, unidade de preço (por peça, por metro, por m², etc.), data e origem (informado pelo cliente / estimativa interna / histórico).
- **FR-013**: O sistema MUST permitir listar as oportunidades sem preço de referência.

**Propostas e resultado**

- **FR-014**: O sistema MUST permitir registrar propostas por oportunidade, com data de envio, valor, moeda e alternativa de solução a que se referem. Uma oportunidade pode ter várias propostas (revisões).
- **FR-015**: Ao marcar uma proposta como recusada, o sistema MUST exigir uma categoria de motivo (preço, prazo de entrega, desempenho técnico/dúvida técnica, preferência pelo fornecedor/solução atual, sem orçamento, outro), com texto livre opcional.
- **FR-016**: O sistema MUST permitir registrar o resultado de um teste de campo (data de início, data de fim, vida útil obtida) e mostrá-lo junto da vida útil da solução atual.

**Resumo da visita**

- **FR-017**: O sistema MUST gerar, a partir de uma visita, um resumo textual com cabeçalho, participantes, oportunidades numeradas (situação atual e próximo passo) e o pedido padrão de preços de referência e de motivos de recusa. O texto pode ser editado antes do envio.
- **FR-018**: O resumo MUST ser gerado no idioma escolhido pela usuária, no mínimo português e espanhol.

**Acesso**

- **FR-019**: Apenas usuários autenticados da equipe comercial/técnica MUST ter acesso aos dados de visitas, oportunidades e preços.

### Key Entities

- **Cliente**: grupo empresarial (ex.: Grupo México). Tem uma ou mais unidades.
- **Unidade/Planta**: local físico do cliente (ex.: Concentradora 2). As visitas e os equipamentos pertencem a ela.
- **Visita**: encontro numa unidade, numa data, com participantes. Agrupa oportunidades.
- **Participante**: pessoa presente na visita (nome; empresa e função opcionais; lado cliente ou nossa empresa).
- **Oportunidade**: aplicação ou equipamento com potencial comercial (ex.: calha de descarga do hidrociclone). Tem solução atual, vida útil, condições de operação, dados técnicos, alternativas de solução, status e histórico.
- **Alternativa de solução**: material/configuração proposta para uma oportunidade (ex.: poliuretano + cerâmica).
- **Próximo passo**: ação pendente vinculada a uma oportunidade, com lado responsável, tipo, prazo e conclusão.
- **Preço de referência**: valor atual ou de referência da solução, com moeda, unidade, data e origem.
- **Proposta**: oferta enviada para uma alternativa de solução, com valor, data e resultado (aceita, recusada + motivo, em teste, em negociação).
- **Teste de campo**: avaliação prática de uma solução aceita para teste, com período e vida útil obtida.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Uma visita com 8 oportunidades, como a de referência, pode ser registrada por completo em até 20 minutos.
- **SC-002**: Em até 30 segundos, qualquer membro da equipe responde "o que estamos aguardando do cliente X?" e "quais cotações precisamos preparar?".
- **SC-003**: 100% das propostas marcadas como recusadas têm motivo registrado.
- **SC-004**: Nenhum próximo passo fica mais de 7 dias atrasado sem ação, porque todos os atrasos aparecem na lista de pendências.
- **SC-005**: Pelo menos 80% das oportunidades com proposta enviada têm preço de referência registrado antes do envio.
- **SC-006**: O resumo gerado da visita de referência contém as 8 oportunidades, com situação atual e próximo passo, sem precisar reescrever o conteúdo.

## Assumptions

- **Natureza da funcionalidade**: o e-mail fornecido é o caso de referência de uma ferramenta interna de acompanhamento de visitas e oportunidades. Não é uma especificação de produto industrial (revestimentos), e as decisões técnicas de cada revestimento ficam fora do escopo.
- Os usuários são a equipe comercial e técnica da empresa fornecedora (por exemplo, Laís, Isidro). O cliente não acessa a ferramenta na primeira versão. A comunicação com o cliente continua por e-mail, usando o resumo gerado.
- O envio automático de e-mails, a integração com CRM/ERP e o cálculo de preço da cotação ficam fora do escopo da primeira versão. A ferramenta guarda as cotações e propostas, mas não as calcula.
- Os anexos (desenhos, fotos) podem ser referenciados por link ou anexados. O armazenamento de arquivos grandes de engenharia não é requisito da primeira versão.
- O prazo padrão de acompanhamento é de 14 dias. Ele pode ser ajustado por passo.
- As categorias de motivo de recusa seguem a lista do FR-015 e podem ser revistas depois.
- Moedas usuais: MXN, USD e BRL. Unidades de medida em polegadas e no sistema métrico são aceitas e guardadas como informadas.
- **Dados de referência (visita 09/09/2026, Grupo México – Concentradora 2)**, para cadastro inicial e testes de aceitação:

  | # | Oportunidade | Solução atual | Proposta | Próximo passo | Lado |
  |---|---|---|---|---|---|
  | 1 | Revestimento inferior dos britadores cônicos | Hardox (>17.000 h); em teste: borracha + cerâmica | Teste com poliuretano + cerâmica | Enviar desenhos | Cliente |
  | 2 | Peças magnéticas para reparos provisórios | Solução semelhante já em uso | Peças com ímãs para cobrir perfurações | Preparar cotação | Nossa empresa |
  | 3 | Revestimento de hidrociclones (inclui Cavex 48) | Borracha + cerâmica de carbeto de silício | Poliuretano com ou sem cerâmica | Enviar desenhos | Cliente |
  | 4 | Calha de descarga do hidrociclone | Cerâmica padrão aparafusada (~8 meses; meta >1 ano; abrasão + impacto de bolas de 3") | A definir com a Engenharia | Enviar fotos e desenhos; avaliar com a Engenharia | Cliente → Nossa empresa |
  | 5 | Tubulações revestidas | Borracha (24", maioria com 6 m) | Teste com nossa solução | Enviar desenhos; preparar cotação | Cliente → Nossa empresa |
  | 6 | Placas de desgaste | Hardox 5/8" (16 mm), cortado no local | Teste com Rhino Hyde 1" | Preparar cotação | Nossa empresa |
  | 7 | Célula de flotação | Borracha e poliuretano | Proposta do modelo já medido | Confirmar equivalência; preparar proposta | Nossa empresa |
  | 8 | Belt skirting (observado no pátio) | Rolo de poliuretano | Proposta competitiva | Confirmar dimensões e preço atual | Cliente |
