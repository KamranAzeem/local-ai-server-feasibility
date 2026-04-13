# CPU-Only Local AI Server Guide (Single User)

This guide answers one question: what is good enough for a single heavy user doing IT development and platform engineering, without any GPU.

## 1. Practical Recommendation

For your use case, the best CPU-only balance is:

- CPU: 16 cores / 32 threads (modern high-clock desktop/server CPU)
- RAM: 128 GB DDR5
- Storage: 2 TB NVMe SSD
- OS: Linux preferred for best inference stack stability

Why this is the best balance:

- 64 GB RAM can work for smaller models, but 128 GB gives safer headroom for larger context windows and smoother multitasking.
- 16 cores is where CPU-only generation becomes practical for daily development assistance.

## 2. Hardware Tiers

| Tier | CPU | RAM | Expected use |
|---|---|---|---|
| Minimum usable | 8-12 cores | 64 GB | 7B-class models, short prompts, basic coding help |
| Recommended | 16 cores | 128 GB | 7B-14B coding models, platform engineering workflows |
| Premium CPU-only | 24-32 cores | 128-192 GB | 14B-32B with better responsiveness, still slower than GPU |

## 3. Model Recommendations for Your Tasks

For IT development and platform engineering, prioritize code-tuned instruct models.

### Best starting model (CPU-only)

- Qwen2.5-Coder 14B Instruct (quantized, Q4_K_M or similar)

Why:

- Better technical reasoning than many smaller models
- Good support for coding, IaC drafting, scripts, and troubleshooting
- Still feasible on CPU-only with 128 GB RAM

### Fast fallback model

- Qwen2.5-Coder 7B Instruct (quantized)

Why:

- Much faster responses on CPU
- Good for iterative editing, YAML/Terraform/Bicep boilerplate, shell scripting

### Larger option (only if you accept slower speed)

- 32B-class instruct model, quantized

Why:

- Higher quality on complex tasks
- CPU-only latency can become frustrating for interactive use

## 4. Estimated Token Generation Rate (CPU-only)

These are practical ranges for generation speed (decode speed), not peak benchmark claims.

Assuming modern 16-core CPU, optimized runtime (for example llama.cpp/Ollama), and Q4 quantization:

| Model size | Estimated generation rate | Typical user experience |
|---|---:|---|
| 7B | 12-25 tokens/sec | Comfortable for chat + coding iteration |
| 14B | 6-12 tokens/sec | Usable for serious work, moderate waiting |
| 32B | 2-5 tokens/sec | Better quality, but often too slow for all-day interactive use |

Prompt processing (prefill) can be higher than generation rate, but long contexts still increase end-to-end latency.

## 5. RAM Guidance by Model Class (Quantized)

| Model class | Approx model footprint | Recommended system RAM |
|---|---:|---:|
| 7B Q4 | ~4-6 GB | 64 GB |
| 14B Q4 | ~8-12 GB | 128 GB |
| 32B Q4 | ~18-24 GB | 128-192 GB |

Notes:

- Real memory usage also depends on context length and runtime overhead.
- If you run IDE, browser, containers, and local databases simultaneously, extra RAM headroom matters.

## 6. What is Good Enough for You

Given your profile (single heavy user, 8h/day, platform engineering):

1. Start with 16-core CPU + 128 GB RAM.
2. Run 14B quantized as default quality model.
3. Keep 7B quantized as fast model for quick iterative tasks.
4. Use routing rule:
   - 7B for drafting, small edits, repetitive infra snippets
   - 14B for architecture reasoning, incident analysis, complex refactors

## 7. Decision Threshold to Upgrade Beyond CPU-only

Move to GPU (or hybrid local+SaaS) if either happens for 2 consecutive months:

- Median interactive response time feels too slow for daily use
- You repeatedly avoid using local model for complex tasks due to latency
- You need sustained >10-15 tokens/sec at 14B+ quality

## 8. Suggested Runtime Stack

- Ollama (simple operations) or llama.cpp server mode (more tuning control)
- Keep quantized GGUF models
- Track monthly KPIs:
  - tokens/sec
  - latency p95
  - accepted outputs/day
  - cost per successful task

## 9. Bottom Line

Without GPU, a single-user server is feasible and useful.

The most practical CPU-only setup for your workload is:

- 16 cores
- 128 GB RAM
- 14B quantized coding model as primary
- Expected generation speed: about 6-12 tokens/sec

## 10. Ready-to-Buy Hardware Configurations

For concrete component specifications and exact pricing, see [CPU-Only Hardware Builds](cpu-only-hardware-builds.md).

That document provides:

- **Budget tier** (~$3.5K–$5K): Entry-level testing and learning
- **Balanced tier** (~$8K–$12K): Recommended for your daily platform engineering workflow
- **Premium tier** (~$15K–$25K): For high-concurrency or multi-user setups

Each build includes exact component specs, vendor recommendations, expected token/sec performance, and upgrade paths to GPU.
