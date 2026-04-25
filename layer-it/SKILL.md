---
name: layer-it
description: Decompose a frame-shaped foundation node into its load-bearing pillars — the main vertical concepts that hold the parent's essence up. Use when the user wants to break down a frame, identify the main pillars of an idea, extract the structural axes of a topic, or recursively deepen a foundation tree. Operates only on frame-shaped nodes.
---

# Layer It

Decompose a **frame-shaped node** into N **pillars** — the load-bearing concepts that, together, hold the parent's essence up.

## What this is NOT

This is **not** a spec, PRD, plan, design doc, or feature list. The pillars `layer-it` produces are **conceptual axes**, not modules, components, or work items.

The output of `layer-it` is **upstream of any implementation artifact**. Specs, PRDs, plans, and feature breakdowns derive *from* this foundation; they do not replace it.

If the user wants features → `write-a-prd`. Phased delivery → `prd-to-plan`. Tickets → `prd-to-issues`.

## Strict input contract

`layer-it` operates **only on frame-shaped nodes** — files matching the structure defined in `../frame-it/NODE-FORMAT.md` (required frontmatter, essence paragraph, Carves and Falsifier lines).

If the user points this skill at:
- An external doc (PRD, essay, notes) → **refuse**, and tell the user to first run `frame-it` on it. The user can then run `layer-it` on the resulting node.
- A frame-shaped node → proceed.

This is deliberate. Pillars only carry meaning if they decompose a parent that has a hard-to-vary essence. Without a grilled parent, `Carves:` lines have no firm ground.

## What makes a good set of pillars

A *set* of pillars is **hard-to-vary at the set level** — the same Deutschian standard `frame-it` enforces on essences, applied to the decomposition.

Four set-level tests:

| Test | Question |
|---|---|
| **Substitution** | Replace pillar X with a near-synonym pillar. Does the carving still feel load-bearing? If yes → X wasn't pulling weight. |
| **Subtraction** | Drop pillar X entirely. Does the parent feel underdescribed? If no → X was decoration. |
| **Negation** | State an alternative carving along a different axis. Could a reasonable person hold the alternative? If both work equally → the chosen axis isn't justified. Surface this. |
| **Specificity** | Could this same set of pillars decompose a *different* parent? If yes → too generic. The pillars aren't actually about *this* parent. |

Plus the **DOMAIN.md conformance check** on pillar names and Carves lines.

**Cardinality — soft 3–7 band.** Challenge anything outside this range, but don't refuse:
- N < 3 → *"You've got a binary worldview. Is there really no third axis here?"*
- N > 7 → *"This looks like a list, not a carving. Can any of these be merged, or are some descendants of others?"*

Accept the user's defense if they have one.

## Workflow

### 1. Setup

- Validate the input is frame-shaped. If not → refuse with a clear message and suggest running `frame-it` first.
- Load `./foundation/DOMAIN.md` if it exists.
- Determine where children will live:
  - **Root (`./foundation/FRAME.md`)** → children go in `./foundation/pillars/`.
  - **Any other node** at `<path>/<slug>.md` → children go in the sibling directory `<path>/<slug>/`.
- If children already exist → enter **revise mode** (step 5). Otherwise → **fresh decomposition**.

### 2. Pillar set draft

Read the parent's essence and Carves carefully. Propose a first-pass set of 3–7 candidate pillars. For each candidate include:
- Working title
- One-line essence
- One-line Carves (what slice of the parent this owns and how it differs from siblings)

Present the candidates as a numbered list to the user.

### 3. Set-level grill

Apply the four tests to the proposed *set*. Walk through them with the user:
- **Substitution** on each pillar.
- **Subtraction** on each pillar.
- **Negation** against the whole set — *"Is there a different axis we could be carving along instead?"*
- **Specificity** on the whole set — *"Could this same set decompose a different parent?"*

Apply DOMAIN.md conformance: if any pillar name or Carves line uses a non-canonical term, surface it. Resolve before continuing — either by promoting a new term to `DOMAIN.md` (append immediately, see `../frame-it/DOMAIN-FORMAT.md`) or by rewriting the pillar in canonical language.

Cardinality challenge if the set is outside 3–7.

Iterate until the set holds.

### 4. Per-pillar quick pass

For each pillar in the locked set, do a *light* validation:
- Is the title canonical (or now-canonical via this session)?
- Does the one-line essence read as hard-to-vary at first glance?
- Does the Carves line clearly distinguish this pillar from its siblings?

This is **not** a deep grilling — that's `frame-it`'s job. The goal is stubs coherent enough for the parent to read sensibly, not fully grilled children.

### 5. Revise mode (only if children already exist)

When the parent already has children, present them and ask, per child:
- **Keep** as-is
- **Revise** (change essence/Carves/title — write a new version of that file)
- **Drop** (move to `_deprecated/`, never delete)

Then ask: should new pillars be added? If yes, run steps 2–4 for the additions only.

When dropping: move the file (and any of its sub-tree) into `./foundation/_deprecated/` preserving the relative path. **Never use `rm`.** The parent's `Children:` link is updated to remove the dropped node.

### 6. Write

For each new or revised pillar:
- Create the children directory if it doesn't exist (per the rule in step 1).
- Write the file using the template in `../frame-it/NODE-FORMAT.md`. Frontmatter: `status: stub`. Fill in title, essence (the one-line draft expanded into a short paragraph if helpful), Carves, and a placeholder Falsifier line `(to be defined when graduated)` — `frame-it` will fill it in during graduation.
- File naming: `NN-<slug>.md` where `NN` is a zero-padded order number (`01-`, `02-`, …) by the order presented in the session, and `<slug>` is kebab-case from the title.

For the parent:
- After all child writes, rewrite the parent's `Children:` line to list every current (non-deprecated) child as a relative link.

### 7. Graduate (default-offered)

After writing the stubs, ask:

> *"Want to graduate any of these stubs to `grilled` now? I'll run the `frame-it` process on the selected ones."*

If the user picks one or more:
- For each selected stub, follow the workflow in `../frame-it/SKILL.md` (Mode C — re-grill an existing frame-shaped node), starting from the stub's content.
- On write, flip `status: stub` → `status: grilled`.

If the user declines, exit cleanly. They can run `frame-it` on any stub later.

## Boundaries

- **Never delete files.** Dropped pillars move to `./foundation/_deprecated/` with their sub-tree intact.
- **Don't write outside `foundation/`.**
- **Don't scan the repository unless the user asks.** This skill operates inside `foundation/` only.
- **Don't accept non-frame-shaped input.** The strict input contract is the whole reason for this skill's rigor.
