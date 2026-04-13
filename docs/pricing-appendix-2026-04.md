# Pricing Appendix (Snapshot): 2026-04-13

This appendix provides a practical pricing snapshot for management discussion.

Important notes:

- Prices are public list-price signals captured on 2026-04-13.
- Vendor pricing changes frequently.
- Currency and region can change displayed prices.
- Use this as planning input, then replace with contracted quotes.

## 1. Public Pricing Snapshot

### 1.1 Per-user SaaS plans (developer-facing)

| Provider | Plan | Public Price Signal | Normalized Reference |
|---|---|---|---|
| GitHub Copilot | Pro | $10/user/month | $10/user/month |
| GitHub Copilot | Pro+ | $39/user/month | $39/user/month |
| OpenAI ChatGPT | Plus | NOK 249/month (localized page) | ~$23/user/month |
| OpenAI ChatGPT | Pro | NOK 1,190/month (localized page) | ~$111/user/month |
| Anthropic Claude | Pro | $20/month (or $17 annual equivalent) | $20/user/month |
| Anthropic Claude | Max | From $100/month | $100/user/month |
| Anthropic Claude Team | Standard seat | $25/user/month (or $20 annual equivalent) | $25/user/month |
| Google AI | Pro | 259 kr/month (localized page) | ~region dependent (roughly $30-$40/user/month in many markets) |

Normalization assumptions used above:

- For localized NOK and kr values, rough conversion bands are used for management-level planning.
- Final business case should use your billing region and negotiated enterprise prices.

### 1.2 API pricing signal (DeepSeek example)

DeepSeek API page (DeepSeek-V3.2 family) shows:

- Input (cache hit): $0.028 / 1M tokens
- Input (cache miss): $0.28 / 1M tokens
- Output: $0.42 / 1M tokens

This is materially lower than many premium frontier offerings, but quality and reliability must be benchmarked on your code and platform engineering tasks.

### 1.3 Usage Volume and Token Availability Signals

Pricing alone is not enough for planning. For engineering teams, usable capacity is determined by request caps, model-tier quotas, and fair-use guardrails.

| Provider | Plan/Route | Public volume signal | Planning interpretation |
|---|---|---|---|
| GitHub Copilot | Free | 50 chat/agent requests per month, 2,000 completions per month | Too limited for full-time engineering workflows |
| GitHub Copilot | Pro | 300 premium requests; unlimited GPT-5 mini chats/agent and unlimited inline suggestions | Good baseline, but heavy premium-model users can still exhaust premium quota |
| GitHub Copilot | Pro+ | 5x premium requests vs Pro | Better for heavy users; still governed by provider policies |
| ChatGPT | Plus/Pro/Business | "Unlimited" usage language with abuse/fair-use guardrails | Treat as high-capacity, not truly infinite; monitor throttling/rate events |
| Claude | Pro/Max/Team | Usage limits apply and vary by plan; higher tiers increase limits | Capacity is tiered; validate heavy-user experience in pilot |
| Google AI | Plus/Pro/Ultra | "More/Higher/Highest" model access and limits by plan | Capacity is relative by plan; use pilot measurements for concurrency reality |
| DeepSeek API | Token-metered API pricing | Input/output billed per token with explicit rates | Highly controllable cost-volume model; depends on quality and ops setup |

Important practical note:

- Most seat plans do not publish deterministic token-per-month guarantees.
- For management planning, track effective capacity as: successful requests at acceptable latency and quality per developer per day.

### 1.4 Capacity KPI Table (Monthly Management View)

Use this compact table in monthly reporting to compare practical capacity across plans/routes.

| KPI | Definition | Target/Threshold | Why it matters |
|---|---|---|---|
| Effective requests/day/developer | Successful AI-assisted requests at acceptable quality and latency | Track trend by route; improve month-over-month | Measures real usable capacity, not marketing limits |
| Exhaustion rate | % of active users reporting hard quota/limit blocks in month | <=10% preferred, >=20% indicates pressure | Detects where plan limits hurt delivery |
| Throttle/rate-limit event rate | # of throttle/rate-limit events per 1,000 requests | <=15 events per 1,000 requests | Indicates practical service headroom |
| Premium-quota depletion rate | % users consuming premium-tier allocation before month end | <=15% preferred, >=30% indicates under-provisioning | Signals need for rerouting or plan adjustment |
| p95 interactive latency | 95th percentile response time for interactive workflows | <=8-12 seconds | Protects developer experience |
| Quality acceptance rate | % AI outputs accepted with minor/no edits | Local route within 85%-95% of SaaS baseline | Ensures capacity gains do not reduce quality |
| Cost per successful task | Total monthly spend divided by successful AI-assisted engineering outcomes | Downward trend month-over-month | Connects capacity to financial outcome |

