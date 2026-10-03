---
name: "speckit-email"
description: "Generate a plain-language consolidation e-mail of the current feature plan, addressed to the field salesperson, in the language chosen by the user."
argument-hint: "Idioma (pt/es/en), nome do vendedor, remetente, participantes e contexto da visita"
compatibility: "Requires spec-kit project structure with .specify/ directory"
metadata:
  author: "haver"
  source: ".claude/skills/speckit-email/SKILL.md"
user-invocable: true
disable-model-invocation: false
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Propósito

Gerar um **e-mail de consolidação** das informações do plano (`plan.md`, apoiado por `spec.md`
e `tasks.md` quando existirem) para o **vendedor de ponta**. O e-mail resume, em linguagem
simples e comercial, cada oportunidade/produto, a situação atual do cliente, o que propomos e
o **próximo passo** de cada item, no formato de `.specify/templates/email-template.md`.

O e-mail **não é um documento técnico**. Quem lê é um vendedor que vai usá-lo na conversa com o
cliente: precisa entender em segundos o que está em jogo e o que precisa fazer.

## Contexto do Domínio (OBRIGATÓRIO)

Este projeto **nunca** entrega software como solução. Toda solução é um **produto manufaturado
para equipamentos de mineração** (peças, componentes, conjuntos, peças de desgaste, peças de
reposição ou equipamentos). Antes de executar este comando, leia
`.specify/memory/constitution.md`. No e-mail, descreva sempre o produto físico (revestimento,
placa, tubulação, peça de poliuretano/cerâmica etc.), nunca sistemas ou software.

## Pre-Execution Checks

**Check for extension hooks (before e-mail generation)**:
- Check if `.specify/extensions.yml` exists in the project root.
- If it exists, read it and look for entries under the `hooks.before_email` key
- If the YAML cannot be parsed or is invalid, do not skip silently: tell the user that `.specify/extensions.yml` could not be read (include the parser error) and that no hooks were checked, including any mandatory (`optional: false`) hooks registered there, then continue normally
- Filter out hooks where `enabled` is explicitly `false`. Treat hooks without an `enabled` field as enabled by default.
- For each remaining hook, do **not** attempt to interpret or evaluate hook `condition` expressions:
  - If the hook has no `condition` field, or it is null/empty, treat the hook as executable
  - If the hook defines a non-empty `condition`, skip the hook and leave condition evaluation to the HookExecutor implementation
- When constructing command invocations from hook command names, replace dots (`.`) with hyphens (`-`). For example, `speckit.git.commit` → `/speckit-git-commit`.
- For each executable hook, output the following based on its `optional` flag:
  - **Optional hook** (`optional: true`):
    ```
    ## Extension Hooks

    **Optional Pre-Hook**: {extension}
    Command: `/{command}`
    Description: {description}

    Prompt: {prompt}
    To execute: `/{command}`
    ```
  - **Mandatory hook** (`optional: false`):
    ```
    ## Extension Hooks

    **Automatic Pre-Hook**: {extension}
    Executing: `/{command}`
    EXECUTE_COMMAND: {command}

    Wait for the result of the hook command before proceeding to the Execution Steps.
    ```
    After emitting the block above you MUST actually invoke the hook and wait for it to finish before continuing. Run it the same way you would run the command yourself in this agent/session (the invocation may differ from the literal `{command}` id shown above, e.g. a skills-mode agent runs it as `/skill:speckit-...` or `$speckit-...`). Emitting the block alone does not run the hook.
- If no hooks are registered or `.specify/extensions.yml` does not exist, skip silently

## Execution Steps

1. **Setup**: Run `.specify/scripts/bash/check-prerequisites.sh --json --template email-template` from repo root and parse JSON for FEATURE_DIR, AVAILABLE_DOCS list, and TEMPLATE_CONTENT.
   - All file paths must be absolute.
   - For single quotes in args like "I'm Groot", use escape syntax: e.g 'I'\''m Groot' (or double-quote if possible: "I'm Groot").
   - If the script fails because `plan.md` is missing, STOP and instruct the user to run `/speckit-plan` first.

