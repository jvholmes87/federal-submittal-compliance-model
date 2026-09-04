# Limitations

## Scope

The instrument is deployed and in use by a small subcontractor performing federal construction task orders at an overseas installation. The available observations come from one organization and one operating context. The artifact documents architecture and preliminary measurements rather than a general estimate of federal-construction performance.

## Single-organization sample

The sample reflects one organization's contracts, personnel structure, prime-contractor routing, government interfaces, and record practices. These conditions may differ across agencies, installations, contract vehicles, primes, and firms. The current data cannot separate organization-specific effects from wider process effects.

## No control group

No comparable organization or project group operates without the instrument under otherwise matched conditions. Changes over time could reflect project mix, reviewer behavior, workforce learning, contract requirements, or other causes. The current observations cannot support a causal claim that the instrument changed approval or timeliness outcomes.

## No inter-rater reliability estimate

Gate applicability, gate type, state, and evidence sufficiency have not yet been independently coded by multiple raters. No inter-rater reliability statistic has been computed. Classification consistency therefore remains an unmeasured source of error.

## Denominator validity

The first dashboard KPI computed first-pass approval across all adjudicated gate rows. That population mixed non-adjudicated administrative gates with true submittals eligible for government approval or rejection. The resulting dashboard value was 17 percent.

The deployed gate typing showed that the denominator combined rows with different possible outcomes. Administrative gates use `Pending` to `Closed` and are prohibited from entering `Rejected` or `Approved`. Their inclusion changed the meaning of the rate.

The corrected definition limits the denominator to adjudicated submittal-type rows eligible to enter `Rejected` or `Approved`. First-pass approval counts an eligible row that reaches `Approved` without an earlier `Rejected` state in its adjudication history. Under that definition, the 3 September 2026 snapshot contains 3 first-pass approvals among 7 adjudicated submittal rows, which is 43 percent after rounding.

The 17 percent value is superseded and is retained only as the record of a measurement-design error. The correction is a metric-validity finding because the instrument's gate-type and transition constraints exposed the invalid denominator. It is not evidence of an operational improvement from 17 to 43 percent.

## Small denominator

Seven adjudicated rows provide an unstable rate. One additional adjudication can materially change the percentage. Every report of the measure must include the numerator, denominator, population, metric definition, and snapshot date.

The rate will move as the portfolio produces additional government decisions. A longitudinal series requires the same eligibility and first-pass definitions at every observation point.

## Measurement effects

Deployment may change how obligations are identified, classified, and retained. Better detection can initially increase the recorded number of late, rejected, or incomplete items. Apparent deterioration may reflect improved visibility rather than a change in underlying performance.

The template also evolved during deployment. The current baseline has 61 gates, while project instances range from 60 to 72 rows. Analyses must distinguish template growth, applicable obligations, completed gates, and adjudicated submittals.

## Structural-conflict observation

The award-plus-30-day and access-dependency case demonstrates a logically infeasible sequence when access occurs after the deadline. It does not establish how often the condition occurs across projects or agencies. Access duration, personnel category, measurement requirements, and available contractual remedies require separate coding before prevalence can be estimated.

## Generalization requirements

Broader claims would require:

- Multiple small contractors and subcontractors across different primes, agencies, locations, and contract types
- A preregistered definition of gate types, adjudication, first-pass approval, timeliness, and compliance failure
- Independent coding and an inter-rater reliability assessment
- A stable observation period with consistent denominator rules
- Project-level covariates for scope, complexity, reviewer, contract type, and access dependency
- A comparison design, such as matched cohorts, phased implementation, or interrupted time series
- Sensitivity analysis for template changes, missing evidence, and state-classification choices
- Documented authority and consent for any operational data used beyond sanitized aggregates

Until those conditions are met, the repository should be read as a deployed architecture description and a record of preliminary, bounded measurements.
