# Frame Document Format

One document per domain scope. Numbered, slugged, and linked to its parent (when it has one) via frontmatter only.

## Frontmatter

```yaml
---
slug: <kebab-case-slug>
parent: <relative path to parent frame>   # omit on the root
---
```

- The root frame (`000-<slug>.md`) has no `parent`.
- Children reference their parent by relative path:
  - From `docs/frame/001-pricing.md`, parent is `./000-billing.md`.
  - From `docs/frame/001-pricing/001-tiers.md`, parent is `../001-pricing.md`.

## Body

Free prose. No scaffold. Each frame is shaped by its own topic — let the discovery dictate the structure, not the format.

A frame has done its job when it contains, in whatever shape fits:

- the **distilled answer** to "what is this scope" — usually one sentence;
- the **decisions** that were resolved, with the reasoning behind each — not just the choice;
- the **unresolved questions** that surfaced but weren't closed inside this scope.

These are obligations, not sections. Whether they live as headings, prose, or bullets is per-topic. Don't impose a template the topic doesn't earn.

## Cross-frame references

The only link to another frame is `parent:` in the frontmatter. The body **never references** other frames — not parents, not children, not siblings.

Children are discovered structurally: a frame's children live in the sibling folder named after its slug (`001-pricing.md` → `001-pricing/`). If you need to know what branched off a frame, look at the folder, not the doc.

## Rules

- **One scope per file.** If a sub-topic gains its own decisions, branch it into a child frame.
- **DOMAIN.md owns vocabulary.** Reference domain terms in **bold** (`**Customer**`). Never redefine them in a frame doc.
- **Capture reasoning, not just choices.** The choice is recoverable from the file; the reasoning is not.
- **Edit in place.** The doc is the current state, not a log. Revise sections rather than appending "Update:" notes.
- **Write only what's crystallized.** No empty headings, no batched end-of-session writes.
- **Surface contradictions, don't paper over them.** If a later decision contradicts an earlier one, edit both — and note the resolution explicitly if it was load-bearing.
