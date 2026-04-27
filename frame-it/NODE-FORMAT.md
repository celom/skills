# Frame-shaped node format

> **Shared contract.** This file defines the artifact shape used by both `frame-it` and `layer-it`. Every node in a `foundation/` tree — the root `FRAME.md` and every pillar at every depth — follows it. The uniformity is what makes recursion clean: any node can be re-grilled (`frame-it`) or decomposed (`layer-it`) without special-casing depth.

## Template

````md
---
status: stub | grilled
---

# {Title}

{One short paragraph — the hard-to-vary essence. Aim for 2–5 sentences. Every word load-bearing.}

**Carves:** {one line — what slice of the parent this node owns and how it's distinct from its siblings; or `(root)` for the root frame}

**Falsifier:** {one line — what observable evidence would prove this essence is wrong}

> Parent: {relative link to parent .md file, or `root`}
````

## Field rules

- **`status`** — `stub` for nodes created by `layer-it` that haven't been independently grilled; `grilled` for nodes that have been through a full `frame-it` session. The root `FRAME.md` is always `grilled` (it can't be a stub — `frame-it` produced it directly).
- **Title** — concise. The canonical name of this node. Should match (or align with) terms in `DOMAIN.md`.
- **Essence paragraph** — *the* artifact. Hard-to-vary. Every domain term canonical per `DOMAIN.md`. No filler, no jargon-for-jargon's-sake.
- **Carves** — required on every non-root node. The justification for this node's *existence* as a sibling. If you can't write this line, the node shouldn't exist as a separate pillar.
- **Falsifier** — required on every node. Concrete and observable. *"Users wouldn't like it"* is not a falsifier; *"fewer than 10% return within a week"* is. Stubs created by `layer-it` may carry the placeholder `(to be defined when graduated)` — `frame-it` fills it in during graduation.
- **Parent** — relative path to the parent `.md` file, or `root`. Set on the child at write time. **The parent is never mutated to track its children** — to enumerate a node's children, list the files in the sibling directory (per the path scheme in `../layer-it/SKILL.md`), excluding anything under `_deprecated/`. This avoids write amplification on the parent (the most load-bearing file in the tree) and removes the risk of a stale child index drifting from the filesystem.

## Length

The essence should fit in one short paragraph. If it grows past ~5 sentences, the node is probably trying to do two jobs and should be **layered** into pillars rather than padded.

## Why uniformity matters

Every node — from the root frame to the deepest sub-sub-pillar — has the same shape. This is what lets `frame-it` and `layer-it` operate at any depth without special-casing. A pillar of a pillar of a pillar reads the same as the root: a hard-to-vary essence, a Carves line, a Falsifier, and links to its place in the tree.
