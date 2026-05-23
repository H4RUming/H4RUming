<!--
**H4RUming/H4RUming** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->

## H4RUming

CS undergrad in Korea. I run a self-hosted LLM stack and learn AI
inference by operating it — quantization, scheduling, memory management,
edge deployment.

### What I'm working on

- Running Gemma 4 31B inference on a lab RTX PRO 6000 Blackwell node
  with FP8 KV cache and MTP speculative decoding
- Investigating prefill regressions and TurboQuant compatibility on
  heterogeneous attention head dimensions (256 local / 512 global)
- Migrating quantization formats based on GSM8K Platinum measurements
  while preserving client-facing model names for zero-downtime cutover

### Infrastructure

| | |
|---|---|
| Primary inference node | RTX PRO 6000 Blackwell (96GB VRAM), Ubuntu — university lab GPU I'm the primary operator of |
| Edge node (home) | Jetson, L4T container builds |
| Network | Tailscale mesh across nodes |
| Service split | vLLM / FastAPI proxy / tooling each in separate venvs and systemd units |

### Pinned projects

**[gemma4-vllm-stack](https://github.com/H4RUming/gemma4-vllm-stack)** ·
Production-style vLLM serving for Gemma 4 31B. 2.45× speedup with MTP=5
(measured over 5 runs, σ tracked), 256K context with KV cache profiling,
7 ADRs documenting decisions. Multilingual README (en / ko / ja).

**[gemma4-vllm-proxy](https://github.com/H4RUming/gemma4-vllm-proxy)** ·
Async FastAPI proxy in front of vLLM. Normalizes 4 thinking-mode formats
(`reasoning_effort` / `extra_body.thinking` / `thinking_config` /
`chat_template_kwargs.enable_thinking`) into one consistent surface for
clients. Streams responses with background JSONL logging.

### Stack

**Inference & serving** — vLLM · Gemma · NVFP4 / FP8 quantization · MTP speculative decoding
**Edge** — Jetson · L4T containers
**Application** — FastAPI · async Python
**Infrastructure** — systemd · Tailscale · Docker · Ubuntu

### Reading & exploring

- vLLM source (scheduler, KV cache manager, attention backends)
- NVIDIA TensorRT-LLM documentation
- Speculative decoding (Leviathan et al., 2023)
- PagedAttention and FlashAttention papers

### Where I'm headed

Looking toward AI Inference / Optimization Engineer roles.

### Contact

[h4ruming@gmail.com](mailto:h4ruming@gmail.com)
