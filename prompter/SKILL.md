---
name: prompter
description: Take a rough prompt the user wrote and return a sharper, engineering-oriented version — for Claude or any LLM. Diagnoses what weakens the prompt, rewrites it using established prompt-engineering techniques, and explains what changed. Use when the user shares a prompt they want improved, asks "how would you phrase this", or wants a prompt reviewed before using it.
---

# Prompter

Refine a rough prompt into one that gets better results. Input is the user's draft; output is a rewritten prompt ready to copy, plus a short account of what changed and why.

This is refinement, not authorship. Preserve the user's intent exactly — sharpen how it's asked, never what is asked. If intent itself is unclear, that's a question, not a guess.

## Process

1. **Read for intent first.** State the prompt's goal in one line. If you can't, ask — one question, only when the answer would change the rewrite. Never stack questions.
2. **Diagnose before rewriting.** Identify the specific weaknesses (see checklist below). Don't rewrite a prompt you haven't diagnosed — the diagnosis is what makes the rationale honest.
3. **Rewrite once, completely.** Produce a single improved version, not variants. Offer an alternative only when two genuinely different strategies fit (e.g. zero-shot vs. few-shot) — then say which you'd pick.
4. **Explain the delta.** For each meaningful change, one line: what changed → what failure it prevents. Skip cosmetic changes.

## Diagnosis checklist

Weaknesses to look for, roughly in order of impact:

- **Buried or ambiguous intent** — the actual ask is implicit, mid-paragraph, or entangled with background.
- **Missing context the model can't infer** — audience, domain, constraints, definitions the user is silently assuming.
- **No output contract** — format, length, structure, or language of the response left unspecified when it matters.
- **Underspecified quality bar** — no criteria for what a good answer looks like, no examples when the task is pattern-shaped.
- **Negative-only instructions** — told what not to do, never what to do instead.
- **Missing edge-case handling** — what the model should do when input is empty, contradictory, or out of scope.
- **Role/framing mismatch** — a persona or tone that fights the task, or none where one would anchor it.
- **Prompt bloat** — instructions that repeat, hedge, or add nothing; length that dilutes the signal.

## Rewrite techniques

Apply what the prompt needs, not everything:

- Lead with the task. Context follows; it doesn't precede.
- Make the output contract explicit: format, structure, length, what to do when unsure.
- Use delimiters or tags to separate instructions from data the prompt operates on.
- Add 1–3 examples when the task is easier to show than to describe. Examples beat adjectives.
- Convert prohibitions to positive instructions ("respond in plain prose" over "don't use bullet points").
- Name the audience and quality bar when they shape the answer.
- Cut everything that survives deletion without changing the expected output.

## Output format

1. The rewritten prompt in a fenced code block, copy-ready.
2. **What changed:** 3–6 bullets, each `change → failure prevented`.
3. If a critical assumption was made, name it in one line at the end.

No preamble, no restating the original, no prompt-engineering lecture.
