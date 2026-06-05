# The AgileData delivery model

This is the vocabulary that turns intent into buildable scope. The three artefacts describe demand (why, what, how). This model describes supply (the things a data team actually builds). Scoping is the act of meeting the demand with the supply, using these terms precisely.

Use the exact words. A team that says "table" when they mean "Information Product", or "field" when they mean "grain", loses the ability to reason about scope. Precision here is not pedantry, it is how the line of sight stays visible.

## Table of contents

- [Information Product: the unit of demand](#information-product)
- [Grain: the most important decision](#grain)
- [Concepts, Details, Events: the modelling primitives](#concepts-details-events)
- [Data Contract: the agreement before the build](#data-contract)
- [Business Key: the natural identifier](#business-key)
- [Load Type: change data vs event data](#load-type)
- [The pipeline: Land to Consume](#the-pipeline)
- [The consume layer: where questions get answered](#the-consume-layer)
- [Change Rules vs Trust Rules](#change-rules-vs-trust-rules)
- [Tenancy and the catalog](#tenancy-and-the-catalog)
- [The Golden Path](#the-golden-path)
- [T-shirt sizing](#t-shirt-sizing)

---

## Information Product

The **question a stakeholder needs answered, plus the shape of data that answers it.** This is the unit of demand. Everything downstream (the Data Contract, the pipeline) exists to serve an Information Product. Design always starts here.

In scoping, the "what" artefact decomposes into Information Products. From an **Information Product Canvas**, each Business Question is one Information Product, already framed with its persona, events, sources, delivery and scope. From a **Press Release**, each benefit typically maps to one Information Product: one question, one shape of answer. Either way, if you cannot phrase the demand as a question a stakeholder would ask, it is not yet a designable Information Product, and that is a finding.

An Information Product spec, once framed, states:

- the **question** and the **stakeholder**
- the **grain** (one row per ...)
- the **Concepts / Details / Events** involved
- the **consume shape** that answers it
- **what exists already** versus **what is new**

### Captured on an Information Product Canvas

The Information Product Canvas is AgileData's one-page tool for capturing an Information Product's demand before design, filled in with the stakeholder in about 30 minutes. It maps almost directly onto the spec above: Business Questions are the questions, Personas the stakeholder, Core Business Events the Events, Systems of Capture the sources, Delivery Types the consume shape, Data Sync the freshness, and Will/Won't the scope. It does **not** capture grain or business keys, so those are the first things scoping adds. See `reading-the-artefacts.md` for the field-by-field read.

## Grain

**What one row represents.** "One row per grant programme per month." The single most important design decision: everything downstream is shaped by it, and getting it wrong means rebuilding. Always pin the grain, write it down, and read it back to the stakeholder before going further.

In scoping, an Information Product with no agreed grain is not yet scoped. Grain ambiguity is one of the most common and most expensive unknowns, so surface it early and explicitly. Two stakeholders who picture different grains for "the same" report are describing two different builds.

## Concepts, Details, Events

The modelling primitives. From the question and the grain, name:

- **Concepts**: the business things, the nouns: grant programme, recipient, payment.
- **Details**: their descriptive attributes: a programme's name, budget, opening date.
- **Events**: what happens to or between Concepts over time, the verbs: grant awarded, payment made, application withdrawn.

In scoping, naming the Concepts and Events for each Information Product tells you what has to be modelled, which tells you the pipeline work. Concepts and Events that already exist in the tenancy are reuse. New ones are build.

## Data Contract

The **agreed shape of a data set before it is built.** No data gets built without one. A contract states:

- **shape**: columns and types
- **grain**: what one row represents
- **keys**: the business key, entity_key naming
- **load type / pattern**: how the data arrives and is applied
- **rules**: quality, allowed values, freshness

In scoping, each Information Product implies one or more Data Contracts (one per data set it needs). You do not author the contracts here, that is the next skill, but you do identify which contracts the scope requires. "This Information Product needs three contracts, two of which we already have" is a scope statement.

## Business Key

The **natural identifier for a row**, named `{entity}_key` (for example `grant_programme_key`), validated for uniqueness. Use a composite key only when no single column is unique. Tables that share an `{entity}_key` join automatically in the consume layer, which is why consistent key naming is a design decision, not a detail.

In scoping, an entity whose business key is undefined or not unique is an open question: you cannot write the contract or guarantee the joins until it is settled.

## Load Type

How a data set arrives and is applied:

- **change_data**: the current state of things that change over time (a programme's budget, a recipient's status). Applied by insert or upsert against history.
- **event_data**: things that happen at a point in time and do not change (a payment was made, an application was submitted). Applied by insert.

The load type drives the pipeline pattern. It can be auto-detected, but in scoping it is worth naming per source because it affects how much history work each source needs.

## The pipeline

The AgileData data architecture, the stages every data set moves through:

**Land → History → Capture → Acquire → Model → Consume**

| Stage | What happens |
|---|---|
| **Land** | Raw data arrives from a source (file drop, API, extract) and is landed as-is. |
| **History** | Every version of every row is kept, so you can always see what the data said at any point in time. |
| **Capture** | The data is captured into the design model, typed and keyed. |
| **Acquire** | Business logic begins: the data is shaped towards Concepts, Details, Events. |
| **Model** | The Concepts, Details, and Events are modelled, keys assigned, relationships set. |
| **Consume** | Consume-layer tables and views are built that answer the Information Product questions, with auto-join across shared keys. |

In scoping, for each Information Product work out which stages are **new** versus **already there** for each source. A source already landing and historised is mostly reuse, you may only need new Model and Consume work. A brand-new source needs the whole path. The new-stage count per source is a strong driver of the slice size.

## The consume layer

Where questions get answered. The consume layer holds the tables and views the Information Products read. Tables sharing an `{entity}_key` join automatically here, so a well-keyed model produces consume answers with little extra work. The consume shape (the table or view at the Information Product's grain) is what the team is really building towards, every earlier stage exists to make it possible.

## Change Rules vs Trust Rules

Two different things, do not conflate them:

- **Change Rules**: the pipeline rules that transform and load data, the logic that moves data through the stages and builds the model. This is the build.
- **Trust Rules**: data quality and validation rules that check the data can be trusted (uniqueness, allowed values, freshness, row counts). This is the assurance.

In scoping, both are work. Change Rules deliver the data, Trust Rules make it trustworthy enough for the stakeholder to act on. A press-release benefit that says "funders can rely on" implies Trust Rules, not just Change Rules.

## Tenancy and the catalog

A **tenancy** is an isolated AgileData environment with its own data plane, context plane, and surfaces. A build targets exactly one tenancy. Reads can draw on a shared reference tenancy for examples, but never write to it.

The **catalog** is the searchable inventory of what a tenancy already holds: tables, Concepts, fields. If the MCP is connected, `get_catalog_overview`, `search_catalog_tiles`, and `search_catalog_fields` turn reuse-before-rebuild into evidence. Always confirm which tenancy the MCP resolves to before any data call.

## The Golden Path

The recommended end-to-end journey: **Frame** (design the Information Product) → **Design** (author the Data Contract) → **Build** (create Change Rules, run the pipeline) → **Verify** (profile the data) → **Record**. This skill lives at the very start, before Frame: it scopes the work so the team knows which Information Products to take onto the Golden Path, and in what order.

## T-shirt sizing

Estimate in sizes, never in hours: **XS / S / M / L / XL**. The size exists to force a conversation about scope before work starts, not to predict a delivery date.

| Size | Roughly |
|---|---|
| **XS** | A trivial change, reuse with a tweak. |
| **S** | One contract, one mostly-existing source, light new Model and Consume work. |
| **M** | A few contracts, some exploration, new modelling, one new source. |
| **L** | Multiple contracts, multiple new sources, real design decisions, several pipeline stages new. |
| **XL** | Needs to be sliced before it can be built. An XL is a signal, not an estimate: break it down. |

In scoping, size each slice. An XL slice is telling you the slice is still too big to start, go back to step 5 and cut it thinner.
