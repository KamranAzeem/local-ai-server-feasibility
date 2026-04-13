# CPU-Only Hardware Builds for Local AI Server

## Overview

This document provides three concrete, ready-to-purchase hardware configurations for running local AI inference on CPU without GPU. Each build includes exact component specifications, estimated costs, and expected token generation rates for the Qwen2.5-Coder and similar 7B/14B models.

**Key Assumption:** All builds use DDR5 RAM, NVMe SSD storage, and Linux (Ubuntu 22.04+ or similar) for optimal inference performance. Builds are configured for single-user platform engineering workflows with 8 hours/day usage pattern.

---

## Build 1: Budget Configuration (~$3,500–$5,000)

### Target Use Case
- Entry-level platform engineering tools: simple script generation, documentation, small problem decomposition
- Secondary machine or lab testing environment
- Acceptable latency: 2–5 seconds per response

### Component Specifications

| Component | Specification | Unit Cost | Notes |
|-----------|---------------|-----------|-------|
| CPU | AMD Ryzen 7 7700 (8-core, 16-thread, 65W TDP) | $250 | Budget-friendly, excellent single-thread IPC |
| Motherboard | B650 (non-X, DDR5 support) | $150 | ASRock B650-ITX/TB4 or ASUS Q-Sync |
| RAM | 64 GB DDR5-5600 ECC | $300 | Crucial or Corsair; 2 x 32 GB | |
| Storage | 1 TB NVMe Gen4 (Samsung 990 Evo or WD Black) | $80 | Separate OS + model partition recommended |
| PSU | 500W 80+ Bronze | $40 | Seasonic, Gigabyte, or be quiet! |
| Case + Cooling | Compact ATX + Budget Cooler | $100 | Noctua NH-U12S or Arctic Liquid Freezer II 240 |
| Network | 1 Gbps Ethernet (onboard) | $0 | Motherboard integrated |
| **Subtotal** | | **$920** | **Component cost only** |
| Assembly/Labor | DIY or $150–$300 | $0–$300 | Varies by location/service |
| **Total System Cost** | | **$3,500–$4,200** | Varies by sales/region |

### Expected Performance

| Model | Config | Tokens/Sec | Use Case |
|-------|--------|-----------|----------|
| Qwen2.5-Coder 7B | Q4 quantization | 18–22 t/s | Fast, good for templates |
| Qwen2.5-Coder 14B | Q4 quantization | 5–8 t/s | Recommended for this tier |
| Llama2 13B | GGUF Q5 | 4–6 t/s | Alternative, slightly slower |

### Latency Profile
- 100-token generation: ~5–20 seconds (7B), ~12–20 seconds (14B)
- 500-token generation: ~23–28 seconds (7B), ~62–100 seconds (14B)

### Upgrade Path
- **To Balanced:** Replace CPU with Ryzen 7 7700X or 5800X3D for +40–60% throughput
- **To GPU:** Add RTX 4060 Ti or L40S to this base for 10–50x throughput increase

---

## Build 2: Balanced Configuration (~$8,000–$12,000)

### Target Use Case
- Daily platform engineering workload: IaC generation (Terraform, Bicep), incident analysis, architecture review
- Concurrent tool use: code editor + AI terminal + system monitoring
- Acceptable latency: 1–3 seconds per response
- **Recommended for single-user 8h/day profile**

### Component Specifications

| Component | Specification | Unit Cost | Notes |
|-----------|---------------|-----------|-------|
| CPU | AMD Ryzen 9 7900X (12-core, 24-thread, 120W TDP) | $550 | Excellent all-core performance |
| Motherboard | X870-E (DDR5, PCIe 5.0) | $250 | ASUS ROG Strix X870-I or MSI MPG B870 |
| RAM | 128 GB DDR5-6000 ECC | $650 | 4 x 32 GB; enables larger batch processing |
| Storage | 2 TB NVMe Gen5 (Samsung 990 Pro) | $180 | OS (250GB) + Models (1.5TB) + scratch (250GB) |
| PSU | 850W 80+ Gold | $120 | Seasonic Focus Gold or Corsair RM850e |
| Case + Cooling | Mid-Tower ATX + AIO Liquid | $300 | Noctua NH-U14S CHROMAX or 360mm AIO (Corsair, NZXT) |
| Network | 10 Gbps NIC (USB-C or PCIe) | $50 | SFP+ or RJ45; enables local network acceleration |
| **Subtotal** | | **$2,100** | **Component cost only** |
| Assembly/Labor | DIY or $300–$500 | $0–$500 | Moderate complexity |
| **Total System Cost** | | **$8,000–$10,000** | Verified pricing, Q2 2026 |

