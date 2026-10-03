# Implementation Plan: Soluções de Revestimento e Peças de Desgaste – Concentradora 2 (fase P1)

**Branch**: `001-visit-opportunity-tracker` | **Date**: 2026-10-03 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `specs/001-concentradora2-wear-solutions/spec.md`

**Escopo desta fase** (Clarifications Q1): somente **S1, a calha de descarga do hidrociclone**, e **S2, as placas de desgaste no lugar do Hardox 5/8"**. As histórias S3 a S8 esperam dados do cliente e serão planejadas depois.

## Summary

- **S1**: kit de **painéis compósitos de cerâmica de alumina encapsulada em poliuretano termofixo com base de aço** (linha Rhino Hyde, variante cerâmica + uretano), aparafusados na furação existente da calha.
  - O PU amortece o impacto das bolas de 3", o que evita a quebra da cerâmica.
  - O encapsulamento impede que as peças se soltem, os dois modos de falha atuais.
  - Validação: teste de campo com 1 calha revestida e 1 calha gêmea com a solução atual. Meta: ≥ 12 meses **e** ≥ 1,5× a vida da comparação.
- **S2**: **painéis Rhino Hyde Blue de 25,4 mm** pré-cortados, em versão aparafusada ou soldável (com base de aço), conforme a fixação atual de cada posição.
  - Teste em 2 a 4 posições lado a lado com o Hardox 5/8".
  - O teste termina quando o Hardox chega à espessura de troca.
  - Meta: vida projetada ≥ 1,5× **e** custo por hora ≤ o do Hardox.

## Technical Context

**Equipamento hospedeiro / OEM**:
- S1: calha de descarga (underflow) dos hidrociclones da Concentradora 2. Fabricante e geometria: **pendentes** (desenhos e fotos do cliente), research.md §R7.
- S2: várias superfícies de desgaste revestidas hoje com Hardox 5/8" (16 mm) cortado e instalado pelo cliente. As posições serão escolhidas pelos critérios do contrato S2.

**Materiais candidatos** (research.md §R1–R3):
- PU termofixo Rhino Hyde (ref. 85–90 Shore A);
- alumina ≥ 92% (insertos S1);
- base de aço ASTM A36 (S1 e S2-W);
- fixações classe 8.8.

**Processos de fabricação**: moldagem de PU termofixo (vazamento em molde aquecido e pós-cura), encapsulamento dos insertos cerâmicos, ligação química PU–aço, corte e furação da base de aço, corte a frio e furação do PU, montagem e embalagem. Fabricação na linha Rhino Hyde (Haver & Boecker Niagara / Tandem Products).

**Normas aplicáveis** (research.md §R4):
- segurança: NOM-023-STPS-2012, NOM-004-STPS-1999 e NOM-006-STPS-2014; NR-12 e NR-22 como referência complementar;
- materiais: ASTM D2240, D412, D624, D429, ISO 4649 e ASTM C373.

**Condições de operação**:
- S1: polpa abrasiva (premissa: 55–70% de sólidos) com bolas de aço de 3" (1,8 kg; 18–36 J por impacto, premissa).
- S2: deslizamento de minério britado ≤ 150 mm, < 80 °C, sem óleo.
- Os dados reais estão **pendentes** do cliente (§R7). As premissas de projeto valem até eles chegarem.

**Métodos de ensaio e inspeção**:
- ensaios de material por lote;
- FAI dimensional e de massa;
- espessura por ultrassom em pontos marcados;
- teste de campo com comparação lado a lado (quickstart.md).

**Volume / lote de produção**:
- S1: 1 kit para 1 calha + reserva de 2 painéis.
- S2: 2 a 4 painéis.
- Fornecimento em série só após aprovação do teste.

**Restrições**:
- ≤ 25 kg por painel;
- troca sem solda nem corte na calha (S1);
- espessura da S1 ≤ a atual + 10 mm;
- o PU não é cortado a quente nem soldado diretamente;
- troca dentro da parada programada.

