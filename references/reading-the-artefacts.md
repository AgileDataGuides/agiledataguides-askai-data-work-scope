# Reading the artefacts

Your read of the scope is only as good as your read of the inputs. The team is handed completed **Pattern Templates** carrying three dimensions of intent: the **WHY** (the outcome), the **WHAT** (what to build), and the **HOW** (the technical shape). These are not one template each: a Mission carries mostly WHY but also names WHATs (its boundaries and key tasks), and a Press Release carries mostly WHAT but also WHYs (its benefits trace to the mission). The dominant WHAT comes in one of two forms: an **Information Product Canvas** for a business problem, or an **AgileData Press Release** for a platform capability. A fourth input sometimes arrives: a **received Data Demand** (section 4), a downstream product's ask for data the warehouse does not yet serve, carrying its intent and the acceptance contract it will test delivery against. Each template carries part of the intent, and each has a characteristic way of being weak. This reference covers, for each: what it is, what a good one contains, how to read it for scope, the gaps to flag, and how to cope when it is thin or missing.

The discipline that runs through all of them: separate **stated** (what it says) from **implied** (your inference) from **unknown** (what it leaves open). When you quote the artefact you are on solid ground. When you infer, mark it. When you hit an unknown, turn it into a question for the team rather than filling it yourself.

---

## 1. Mission Statement: the WHY

### What it is

The reason the work is worth doing. In the AgileData world a mission takes a person or organisation from one state to a better one: "take a stakeholder from a question to a trusted answer", "move grant funding to where it does the most good". It names an outcome and who it is for. It is the umbrella over the work; one mission usually sits above several Information Products.

### Mission Statement or Mission Command Statement

A mission can arrive as a single line, or as a fuller **Mission Command Statement**. The longer form adds structure worth mining:

- **Higher Intent** the strategic outcome, the umbrella. This is the mission proper; read it as the WHY.
- **Squad Intent** how this squad will pursue it, often already naming the narrow first focus and the "start narrow, earn trust, then widen" shape.
- **Success Looks Like** the few measures that show the mission was met. Your acceptance signals at mission level.
- **Boundaries** mission-level guardrails. Read these like a Canvas's Will/Won't: honour them, and flag any benefit or question that would breach one.
- **Key Tasks** a first cut at the work. Treat them as a candidate slice sequence to pressure-test, not a committed plan.

The Boundaries and Key Tasks are a gift: they pre-state scope and sequence the team already has in mind. Hold them in the stated register, then test them against the WHAT the same way you test everything else.

### What a good one contains

- A **clear outcome**, not a slogan. "Help funders see which programmes are over-subscribed so they can rebalance" is an outcome. "Be data-driven" is a slogan.
- A **who**: whose decision or work improves.
- A sense of **what good looks like** when the mission is met.

### How to read it for scope

The mission is your anchor for **why**. Everything in the scope traces back here. Extract the **decisions or actions** the mission is trying to improve, because those become the outcomes the work must serve. With a Canvas present, check that the canvas's Outcomes/Actions ladder up to the mission.

### Gaps to flag

- **Slogan, not outcome.** If you cannot name the decision behind the mission, say so. A vague mission cannot anchor scope.
- **No who.** An outcome with no owner has no stakeholder to frame work around.
- **Unmeasurable.** If you cannot imagine the few numbers that would show the mission was met, the work will struggle to promise anything concrete.

### When it is thin or missing

For a business problem, the Canvas's Outcomes/Actions carry the product-level why, so you can scope without a separate mission, you just lose the umbrella that confirms several products pull the same way. State that the Outcomes are standing in for the mission and recommend the team confirm the strategic why.

---

## 2. The WHAT: Canvas or Press Release

The "what" artefact describes what gets built. Which one you are reading depends on the kind of work:

- **A business problem to solve** (a stakeholder needs questions answered so they can act) → an **Information Product Canvas** (section 2a). The common case for a data team.
- **A platform capability or tooling to create** (a reusable feature built into the platform) → an **AgileData Press Release** (section 2b).
- **A large platform capability** decomposes into Information Products, so you may get a Press Release *and* one or more Canvases. The Press Release is the capability; each Canvas is a product it delivers.

### 2a. Information Product Canvas (business problem)

#### What it is

