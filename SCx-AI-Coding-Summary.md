# SCx: Building Production Supercomputer Operations Software with AI Coding Tools

**Author:** Diego Iruretagoyena
**Project:** SCx (Supercomputer Client + Service), Azure HPC / AI Customer Experience
**Period:** January 2026 to May 2026

---

## What the project is

SCx is internal operations software for **Azure's largest dedicated GPU supercomputers** (Telemachus, Inglewood, Fairwater, and their GB200 and validation variants). Datacenter operators use it to monitor fleet health and run controlled power and lifecycle operations across thousands of nodes from a single desktop client, backed by a service deployed on production Pilotfish nodes.

It is a real, shipping system under tight constraints: secure admin workstations, smart-card identity, just-in-time access to production, and operations that physically power-cycle and repave hardware. A mistake takes real GPU capacity offline, so correctness and safety gating matter more than speed of feature delivery.

**Architecture:** a WPF .NET 10 client and an ASP.NET Core service, glued to Azure infrastructure (Titan/OneDevice for hardware power, Fabric Controller for OS lifecycle, DCM Kusto for telemetry) through shared client libraries and a WebSocket pipeline engine.

**Scale of the codebase:** ~418 commits, ~737 source files, ~41k lines of C#, 263 merged pull requests, built by a six-person team.

---

## My contribution

I am the top contributor to the project and the owner of the **client-to-infrastructure integration layer**: the code that makes the desktop app actually talk to Titan, Fabric, Kusto, and the SCx service, plus the client-side orchestration that drives multi-step power operations.

### By the numbers (from `origin/scx-working-branch`)

| Metric | Value |
|---|---|
| Commits to SCx | 176 (most of any contributor) |
| Merged pull requests | 87 of 263 total (~33%) |
| Lines changed | ~32,700 added / ~15,200 removed |
| Active development days | 46 days across 5 months |
| Span | Jan 13 to May 29, 2026 |

### File and subsystem ownership

| Area | My commits | Next contributor |
|---|---|---|
| `NodeOperationsTab.cs` (client op orchestration) | 40 | 12 |
| `DatacenterService.cs` (node data layer) | 19 | 12 |
| Client `Services/` | 29 | — |
| Shared `Common/` (Fabric + Titan clients) | 26 | — |
| `SupercomputerService/` (backend) | 42 | — |
| Orchestrator client | 10 | 10 (tied) |

### What I actually built

- **Integration spine:** wired Titan power operations and the early power-cycle REST flow into the client; built the `FabricClient` path for OS shutdown and Fabric Controller lifecycle notifications; fixed the hard parts (`SetNodeRecoveryProperty` serialization, `WaitForShutdown` endpoints and timeout semantics).
- **Node data layer:** Fabric-backed node status with automatic Fabric-vs-Kusto source detection (`NodeStatusSourceResolver`), thread-safe caching, per-cluster fallback, and VPN-disconnection detection.
- **Operation pipelines:** the client-side engine in `NodeOperationsTab` that composes pipeline steps (power on/off/cycle, OS shutdown, repave, reset health), streams batches over WebSocket, and tracks per-node progress.
- **Safety and correctness:** repave guardrails for mass operations, opt-in wait steps, and a server-side authorization fix (`JwtRoleHandler` fail-open bypass).
- **Release-quality UX on top of that base:** the `scx-release-6` wave (copy across all views, a Selected Nodes scratchpad, selection-scoped stats, sort indicators, empty-state placeholders, normalized naming).

---

## How I worked: AI coding tools in a real production codebase

This project is the case study I would point to for what an experienced engineer can do with AI coding tools inside a large, unfamiliar, high-stakes enterprise repository.

- **Velocity that scaled with the tools.** My output was not flat. It climbed as I got better at directing the agent: 12 commits in January, ramping to 36 in March and 95 in May. The May spike was the `scx-release-6` push, where I shipped roughly a dozen reviewable PRs in parallel using isolated git worktrees, each agent-assisted but independently scoped, built, and tested.
- **Small, reviewable diffs in a shared codebase.** Working alongside five other engineers in a Microsoft monorepo meant every change had to be conservative and pass human review. I used AI to move fast on the first draft, then tightened relentlessly: minimal diffs, matched surrounding style, comments that explain intent and not mechanics. A large share of my commits are follow-up tightening passes, which is exactly the discipline that keeps AI-generated code mergeable.
- **AI for the unglamorous, correctness-critical work.** The integration layer is full of serialization formats, timeout edge cases, thread-safety, and auth subtleties where a plausible-looking wrong answer is dangerous. I used AI to accelerate exploration and drafting, then verified against internal docs, real Fabric/Titan behavior, and unit tests (the project carries ~200 client and ~49 service tests).
- **Owning the whole vertical.** Most of my work crosses the client, the shared libraries, and the backend in a single change. AI made it tractable to hold that much context at once and to keep moving across layers that would normally each have a dedicated owner.

---

## Summary

Over five months I became the primary contributor to a production supercomputer operations platform, owning the integration layer that connects an operator desktop app to live Azure hardware-control systems. I used AI coding tools not to generate throwaway prototypes but to ship real, reviewed, safety-critical changes into a six-person enterprise codebase: 176 commits, 87 merged PRs, ~48k lines changed, with output that accelerated as my command of the tooling improved. The work demonstrates that AI tooling, in the hands of someone who knows what correct looks like, compresses the time from understanding an unfamiliar system to safely changing its most sensitive parts.
