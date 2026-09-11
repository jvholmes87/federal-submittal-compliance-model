# Work Breakdown Structure

## Purpose

The work breakdown structure organizes government-facing obligations for a small subcontractor performing federal construction task orders at an overseas installation. Each gate represents an auditable obligation and connects scope, ownership, deadline logic, lifecycle status, and satisfaction evidence.

The deployed instrument began as an approximately 60-gate template. The verified current baseline contains 61 gates across six phase bands. One conditional gate was added during deployment, and instantiated projects contain 60 to 72 rows as conditional and project-specific gates are added or excluded.

## Baseline phase bands

| Phase band | Deployed code range | Baseline gates | Scope |
|---|---:|---:|---|
| `0000` Award & Setup | `0010–0070`, including the gate added at `0025` | 8 | Contract initiation, obligation setup, initial controls, and applicability decisions |
| `0500` Design | `0510–0540` | 4 | Required design-stage packages and design-dependent approvals |
| `1000` Pre-Construction | `1005–1095`; the NTP milestone at `1095` is terminal for the band | 24 | Plans, permits, access requirements, product information, and other prerequisites to field execution |
| `2000` Construction | `2010–2065` | 12 | Execution-phase records, inspections, tests, recurring compliance items, and payment gates |
| `3000` Closeout | `3010–3060`; the property-transfer milestone at `3060` is terminal for the band | 8 | Completion records, turnover artifacts, acceptance evidence, and administrative discharge |
| `4000` Warranty | `4010–4050` | 5 | Warranty-period inspections, corrective obligations, renewal-sensitive items, and final discharge |
| **Total** |  | **61** | Current verified baseline |

Payment is a recurring gate within the Construction band. It is not a separate phase band. Closeout remains one of the six deployed phase bands and is not represented by a separate `9000–9999` structure.

## Numbering scheme

Gate identifiers use four-digit WBS-style codes organized by the six deployed phase bands. Codes advance in increments of 5 or 10 to leave room for later insertions. Project-specific gates use an unused code within the matching phase band and cannot overwrite a baseline identifier.

## Gate record requirements

Each instantiated gate contains or references the following fields:

| Field | Function |
|---|---|
| Gate identifier | Provides the stable four-digit WBS-style reference |
| Phase band | Places the obligation in one of the six deployed phases |
| Gate title | Names the obligation in sanitized, operational terms |
| Applicability | Records whether the gate applies to the project |
| Applicability reason | Makes `N/A` auditable and prevents a blank from being treated as a decision |
| Obligation source | Identifies the governing requirement without reproducing controlled or identifying content |
| Owner | Identifies the party responsible for the current action |
| Lifecycle state | Uses the deployed 11-state set |
| Anchor event | Identifies the event from which a deadline is derived |
| Due date | Stores or computes the obligation deadline when an anchor exists |
| Evidence reference | Points to the filed artifact used to establish status or satisfaction |
| Rejection counter | Records government rejection and cure cycles where applicable |
| Expiry date | Supports `Expiring` and `Expired` controls for time-limited approvals |

## Gate satisfaction

A gate is satisfied only when its defined evidence artifact exists at the required location in the record system. Acceptable evidence may include a signed government artifact, a filed PDF, or a logged government email. A verbal statement, unfiled message, blank applicability field, or elapsed deadline does not satisfy a gate.

Gate satisfaction is distinct from lifecycle status. An item can be `Approved` but remain unsatisfied until the approval artifact is filed and any discharge condition is met. A time-limited item can also move from `Approved` to `Expiring` and `Expired`, which means a prior approval does not establish continuing satisfaction.

## Baseline, conditional, and project-specific gates

| Gate type | Meaning | Instantiation rule |
|---|---|---|
| Baseline | A gate included in the current 61-gate template | Instantiate for applicability review on each project |
| Conditional | A known gate triggered by a defined project condition | Add or activate when the triggering condition exists; otherwise record `N/A` with a reason when the row is present |
| Project-specific | An obligation derived from the governing documents or project conditions that is absent from the baseline | Add under the correct phase band with a unique identifier and source reference |

The 61-gate baseline is a template, not a claim that every project has exactly 61 applicable obligations. Instantiated projects currently range from 60 to 72 rows. Row count and applicable-gate count must therefore be reported separately.

## Mapping gates to lifecycle states

All instantiated gates use the same deployed state vocabulary, with permitted states governed by applicability and obligation type.

| Gate condition or type | Applicable lifecycle path |
|---|---|
| Gate does not apply | `N/A`, with a recorded reason |
| Applicable government-facing submittal | `Not Started` → `In Prep` → `Prime Review` → `Submitted` → `Pending` → `Approved` → `Closed` |
| Government rejection and cure | `Pending` → `Rejected` → `In Prep` → `Prime Review` → `Submitted` → `Pending` |
| Time-limited approval | `Approved` → `Closed` → `Expiring` → `Expired` → `In Prep` for renewal |
| Recurring construction or payment obligation | A new or retained gate instance follows the applicable preparation, prime-review, submission, decision, and closure path for each required cycle |
| Non-adjudicated administrative gate | `Not Started` → `In Prep` → optional `Prime Review` → `Submitted` → `Pending` → `Closed` |

`Prime Review` is required when the subcontractor must route an artifact through the prime contractor before government submission. This state prevents the model from conflating contractor preparation, prime approval or signature, and government receipt.

`Rejected` and `Approved` are reserved for adjudicated submittal gates. An administrative item returned by the recipient moves from `Pending` to `In Prep` without incrementing the rejection counter. This gate-type constraint is important for measurement validity.

`Expiring` and `Expired` apply only to time-limited approvals. These states support permits, passes, and recurring certifications whose validity can lapse after closure.

## Metric implications

Gate type and unit of analysis are part of the metric definition. Administrative, recurring, true submittal rows, package-level outcomes, and line-item outcomes cannot be placed in one approval-rate denominator without changing the meaning of the measure.

At the 11 September 2026 research snapshot, first-pass submittal approval was **69 percent by line item (20 of 29 dispositioned line items)** and **47 percent by package (8 of 17 packages)**. These metrics must be reported separately.

The dashboard's **85 percent current-state gate approval share** is not a first-pass metric. It describes the current state distribution of approval-eligible gates.

A 3 September 2026 gate-row snapshot reported **43 percent (3 of 7)** under an earlier gate-row adjudication definition. It is retained only as a dated historical measurement. The earlier **17 percent** dashboard figure is superseded and retained only as a measurement-design error because it mixed administrative gates with approval-eligible submittals.

These figures do not establish improvement over time because the definitions, units, and populations differ. A longitudinal analysis must use one stable eligibility rule and unit of analysis across observations.

## Change control

Changes to the template require a recorded rationale, phase-band assignment, applicability rule, obligation source, evidence definition, and lifecycle behavior. A new gate must receive a unique identifier. Removing or replacing a gate must preserve the historical records of projects that used it.

Template version and project instantiation are separate concepts. A project retains the template version from which it was instantiated, plus a record of conditional and project-specific changes. This separation permits row-count differences without rewriting the historical baseline.

## Sanitization

This public structure omits gate titles or descriptions that could identify a project, task order, contract, contractor, government personnel member, installation, country, unit, dollar value, or identifying project date. It contains no controlled unclassified information, government forms, reviewer comments, or correspondence.
