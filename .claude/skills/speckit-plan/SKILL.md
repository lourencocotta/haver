---
name: "speckit-plan"
description: "Execute the implementation planning workflow using the plan template to generate design artifacts."
argument-hint: "Optional guidance for the planning phase"
compatibility: "Requires spec-kit project structure with .specify/ directory"
metadata:
  author: "github-spec-kit"
  source: "templates/commands/plan.md"
user-invocable: true
disable-model-invocation: false
---


## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Contexto do Domínio (OBRIGATÓRIO)

Este projeto **nunca** entrega software como solução. Toda solução é um **produto manufaturado
para equipamentos de mineração** (peças, componentes, conjuntos, peças de desgaste, peças de
reposição ou equipamentos). Antes de executar este comando, leia
`.specify/memory/constitution.md` e aplique a tabela de tradução de termos ali definida:
este comando foi escrito originalmente para software, então "feature" = produto/componente,
"usuário" = cliente/operador/mantenedor/OEM, "tech stack" = materiais, processos e normas,
"testes" = inspeções e ensaios físicos, "código" = documentação técnica do produto.

- Se a entrada do usuário ou um artefato propuser software, aplicativo, API, banco de dados,
  interface de usuário ou firmware como solução, **não prossiga com essa abordagem**: sinalize a
  violação do Princípio I e reformule como produto físico (ou pergunte ao usuário).
- Exemplos de software neste arquivo (APIs, endpoints, `src/`, frameworks, UI) são apenas
  ilustrativos do formato; substitua-os pelos equivalentes de engenharia e manufatura.
- No Technical Context, substitua os campos de software por: **Equipamento hospedeiro / OEM**,
  **Materiais candidatos**, **Processos de fabricação**, **Normas aplicáveis**, **Condições de
  operação**, **Métodos de ensaio e inspeção**, **Volume/lote de produção**, **Restrições**
  (massa, envelope, tempo de troca, custo) e **Metas de desempenho** (vida útil, capacidade).
- `data-model.md` = estrutura do produto (árvore de itens, BOM, materiais, massas);
  `contracts/` = interfaces físicas (dimensões, furações, fixações, cargas transmitidas);
  `quickstart.md` = plano de validação (protótipo, FAI, ensaios, critérios de aceitação).
- Em "Project Structure", troque a árvore `src/`/`tests/` por uma estrutura de documentação
  técnica do produto (ex.: `docs/produto/`, `desenhos/`, `bom/`, `processos/`, `qualidade/`).

## Pre-Execution Checks

