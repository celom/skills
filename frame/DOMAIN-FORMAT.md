# DOMAIN.md Format

`DOMAIN.md` is the project's shared language. One file per project, lives at `docs/frame/DOMAIN.md`.

## Spine

The one section every `DOMAIN.md` has:

```md
# {Domain Name}

{One sentence on what this domain is and why it exists.}

## Language

**Order**:
A request from a **Customer** to deliver goods or services.
_Avoid_: Purchase, transaction

**Invoice**:
A request for payment sent to a **Customer** after delivery.
_Avoid_: Bill, payment request

**Customer**:
A person or organization that places **Orders**.
_Avoid_: Client, buyer, account
```

That's the obligation. Everything else is optional and only appears when the domain earns it.

## Optional sections

- **Relationships** — when there are enough cross-cutting links between terms that listing them separately is clearer than embedding in definitions. Bold the term names, express cardinality.

  ```md
  ## Relationships
  - An **Order** produces one or more **Invoices**
  - An **Invoice** belongs to exactly one **Customer**
  ```

- **Flagged ambiguities** — when a term was used to mean two things and got resolved. Record both the conflict and the resolution.

  ```md
  ## Flagged ambiguities
  - "account" was used to mean both **Customer** and **User** — resolved: distinct concepts. **User** authenticates; **Customer** owns **Orders**.
  ```

- **Subgroupings inside Language** — when terms cluster into natural areas, group them under subheadings. If they don't, keep the list flat. Don't invent groups for the sake of structure.

## Rules

- **Be opinionated.** When multiple words exist for the same concept, pick one canonical term. List the rest as `_Avoid_:` aliases on the entry. The point of the glossary is to remove ambiguity, not to catalog it.
- **Tight definitions.** One sentence. Define what it IS, not what it does or how it works.
- **Domain terms only.** A term belongs here if a domain expert would recognize it. Internal types, modules, retry policies, queue names, error classes — none of those, even if the project uses them constantly. Before adding a term, ask: would the domain expert use this word? If not, it doesn't belong.
- **Bold every reference.** Whenever a defined term appears — inside another definition, in Relationships, in Flagged ambiguities — wrap it in `**...**`. Bold marks the canonical vocabulary.
- **Edit in place.** When a term is refined, renamed, or deprecated, edit the entry. Don't append "Update:" notes; the doc is the current state, not a log.
