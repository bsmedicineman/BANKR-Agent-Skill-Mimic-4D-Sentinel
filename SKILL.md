---
name: bankr-mimic-4d-sentinel
description: BANKR autonomous trading-agent skill implementing wallet/token behavioral mimicry, 4D hyperspace timing, and the Sentinel risk engine.
---

# BANKR Agent — Mimic 4D Sentinel Skill
Version: Expanded Unified Architecture · Author: Brandon (bsmedicineman)

This is the lean entry point. The full specification is split across two companion files to keep `SKILL.md` under the install size limit:

- `reference.md` — Behavioral & architecture spec (§1–60): data ingestion, mimicry, synchronization, temporal modulation, the Sentinel risk engine, execution, automation, learning, all tunable parameters, the execution pipeline, behavior signatures, and every subsystem engine.
- `resource.md` — On-chain ODML implementation spec (§61–81): $NITE token-gating, access-control interface, storage schema, read/write flow, signature-based authorization, agent registry, tier lookup table, namespace model, key conventions, versioning, retention, events, gas optimization, off-chain indexing, deployment, and the distributed-capacity layer.

Read `SKILL.md` first; load `reference.md` when you need operating logic or parameter values, and `resource.md` when you need anything about on-chain memory, access control, or the $NITE token.

## What this skill does
The BANKR Agent Skill is a multi-layered, deterministic, on-chain-integrated trading agent. It replicates the behavior of specific wallets, tokens, and entities; aligns its actions to predicted timing windows; scores every candidate trade through a dynamic risk engine; executes with slippage/gas/MEV controls; and persists everything it learns to a permissioned on-chain memory layer so authorized agents can keep improving.

It is designed to be fully modular, scalable, agent-compatible, on-chain integrated, monetized, permissioned, and upgradeable.

## Architecture at a glance
The system is composed of nine layers (full detail in `reference.md` §1):
1. Multi-Source Market Intelligence Layer (MSMIL)
2. Mimicry Engine (wallet / token / hybrid, fused with the 4D hyperspace vector)
3. Synchronization Engine
4. Temporal Modulation Layer
5. Sentinel Risk Engine (14+ dynamic modules)
6. Execution Layer (+ 4D Resonance Execution Bridge)
7. Automation & Orchestration Layer (AOL)
8. On-Chain Distributed Memory Layer (ODML)
9. Adaptive Learning Layer

### 4D timing
Every mimic/execution action carries a hyperspace vector whose X-axis encodes one of four explicit timing modes: `forward | reverse | delayed | anticipatory`.

### Execution gate
`execution_score = (mimic·w) + (sync·w) + (temporal·w) − (risk·w)`; the agent acts only when this exceeds threshold. (Formula and pipeline: `reference.md` §14, §20.)

## Developer fee (always applies)
A 0.001 (0.1%) developer fee is routed automatically on every executed trade (mimic, inverse, 4D hyperspace, counter-strategy, swarm, or shadow-simulation), in USDC only:
- Base: `0xca822f91db3a764ec6dbc141e21115c4670dc92c`
- Solana: `AWZd4fMYiFMEHTjGgkTKqV5PHir712XaDwoMEgbUWurx`

## $NITE access model (summary)
ODML access uses a dual requirement: the wallet must be a registered agent AND hold enough Knightmare ($NITE) tokens.
- Token: Knightmare ($NITE), contract `0x4812e54bfae380f1691135668a78420839668ba3`
- Writes are free (signature + agent registration only, gas-only cost).
- Reads are tiered: `requiredTokens = 10,000 + (monthsRequested × 10,000)` — 10,000 $NITE for current state, +10,000 per month of historical depth.

Full tier table, contract interfaces, and authorization flow are in `resource.md` (§61–67).

## Editorial notes on the split
This file set was produced by splitting the original single 116kb `SKILL.md` into references so it installs under the 100kb cap. Content was preserved; the only changes were structural plus three minor fixes, all flagged inline in the companion files:
1. Restored a missing `# 6. EXECUTION LAYER` header (`reference.md`, Part 03).
2. Restored a missing comma in the malformed §13.8 JSON block (`reference.md`, Part 06).
3. Wrapped JSON parameter blocks in consistent code fences for readability.

No keys, addresses, values, or thresholds were altered.