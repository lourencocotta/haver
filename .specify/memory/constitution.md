# Haver Constitution

## Core Principles

### I. Produto Manufaturado, Nunca Software (NÃO-NEGOCIÁVEL)

Toda solução entregue por este projeto é um **produto físico manufaturado destinado a
equipamentos de mineração** (peças, componentes, conjuntos, peças de desgaste, peças de
reposição ou equipamentos completos).

- Uma solução MUST NOT ser um software, aplicativo, sistema web, API, serviço digital,
  dashboard ou firmware entregue como produto.
- Ferramentas digitais (CAD, CAE/FEA, planilhas, simulação) MAY ser usadas apenas como
  **meios de engenharia**; o entregável é sempre o produto físico e sua documentação técnica.
- Todo artefato do Spec Kit (spec, plan, tasks, checklists) MUST descrever o produto, sua
  fabricação, sua montagem no equipamento hospedeiro e sua validação física.
- Qualquer proposta cuja resposta seja "desenvolver um software" MUST ser reformulada como
  produto manufaturado ou rejeitada como fora de escopo.

**Racional**: o negócio da Haver é fabricar produtos para mineração; resolver um problema com
software desvia esforço do que o cliente compra e do que a fábrica produz.

### II. Segurança e Conformidade Normativa

- Todo produto MUST atender às normas aplicáveis ao seu uso em mineração, incluindo, quando
  pertinentes, NR-12 (segurança em máquinas), NR-22 (segurança na mineração), normas ABNT/ISO
  de materiais, soldagem, tratamento térmico e ensaios, e requisitos específicos do cliente ou do
  fabricante do equipamento hospedeiro (OEM).
- Requisitos de segurança (pontos de pega, içamento, massa por peça, travamentos, proteções,
  bordas cortantes, risco de projeção) MUST ser explícitos na especificação.
- Riscos de falha MUST ser analisados (ex.: FMEA de projeto e de processo) antes da liberação
  para fabricação.

**Racional**: falhas em equipamentos de mineração causam acidentes graves e paradas de alto
custo; conformidade não é opcional.

### III. Projeto Orientado às Condições Reais de Operação

- Toda especificação MUST declarar as condições de campo: equipamento hospedeiro (tipo, modelo,
  fabricante), material processado (minério, granulometria, abrasividade, umidade), cargas,
  impacto, vibração, temperatura, ambiente corrosivo e regime de operação.
- Requisitos de desempenho MUST ser mensuráveis em grandezas físicas (vida útil em horas ou
  toneladas processadas, eficiência de peneiramento, taxa de desgaste, carga admissível,
  tolerâncias dimensionais).
- Interfaces com o equipamento hospedeiro (furação, fixação, encaixes, dimensões envelope)
  MUST ser definidas e verificadas contra o equipamento real ou documentação do OEM.

**Racional**: o produto só tem valor se encaixa e resiste no equipamento do cliente.

### IV. Fabricabilidade e Qualidade Verificável

- O projeto MUST ser fabricável com os processos disponíveis ou explicitamente contratados
  (corte, conformação, soldagem, usinagem, fundição, moldagem de poliuretano/borracha,
  tratamento térmico, revestimento), com tolerâncias compatíveis com esses processos (DFM/DFA).
- Cada requisito MUST ter um método de verificação física definido: inspeção dimensional,
  ensaio de material, ensaio não destrutivo, ensaio de protótipo em bancada ou em campo.
- Materiais, lotes e números de série MUST ser rastreáveis (certificados de material, registros
  de inspeção), alinhado a um sistema de gestão da qualidade (ex.: ISO 9001).
- Nenhum produto é liberado para produção seriada sem aprovação de protótipo ou primeira peça
  (FAI) contra os critérios de aceitação da especificação.

**Racional**: qualidade se prova com medição e ensaio, não com declaração.

### V. Durabilidade, Manutenibilidade e Custo Total

- Produtos MUST priorizar vida útil, facilidade e segurança de troca em campo (tempo de parada
  mínimo) e intercambiabilidade com peças existentes, quando aplicável.
- Decisões de projeto MUST considerar o custo total de propriedade do cliente (custo da peça +
  parada + mão de obra de troca + frequência de reposição), não apenas o custo de fabricação.
