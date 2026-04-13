# Detailed Feasibility: Local AI Server for Development and Platform Engineering

## 1. Problem Statement

Evaluate whether self-hosting AI inference is better than purchasing individual SaaS AI subscriptions for engineering teams of 1, 10, 50, and 100 developers.

The target workloads include:

- Software development and coding assistance
- Code understanding and refactoring support
- DevOps and platform engineering tasks (IaC, CI/CD, cloud architecture support)

## 2. Assumptions and Constraints

These assumptions should be customized with your internal numbers.

- Engineers are active AI users during work hours.
- A subset of users are heavy users and may hit token/usage limits in some plans.
- Management needs an option that is economically sustainable and operationally reliable.
- Quality must be comparable to current premium assistants.

## 3. Feasibility by Team Size (Initial Ranges)

All costs below are rough order-of-magnitude monthly ranges and should be replaced with vendor quotes.

| Team Size | Preferred Mode | Estimated Monthly Cost (All-in) | Notes |
|---|---|---:|---|
| 1 | SaaS only | $20-$200 | Local server almost never justified financially. |
| 10 | SaaS first / micro-local pilot | $300-$2,500 (SaaS), $2,000-$8,000 (local pilot) | Pilot only if data-control or experimentation is required. |
| 50 | Hybrid | $1,500-$12,000 (SaaS mix), $8,000-$35,000 (hybrid local infra + SaaS) | Hybrid can control sensitive workloads and reduce some API usage. |
| 100 | Hybrid with local expansion candidate | $3,000-$25,000 (SaaS mix), $20,000-$120,000 (serious local setup) | Local-first is feasible only with high utilization and strong ops maturity. |

Interpretation:

- For small teams, SaaS usually wins on cost and quality.
- For large teams, local can become strategic, but only if utilization is high and operations are mature.

## 4. Model/Assistant Suitability for Engineering Work

Use a benchmark harness with real internal tasks before final selection.

### 4.1 Workload Fit Matrix (Initial)

| Work Type | Desired Strength | Usually Best Option |
|---|---|---|
| IDE inline coding help | best-in-class quality + latency | Premium SaaS copilots |
| Multi-file refactoring | long context + reliability | Premium SaaS or top-tier hosted APIs |
| Internal codebase Q&A (sensitive) | private retrieval + policy controls | Local/self-hosted or private VPC-hosted models |
| IaC generation/review (Bicep/Terraform) | instruction following + domain quality | Hybrid: premium model for critical changes, local for drafts |
| CI/CD and platform runbook generation | consistency + compliance templates | Hybrid |

### 4.2 Candidate Model Strategy (not final model picks)

- Tier A (quality-first): Premium frontier models via SaaS/API.
- Tier B (cost/privacy-balanced): Strong open-weight coding instruct models on local GPUs.
- Tier C (utility/local automation): Smaller local models for batch and helper workflows.

## 5. Hardware and Capacity Direction

### 5.1 Sizing Drivers

- Concurrent users at peak (not total team size)
- Tokens per second required at peak
- Average context window per request
- Mix of simple vs complex coding tasks
- SLA targets (latency, uptime)

### 5.2 Practical Sizing Heuristic (for planning)

1. Estimate peak concurrent active users as 15%-35% of team.
2. Estimate requests/user/hour and average tokens/request.
3. Convert to required sustained tokens/sec.
4. Add 30%-50% headroom for spikes.

## 6. Risks

- Quality gap between local open models and premium SaaS for difficult tasks
- Hidden costs: MLOps, observability, security controls, on-call operations
- Underutilized expensive GPU capacity
- Rapid model churn causing frequent re-evaluation

## 7. Recommended Delivery Approach

1. Start with baseline SaaS metrics (cost, usage, satisfaction).
2. Run a controlled local pilot for high-value/sensitive workloads.
3. Measure side-by-side quality and cost per successful outcome.
4. Decide between SaaS-first, hybrid, or local expansion.

## 8. ASCII Pilot Timeline

```text
Week 1-2: Baseline
  - Collect SaaS usage, quality, pain points

Week 3-4: Pilot Build
  - Deploy gateway + 1 local model stack
  - Integrate with selected workflows

Week 5-6: A/B Evaluation
  - Compare quality, latency, and cost
  - Evaluate team acceptance

Week 7-8: Decision
  - Management review
  - Approve next operating model
```
