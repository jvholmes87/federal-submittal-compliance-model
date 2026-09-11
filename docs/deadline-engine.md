# Deadline Engine

## Purpose

The deadline engine converts contract and execution events into traceable obligation dates. Every computed deadline retains its anchor, offset, day-count rule, and dependency path. The engine leaves an obligation unanchored when its required event has not occurred.

## Anchor event types

| Anchor | Definition | Example derived deadline |
|---|---|---|
| `AWARD` | Contract award date | Award plus 30 calendar days for an initial submittal set |
| `NTP` | Notice to Proceed issue date | NTP plus a specified number of days for schedule windows or performance-period activities |
| `GOV_RESPONSE` | Government review-decision date | Response plus 10 calendar days for resubmission |
| `SUBMIT` | Contractor transmittal date | Start of the government-review expectation window |
| `ACCESS_GRANT` | Installation access issued for required personnel | Release of site-measurement-dependent work |
| `SITE_EVENT` | Site release, site visit, or survey completion | Release of condition-dependent deliverables |
| `ACTIVITY_COMPLETE` | Completion of a predecessor field activity | Completion plus 30 days for a cure-gated successor |
| `SUBSTANTIAL_COMPLETION` | Area acceptance or beneficial occupancy | Warranty start and interim inspection gates at plus 4 and plus 9 months |
| `CDD` | Contract delivery date | Closeout obligations back-planned from the delivery date |

## Computation model

Each deadline rule contains an anchor type, signed offset, unit, day-count basis, and adjustment rule. A forward deadline uses a positive offset. A back-planned deadline uses a negative offset.

For a calendar-day rule:

\[
D = A + o
\]

where \(D\) is the derived due date, \(A\) is the recorded anchor date, and \(o\) is the signed calendar-day offset.

For a month-based warranty rule, the engine applies the specified calendar-month offset to the substantial-completion date. It records the resulting date and the rule that produced it. Month-based rules are not converted to a fixed number of days.

## No anchor, no clock

If the required anchor event has not occurred, the engine stores no derived deadline. It records the obligation as unanchored and identifies the missing event. It does not substitute the award date or the current date.

This rule distinguishes an overdue obligation from an obligation whose contractual clock has not started. Alerts may still identify a missing or delayed anchor as a separate control condition.

## Calendar days and business days

Calendar days are the default because the deployed orders use calendar-day clocks unless stated otherwise. A rule may use business days only when the governing obligation explicitly requires them.

A business-day rule requires an approved calendar containing weekends and applicable closure dates. If the required calendar is absent, the deadline remains unresolved and the instrument raises a configuration alert. It does not silently calculate calendar days.

When a computed business-day date falls outside a permitted workday, the configured rule determines the adjustment. The adjustment direction and calendar version remain part of the deadline record.

## Cascade behavior

Each derived deadline points to its anchor event and rule. When an anchor date changes, the engine recomputes every directly dependent date. It then recomputes downstream obligations whose anchors are derived from the changed activity.

For a simple fixed-offset chain:

\[
\Delta D_i = \Delta A
\]

Every downstream date shifts by the same amount when its rule and dependency path remain unchanged. The system retains the previous value, new value, change reason, and event time in the audit history.

A cascade does not overwrite an actual event. If a site visit has already occurred, moving a planned access date cannot replace the recorded site-visit date. Actual events break the forecast chain and become the controlling anchors for later rules.

## Worked structural-conflict example

Assume an initial site-dependent submittal has a contractual deadline of award plus 30 calendar days:

\[
D = A + 30
\]

The submittal requires site measurements. Those measurements require installation access for the assigned personnel, so the earliest feasible site event \(S\) cannot precede access grant \(G\):

\[
S \geq G
\]

If access processing extends beyond the contractual 30-day interval in the stated population:

\[
G > A + 30
\]

and preparation and routing can finish only after the site event, then the earliest feasible submission \(E\) is later than the contractual deadline:

\[
E > S \geq G > D
\]

The deadline engine therefore records the award-based due date while showing that the `ACCESS_GRANT` and `SITE_EVENT` prerequisites remain unanchored. The alert layer identifies the dependency conflict before access occurs. The engine does not invent an access date or redefine the contractual due date.

The appropriate resolution requires a documented contractual, sequencing, access, or scope decision by the responsible parties. The instrument records that decision and recomputes affected dates after a valid anchor or rule change is entered.

This is a formalized observation of a requirements conflict in the studied setting. It does not establish how frequently the pattern occurs across federal construction and should not be presented as a general causal finding without broader validation.

## Review-aging observation

The same engine can distinguish contractor preparation time from post-submission waiting time. At the 11 September 2026 research snapshot, **11 tracked items had been pending more than 14 days and the oldest had been pending 66 days**, against a contractual one-work-week response obligation in the studied context.

For a submitted item, the review-age quantity is:

\[
R = T - S
\]

where \(R\) is elapsed review age, \(S\) is the recorded submission/receipt anchor, and \(T\) is the observation date when no decision has yet been recorded.

A review-aging alert does not assign fault. Formal analysis must preserve the responsible actor, contractual timing rule, any acknowledgment or intermediate response, and any intervening dependency before attributing delay.

## Alerts

| Condition | Alert purpose |
|---|---|
| Due date approaching | Prompts action within the configured lead window |
| Due date breached | Identifies an open obligation past its computed deadline |
| Anchor missing | Identifies an obligation whose clock cannot yet be computed |
| Dependency conflict | Identifies a prerequisite forecast or actual date later than the obligation due date |
| Review aging | Surfaces a `Submitted` or `Pending` item beyond its review expectation |
| Approval expiring | Moves a time-limited closed item to `Expiring` at the configured threshold |
| Approval expired | Moves the item to `Expired` when the expiry date passes without renewal evidence |

Alerts do not change evidence, approval, or satisfaction status except for the defined time-driven expiry transitions. Alert acknowledgment does not close an obligation.
