# Plano de Validação (Quickstart): S1 e S2

**Data**: 2026-10-03 | **Plano**: [plan.md](./plan.md)

> Este é o `quickstart.md` do Spec Kit, lido como **plano de validação**: os cenários físicos que provam, do começo ao fim, que o produto funciona. Os detalhes de interface estão em [contracts/](./contracts/) e os da estrutura do produto em [data-model.md](./data-model.md).

## Pré-requisitos

- Entradas do cliente recebidas: [research.md §R7](./research.md#r7-entradas-que-o-cliente-precisa-enviar-até-lá-valem-as-premissas-de-projeto).
- Desenhos de fabricação aprovados e FMEA de projeto revisado (Portão de Projeto).
- Instrumentos:
  - medidor ultrassônico de espessura (com calibração para PU e para aço);
  - durômetro Shore A;
  - balança de até 50 kg;
  - trena e paquímetro;
  - câmera, para registro fotográfico.
- Autorização de acesso à planta e procedimento de bloqueio do cliente.

---

## V1. Ensaios de material (lote do protótipo): S1 e S2

| Ensaio | Norma | Critério de aceitação |
|---|---|---|
| Dureza do PU | ASTM D2240 | valor nominal da formulação ± 3 Shore A |
| Tração e alongamento | ASTM D412 | ≥ valores da ficha técnica da formulação |
| Resistência ao rasgo | ASTM D624 | ≥ ficha técnica |
| Abrasão | ISO 4649 | perda de volume ≤ ficha técnica |
| Adesão PU–aço (S1, S2-W) | ASTM D429 B | ruptura coesiva no PU (não na interface) |
| Cerâmica (S1) | ASTM C373 / certificado | Al₂O₃ ≥ 92%, densidade ≥ 3,6 g/cm³ |
| Aço da base | certificado de usina | conforme ASTM A36 ou equivalente |

## V2. Inspeção de primeira peça (FAI): S1 e S2

1. Medir as dimensões de 100% dos painéis contra o desenho, incluindo a furação.
2. Pesar cada painel e confirmar que tem ≤ 25 kg.
3. Medir a espessura nos pontos marcados e registrar como valor de fábrica.
4. Inspecionar visualmente: insertos cerâmicos totalmente encapsulados, sem trincas, sem vazios aparentes, bordas da base cobertas.
5. Fazer a montagem a seco do primeiro painel de cada tipo em gabarito ou réplica da furação (S1).
6. Conferir a rastreabilidade: cada número de série ligado aos lotes de PU e cerâmica e à corrida do aço.

**Critério**: 100% dos itens conformes. O Portão de Protótipo/FAI só é liberado com o relatório assinado.

## V3. Instalação em campo (T0)

1. **S1**: instalar o kit numa calha. Na calha gêmea, marcar os mesmos pontos na cerâmica atual.
2. **S2**: instalar 2 a 4 painéis, cada um ao lado de uma chapa Hardox 5/8" em posição equivalente.
3. Registrar:
   - tempo de instalação;
   - quantidade de pessoas;
   - ferramentas usadas;
   - não conformidades de encaixe (meta: nenhum ajuste além do previsto na instrução);
   - espessura T0 em todos os pontos;
   - horas de operação no horímetro ou na contagem da planta.

## V4. Monitoramento

- Medir em cada parada programada (referência: mensal) todos os pontos, no protótipo e na referência.
- Registrar as horas de operação acumuladas, as paradas longas e as mudanças de regime (minério, vazão).
- Fazer registro fotográfico com o mesmo enquadramento em cada inspeção.
- **Falha imediata (S1)**: qualquer inserto ou painel solto, ou painel fraturado → registrar e avaliar a causa.

## V5. Critérios de aceitação

| Produto | Fim do teste | Critério de aprovação | Ref. |
|---|---|---|---|
| S1 | após ≥ 12 meses de operação no regime normal, ou fim de vida antes disso | (a) ≥ 12 meses **e** (b) vida (real ou projetada) ≥ 1,5× a da calha de comparação; nenhuma peça solta ou quebrada; espessura acima do mínimo de troca aos 12 meses | FR-104, SC-001 |
| S2 | quando o Hardox de comparação atinge a espessura de troca | vida projetada (espessura útil ÷ taxa de desgaste no **ponto mais desgastado**) ≥ 1,5× a do Hardox **e** custo por hora ≤ o do Hardox | FR-202, FR-204, SC-002 |

**Cálculos** (research.md §R5 e §R6):

```text
taxa de desgaste [mm/h] = (espessura T0 − espessura Tn) ÷ horas de operação entre T0 e Tn
vida projetada [h]      = espessura útil (T0 − espessura de troca) ÷ taxa de desgaste
custo por hora          = (material + instalação + parada atribuível) ÷ vida [h]
```

## V6. Encerramento

- **Aprovado**: emitir relatório de teste de campo e liberar para o Portão de Produção (plano de controle, instruções finais, cotação de fornecimento em série).
- **Reprovado**: registrar o modo de falha e a causa provável, voltar à revisão de projeto e informar o cliente com o motivo (FR-902).
