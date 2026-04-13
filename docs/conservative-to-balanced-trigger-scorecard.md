# Conservative-to-Balanced Trigger Scorecard

This scorecard defines when to move from the Conservative model (SaaS-first, minimal local pilot) to the Balanced model (hybrid with controlled local capacity).

## 1. Purpose

Use this document as a monthly governance gate for management.

Decision outcomes:

- Stay Conservative
- Expand to Balanced pilot
- Execute Balanced rollout

## 2. Trigger Logic

A move from Conservative to Balanced is approved only if:

1. At least 4 of 6 core metrics pass for 2 consecutive monthly reviews.
2. No hard-stop condition is present.

## 3. Core Metrics and Thresholds

| Metric | Threshold (Pass) | Why it matters |
|---|---|---|
| Heavy-user exhaustion rate | >=20% of active developers report recurring usage-limit friction | Indicates SaaS-only friction is material |
| Productivity impact from limits | >=5% measurable delay on target tasks due to quota/rate constraints | Shows real delivery impact |
| Cost pressure signal | Forecasted SaaS spend growth >=15% quarter-over-quarter | Justifies evaluating alternative capacity |
| Local quality parity | Local pilot quality score >=85% of SaaS baseline on selected tasks | Prevents low-quality expansion |
| Local latency p95 | <=12 seconds on interactive pilot tasks | Keeps workflows practical |
| Platform readiness | Gateway, auth, logs, and runbooks are complete and tested | Ensures operational safety |

## 4. Hard-Stop Conditions (No Expansion)

Any one of these blocks expansion:

- Critical unresolved security/compliance finding
- Local pilot availability <99.0% for core pilot period
- Local quality parity <75% of SaaS baseline
- No owner assigned for platform operations

## 5. Monthly Review Template

## Review Metadata

- Review month:
- Reviewer(s):
- Team size (active developers):
- Pilot participants:
- Decision recommendation: Stay Conservative / Expand Balanced Pilot / Balanced Rollout

## Metric Results

| Metric | Actual | Threshold | Pass/Fail | Notes |
|---|---:|---:|---|---|
| Heavy-user exhaustion rate | | >=20% | | |
| Productivity impact from limits | | >=5% | | |
| SaaS spend growth (QoQ) | | >=15% | | |
| Local quality parity | | >=85% | | |
| Local latency p95 | | <=12s | | |
| Platform readiness complete | | Yes | | |

## Hard-Stop Check

- Security/compliance critical finding: Yes/No
- Availability below 99.0%: Yes/No
- Local quality below 75%: Yes/No
- Platform owner missing: Yes/No

## Final Decision

- Outcome:
- Rationale:
- Actions before next review:
- Owner:
- Target date:

## 6. Recommended Rollout Path if Triggered

```text
Step 1: Expand pilot from small group to 15-25 developers
Step 2: Keep premium SaaS for highest-complexity workflows
Step 3: Route sensitive and batch workflows to local layer
Step 4: Re-measure for 2 more months before broad rollout
```

## 7. Reporting to Management

Minimum monthly dashboard fields:

- Cost per successful task (SaaS route vs local route)
- Suggestion acceptance quality score
- p95 latency
- Availability
- Security/compliance status
- Recommendation and confidence level
