# Federal Submittal Compliance Model

> **Research status (11 September 2026):** Deployed architecture with preliminary, bounded observations from one organization. The current work is suitable for a conference-paper-scale study. Research novelty has **not** been established; a focused literature review now precedes further taxonomy/codebook development or any doctoral-scope claim.

## Purpose

This repository documents the sanitized architecture of a deployed compliance instrument used by a small subcontractor performing federal construction task orders at an overseas installation. The instrument tracks government-facing obligations across concurrent work without publishing operational records.

The research framing is requirements engineering, obligation traceability, lifecycle-state control, and acquisition-interface latency in federal construction compliance. Small organizations may carry obligation loads that exceed the support provided by their tools. This instrument enforces obligation rules in the data model so that lifecycle, evidence, applicability, and deadline controls remain consistent across records.

## Instrument scope

The deployed instrument contains four connected controls:

- An approximately 60-gate work breakdown structure organized into six phase bands
- An 11-state lifecycle model covering preparation, prime-contractor routing, government adjudication, closure, and expiry
- A deadline engine that derives obligation dates from award and other anchor events
- An alert layer that surfaces approaching deadlines, breached deadlines, stalled reviews, and expiring approvals

The current baseline contains 61 gates. Instantiated projects contain 60 to 72 rows because conditional and project-specific gates vary by scope.

## Measured findings

### First-pass submittal approval

At the 11 September 2026 research snapshot, first-pass submittal approval was:

- **69 percent by line item:** 20 first-pass approvals among 29 dispositioned line items
- **47 percent by package:** 8 first-pass approvals among 17 packages

These are different units of analysis and must be reported separately. Neither value should be substituted for the dashboard's **85 percent current-state gate approval share**, which measures the present distribution of gate states rather than first-pass yield.

A 3 September 2026 gate-row snapshot produced **43 percent (3 of 7)** under an earlier gate-row adjudication definition. That figure is retained only as a dated measurement-history observation. An earlier **17 percent** figure is superseded and retained only as an audit-trail example of an invalid denominator. The 17, 43, 69, 47, and 85 percent figures must not be averaged or described as a single trend because they use different definitions, units, or populations.

### Government-review latency

At the 11 September 2026 snapshot, **11 tracked items had been pending more than 14 days, and the oldest had been pending 66 days**, against a contractual one-work-week response obligation in the studied context. These observations measure elapsed waiting time in the tracked portfolio. They do not establish a population-wide government review rate or prove why a particular delay occurred.

### Structurally unsatisfiable timing

The instrument identified a requirement pattern in which certain submittals were due 30 calendar days after contract award, while required installation-access processing for non-U.S. personnel could exceed 30 days. Some affected submittals required site measurements that could occur only after access was granted. When the dependent access event occurred after the contractual due date, the required sequence was arithmetically infeasible without a documented change to sequence, scope, access, or contractual timing.

This is an observed requirements-conflict pattern in the stated population. It does not establish prevalence or effect across federal construction generally.

## Research gate

The next research step is **not** to expand the coding taxonomy. The next step is a focused literature review to determine whether the proposed gap is genuinely unexplored and how existing construction-management and engineering-management research already treats rework, submittal/RFI latency, defect causation, requirements volatility, and small-firm compliance burden.

See [`docs/research-roadmap.md`](docs/research-roadmap.md) for the literature-first sequence and doctoral-scope decision criteria.

## Repository structure

| File | Contents |
|---|---|
| [`docs/lifecycle-model.md`](docs/lifecycle-model.md) | Deployed states, transitions, ownership, guards, and illegal transitions |
| [`docs/wbs-structure.md`](docs/wbs-structure.md) | Six phase bands, gate counts, numbering, satisfaction, and metric typing |
| [`docs/deadline-engine.md`](docs/deadline-engine.md) | Anchor events, date computation, cascades, review aging, and the timing-conflict example |
| [`docs/data-model.md`](docs/data-model.md) | Conceptual entities, relationships, and database invariants |
| [`docs/limitations.md`](docs/limitations.md) | Study limits, metric-definition controls, literature-gap status, and requirements for generalization |
| [`docs/research-roadmap.md`](docs/research-roadmap.md) | Literature-first research sequence and candidate paths to doctoral scope |
| [`CITATION.cff`](CITATION.cff) | Citation metadata |
| [`CHANGELOG.md`](CHANGELOG.md) | Version history |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Public contribution rules |
| [`SECURITY.md`](SECURITY.md) | Sensitive-information reporting guidance |
| [`LICENSE`](LICENSE) | Creative Commons Attribution 4.0 license |

## Data availability

The underlying operational dataset is **not public**. This repository publishes only sanitized architecture, definitions, generalized requirement relationships, and bounded aggregate observations. It does not publish raw project records, source correspondence, reviewer comments, contract documents, identifying dates, or personnel data.

## Sanitization

The public artifact excludes project identifiers, task order numbers, contract numbers, contractor names, government personnel names, installation names, country names, unit designations, dollar values, identifying project dates, and the exact number of task orders in the portfolio. Generic role names and the standard population description replace operational identifiers.

No controlled unclassified information is intentionally included. The repository does not reproduce government forms, source documents, reviewer comments, correspondence, or operational records. Findings appear only as sanitized aggregate measurements or generalized requirement relationships.

## License

This repository contains documentation and a research artifact rather than a software distribution, so its contents use the Creative Commons Attribution 4.0 license. Any executable code added later will carry a separate MIT license within its own subdirectory.

## Author

Jason V. Holmes  
ORCID: [0009-0007-2898-8478](https://orcid.org/0009-0007-2898-8478)  
GitHub: [jvholmes87](https://github.com/jvholmes87)

## Disclaimer

This is independent work. It is not an official project of any employer, university, the U.S. Air Force, or the U.S. Department of Defense. The repository does not represent government approval, institutional endorsement, or an official compliance system.