2. **Idioma (OBRIGATÓRIO — gate)**: Determine o idioma do e-mail a partir de `$ARGUMENTS`
   (ex.: "pt", "português", "es", "espanhol", "español", "en", "inglês", "english").
   - **Se o idioma NÃO estiver explícito em `$ARGUMENTS`, PERGUNTE ao usuário antes de
     continuar** e aguarde a resposta. Não deduza o idioma pelo idioma da conversa, do plano ou
     do nome do cliente. Use a ferramenta de perguntas, se disponível, com as opções:
     - Português
     - Español
     - English
     (o usuário pode responder outro idioma livremente).
   - Não gere nenhum rascunho antes de ter o idioma confirmado.

3. **Dados do e-mail**: Extraia de `$ARGUMENTS` e dos artefatos:
   - **Nome do vendedor** (destinatário) — se ausente, pergunte junto com o idioma ou use o
     placeholder `[NOME DO VENDEDOR]` e avise no relatório final.
   - **Remetente** (assinatura) — se ausente, use `[SEU NOME]` e avise.
   - **Participantes** da visita/reunião — se ausentes, remova a linha.
   - **Contexto** (visita, reunião, data, cliente) — se ausente, use agradecimento genérico
     pelo apoio/reunião, sem inventar datas.
   - Faça no máximo **uma** rodada de perguntas, agrupando idioma + dados faltantes essenciais.

4. **Carregar contexto** de FEATURE_DIR:
   - **REQUIRED**: `plan.md` — produtos/soluções propostos, materiais, abordagem, premissas.
   - **IF EXISTS**: `spec.md` — situação atual do cliente, problema, condições de operação,
     vida útil atual e meta, critérios de sucesso.
   - **IF EXISTS**: `tasks.md` — pendências que viram "próximo passo" (desenhos, fotos,
     medições, cotação, teste em campo).
   - **IF EXISTS**: `research.md`, `quickstart.md` — apenas para confirmar fatos.
   - Carregue apenas o necessário; não copie seções inteiras.

5. **Montar as oportunidades**: para cada produto/aplicação/tema do plano, produza um item
   numerado com:
   - **Título**: nome simples da peça ou aplicação (ex.: "Revestimento de hidrociclones").
   - **Situação atual**: o que o cliente usa hoje, vida útil, satisfação ou problema.
   - **Proposta**: o que sugerimos ou o que o cliente aceita testar.
   - **Próximo passo**: uma ação única, concreta, com responsável implícito. Priorize
     pendências que dependem do cliente ou do vendedor (enviar desenhos, fotos, medidas,
     preço atual; confirmar se equipamentos são iguais) e as nossas (preparar cotação/proposta,
     avaliar com Engenharia).
   - Ordem: a mesma do plano; se não houver ordem clara, da maior para a menor oportunidade.
   - Junte itens repetidos; não crie itens sem base nos artefatos.

6. **Regras de linguagem (para o vendedor de ponta)**:
   - Frases curtas, voz ativa, tom cordial, positivo e comercial.
   - **PROIBIDO** no corpo do e-mail: IDs de requisito/tarefa (FR-001, SC-002, T014), nomes de
     arquivos ou do Spec Kit, siglas internas não explicadas (DFM, FAI, FMEA, FEA), normas
     citadas por número, tolerâncias, fórmulas, tabelas técnicas e detalhes de processo de
     fabricação.
   - Traduza o técnico para o benefício: "maior vida útil", "menos paradas", "teste em campo",
     "reparo provisório até a parada do equipamento".
   - Mantenha somente os números que ajudam a vender (vida útil em horas/meses, diâmetro,
     espessura, comprimento) na unidade usada pelo cliente; equivalência entre parênteses
     quando útil: 5/8" (16 mm).
   - Mantenha nomes comerciais de materiais/modelos citados (ex.: Hardox, Rhino Hyde, Cavex 48).
   - Escreva **todo** o e-mail no idioma escolhido (saudação, rótulos como
     "Participantes"/"Próximo passo", parágrafos fixos e despedida). Não misture idiomas.
   - Fatos ausentes nos artefatos não devem ser inventados: omita ou transforme em próximo
     passo ("confirmar dimensões", "confirmar preço atual").

