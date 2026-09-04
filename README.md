# Federal Submittal Compliance Model

## Purpose

This repository documents the sanitized architecture of a deployed compliance instrument used by a small subcontractor performing federal construction task orders at an overseas installation. The instrument tracks government-facing obligations across concurrent work without publishing operational records.

The research framing is requirements engineering and obligation traceability in federal construction compliance. Small organizations carry obligation loads that may exceed the support provided by their tools. This instrument enforces obligation rules in the data model so that lifecycle, evidence, applicability, and deadline controls remain consistent across records.

## Instrument scope

The deployed instrument contains four connected controls:

- An approximately 60-gate work breakdown structure organized into six phase bands
- An 11-state lifecycle model covering preparation, prime-contractor routing, government adjudication, closure, and expiry
- A deadline engine that derives obligation dates from award and other anchor events
- An alert layer that surfaces approaching deadlines, breached deadlines, stalled reviews, and expiring approvals

The current baseline contains 61 gates. Instantiated projects contain 60 to 72 rows because conditional and project-specific gates vary by scope.

## Measured findings

### First-pass approval

At the 3 September 2026 snapshot, the first-pass approval rate was 43 percent, defined as 3 first-pass approvals among 7 adjudicated submittal rows. The population was a small subcontractor performing federal construction task orders at an overseas installation. The denominator includes only submittal-type rows eligible to enter `Rejected` or `Approved` and excludes non-adjudicated administrative gates.

The denominator is small, the sample comes from one organization, and no control group exists. The rate will change as additional rows are adjudicated. It is a measured snapshot rather than a general performance claim.

An earlier dashboard calculation produced 17 percent because it mixed administrative gates with true submittals. That value is superseded. Detection and correction of the denominator error is documented as a metric-validity finding because the instrument's gate typing exposed the invalid population definition.

### Structurally unsatisfiable timing

The instrument identified a requirement pattern in which certain submittals were due 30 calendar days after contract award, while required installation-access processing for non-U.S. personnel routinely exceeded 30 days. Some affected submittals required site measurements that could occur only after access was granted. The required sequence made on-time completion structurally infeasible when access extended beyond the contractual due date.

This is an observed requirement conflict in the stated population. It does not establish the frequency or effect of the conflict across federal construction generally.

## Repository structure

| File | Contents |
|---|---|
| [`docs/lifecycle-model.md`](docs/lifecycle-model.md) | Deployed states, transitions, ownership, guards, and illegal transitions |
| [`docs/wbs-structure.md`](docs/wbs-structure.md) | Six phase bands, gate counts, numbering, satisfaction, and metric typing |
| [`docs/deadline-engine.md`](docs/deadline-engine.md) | Anchor events, date computation, cascades, and the timing-conflict example |
| [`docs/data-model.md`](docs/data-model.md) | Conceptual entities, relationships, and database invariants |
| [`docs/limitations.md`](docs/limitations.md) | Study limits, denominator correction, and requirements for generalization |
| [`LICENSE`](LICENSE) | Creative Commons Attribution 4.0 license |

## Sanitization

The public artifact excludes project identifiers, task order numbers, contract numbers, contractor names, government personnel names, installation names, country names, unit designations, dollar values, identifying project dates, and the exact number of task orders in the portfolio. Generic role names and the standard population description replace operational identifiers.

No controlled unclassified information is included. The repository does not reproduce government forms, source documents, reviewer comments, correspondence, or operational records. Findings appear only as sanitized aggregate measurements or generalized requirement relationships.

## License

This repository contains documentation and a research artifact rather than a software distribution, so its contents use the Creative Commons Attribution 4.0 license. Any executable code added later will carry a separate MIT license within its own subdirectory.

## Author

Jason V. Holmes  
ORCID: [0009-0007-2898-8478](https://orcid.org/0009-0007-2898-8478)  
GitHub: [jvholmes87](https://github.com/jvholmes87)

## Disclaimer

This is independent work. It is not an official project of any employer, university, the U.S. Air Force, or the U.S. Department of Defense. The repository does not represent government approval, institutional endorsement, or an official compliance system.
