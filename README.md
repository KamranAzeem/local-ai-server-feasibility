# Local AI Server Feasibility

This repository evaluates whether running AI locally for software and platform engineering is a better fit than per-user SaaS subscriptions.

The information is current as per April 2026.

## Goal

Assess technical and financial feasibility for team sizes:

- 1 developer
- 10 developers
- 50 developers
- 100 developers

Key concerns include:

- Total cost of ownership (TCO)
- Hardware sizing and scaling
- Model quality for coding and cloud/platform engineering work
- Token exhaustion and usage limits in SaaS plans
- Management-ready decision guidance

## Documentation

- [Documentation Index](docs/README.md)
- [Management Brief](docs/management-brief.md)
- [Management Decision Dashboard](docs/management-decision-dashboard.md)
- [Executive Scenario Summaries](docs/executive-scenario-summaries.md)
- [Conservative-to-Balanced Trigger Scorecard](docs/conservative-to-balanced-trigger-scorecard.md)
- [Heavy-User Budget Simulation](docs/heavy-user-budget-simulation.md)
- [CPU-Only Local AI Server Guide](docs/cpu-only-local-ai-server-guide.md)
- [CPU-Only Hardware Builds](docs/cpu-only-hardware-builds.md)
- [Detailed Feasibility](docs/local-ai-server-feasibility.md)
- [Cost Model and Sizing](docs/cost-model-and-sizing.md)
- [Pricing Appendix (2026-04-13)](docs/pricing-appendix-2026-04.md)

## Current Direction

The current baseline recommendation is a hybrid approach for larger teams (especially around 100 developers):

- Keep premium SaaS assistants for highest-complexity tasks.
- Add local inference for sensitive/internal and batch-heavy workloads.
- Use measured pilot outcomes before moving to local-first.

## Status

This repository is in discovery and decision-support mode. Documents will evolve as pricing data, benchmark results, and pilot evidence are added.
