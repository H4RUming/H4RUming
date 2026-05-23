[English](README.md) · **한국어**

## H4RUming

한국에서 컴퓨터공학을 공부하는 학부생. self-hosted LLM 스택을 운영하면서 AI 인퍼런스를 익히는 중.

quantization, scheduling, memory management, edge deployment.

### 현재 작업

- 학교 연구실의 RTX PRO 6000 Blackwell 노드에서 Gemma 4 31B 인퍼런스 운영
  (FP8 KV cache + MTP speculative decoding)
- Heterogeneous attention head dimensions (local 256 / global 512) 환경에서
  prefill regression 및 TurboQuant 호환성 조사
- GSM8K Platinum 측정 기반으로 quantization 포맷 마이그레이션 진행,
  클라이언트 노출 model name 유지로 무중단 전환

### 인프라

| | |
|---|---|
| 주 인퍼런스 노드 | RTX PRO 6000 Blackwell (96GB VRAM), Ubuntu — 학교 연구실 GPU, 단독 운영 |
| 엣지 노드 (집) | Jetson, L4T 컨테이너 빌드 |
| 네트워크 | Tailscale mesh |
| 서비스 분리 | vLLM / FastAPI proxy / tooling 각각 별도 venv + systemd unit |

### 핀 고정 프로젝트

**[gemma4-vllm-stack](https://github.com/H4RUming/gemma4-vllm-stack)** ·
Gemma 4 31B를 위한 production-style vLLM 서빙 구성. MTP=5에서 baseline 대비
2.45× speedup (5회 측정, σ 추적), 256K context + KV cache 프로파일링,
의사결정 ADR 7건. 다국어 README (en / ko / ja).

**[gemma4-vllm-proxy](https://github.com/H4RUming/gemma4-vllm-proxy)** ·
vLLM 앞단의 async FastAPI proxy. 4종 thinking-mode 포맷
(`reasoning_effort` / `extra_body.thinking` / `thinking_config` /
`chat_template_kwargs.enable_thinking`)을 단일 인터페이스로 정규화.
스트리밍 응답 + 백그라운드 JSONL 로깅.

### 스택

**Inference & serving** : vLLM · Gemma · NVFP4 / FP8 quantization · MTP speculative decoding
**Edge** : Jetson · L4T containers
**Application** : FastAPI · async Python
**Infrastructure** : systemd · Tailscale · Docker · Ubuntu

### 공부 중

- vLLM 소스 (scheduler, KV cache manager, attention backends)
- NVIDIA TensorR, LLM 문서
- Speculative decoding (Leviathan et al., 2023)
- PagedAttention, FlashAttention 논문

### 관심 직무

AI Inference / Optimization Engineer.

### 연락처

[h4ruming@gmail.com](mailto:h4ruming@gmail.com)