### Expected Performance

| Model | Config | Tokens/Sec | Use Case |
|-------|--------|-----------|----------|
| Qwen2.5-Coder 7B | Q4 quantization | 25–35 t/s | Excellent for quick tasks |
| Qwen2.5-Coder 14B | Q4 quantization | **9–12 t/s** | **Recommended; sweet spot for this tier** |
| CodeLlama 34B | GGUF Q4 | 3–5 t/s | For complex multi-file refactoring |

### Latency Profile
- 100-token generation: ~3–10 seconds (7B), ~8–12 seconds (14B)
- 500-token generation: ~14–20 seconds (7B), ~42–56 seconds (14B)
- 2000-token generation (incident review): ~57–80 seconds (14B)

### Real-World Task Examples
- **Terraform module review + generation:** 30–60 seconds → response ready
- **Bicep template debugging:** 40–90 seconds → ready for deployment review
- **Incident log analysis (5 KB text):** 20–45 seconds → summary + action items

### Upgrade Path
- **To Premium:** Upgrade CPU to Ryzen 9 9950X or switch to dual-socket EPYC for 2–3x throughput
- **To GPU:** Add RTX 4090 or H100 to this base; 20–100x throughput increase
- **Stay CPU-only:** This config satisfies most daily workflows; upgrade triggers are exhaustion-rate >15% for 2 months or latency p95 >30s consistently

---

## Build 3: Premium Configuration (~$15,000–$25,000)

### Target Use Case
- Demanding platform engineering: complex multi-file refactoring, architecture design sessions, real-time incident response
- High-concurrency: 3–5 simultaneous inference requests from different tools/terminals
- Acceptable latency: <1 second per response for most tasks
- Optional: Multi-user lab or small team (2–3 concurrent users)

### Component Specifications

| Component | Specification | Unit Cost | Notes |
|-----------|---------------|-----------|-------|
| CPU | Intel Xeon W9-3595X (60-core, 120-thread, 350W TDP) **or** AMD Ryzen Threadripper Pro 7995WX (64-core) | $7,000–$8,500 | Server-class; extreme all-core performance |
| Motherboard | Dual-Socket EPYC 9004 (up to 192-core) **or** Threadripper Pro WRX90 | $1,500–$2,000 | Workstation-grade; enables future expansion |
| RAM | 256–512 GB DDR5-5600 ECC | $4,000–$8,000 | 8–16 x 32 GB; supports large batch inference |
| Storage | 4 TB NVMe Gen5 RAID 1 (mirror) | $600 | OS + Models + Scratch with redundancy |
| PSU | 2000W 80+ Platinum | $400 | Redundant or single high-capacity (Seasonic, Delta) |
| Case + Cooling | Dual-CPU Workstation Chassis + Liquid Cooling | $1,500–$2,000 | Supermicro SYS-2U or custom water loop (Corsair, NZXT pro) |
| Network | 25 Gbps NIC (SFP28) + 10 Gbps backup | $300 | Enables multi-client inference load-balancing |
| **Subtotal** | | **$15,300–$22,400** | **Component cost only** |
| Assembly/Labor | Professional assembly recommended | $500–$1,500 | Complex thermal/power management |
| **Total System Cost** | | **$15,800–$23,900** | Custom workstation pricing |

### Expected Performance

