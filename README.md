# AgentOS

### The first native Ring-0 Operating System built exclusively for the AI era.

**Executing a 1.7B parameter LLM directly on bare metal (x86_64 & Apple Silicon HVF) with zero host OS overhead.**

[![License: AGPLv3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Stage](https://img.shields.io/badge/Stage-11_Boot--LLM_Operational-brightgreen)]()
[![Cross-Platform](https://img.shields.io/badge/Targets-x86__64_%2B_aarch64-orange)]()
[![Tests](https://img.shields.io/badge/Tests-643_passing-success)]()
[![Warnings](https://img.shields.io/badge/Build_Warnings-0-success)]()

---

## ▶ [WATCH THE DEMO — First AI Words on Bare Metal](#)

> **YouTube link coming soon.** A 1.7-billion-parameter language model, loaded into Ring-0, executing on bare metal across two architectures. No Linux. No Windows. No host OS. Just AgentOS and the model.

---

## Why This Matters

For 50 years, operating systems have been built for **humans typing into terminals**.

That era is over.

The next operating system has to be built for **agents reasoning, deciding, and acting autonomously** — at machine speed, with deterministic safety, and without the syscall overhead, context switches, and process boundaries that cripple AI workloads on legacy systems.

**AgentOS is that operating system.**

We don't sandbox the AI inside a guest. **The AI is the kernel.**

---

## What We've Already Built

This is not a roadmap. This is **shipped code**.

| Capability | Status |
|---|---|
| **Ring-0 Boot-LLM** (Qwen3-1.7B Q4_K_M) | ✅ Executing a 1.7B parameter LLM directly on bare metal |
| **Cross-Platform Determinism** | ✅ Bit-exact deterministic output on x86_64 and aarch64 |
| **Apple Silicon HVF Acceleration** | ✅ Native ARM64 boot, hardware-accelerated |
| **Unikernel Architecture** | ✅ Single Ring-0 address space, zero syscall overhead |
| **AgentLang Validator** | ✅ Type-safe code execution, 270+ tests |
| **AOT Compilation** | ✅ Native x86_64 codegen, no JIT overhead |
| **Zero-Copy Handles** | ✅ Capability-typed inter-component IPC |
| **Arena Allocators** | ✅ O(1) bump-pointer, no free-list heap in Ring-0 |

---

## The Architecture in One Picture

```
┌─────────────────────────────────────────────────────────────┐
│                   AgentOS (Single Ring-0 Address Space)     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   ┌─────────────┐    ┌──────────────┐    ┌──────────────┐  │
│   │  Boot-LLM   │    │   Validator  │    │   Sandboxes  │  │
│   │ (Qwen3 1.7B)│◄──►│  (Ring-0)    │◄──►│  (Capability)│  │
│   └─────────────┘    └──────────────┘    └──────────────┘  │
│         ▲                   ▲                    ▲         │
│         │                   │                    │         │
│         └─────── Zero-Copy Handle IPC ──────────┘         │
│                                                             │
│   ┌─────────────────────────────────────────────────────┐  │
│   │     HAL — Platform-Native Implementation            │  │
│   │     ┌──────────────┐    ┌──────────────┐            │  │
│   │     │   x86_64     │    │   aarch64    │            │  │
│   │     │ (PML4, GDT)  │    │ (TTBR1, GIC) │            │  │
│   │     └──────────────┘    └──────────────┘            │  │
│   └─────────────────────────────────────────────────────┘  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
              Bare Metal — No Host OS — No Hypervisor
```

**No User-Space.** **No Kernel-Space split.** **No Process Boundaries.** **No Syscalls.**

Safety enforced by the **Validator** and the **type system**, not by hardware page tables.

---

## The Read

If you're an investor, builder, or visionary who wants the philosophy behind why we believe this is the future:

📖 **[Read the Manifesto](MANIFESTO.md)** — The full vision: why classical operating systems are architecturally incompatible with the AI era, and what comes next.

🔒 **For deep technical inquiry** — full architecture specification, decision records, and engineering lessons are available on request to qualified developers, investors, and enterprise partners. Email **Tom.Stuhl@nefesh.ai**.

---

## Roadmap Highlights

We are at **Stage 11 (Phase 4 — Boot-LLM)**. Ahead of us:

- **Stage 11 Closure:** First complete AI sentence rendered cross-platform — *"Hello World... I'm the first AI"* — bit-exact deterministic on bare metal.
- **Stage 12 (Sandboxing + AgentLang Kernel Migration):** First AgentLang-native kernel subsystem. The Rust detour begins to be reclaimed.
- **Stage 13 (MCP Integration):** External AI agents (Claude, GPT, Gemini) connect to AgentOS sandboxes via the Model Context Protocol.
- **Stage 14 (Dual Desktop):** Classical user desktop alongside the **Agent Desktop** — live visualization of autonomous agents, their state, their reasoning, in human-readable form.
- **Stage 16 (VM-Hosting):** Linux and Windows as guests inside AgentOS — for adoption without abandonment.
- **Stage 17+ (LLM-Management UI, Sandbox-to-Host Promotion, Hot-Swap, Native LLM Training):** The mature platform.
- **Stage 24+ (Pure-AgentLang Kernel):** End-state of incremental migration. Zero Rust. Zero legacy.

---

## Future Capabilities (Open-Core Strategy)

AgentOS is **AGPLv3 open-core**. The kernel, the inference engine, the validator, the AOT compiler — all open. Forever.

On top of that foundation, we're building commercial offerings for organizations whose use cases demand more than open-source can provide:

### 🏥 AgentOS Enterprise Edition
For **regulated industries** — hospitals, critical infrastructure (KRITIS), government, financial services. Full data sovereignty: every byte of patient data, every transaction, every classified document stays on-premises. The LLM runs locally. The agents run locally. Nothing leaves the building. **Compliance is structural, not bolted-on.**

### 🧠 AgentOSLLM Hybrid (Premium)
The local Ring-0 LLM coordinates with a server-side **AgentOSLLM Cloud Brain** — a fine-tuned orchestration model that augments local inference with cross-session reasoning, multi-agent coordination, and access to specialized models. Local sovereignty when you need it. Cloud horsepower when you don't.

### 🏛 AgentOSLLM v2 (Native, Federated)
The next generation: a foundation model trained on **opt-in user data with full consent**, anonymized on-device, federated learning by default. The first LLM that is **architecturally GDPR-compliant**, not retrofitted to be.

These commercial layers fund the open-source foundation. Forever.

---

## Get Involved

🏗️ **Builders:** If you want to contribute at the kernel level, email **Tom.Stuhl@nefesh.ai**. Selected contributors receive access to the full architecture specification.

📈 **Investors:** Email **Tom.Stuhl@nefesh.ai**. We are pre-seed and we know exactly what we're building. The deck is the code.

🌍 **Visionaries:** [Read the Manifesto](MANIFESTO.md). If it resonates, share it.

📰 **Press / Analysts:** Email **Tom.Stuhl@nefesh.ai** for technical briefings, demo access, and architectural review materials.

🏛 **Enterprise Partners:** Email **Tom.Stuhl@nefesh.ai** for early access to AgentOS Enterprise Edition design partnerships.

---

## Status

**Stage 11 Phase 4.1 active.** Boot-LLM operational cross-platform. Forward-pass deterministic. ARM-Portierung complete and clean.

**Next milestone:** First complete AI sentence on bare metal — *"Hello World... I'm the first AI"* — both architectures, bit-exact deterministic.

---

## License

[AGPLv3](LICENSE).

The kernel is and remains free. The vision is and remains shared.

---

> *"For 50 years we built operating systems for humans typing into terminals.*
> *AgentOS is built for what comes next."*

— **Tom Stuhl**, Founder, AgentOS