7. **Parágrafos de fechamento** (sempre incluir, traduzidos para o idioma escolhido, salvo
   pedido contrário do usuário):
   - Pedido de **preços atuais ou de referência** para preparar propostas comercialmente
     viáveis e alinhadas às expectativas do cliente.
   - Pedido para informar o **motivo de respostas negativas**, para trabalhar as objeções,
     ajustar a proposta e tentar reverter a situação.
   - Convite para **complementar pontos esquecidos**.
   - Agradecimento final, despedida e nome do remetente em MAIÚSCULAS.

8. **Gerar o arquivo**: Use TEMPLATE_CONTENT como estrutura e escreva
   `FEATURE_DIR/email.md` (se já existir, acrescente sufixo do idioma: `email-es.md`,
   `email-en.md`, `email-pt.md`; nunca sobrescreva sem confirmação).
   - Preencha o cabeçalho (Idioma, Destinatário, Data de hoje, Fonte) e o **Assunto** no idioma
     escolhido.
   - Substitua todos os placeholders entre colchetes; remova o bloco de comentário de
     instruções/exemplo do template.
   - O corpo após `---` deve estar pronto para copiar e colar em um cliente de e-mail (texto
     simples, sem negrito/markdown no corpo além da lista numerada).

9. **Validação antes de concluir** (corrija e revalide; no máximo 2 iterações):
   - [ ] Idioma confirmado pelo usuário e usado em 100% do corpo.
   - [ ] Nenhum ID de requisito/tarefa, nome de arquivo ou jargão de engenharia no corpo.
   - [ ] Toda oportunidade tem situação atual + proposta + "próximo passo".
   - [ ] Nenhum fato inventado (cada item rastreável a `plan.md`/`spec.md`/`tasks.md`).
   - [ ] Nenhum placeholder `[...]` restante, exceto os avisados ao usuário.
   - [ ] Nenhuma solução descrita como software (Princípio I da constituição).

10. **Relatório**: Informe o caminho do arquivo gerado, o idioma, o número de oportunidades,
    os placeholders que ficaram pendentes e exiba o corpo do e-mail para revisão rápida.

## Post-Execution Checks

**Check for extension hooks (after e-mail generation)**:
Check if `.specify/extensions.yml` exists in the project root.
- If it exists, read it and look for entries under the `hooks.after_email` key
- If the YAML cannot be parsed or is invalid, do not skip silently: tell the user that `.specify/extensions.yml` could not be read (include the parser error) and that no hooks were checked, including any mandatory (`optional: false`) hooks registered there, then continue normally
- Filter out hooks where `enabled` is explicitly `false`. Treat hooks without an `enabled` field as enabled by default.
- For each remaining hook, do **not** attempt to interpret or evaluate hook `condition` expressions:
  - If the hook has no `condition` field, or it is null/empty, treat the hook as executable
  - If the hook defines a non-empty `condition`, skip the hook and leave condition evaluation to the HookExecutor implementation
- When constructing command invocations from hook command names, replace dots (`.`) with hyphens (`-`). For example, `speckit.git.commit` → `/speckit-git-commit`.
- For each executable hook, output the following based on its `optional` flag:
  - **Optional hook** (`optional: true`):
    ```
    ## Extension Hooks

    **Optional Hook**: {extension}
    Command: `/{command}`
    Description: {description}

    Prompt: {prompt}
    To execute: `/{command}`
    ```
  - **Mandatory hook** (`optional: false`):
    ```
    ## Extension Hooks

    **Automatic Hook**: {extension}
    Executing: `/{command}`
    EXECUTE_COMMAND: {command}
    ```
    After emitting the block above you MUST actually invoke the hook and wait for it to finish. Run it the same way you would run the command yourself in this agent/session. Emitting the block alone does not run the hook.
- If no hooks are registered or `.specify/extensions.yml` does not exist, skip silently

## Exemplo de Uso

```text
/speckit-email es vendedor: Isidro; remetente: Laís Andrade; participantes: Gilberto Lopes, Ismael Burgos, Jorge, Isidro, Laís; visita de ontem
```

```text
/speckit-email vendedor: Isidro
→ o comando pergunta: "Em qual idioma o e-mail deve ser escrito? (Português / Español / English)"
```
