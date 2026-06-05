# AskAI: Scope the Work

A Claude skill for AgileData data teams. You have been handed a vision and asked to build it. This skill helps you **understand the scope**: what's clear, what's unclear, and the sharp questions to resolve. It turns the gap between "here is the vision" and "here is the first table I write" into shared understanding before anyone builds, and answers your what / how / why along the way.

## What you bring

A **why**, a **what**, and a **how**. The **what** comes in one of two forms, depending on the kind of work:

| Layer | Artefact | Use when |
|---|---|---|
| **why** | Mission Statement | the strategic outcome (umbrella over the work) |
| **what** | **Information Product Canvas** | there is a **business problem** to solve (a stakeholder needs questions answered) |
| **what** | **AgileData Press Release** | there is a **platform capability / tooling** to create |
| **how** | Architecture Sketch | the sources, pipeline and outputs on the AgileData stack |

Most data-team work is a business problem, so the **Information Product Canvas** is the usual "what". Use a **Press Release** when you are building reusable platform capability. A large capability can have both: a Press Release for the capability and a Canvas per Information Product under it.

You can start with only one artefact. The skill works with what you have and tells you what the missing pieces would change.

## How to use it

1. Drop your templates into the conversation (paste them, or point Claude at the files).
2. Ask what you want to understand: "help me understand this scope", "what's unclear here?", "what do we need to build?", "where do we start?", "why are we building this?".
3. Claude leads with **what's clear and what's unclear** (every gap as a sharp question), answers your what / how / why with the **line of sight** in view, and lays out the full structured scope (see `assets/scope-understanding-template.md`) when you want the complete picture.

If your AgileData MCP is connected to your tenancy, the skill also checks the catalog so "reuse before rebuild" is grounded in what your tenancy actually holds.

Each session is also saved as a local **session log** (`~/.claude/askai-scope-sessions/`) so the skill can be improved from real use. Say "don't log this" to opt out.

## What you get back

- **What's clear and what's unclear** — the scope you can stand behind, and every gap turned into a sharp question (why it matters, who owns the answer). The headline.
- A **line-of-sight check** across your templates: where they cohere, and where they break (the breaks are your sharpest questions).
- The **Information Products** behind each Business Question or benefit, each with a question and a grain (the canvas does not capture grain, the skill pins it).
- The **new-to-build scope** separated from what you can reuse.
- **Slices**, thinnest valuable first, each T-shirt sized and sequenced.
- The **scope boundaries** (a canvas's Will/Won't), honoured and pressure-tested.
- The **unknowns and risks** to resolve before building, and a concrete **first move**.

## What it does not do

It builds understanding, scopes and frames. It does not author data contracts or build pipelines. Those come next, on the AgileData Golden Path: Frame → Design → Build → Verify.

## See it work

`pattern-templates/` holds two worked examples, one per form of the "what":

- `pattern-templates/business-problem/` scopes an **Information Product Canvas** (the canonical Revenue Metrics canvas). See how the skill pins the grain the canvas leaves open, maps Core Business Events and Systems of Capture to sources, slices seven Business Questions into buildable increments, and catches two boundary conflicts hidden in the Will/Won't.
- `pattern-templates/platform-capability/` is the **AI Analyst** platform capability, given as a **Press Release** with its **Mission Command Statement** and **Architecture Sketch**. Point the skill at it and ask it to scope: it has to decompose the press release into Information Products, pin the grain the artefacts leave open, weigh the mission's Boundaries, and notice that the architecture is a generic LLM-agent pattern not yet mapped to the AgileData stack.

## What is in here

```
agiledataguides-askai-data-work-scope/
├── SKILL.md                          the method Claude follows
├── README.md                         this file
├── references/
│   ├── reading-the-artefacts.md      how to read and critique each input (incl. the Canvas field by field)
│   └── delivery-model.md             the AgileData delivery vocabulary
├── assets/
│   ├── scope-understanding-template.md  the output template (clear, questions, then structured scope)
│   └── session-log-template.md          the per-session log, saved for iterating the skill
└── pattern-templates/
    ├── business-problem/             an Information Product Canvas (Revenue Metrics)
    └── platform-capability/          a Mission + Press Release + Architecture Sketch (AI Analyst)
```

## Licence

Licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). Share and adapt with attribution to Agile Data Guides; derivatives under the same licence. See [`LICENSE`](LICENSE).
