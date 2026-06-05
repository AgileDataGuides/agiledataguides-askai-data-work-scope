# Scope Understanding: <Solution name>

> What the team does and does not yet understand about the scope, and the questions that resolve it.
> Lead with what's clear and the open questions. Keep it tight: tables not prose, a cell holds a phrase.
> Stated = quoted from a template. Implied = our inference. Unknown = needs the team.
> Note which WHAT you read: an Information Product Canvas (business problem) or a Press Release (platform capability).

## What's clear

The scope you can state with confidence, traced to the templates. One line each. If a line is an inference, mark it *(implied)*.

- **Why:** <the outcome that matters, from the Mission, or the canvas Outcomes if no Mission was supplied>
- **What:** <the Information Products or capability, at a glance>
- **How:** <the technical shape, or "not yet drawn">
- **Boundaries:** <what is explicitly in / out>

## Open questions (what's unclear)

The headline. Every gap and every break in the line of sight, as a question the team can act on. Ranked by what blocks building first.

| # | Question | Why it matters | Owner | Register |
|---|---|---|---|---|
| 1 | <the sharp question, in the team's words> | <what it blocks, what goes wrong if guessed> | team / stakeholder | unknown / implied |
| 2 | ... | ... | ... | ... |

## Line of sight

Does the intent form one line why → what → how? Each break is one of the questions above. Use the rows for your WHAT.

**If the WHAT is a Canvas:**

| Link | Holds? | Notes |
|---|---|---|
| Questions → Outcomes (does every Business Question serve an Outcome?) | ✓ / ⚠ / ✗ | <which serve, which do not> |
| Outcomes → Mission (do the Outcomes ladder up to the strategic why?) | ✓ / ⚠ / ✗ | <or "no Mission supplied, Outcomes are the why"> |
| How → Questions (can Delivery / Sync / Systems answer the questions?) | ✓ / ⚠ / ✗ | <source sets, cadence, slicing seams> |
| Will/Won't consistent (any boundary conflict with a question or Outcome?) | ✓ / ⚠ / ✗ | <conflicts to surface> |

**If the WHAT is a Press Release:**

| Link | Holds? | Notes |
|---|---|---|
| Mission → Press Release (does every benefit serve a mission outcome?) | ✓ / ⚠ / ✗ | <which benefits trace> |
| Press Release → Architecture (does every benefit have a home?) | ✓ / ⚠ / ✗ | <homes and gaps> |
| Architecture → Press Release (does every component serve a benefit?) | ✓ / ⚠ / ✗ | <speculative components to cut> |

**Verdict:** <one line: a coherent intent, or where it breaks>

---

## The full structured scope

> Produce this section when the team wants the complete picture, not just what's unclear. Every row still obeys stated / implied / unknown.

### The what (Information Products)

Each Business Question (Canvas) or benefit (Press Release) as one Information Product. Pin the grain even if unstated.

| # | Information Product (the question) | Stakeholder | Grain (one row per ...) | Events / source | Consume shape |
|---|---|---|---|---|---|
| 1 | <question in the stakeholder's words> | <persona> | <grain, or UNKNOWN, flag it> | <events / system of capture> | <dashboard, extract, alert ...> |
| 2 | ... | ... | ... | ... | ... |

### The how

Source-to-answer per Information Product. A Canvas gives sources + cadence; still confirm they exist and their keys join.

| Information Product | Sources needed | Exists already | New to build (the scope) | New pipeline stages |
|---|---|---|---|---|
| 1 | <sources> | <what the tenancy has, or "assumed, no MCP"> | <net-new sources / models / consume> | <which of Land→...→Consume are new> |
| 2 | ... | ... | ... | ... |

> Flag Feature Stories that quietly add scope: "as at" history (full History layer), drill-down (atomic grain + detail), export (an extract delivery).

### The slices

Thinnest valuable slice first, then increments. Each is one or a few Information Products end to end, sized. Split on which sources each needs.

| Order | Slice | Size | Line of sight (why) | Depends on |
|---|---|---|---|---|
| 1 | <the thinnest slice that delivers real value> | XS–XL | <Outcome / mission goal it advances> | none |
| 2 | ... | ... | ... | slice 1 |

**Slice 1 proves:** <what it demonstrates end to end, e.g. "real source data resolves onto one key into an answer on the stakeholder's screen">

### Data contracts implied

Identified here, not authored (authoring is the next skill).

| Contract | For Information Product | Grain | Business key | Load type | Already exists? |
|---|---|---|---|---|---|
| <data set> | 1 | <grain> | <{entity}_key> | change_data / event_data | yes / no |

### Scope boundaries (from a Canvas's Will/Won't, or the Mission's Boundaries)

Honour the stated scope. Flag any boundary that conflicts with a question or an Outcome.

- **Will:** <what is explicitly in>
- **Won't:** <what is explicitly out>
- **Conflicts to resolve:** <a Won't that blocks an Outcome, a Will that contradicts a Business Question>

### The first move

One concrete next action that moves the line of sight from paper to working data.

> <e.g. "Confirm a shared customer key across the named sources, pin the atomic grain, and write the first source's data contract — slice 1's foundation and the biggest unknown resolved.">
