# Data Demand: Monthly Recurring Revenue, customer-month grain

> A worked example of the fourth input this skill reads: a **received data demand**.
> Raised by the Revenue Metrics Information Product (the dashboard framed in `information-product-canvas.md`) to the AgileData Data Team.
> A real demand's canonical copy lives in the product repo at `outbox/data-work-needed/monthly-recurring-revenue.md`; this is the copy handed to the Data Team.
> Shape follows the harness protocol `data-demand-pattern.md`: intent plus an acceptance contract, never the how.

## Intent

**What the product must be able to answer, and why.**

The Revenue Metrics dashboard needs a monthly recurring-revenue consume object so the Chief Revenue Officer can act on:

- **Decisions**
  - Target high-value customer segments for expansion (needs recurring revenue by segment).
  - Increase Net Revenue Retention by driving upgrades (needs the monthly revenue movement: new, expansion, contraction, churn).
  - Focus acquisition on profitable channels (needs recurring revenue by acquisition channel).
- **Questions** (from the Revenue Metrics canvas)
  - What is the MRR trend over the last 12 months?
  - How much ARR are we generating across all customer segments?
  - What is ARPU for each customer segment?
  - How much revenue is added through expansion each month?
  - What is Net Revenue Retention after churn and expansion?
  - What is each channel's contribution to MRR and ARR?

### The one hard constraint (grain)

**One row per customer per calendar month.** Every question above rolls up from this grain: segment and channel are attributes of the row, ARR is the annualised monthly figure, and NRR and expansion need the month-on-month movement per customer. A coarser grain (one row per segment per month) cannot answer the per-customer movement or the drill-down the dashboard promises, so this grain is not negotiable.

### Evidence the capture exists upstream

- **Stripe Subscriptions** already captures subscription start, plan change, renewal and cancellation events, and invoices net of discounts. This is the recurring-revenue source.
- **Salesforce CRM** already carries the customer and their demographic segment.
- **Google Ads and Website** already carry the acquisition touch that sets the channel.

We believe the raw capture is present. We have not confirmed it is landed and historised in the warehouse. That check is the Data Team's.

### Traps already known

- **Internal and trial accounts** must not count as revenue.
- **Discounts** are part of recurring revenue: report net of discount, not list price.
- **One-time and non-recurring** charges are not recurring revenue.
- Segment is **demographic**, not an acquisition cohort.

## What we are NOT asking for

- Not table or view designs, not a column list offered as the build, not load patterns, not SQL. The measures named in the acceptance contract are the outcomes we will test, not a schema we are handing you.
- Not the producer's Data Contract. The Data Team authors that in answer to this demand.
- Not non-recurring or one-time revenue.
- Not acquisition-cohort segmentation.

## Acceptance contract

The read-only checks we will run when the data lands. Green means the intent was met. These are observable outcomes, not implementations, grouped by the five clause groups a Data Contract answers with.

| Clause group | Check we will run (read-only) |
|---|---|
| **shape** | Each row exposes opening MRR, closing MRR and the movement between them (new, expansion, contraction, churn, reactivation), plus segment and channel, so NRR and expansion are computable from the row alone. |
| **grain** | Exactly one row per customer per calendar month: no (customer, month) pair appears twice, and no month is skipped while a customer is active. |
| **keys** | The customer key is non-null on every row and resolves to exactly one Salesforce customer; segment and channel are populated on every row. |
| **load type** | The monthly series reconstructs "as at" any prior month-end, and 24 months of history are present, so a restated past month matches what the dashboard showed then. |
| **rules** | Internal and trial accounts contribute zero rows; recurring revenue is net of discounts; one-time charges are absent; for every row `closing = opening + new + expansion - contraction - churn + reactivation`; the object is refreshed daily before 7am. |

When these checks pass, the data answers the CRO's questions at the grain the dashboard needs.

_Data demand, raised to the AgileData Data Team. Protocol: `data-demand-pattern.md` (harness, 2026-09-22)._