- Projetos MUST preferir soluções simples, padronizadas e com componentes de catálogo; toda
  complexidade adicional MUST ser justificada.

**Racional**: na mineração, disponibilidade do equipamento vale mais que a peça.

## Restrições de Engenharia e Manufatura

- **Entregáveis válidos**: requisitos do produto, conceito de engenharia, memorial de cálculo,
  desenhos técnicos e modelos 3D (como referência), lista de materiais (BOM), especificação de
  materiais, roteiro/processo de fabricação, plano de controle e inspeção, FMEA, plano de
  ensaio e validação, instruções de montagem/instalação/manutenção, catálogo de peças de
  reposição e embalagem/transporte.
- **Entregáveis proibidos como solução**: código-fonte de aplicação, APIs, bancos de dados,
  interfaces de usuário, serviços em nuvem ou firmware como produto final.
- **Tradução obrigatória de termos do Spec Kit** (os comandos foram escritos para software e
  MUST ser interpretados assim):

  | Termo do Spec Kit              | Significado neste projeto                                   |
  |--------------------------------|-------------------------------------------------------------|
  | Feature / funcionalidade       | Produto, componente, conjunto ou melhoria de produto        |
  | Usuário / user story           | Cliente, operador, mantenedor ou OEM e sua necessidade      |
  | Tech stack / Technical Context | Materiais, processos de fabricação, normas, equipamento     |
  |                                | hospedeiro, condições de operação                           |
  | data-model.md                  | Estrutura do produto: árvore de itens, BOM, materiais       |
  | contracts/                     | Interfaces físicas com o equipamento hospedeiro e entre     |
  |                                | componentes (dimensões, fixações, cargas)                   |
  | quickstart.md                  | Plano de validação: protótipo, FAI, ensaios e critérios     |
  | Código-fonte / `src/`          | Documentação técnica do produto no repositório              |
  | Testes                         | Inspeções, ensaios e validação física                       |
  | Implementar                    | Elaborar a documentação de engenharia e manufatura          |
  | Deploy / release               | Liberação para produção, entrega e instalação em campo      |
  | Performance                    | Vida útil, capacidade, eficiência, resistência              |

## Fluxo de Desenvolvimento e Portões de Qualidade

1. **Especificação** (`/speckit-specify`, `/speckit-clarify`): necessidade do cliente, equipamento
   hospedeiro, condições de operação, requisitos mensuráveis e critérios de aceitação físicos.
2. **Plano de engenharia** (`/speckit-plan`): conceito de solução, seleção de materiais e
   processos, normas aplicáveis, estrutura do produto, interfaces e plano de validação.
3. **Tarefas** (`/speckit-tasks`): atividades de engenharia, compras, fabricação de protótipo,
   inspeção, ensaio e liberação, organizadas por necessidade do cliente.
4. **Execução** (`/speckit-implement`): produção dos documentos de engenharia e manufatura no
   repositório; atividades físicas (fabricar, ensaiar, instalar) são registradas como tarefas
   com responsável humano e evidência requerida.

Portões obrigatórios:

- **Portão de Conceito**: Princípio I verificado — a solução é um produto físico.
- **Portão de Projeto**: segurança, normas, interfaces e fabricabilidade revisadas; FMEA feito.
- **Portão de Protótipo/FAI**: critérios de aceitação atendidos com evidência de ensaio.
- **Portão de Produção**: plano de controle, rastreabilidade e instruções de montagem completos.

## Governance

- Esta constituição prevalece sobre qualquer outra prática, template ou instrução de comando do
  Spec Kit. Em conflito, os comandos MUST ser reinterpretados conforme a tabela de tradução.
- Toda especificação, plano e revisão MUST verificar conformidade com os Princípios I a V; o
  Princípio I é bloqueante e não admite justificativa de exceção.
- Emendas MUST ser documentadas neste arquivo, com justificativa e impacto nos artefatos
  existentes, e aprovadas pelo responsável técnico de engenharia do produto.
- Versionamento semântico: MAJOR para remoção ou redefinição de princípios; MINOR para novos
  princípios ou seções; PATCH para esclarecimentos de redação.
- Conformidade MUST ser revisada a cada novo produto e em cada portão de qualidade.

**Version**: 1.0.0 | **Ratified**: 2026-10-03 | **Last Amended**: 2026-10-03