A one-page canvas that captures the requirements for a single Information Product before it is designed or built. It is AgileData's adaptation of the Business Model Canvas to data requirements, and it is meant to be filled in with the stakeholder in about 30 minutes, in shared language. It frames the demand: what questions, for whom, to drive what action, fed by what events, delivered how and how often, and explicitly what is in and out.

#### The fields, and how to read each for scope

| Field | What it gives you for scope |
|---|---|
| **Name / Product Owner** | The product's identity and who owns the decisions. |
| **T-Shirt Size** | The team's first estimate for the *whole* product. A starting point you will refine per slice; a suspiciously small size on a multi-question canvas is a flag. |
| **Outcomes / Actions** | The **why** at product level: the action the stakeholder takes once they have the answer. This is the line-of-sight target. Every Business Question should serve an Outcome. |
| **Business Questions** | The heart. Treat **each question as a candidate Information Product**. Read them for the grain they imply (the canvas does not state grain), whether they share a grain or need different ones, and the dimensions they slice by (segment, channel, month). |
| **Vision (FOR / WHO / THE / THAT / UNLIKE)** | The elevator pitch: the persona and their need, the delivery and what it automates, and the status quo it replaces. A sanity check that the product has a clear shape and a real "before". |
| **Personas** | The stakeholder(s). Every Business Question should belong to a persona. A question with no persona is orphaned. |
| **Core Business Events** | The **Events** to model (the verbs). The richest statement of what has to be captured. |
| **Systems of Capture** | The **sources**: which system carries each event. Your source list, but confirm each exists in the tenancy and that they share a business key, or the data will not join. |
| **Delivery Types** | The **consume shape** (dashboard, extract, API). More than one delivery type means more than one consume build. |
| **Data Sync** | The **freshness** the pipeline must meet (daily before 7am, real-time). A hard constraint and a real scope driver: real-time is a different build from daily. |
| **Feature Stories** | The hidden scope. Read these carefully, they quietly add work: "as at any point of historical time" means the History layer must be built in full; "drill down to the transactions behind a number" sets the atomic grain and the detail; "export" adds an extract delivery. |
| **Will / Won't** | The explicit scope boundaries, already decided by the stakeholder. Honour them. |

#### Gaps the canvas characteristically leaves (what scoping must add)

- **Grain.** Not captured anywhere. Pin it per question (one row per ...). The single most important thing you add.
- **Business keys.** Not captured. Confirm the shared key across the Systems of Capture, or there is no join and no product.
- **Source existence.** The canvas *names* Systems of Capture; it does not confirm they are landed in the tenancy. Check (catalog if MCP is connected).
- **Full Concept / Detail modelling.** The canvas gives Events and Personas, not the whole Concept / Detail / Event model.
- **Data Contracts.** Not authored. The canvas tells you which contracts are needed, not their detail.

#### Gaps and conflicts to flag

- **Too many questions treated as one build.** A canvas with seven Business Questions is seven candidate Information Products. Scope and slice them; do not let the team promise all of them at once.
- **A question and a boundary that quietly conflict.** A question about "the last 12 months" beside a Will that says "trends for the past 24 months", or a Won't that blocks an Outcome. These are easy to miss and expensive to discover late.
- **Systems of Capture assumed to share a key.** Several source systems are listed as if the same customer or entity is identifiable across all of them. Often it is not. Raise it.
- **An Outcome with no question, or a question with no Outcome.** The first is an unmet need, the second is curiosity. Both are line-of-sight breaks.

#### When it is thin or missing

If the work is a business problem and there is no canvas, you have no concrete questions to answer, so the Information Products are guesses. Recommend running an Information Product Canvas with the stakeholder first; it is a 30-minute exercise and it is exactly the input this skill scopes from. A half-filled canvas (questions but no Outcomes, or events but no Systems of Capture) is worth completing before scoping, and saying which fields are missing is itself a finding.

### 2b. AgileData Press Release (platform capability)

#### What it is

A working-backwards announcement, written as if the thing already shipped. Amazon's customer-announcement style, adapted by AgileData: third-person, problem-before-solution, **outcomes not features**. It describes the future state of a platform capability or tool from the user's point of view. It is not a changelog and not an implementation plan.

A well-formed AgileData press release has these sections:

- **Narrative title** a full third-person sentence of news.
- **Date line** DD Month YYYY.
- **Lead** "<Org> today released <feature>, <one-sentence value-prop>."
- **The Problem** the user pain, concretely, before any solution.
- **The Solution** what shipped, as an outcome from the user's view.
- **How It Works** optional, only the mechanics that shape the user's mental model.
- **Key Benefits** outcomes the user gains, not features that were built.
- **Closing** an "available now" line.

