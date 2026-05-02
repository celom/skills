# Frame Document Format

One document per domain scope. Numbered, slugged, and linked to its parent (when it has one) via frontmatter only.

## Frontmatter

```yaml
---
slug: <kebab-case-slug>
parent: <relative path to parent frame>   # omit on the root
---
```

- The root frame (`00-<slug>.md`) has no `parent`.
- Children reference their parent by relative path:
  - From `docs/frame/01-pricing.md`, parent is `./00-billing.md`.
  - From `docs/frame/01-pricing/01-tiers.md`, parent is `../01-pricing.md`.

## Body

Free prose. No scaffold. Each frame is shaped by its own topic — let the discovery dictate the structure, not the format.

A frame has done its job when it contains, in whatever shape fits:

- the **distilled answer** to "what is this scope" — usually one sentence;
- the **decisions** that were resolved, with the reasoning behind each — not just the choice;
- the **assumptions** the framing depends on — what must be true about the world, users, or systems for this scope to hold;
- the **unresolved questions** that surfaced but weren't closed inside this scope;
- the **stubs** — sub-topics deferred to their own future frame.

These are obligations, not sections. Whether they live as headings, prose, or bullets is per-topic. Don't impose a template the topic doesn't earn. A short frame might weave assumptions and unresolved questions into prose; a complex one might list them. Both are fine, as long as a downstream reader can find them.

## Stubs

A stub is a one-line note on a deferred sub-topic. It lives in the parent frame until it's promoted to its own child frame, killed, or kept as a stub through review.

Each stub records:

- a one-line description of the deferred topic;
- the date it was created.

That's the minimum. Format is per-topic — a list, a paragraph, woven into prose. Whatever fits.

When a frame is reopened, its stubs are audited against the current state. The audit is not logged. A stub that survives audit keeps its original creation date. A stub that's promoted to a child frame is removed from the parent. A stub that's killed is removed. A stub that's been deferred through two audits is a signal — it's either not actually important, or it's been wrongly scoped as a sub-topic when it's really independent. Surface that, don't bury it.

## Cross-frame references

The only link to another frame is `parent:` in the frontmatter. The body **never references** other frames — not parents, not children, not siblings.

Children are discovered structurally: a frame's children live in the sibling folder named after its slug (`01-pricing.md` → `01-pricing/`). If you need to know what branched off a frame, look at the folder, not the doc.

## Rules

- **One scope per file.** If a sub-topic gains its own decisions, branch it into a child frame.
- **DOMAIN.md owns vocabulary.** Reference domain terms in **bold** (`**Customer**`). Never redefine them in a frame doc.
- **Capture reasoning, not just choices.** The choice is recoverable from the file; the reasoning is not.
- **Capture assumptions, not just decisions.** Decisions are what you chose; assumptions are what has to hold for the choice to make sense. Both are load-bearing.
- **Edit in place.** The doc is the current state, not a log. Revise sections rather than appending "Update:" notes. Stub creation dates are state (when it entered the queue), not log entries — they get carried forward, not accumulated.
- **Write only what's crystallized.** No empty headings, no batched end-of-session writes.
- **Surface contradictions, don't paper over them.** If a later decision contradicts an earlier one, edit both — and note the resolution explicitly if it was load-bearing.