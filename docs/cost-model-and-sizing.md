# Cost Model and Hardware Sizing

Companion pricing snapshot:

- [Pricing Appendix (2026-04-13)](pricing-appendix-2026-04.md)

## 1. Cost Components

Total Monthly Cost = Infrastructure + Energy + Operations + Software + Risk Buffer

```text
TCO_monthly = C_hw_amortized + C_power_cooling + C_staff_ops + C_software + C_network_storage + C_risk
```

Where:

- `C_hw_amortized`: GPU servers and supporting hardware amortized over 36 months
- `C_power_cooling`: electricity and cooling
- `C_staff_ops`: platform/SRE/MLOps staffing cost share
- `C_software`: observability, security tooling, orchestration, enterprise support
- `C_network_storage`: artifact/model storage and internal traffic overhead
- `C_risk`: downtime/rework contingency

## 2. Team Scenario Worksheet

Replace all values with your local rates and quotes.

| Scenario | Team | Peak Concurrent Users (15%-35%) | Typical Local Setup | Indicative Monthly TCO Range |
|---|---:|---:|---|---:|
| S1 | 1 | 1 | No local infra | $0 local / SaaS only |
| S2 | 10 | 2-4 | 1 small GPU node pilot | $2,000-$8,000 |
| S3 | 50 | 8-18 | 2-4 medium GPU nodes + gateway | $8,000-$35,000 |
| S4 | 100 | 15-35 | 4-10 medium/large GPU nodes + HA stack | $20,000-$120,000 |

## 3. Hardware Evolution by Team Size

```text
Team 1-10
  - Prefer SaaS
  - Optional: 1 pilot node for experiments

Team 50
  - Add API gateway and quotas
  - Build small model farm for sensitive/internal workloads

Team 100
  - HA gateway + model routing
  - Multi-node GPU pool
  - Strong observability, RBAC, audit, backup plans
```

## 4. Break-Even View

```text
Break-even when:
(Local monthly TCO / Monthly successful AI tasks) <= (SaaS monthly spend / Monthly successful AI tasks)
```

Important:

- Do not compare raw token price only.
- Compare cost per successful engineering outcome.

## 5. SaaS Benchmark Reference Bucket (to customize)

Use this template with your real contracted prices:

| Tool Plan | Unit Price/User/Month | Users | Monthly Cost |
|---|---:|---:|---:|
| GitHub Copilot plan | TBD | TBD | TBD |
| ChatGPT plan | TBD | TBD | TBD |
| Claude plan | TBD | TBD | TBD |
| Google Gemini plan | TBD | TBD | TBD |
| Other provider plan | TBD | TBD | TBD |

## 6. Minimum Pilot Metrics to Collect

- Acceptance rate of AI suggestions in code reviews
- Time-to-first-working-solution for common tasks
- Cost per successful ticket/task
- Peak-time latency and queue depth
- Failure/retry rates
- Developer satisfaction

## 7. Initial Recommendation

For a company with around 100 developers:

- Start hybrid, not local-only.
- Keep premium SaaS available for high-complexity tasks.
- Route sensitive and batch/internal tasks to local models.
- Re-evaluate quarterly with measured quality and TCO.