**Metas de desempenho**:
- S1: ≥ 12 meses e ≥ 1,5× a vida da calha de comparação, sem peças soltas ou quebradas.
- S2: ≥ 1,5× a vida do Hardox e custo por hora ≤ o do Hardox.

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Princípio / Portão | Verificação | Pré-pesquisa | Pós-design |
|---|---|---|---|
| I. Produto manufaturado, nunca software | S1 e S2 são painéis físicos de revestimento; os entregáveis são desenhos, BOM, processos, ensaios e instruções | ✅ | ✅ |
| II. Segurança e normas | Normas STPS identificadas; massa ≤ 25 kg; bordas cobertas; bloqueio na troca; restrição de solda junto ao PU; FMEA previsto antes da fabricação | ✅ | ✅ (FMEA é tarefa obrigatória antes do Portão de Projeto) |
| III. Condições reais de operação | Equipamento e condições declarados; dados faltantes registrados como entradas do cliente, com premissas de projeto explícitas; interfaces em `contracts/` | ⚠️ parcial | ⚠️ parcial, aceito: o contrato S1 continua **PRELIMINAR** até receber os desenhos. A fabricação fica bloqueada até lá. |
| IV. Fabricabilidade e qualidade verificável | Processos da linha Rhino Hyde; ensaios ASTM/ISO; FAI; rastreabilidade por número de série | ✅ | ✅ |
| V. Durabilidade, manutenção, custo total | Troca aparafusada; peças leves (PU ≈ 4× mais leve que o Hardox); custo por hora como critério de aprovação; produtos de catálogo | ✅ | ✅ |
| Portão de Conceito | A solução é um produto físico | ✅ aprovado | ✅ |

**Resultado**: aprovado, sem violações. O item ⚠️ do Princípio III é uma pendência de entrada do cliente, não uma violação. Fica controlado pelo bloqueio "contrato S1 preliminar → sem liberação para fabricação".

## Project Structure

### Documentation (this feature)

```text
specs/001-concentradora2-wear-solutions/
├── spec.md              # Especificação (necessidade do cliente, requisitos, critérios)
├── plan.md              # Este plano
├── research.md          # Phase 0: decisões de conceito, materiais, normas, medição, entradas do cliente
├── data-model.md        # Phase 1: estrutura do produto (árvore de itens, BOM, massas)
├── quickstart.md        # Phase 1: plano de validação (ensaios, FAI, teste de campo, aceitação)
├── contracts/
│   ├── s1-interface-calha-descarga.md       # Interface painel ↔ calha de descarga
│   └── s2-interface-posicao-desgaste.md     # Interface painel PU ↔ posição de desgaste
├── checklists/requirements.md
└── tasks.md             # Phase 2 (/speckit-tasks)
```

### Documentação técnica do produto (raiz do repositório)

```text
produtos/concentradora2/
├── s1-calha-descarga/
│   ├── desenhos/        # Desenhos de fabricação e de montagem (PDF + referência ao modelo 3D)
│   ├── bom/             # Lista de materiais do kit S1
│   ├── calculos/        # Memorial: impacto das bolas, fixação, massa
│   ├── processos/       # Roteiro de fabricação (moldagem, encapsulamento, ligação)
│   ├── qualidade/       # FMEA, plano de controle, relatórios de FAI e de ensaio
│   └── campo/           # Instrução de instalação, critério de troca, registros de medição
└── s2-placas-desgaste/
    ├── desenhos/
    ├── bom/
    ├── processos/       # Corte a frio, furação, versão soldável
    ├── qualidade/
    └── campo/           # Instrução de corte e fixação, registros de medição, custo por hora
```

**Structure Decision**: uma pasta por produto em `produtos/concentradora2/`, com subpastas por tipo de entregável da constituição (desenhos, BOM, cálculos, processos, qualidade, campo). As histórias S3 a S8 ganham pastas próprias quando entrarem no plano.

## Complexity Tracking

Sem violações da constituição. Nenhuma justificativa necessária.
