# Management Decision Dashboard

This page is the decision cockpit for evaluating AI operating models for software and platform engineering teams.

## 1. Recommended Baseline Stack (100 Developers)

Recommendation: Balanced hybrid baseline.

```text
Primary coding copilot layer:
  - GitHub Copilot Pro for all developers

Premium reasoning layer:
  - Controlled pool of premium seats or usage credits
  - Assigned to heavy/critical workflows

Local/private inference layer:
  - Start with 2-4 GPU nodes
  - Route sensitive internal context and batch workloads here

Control plane:
  - AI gateway for routing, quotas, telemetry, and policy
```

### Why this baseline

- Preserves high coding quality for daily delivery work.
- Reduces risk from token exhaustion by introducing local overflow capacity.
- Maintains a practical path to privacy-focused workloads without overcommitting early.

## 2. Budget Scenarios (Monthly)

All numbers are planning ranges and should be replaced with contracted quotes.

| Scenario | Team Size | SaaS Spend Range | Local/Infra Spend Range | Total Monthly Range | Use Case |
|---|---:|---:|---:|---:|---|
| Conservative | 100 | $2,000-$5,000 | $0-$5,000 | $2,000-$10,000 | SaaS-first, minimal local pilot |
| Balanced | 100 | $4,000-$10,000 | $10,000-$30,000 | $14,000-$40,000 | Hybrid with controlled local capacity |
| Aggressive | 100 | $6,000-$15,000 | $35,000-$100,000 | $41,000-$115,000 | Large local footprint, enterprise controls |

Interpretation:

- Conservative minimizes fixed cost but may not fully solve heavy-user exhaustion.
- Balanced targets operational realism and is typically the most defendable management option.
- Aggressive only makes sense if governance, utilization, and ROI are already proven.

## 3. 90-Day Pilot Plan

### Phase A (Days 1-30): Baseline and Setup

- Confirm baseline workflows and productivity metrics on current SaaS tools.
- Deploy AI gateway with audit logs, routing policies, and quota controls.
- Stand up initial local inference capacity.

Deliverables:

- Approved pilot scope and participating teams
- Baseline report for cost, latency, and acceptance rates
- Security and compliance checklist complete

### Phase B (Days 31-60): Controlled A/B Operation

- Run side-by-side task routing:
  - hard tasks to premium SaaS
  - sensitive and batch tasks to local
- Collect quality outcomes on real engineering work:
  - code tasks
  - IaC tasks
  - incident/runbook tasks

Deliverables:

- Weekly scorecards
- Cost per successful task by route
- User feedback and adoption trends

### Phase C (Days 61-90): Decision and Scale Plan

- Compare outcomes vs thresholds.
- Produce operating model recommendation for next 6-12 months.
- Propose budget and capacity plan for approved model.

Deliverables:

- Management decision memo
- Final TCO model and variance analysis
- Implementation roadmap for next quarter

## 4. Go/No-Go Thresholds

Proceed to scale only if all critical thresholds pass.

| Metric | Threshold | Decision Rule |
|---|---|---|
| Suggestion acceptance rate | Local route within 85%-95% of SaaS baseline | Below threshold blocks expansion |
| Time-to-first-working-solution | Local route within 10%-20% of SaaS baseline | Material slowdown blocks expansion |
| Cost per successful task | Hybrid improves by >=10% over SaaS-only baseline | No improvement limits local rollout |
| Peak latency p95 | <=8-12 seconds for interactive workflows | Above threshold requires tuning |
| Reliability | >=99.5% pilot availability for core path | Lower availability blocks wider use |
| Security/compliance | No critical unresolved findings | Any critical finding is stop condition |

## 5. Decision Matrix

| Condition | Preferred Operating Model |
|---|---|
| Highest coding quality is top priority, modest governance needs | SaaS-first |
| Mixed priorities (quality + privacy + cost control) | Hybrid |
| Strong governance constraints, high sustained utilization, mature ops | Local-first candidate |

## 6. Immediate Next Actions

1. Finalize which of the three budget scenarios management wants to evaluate first.
2. Approve pilot participants (for example 15-25 developers across product and platform teams).
3. Freeze pilot scorecard metrics before execution starts.
4. Begin Day 1 baseline measurements.

## 7. Related Documents

- [Management Brief](management-brief.md)
- [Pricing Appendix (2026-04-13)](pricing-appendix-2026-04.md)
- [Cost Model and Sizing](cost-model-and-sizing.md)
- [Detailed Feasibility](local-ai-server-feasibility.md)
- [Conservative-to-Balanced Trigger Scorecard](conservative-to-balanced-trigger-scorecard.md)