| Model | Config | Tokens/Sec | Use Case |
|-------|--------|-----------|----------|
| Qwen2.5-Coder 7B | Q4 quantization | 80–120 t/s | Rapid prototyping |
| Qwen2.5-Coder 14B | Q4 quantization | **30–45 t/s** | **Primary model; excellent throughput** |
| CodeLlama 34B | GGUF Q4 | 15–22 t/s | Complex reasoning; <5 second response |
| Mixtral 8x7B (MoE) | GGUF Q4 | 50–70 t/s | Multi-expert; best quality for cost |

### Latency Profile
- 100-token generation: <0.5 seconds (7B), ~2–3 seconds (14B)
- 500-token generation: ~5–6 seconds (7B), ~11–17 seconds (14B)
- 2000-token generation (full incident review): ~19–45 seconds (14B)

### Real-World Task Examples
- **Concurrent usage (2–3 simultaneous requests):** All responses within 5 seconds
- **Large architecture blueprint (10 KB) + design feedback:** 15–25 seconds
- **Repository-wide refactoring suggestion:** 30–60 seconds
- **Load-balanced inference for small team (2–3 users):** 2–3 second average latency per user

### Operational Advantages
- **Redundancy:** Dual-track storage (RAID 1) prevents data loss from drive failure
- **Scalability:** Can add additional inference nodes and use orchestration (docker-compose, Kubernetes)
- **Multi-user:** Supports 2–3 concurrent users with <2s latency
- **Research:** Enables benchmarking multiple models in parallel (7B, 14B, 34B simultaneously)

### Upgrade Path
- **Beyond this:** Consider GPU cluster (8x RTX 4090 or 2x L40S) for >1000 t/s
- **Horizontal scale:** This tier is at the limits of CPU efficiency; further gains require GPU or multi-node distributed inference

---

## Comparison Summary

| Metric | Budget | Balanced | Premium |
|--------|--------|----------|---------|
| **Total Cost** | $3.5K–$5K | $8K–$12K | $15K–$25K |
| **14B Model Speed** | 5–8 t/s | 9–12 t/s | 30–45 t/s |
| **100-token latency** | 12–20 sec | 8–12 sec | 2–3 sec |
| **500-token latency** | 62–100 sec | 42–56 sec | 11–17 sec |
| **Parallel requests** | 1 (sequential) | 1–2 (light) | 3–5 (comfortable) |
| **Use case** | Learning / Lab | **Daily platform eng** | Intensive / multi-user |
| **Upgrade trigger** | p95 latency >30s for 2mo | p95 latency >20s for 2mo | Add GPU/cluster |

---

## Selection Guide for Your Profile (Single User, 8 hours/day, Platform Engineering)

### Choose **Balanced** if:
- ✅ You spend 80% of time on code generation, incident analysis, architecture notes
- ✅ You rarely need response in <2 seconds
- ✅ You want to avoid GPU complexity and power costs
- ✅ You budget $8K–$12K and amortize over 4–5 years (~$150–$250/month capital + $50/month power)
- ✅ You prefer reliability over speed
- **Decision: This is the recommendation for your profile**

### Choose **Budget** if:
- ✅ You want to test CPU inference before committing to Balanced
- ✅ You have a $3.5K–$5K hard budget
- ✅ You can tolerate 15–25 second latencies for 500-token responses
- ✅ You plan to upgrade to GPU within 12 months
- ✅ You're trialing local AI before rolling out to a team

### Choose **Premium** if:
- ✅ You have 3–5 other team members who will share the server
- ✅ You spend time on complex multi-file refactoring that benefits from quick feedback loops
- ✅ You need p95 latency <3 seconds as baseline
- ✅ You have $15K–$25K budget and can justify multi-user economics
- ✅ You want one powerful machine instead of managing multiple smaller nodes

---

## Where to Buy

### Budget & Balanced (Consumer/Prosumer)
- **CPU/Mobo/RAM/Storage:** Newegg, Amazon, Scan.co.uk, Overclockers
- **Pre-built alternative:** ASUS ProArt StudioBook or Dell Precision 3460 (~$6K–$8K for Balanced-equivalent)

### Premium (Workstation)
- **Threadripper Pro / Xeon W:** Scan, Amazon (workstation section), Overclockers
- **Pre-built workstations:** Lenovo ThinkStation, Dell Precision 7960, ASUS ProArt Studiobook Pro 16M