#### How to read it for scope

The press release is your source of **what** for a capability build. Mine it in this order:

1. **The Problem** tells you the pain the capability must address.
2. **Key Benefits** are your acceptance criteria. Each is a future-state outcome and a line-of-sight target: it must trace up to the mission and down to the architecture. If the capability delivers Information Products, each benefit may spawn a Canvas.
3. **The Solution and How It Works** hint at the shape of what is built.

#### Gaps to flag

- **Features dressed as benefits.** "Added a status column" is a feature; "users can spot a problem at a glance" is a benefit. A benefit list that is really a feature list means the working-backwards thinking was skipped.
- **Problem missing or vague.** No concrete problem means no clear thing to deliver.
- **Unmeasurable benefits.** A benefit you cannot picture as a result cannot be delivered or verified.
- **Solution that is all implementation.** If the press release reads like an architecture doc, the what and how have collapsed, and you have lost the independent check that the architecture serves a user outcome.

#### When it is thin or missing

With a mission and an architecture but no press release (and no canvas), you have a why and a how but no concrete what. Recommend writing the press release (capability) or canvas (business problem) first; architecture with no outcome to serve is where over-building begins.

---

## 3. Architecture Sketch: the HOW

### What it is

The technical shape that delivers the what, drawn against the AgileData layered stack. For one solution it shows: where the data comes from (sources), how it lands and flows through the pipeline (Land → History → Capture → Acquire → Model → Consume), the key Concepts and Events modelled along the way, and what it produces at the top (consume tables, Information Product apps, the surfaces a consumer uses). It is a *sketch*: enough to show a credible path from source to answer and to expose the big decisions.

For a business problem, the Canvas already sketches a lot of the how (its Systems of Capture are the sources, its Core Business Events are what gets modelled, its Delivery Types are the consume outputs, its Data Sync is the cadence). So the Architecture Sketch may be light, or fold into the canvas. Reconcile the two: the architecture should not contradict the canvas's sources, delivery or cadence.

### What a good one contains

- **Named sources** with some idea of how they arrive (file drop, API, stream, extract).
- A **pipeline path** showing the data moving up the stages to a consume output.
- The **consume outputs**: the tables the Information Products read, and the apps that present them.
- Enough to locate every question or outcome somewhere on the stack.

The canonical shape to sketch against is the AgileData layered architecture: People → App / Experience → AssistedAI surfaces → Interface → API capability → Context plane → Data plane (Landing → History → Design → Consume).

### How to read it for scope

1. **Locate every question/outcome on the stack.** Trace each down to a consume output, then to the sources that feed it. Something you cannot trace to a source is a gap: the promise has no supply.
2. **Spot speculative components.** A box that serves no question or outcome is a candidate for cutting.
3. **Find the new-versus-existing split.** Which sources, stages, and consume tables already exist, and which are net new? The net-new set is the bulk of the build scope.

### Gaps to flag

- **Source with no destination, or destination with no source.** A broken pipeline path.
- **Outcome with no architectural home**, or **component with no outcome.**
- **No grain anywhere.** If the consume outputs have no stated grain, the architecture has not met the Information Product design; reconcile them.
- **Big magic boxes.** A single box labelled "model the data" or "predict" that hides the real work. Push for what Concepts, Events, or logic actually get built, especially when the whole value rests on it.

### When it is thin or missing

With a why and a what but no architecture, you can frame Information Products and identify the data they need, but you cannot confirm the path exists or estimate pipeline work with confidence. Treat sizing as provisional and make "sketch the architecture for the first slice" an early first move.

---

## 4. Data Demand: a received ask (optional fourth input)

### What it is

A **data demand** is an ask raised by a downstream product (an Information Product app) when it needs data the warehouse does not yet serve: a new consume object, a missing column, a wrong grain. Unlike the three templates above, which a stakeholder authors to express a vision, a demand is **received** by the data team from the product, and it arrives already pointed at a specific consume object and grain. It is the AgileData protocol for how the question travels from a product to the data team. Its canonical copy lives in the product repo's `outbox/data-work-needed/<slug>.md`, and a copy is handed to the data team.

A demand carries exactly two things:

