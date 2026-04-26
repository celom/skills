# DOMAIN.md format

`DOMAIN.md` is the **canonical lingua franca** of one foundation tree. Every essence in the tree must conform to it. Specs, PRDs, plans, and any downstream artifact built from this foundation should also inherit the language defined here.

It lives at `./foundation/DOMAIN.md`. There is **one** `DOMAIN.md` per foundation tree — no `DOMAIN-MAP.md`, no per-pillar variants. If a project genuinely needs two domain languages, it has two foundation trees.

## Structure

````md
# {Domain name}

{One or two sentences — what this domain is and why it exists. Often the same essence as the root FRAME.md, condensed further.}

## Language

**Order:**
A customer's request to purchase one or more items.
_Avoid_: Purchase, transaction

**Invoice:**
A request for payment sent to a customer after delivery.
_Avoid_: Bill, payment request

**Customer:**
A person or organization that places orders.
_Avoid_: Client, buyer, account

## Relationships

- An **Order** produces one or more **Invoices**
- An **Invoice** belongs to exactly one **Customer**

## Example dialogue

> **PM:** "When a **Customer** places an **Order**, do we generate the **Invoice** immediately?"
> **Domain expert:** "No — an **Invoice** is only generated once a **Fulfillment** is confirmed."

## Flagged ambiguities

- "account" was used to mean both **Customer** and **User** — resolved: these are distinct.
````

## Rules

- **Be opinionated.** When multiple words exist for the same concept, pick the canonical one and list the others under `_Avoid_`.
- **Flag conflicts explicitly.** If a term is used ambiguously during a session, call it out in `Flagged ambiguities` with a clear resolution.
- **Keep definitions tight.** One sentence. Define what a term *is*, not what it *does*.
- **Show relationships.** Use bold term names. Express cardinality where relevant.
- **Only include domain-specific terms.** General programming concepts (timeouts, caching, error types) don't belong even if the project uses them. Before adding a term, ask: *is this concept specific to this project, or general?*
- **Group by subheading** when natural clusters emerge. Otherwise a flat list is fine.
- **Write an example dialogue** once enough terms exist to demonstrate them in natural use. The dialogue is a stress test of the glossary — if the conversation reads naturally with bolded terms, the language is working.

## Lifecycle

- **Lazy creation.** Don't generate `DOMAIN.md` until the first canonical term is resolved during a grilling session.
- **Append on resolution.** When a new term is needed mid-session, write it to `DOMAIN.md` immediately so it's canonical for the rest of the session.
- **Never delete entries.** If a term is deprecated, move it to a `## Deprecated` section with a one-line note pointing to its replacement.