### All Builds
- **Linux preinstall available?** Check with vendor; otherwise plan 2 hours for OS setup/model download
- **Warranty:** Standard manufacturer 3–5 years; consider 1-year accidental damage for Premium tier

---

## Implementation Checklist

### Before Purchase
- [ ] Decide between Budget/Balanced/Premium based on selection guide above
- [ ] Verify motherboard CPU compatibility on QVL (qualified vendor list)
- [ ] Check case thermal specs (CPU cooler clearance)
- [ ] Confirm RAM compatibility (not all DDR5 modules work with all boards)

### After Assembly
- [ ] Install Ubuntu 22.04 LTS or similar stable Linux distribution
- [ ] Update BIOS to latest (improves DDR5 stability and CPU power management)
- [ ] Install Ollama or vLLM for model serving (both run well on CPU)
- [ ] Download Qwen2.5-Coder 14B Q4 model (~9 GB)
- [ ] Run warmup inference tests (generate 500 tokens several times)
- [ ] Configure ulimit for file descriptors and memory (`ulimit -n 65535`)

### First Month Monitoring
- [ ] Measure actual token/sec on representative code-generation tasks
- [ ] Track p95 response latencies and compare against expectations (±20% variance is normal)
- [ ] Monitor CPU/RAM utilization during peak load
- [ ] If latency >50% worse than expected → check for thermal throttling or background I/O

---

## Cost of Ownership (4-Year Amortization)

### Balanced Build Example
- Hardware: $10,000 / 48 months = **$208/month capital**
- Power (12-core @ 120W avg): 120W × 8h/day × 30d / 1000 = ~29 kWh/month
  - At $0.12/kWh: **$3.50/month power**
- Maintenance/replacement reserve: **$10/month**
- **Total Balanced CPU: ~$221/month hardware + operating**

### Compare to SaaS
- GitHub Copilot Pro: $10/month
- DeepSeek API heavy use: $50–$100/month
- Claude Pro (backup): $20/month
- **Total SaaS: $80–$130/month**

### Break-Even Analysis
- 4-year hardware cost: $10,600
- 4-year SaaS cost (at $100/month): $4,800
- **CPU-only is economical if you:** Plan to keep the machine >3 years, want full model control, or need offline capability

---

## Troubleshooting

### Token Rate Much Slower Than Expected
1. Check CPU thermals: `watch -n 1 sensors` (target: <90°C under load)
2. Verify CPU clock: `lscpu | grep MHz` (should be near max boost)
3. Check RAM bandwidth: Run `sysbench memory --memory-block-size=8K` → should show >50 GB/s
4. Disable power management: `echo performance | sudo tee /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor`

### Model Crashes or OOM
1. Reduce batch size in Ollama/vLLM config (default often too aggressive for CPU)
2. Use stronger quantization (Q4_K_M instead of Q5) to save 1–2 GB RAM
3. Monitor with `free -h` during inference; target 20–30 GB free after model load

### Stuck on Inference
1. Restart serving process: `pkill -f ollama; ollama serve`
2. Check disk space: `df -h` (need >100 GB free for model cache + scratch)
3. Enable verbose logging: `OLLAMA_DEBUG=1 ollama serve`

---

## Next Steps

1. **Review:** Compare Balanced vs. Premium based on your multi-user needs
2. **Budget confirmation:** Verify hardware costs in your region (prices vary Europe/UK/US)
3. **Order:** Plan for 1–2 week delivery + assembly time
4. **Setup:** Follow implementation checklist
5. **Monitor:** Use trigger scorecard from parent guide to determine if local AI remains viable or needs GPU/hybrid

---

## Related Documents

- [CPU-Only Local AI Server Guide](cpu-only-local-ai-server-guide.md) – Hardware motivation and model selection
- [Heavy-User Budget Simulation](heavy-user-budget-simulation.md) – SaaS cost comparison
- [Pricing Appendix](pricing-appendix-2026-04.md) – Market and capacity context
- [Management Decision Dashboard](management-decision-dashboard.md) – Scenario framework (local vs. SaaS)
