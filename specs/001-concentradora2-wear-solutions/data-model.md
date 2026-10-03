# Estrutura do Produto (Phase 1): S1 e S2

**Data**: 2026-10-03 | **Plano**: [plan.md](./plan.md) | **Pesquisa**: [research.md](./research.md)

> Este é o `data-model.md` do Spec Kit, lido como **estrutura do produto**: árvore de itens, lista de materiais (BOM), materiais e massas. As quantidades e as dimensões finais dependem das entradas do cliente listadas em [research.md §R7](./research.md#r7-entradas-que-o-cliente-precisa-enviar-até-lá-valem-as-premissas-de-projeto).

---

## S1 – Kit de revestimento da calha de descarga do hidrociclone (teste de campo)

```text
S1-KIT  Kit de revestimento – calha de descarga (1 calha)
├── S1-PNL-xx  Painel compósito cerâmica/PU com base de aço   (qtde: N painéis, conforme desenho)
│   ├── Base de aço (chapa de fixação, furada)                 ASTM A36, esp. ref. 6,35 mm
│   ├── Matriz de poliuretano termofixo                        Rhino Hyde, dureza ref. 85–90 Shore A
│   ├── Insertos cerâmicos encapsulados                        Alumina ≥ 92%, cilindros/pastilhas
│   └── Pontos de medição + furo-testemunho de desgaste        mapa por painel
├── S1-FIX  Conjunto de fixação por painel                     parafuso escareado + porca + arruela, aço classe 8.8 ou equivalente
├── S1-TAMP Tampões de PU para cabeças de parafuso             1 por parafuso
├── S1-DOC  Documentação: mapa de montagem, instrução de instalação, critério de troca, relatório de FAI
└── S1-SPR  Reserva de campo                                   2 painéis do tipo mais solicitado + 10% de fixações
```

**Regras de validação** (rastreadas à spec):

| Regra | Origem |
|---|---|
| Massa de cada painel ≤ 25 kg; se for maior, ponto de içamento identificado | FR-003 |
| Nenhum inserto pode se soltar da matriz durante a vida útil; peça solta = reprovação | FR-101, FR-102 |
| Fixação compatível com a furação existente e sem solda ou corte na calha | FR-001, FR-002 |
| Espessura útil de desgaste e espessura de troca marcadas em cada painel | FR-006, R5 |
| Lote do PU, lote da cerâmica e corrida do aço rastreáveis por número de série do painel | FR-006 |

**Comparação**: uma calha igual permanece com o revestimento cerâmico aparafusado atual (fornecido pelo cliente) e recebe os mesmos pontos de medição (FR-103).

---

## S2 – Painéis de desgaste PU 1" (teste de campo)

```text
S2-LOTE  Lote de teste – 2 a 4 posições
├── S2-PNL-B-xx  Painel Rhino Hyde Blue 25,4 mm, versão aparafusada   (pré-cortado por posição)
│   ├── Chapa de PU termofixo 25,4 mm
│   └── Buchas/arruelas de aço embutidas nos furos
├── S2-PNL-W-xx  Painel Rhino Hyde 25,4 mm, versão soldável           (pré-cortado por posição)
│   ├── Chapa de PU termofixo 25,4 mm
│   └── Base de aço soldável, ligada ao PU
├── S2-FIX  Fixações (versão aparafusada)
├── S2-DOC  Instrução de corte a frio e de fixação/solda; mapa dos pontos de medição; relatório de inspeção
└── S2-REF  (do cliente) Chapa Hardox 5/8" de comparação ao lado de cada painel
```

A versão (B ou W) de cada posição segue a fixação usada hoje nessa posição (contrato [S2-interface](./contracts/s2-interface-posicao-desgaste.md)).

**Massas de referência**:

| Item | Massa por área | Painel máx. a 25 kg |
|---|---|---|
| PU 25,4 mm | ≈ 30 kg/m² | ≈ 0,80 m² |
| PU 25,4 mm + base de aço 3 mm (soldável) | ≈ 54 kg/m² | ≈ 0,45 m² |
| Hardox 16 mm (referência) | ≈ 126 kg/m² | ≈ 0,20 m² |

**Regras de validação**:

| Regra | Origem |
|---|---|
| Painel ≤ 25 kg ou com içamento definido | FR-003 |
| Posição de teste com temperatura < 80 °C, sem óleo ou solvente e sem bloco com aresta viva > 150 mm | R3 |
| Espessura inicial medida nos pontos marcados, no painel e no Hardox | FR-204 |
| O aumento de espessura (25,4 contra 16 mm) não interfere com folgas nem fluxo | US2, cenário 3 |

---

## Estados do item de teste (S1 e S2)

```text
Projetado → Protótipo fabricado → FAI aprovado → Instalado (T0) → Em monitoramento
   → Aprovado (critérios atingidos) → Liberado para fornecimento em série
   → Reprovado (motivo registrado) → Revisão de projeto → Protótipo fabricado
```

As transições "FAI aprovado" e "Aprovado" exigem evidência registrada: relatório dimensional, certificados e medições de campo ([quickstart.md](./quickstart.md)).