1. **Intent**: the decisions the data supports and the questions being asked, in business language, plus the one hard structural constraint (usually grain), evidence the capture exists upstream, and the traps already known.
2. **An acceptance contract**: the read-only checks the product will run when the data lands. Green means the intent was met. Checks name observable outcomes ("every event carries its date", "history reconstructs", "the change count is at least the source's"), never implementations. They cover the same five clause groups a Data Contract answers with: shape, grain, keys, load type, rules.

### What it always carries, and never carries

| Always | Never |
|---|---|
| The decisions the data supports | Table or view designs |
| Questions in business language | Column lists offered as the solution |
| The one hard constraint (usually grain) | Load patterns, SQL, tool choices |
| Evidence the capture exists upstream | The producer's Data Contract |
| A `What we are NOT asking for` section | Staff contacts or customer data values |
| The acceptance contract | |

The boundary rule: **a demand says what the product needs to be able to answer, never how to build it.** Precision is not prescription: naming the exact consume object (`consume.customer`), the exact source, or the exact grain is wanted, that is the demand being testable. The line is crossed when the demand starts designing what does not exist yet.

### How to read it for scope

A demand is the sharpest input you can get, because it arrives pre-scoped and testable. Read it in this order:

1. **Intent to Information Products.** The decisions and questions map straight to one or more Information Products, at a grain the demand usually states outright (where a Canvas leaves grain open). This is your line-of-sight target.
2. **Acceptance contract to the contracts implied.** The checks pre-fill the *Data contracts implied* table: the consume object, grain, keys, load type and rules are already named and testable. Carry them across as the producer's target, marked *(from demand)*. You identify the contracts; you do not author them or run the checks here.
3. **Evidence of capture to the sources.** The demand names where the data is captured upstream. Confirm those sources exist in the tenancy (catalog if MCP is connected), exactly as for a Canvas's Systems of Capture.

### Gaps to flag

- **A demand that carries the how.** Column lists, table designs, load patterns or SQL mean the ask has overstepped and is quietly transferring the modelling decision from the person who knows the warehouse to the person who knows the app. Flag it and hand the how back to the data team.
- **No acceptance contract, or checks that are not runnable.** A demand with no testable checks cannot be proven fit on delivery, so "fit for purpose" becomes a matter of opinion. Ask for the checks.
- **Intent with no grain.** The one constraint a demand should pin is grain. If it is missing, that is the first question, the same as for a Canvas.
- **A demand that contradicts a Canvas or Mission for the same product.** When both are supplied, the demand's intent and grain should agree with the Canvas's questions and the Mission's outcome. A mismatch (a demand at monthly grain against a Canvas question about daily movements) is a sharp question.

### When it is thin or missing

A demand is optional, and most scoping runs without one. When it is present it is a gift: it pins grain and pre-fills the contracts. When it is thin (intent but no acceptance contract, or an acceptance contract with no runnable checks), name what is missing and recommend completing it before the data team commits, because the acceptance contract is the only thing that makes delivery testable.

---

## Reading them together (the line of sight)

The artefacts are most valuable as a set. The cross-checks between them are the line of sight (SKILL.md, method step 2). In short:

**When the what is a Canvas:**

- Questions ↔ Outcomes: does every Business Question serve an Outcome, and every Outcome have a question?
- Outcomes ↔ Mission: does every Outcome ladder up to the strategic why?
- Questions ↔ how: can the Delivery Types, Data Sync and Systems of Capture answer the questions at the cadence promised (and does the Architecture agree)?
- Will/Won't ↔ the rest: is any boundary in conflict with a question or an Outcome?

**When the what is a Press Release:**

- Benefit ↔ Mission: does every benefit serve a mission outcome, and every mission outcome appear as a benefit?
- Benefit ↔ Architecture: does every benefit have an architectural home, and every component serve a benefit?

**When a Data Demand is present (alongside a Canvas or Mission):**

- Demand ↔ Canvas / Mission: does the demand's intent and grain agree with the Canvas's questions and the Mission's outcome? A mismatch is a sharp question.
- Demand ↔ contracts implied: does every contract the scope needs map to an acceptance check, and every check to a contract clause group (shape, grain, keys, load type, rules)?
- Demand boundary: does the demand stay on the what, or has it strayed into the how? A demand carrying column lists or SQL is a break to flag, not a link that holds.

A coherent set, where each link holds, is the strongest signal that the scope is healthy. Each break is a sharp, specific question for the team, and surfacing those questions is the core of helping them understand the scope.