Suggested roll-up formula:

```text
EffectiveCapacityIndex =
  (AcceptedSuccessfulRequests / ActiveDevelopers / WorkDays)
  * (1 - ThrottleEventRate)
  * (1 - ExhaustionRate)
```

Interpretation:

- Higher index means better practical capacity for daily engineering work.
- Use index trend direction together with cost-per-successful-task trend for management decisions.

## 2. Local/Private Inference Cost Signals

### 2.1 GPU rental reference (cloud GPU, as proxy)

Using public RunPod rates:

- L40S: $0.86/hr => ~$628 per GPU-month
- A100 80GB SXM: $1.49/hr => ~$1,088 per GPU-month
- H100 80GB SXM: $2.99/hr => ~$2,183 per GPU-month

Calculation:

```text
GPU_monthly = hourly_rate * 730
```

These are single-GPU raw compute proxies. Real production cost includes:

- orchestration/gateway
- storage/networking
- observability/security
- platform operations staffing
- high-availability overhead

## 3. Side-by-Side Cost Table (1 / 10 / 50 / 100 developers)

The table below compares representative monthly spend envelopes.

| Team Size | SaaS Baseline (Copilot Pro only) | SaaS Premium Mix (Copilot Pro + one premium chat plan average) | Local/Hybrid Starter Envelope | Typical Recommendation |
|---:|---:|---:|---:|---|
| 1 | ~$10 | ~$30-$130 | ~$800-$4,000 | SaaS only |
| 10 | ~$100 | ~$300-$1,300 | ~$2,000-$8,000 | SaaS first, optional pilot |
| 50 | ~$500 | ~$1,500-$6,500 | ~$8,000-$35,000 | Hybrid |
| 100 | ~$1,000 | ~$3,000-$13,000 | ~$20,000-$120,000 | Hybrid, scale local selectively |

How to read:

- `SaaS Baseline` is intentionally conservative and usually underestimates real enterprise stack spend.
- `SaaS Premium Mix` assumes each developer has Copilot plus one higher-tier chat/tool seat mix.
- `Local/Hybrid` includes infra + ops + reliability overhead (not just GPU hours).

## 4. Break-Even Lens

Use cost per successful engineering outcome, not token price alone.

```text
BreakEven if:
( Local_TCO_monthly / SuccessfulTasks_monthly_local )
<=
( SaaS_Spend_monthly / SuccessfulTasks_monthly_saas )
```

Where successful task is a completed engineering outcome (for example merged PR, validated IaC change, incident runbook delivered) with acceptable quality.

## 5. Hardware Growth Pattern by Team Size

```text
1 dev:
  SaaS only

10 devs:
  SaaS + optional 1-node local pilot

50 devs:
  Shared gateway + 2-4 GPU nodes for selected workloads

100 devs:
  HA gateway + model routing + 4-10 nodes + strong ops controls
```

## 6. Practical Conclusion for ~100 Developers

Based on public pricing signals and operational realities:

- Full local-first can be feasible technically, but often not cheapest in early phases.
- Pure SaaS can hit usage limits/token frustrations for heavy users and can raise data-governance concerns.
- Hybrid is usually the best near-term operating model:
  - keep premium SaaS for hardest coding/refactoring tasks
  - route sensitive/internal/batch workloads to local models
  - expand local only when measured ROI is proven

## 7. Source Pages Captured

- GitHub Copilot plans: https://github.com/features/copilot/plans
- GitHub pricing: https://github.com/pricing
- ChatGPT pricing: https://chatgpt.com/pricing
- Claude pricing: https://claude.com/pricing
- Claude Team pricing: https://claude.com/pricing/team
- Google AI plans: https://one.google.com/about/ai-premium/
- DeepSeek pricing: https://api-docs.deepseek.com/quick_start/pricing
- RunPod GPU pricing: https://www.runpod.io/gpu-instance/pricing

## 8. Related Analysis

- [Heavy-User Budget Simulation](heavy-user-budget-simulation.md)
- [CPU-Only Local AI Server Guide](cpu-only-local-ai-server-guide.md)