**Check for extension hooks (before planning)**:
- Check if `.specify/extensions.yml` exists in the project root.
- If it exists, read it and look for entries under the `hooks.before_plan` key
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

    Wait for the result of the hook command before proceeding to the Outline.
    ```
    After emitting the block above you MUST actually invoke the hook and wait for it to finish before continuing. Run it the same way you would run the command yourself in this agent/session (the invocation may differ from the literal `{command}` id shown above, e.g. a skills-mode agent runs it as `/skill:speckit-...` or `$speckit-...`). Emitting the block alone does not run the hook.
- If no hooks are registered or `.specify/extensions.yml` does not exist, skip silently

## Outline

1. **Setup**: Run `.specify/scripts/bash/setup-plan.sh --json` from repo root and parse JSON for FEATURE_SPEC, IMPL_PLAN, FEATURE_DIR, BRANCH. For single quotes in args like "I'm Groot", use escape syntax: e.g 'I'\''m Groot' (or double-quote if possible: "I'm Groot").

2. **Load context**: Read FEATURE_SPEC and `.specify/memory/constitution.md`. Load IMPL_PLAN template (already copied).

3. **Execute plan workflow**: Follow the structure in IMPL_PLAN template to:
   - Fill Technical Context (mark unknowns as "NEEDS CLARIFICATION")
   - Fill Constitution Check section from constitution
   - Evaluate gates (ERROR if violations unjustified)
   - Phase 0: Generate research.md (resolve all NEEDS CLARIFICATION)
   - Phase 1: Generate data-model.md, contracts/, quickstart.md
   - Re-evaluate Constitution Check post-design

## Mandatory Post-Execution Hooks

**You MUST complete this section before reporting completion to the user.**

Check if `.specify/extensions.yml` exists in the project root.
- If it does not exist, or no hooks are registered under `hooks.after_plan`, skip to the Completion Report.
- If it exists, read it and look for entries under the `hooks.after_plan` key.
- If the YAML cannot be parsed or is invalid, do not skip silently: tell the user that `.specify/extensions.yml` could not be read (include the parser error) and that no hooks were checked, including any mandatory (`optional: false`) hooks registered there, then continue to the Completion Report.
- Filter out hooks where `enabled` is explicitly `false`. Treat hooks without an `enabled` field as enabled by default.
- For each remaining hook, do **not** attempt to interpret or evaluate hook `condition` expressions:
  - If the hook has no `condition` field, or it is null/empty, treat the hook as executable
  - If the hook defines a non-empty `condition`, skip the hook and leave condition evaluation to the HookExecutor implementation
- When constructing command invocations from hook command names, replace dots (`.`) with hyphens (`-`). For example, `speckit.git.commit` → `/speckit-git-commit`.
- For each executable hook, output the following based on its `optional` flag:
  - **Mandatory hook** (`optional: false`) — **You MUST emit `EXECUTE_COMMAND:` for each mandatory hook**:
    ```
    ## Extension Hooks

    **Automatic Hook**: {extension}
    Executing: `/{command}`
    EXECUTE_COMMAND: {command}
    ```
    After emitting the block above you MUST actually invoke the hook and wait for it to finish before continuing. Run it the same way you would run the command yourself in this agent/session (the invocation may differ from the literal `{command}` id shown above, e.g. a skills-mode agent runs it as `/skill:speckit-...` or `$speckit-...`). Emitting the block alone does not run the hook.
  - **Optional hook** (`optional: true`):
    ```
    ## Extension Hooks

    **Optional Hook**: {extension}
    Command: `/{command}`
    Description: {description}

    Prompt: {prompt}
    To execute: `/{command}`
    ```

## Completion Report

Command ends after Phase 1 design. Report branch, IMPL_PLAN path, and generated artifacts.

## Phases

### Phase 0: Outline & Research

1. **Extract unknowns from Technical Context** above:
   - For each NEEDS CLARIFICATION → research task
   - For each dependency → best practices task
   - For each integration → patterns task

2. **Generate and dispatch research agents**:

   ```text
   For each unknown in Technical Context:
     Task: "Research {unknown} for {feature context}"
   For each material/process choice:
     Task: "Find best practices for {material/process} in {mining application}"
   ```

3. **Consolidate findings** in `research.md` using format:
   - Decision: [what was chosen]
   - Rationale: [why chosen]
   - Alternatives considered: [what else evaluated]

**Output**: research.md with all NEEDS CLARIFICATION resolved

### Phase 1: Design & Contracts

**Prerequisites:** `research.md` complete

1. **Extract product structure from feature spec** → `data-model.md`:
   - Items/components, materials, masses, quantities, assembly relationships (BOM tree)
   - Validation rules from requirements
   - State transitions if applicable

2. **Define physical interface contracts** → `/contracts/`:
   - Identify the interfaces of the product with the host mining equipment and between its components
   - Document dimensions, envelope, hole patterns, fastening/locking systems, fits and tolerances, transmitted loads and mass limits
   - Examples: screen deck mounting interface, liner bolt pattern, chute/hopper flange, lifting points
   - Reference the OEM drawing or field survey that each interface is based on

3. **Create quickstart validation guide** → `quickstart.md`:
   - Document physical validation scenarios that prove the product works end-to-end (FAI, bench test, field trial)
   - Include prerequisites, required instruments/fixtures, inspection/test procedures, and acceptance criteria
   - Use links or references to contracts and data model details instead of duplicating them
   - Do not include full drawings, complete BOMs or full manufacturing routes
   - Keep this artifact as a validation/run guide; implementation details belong in `tasks.md` and the implementation phase

**Output**: data-model.md, /contracts/*, quickstart.md

## Key rules

- Use absolute paths for filesystem operations; use project-relative paths for references in documentation
- ERROR on gate failures or unresolved clarifications

## Done When

- [ ] Plan workflow executed and design artifacts generated
- [ ] Extension hooks dispatched or skipped according to the rules in Mandatory Post-Execution Hooks above
- [ ] Completion reported to user with branch, plan path, and generated artifacts
