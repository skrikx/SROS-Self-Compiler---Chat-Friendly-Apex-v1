# SROS Self-Compiler (OSS) - Chat Friendly Apex v1

This is the open-source release of the **SROS Self-Compiler (OSS)** - a chat-first compiler agent that turns a short message into a structured, receipt-driven XML artifact.

It is designed to be:
- **Chat-friendly**: type `compile:` and get a compiled package
- **Receipt-driven**: every major decision produces a receipt
- **Schema-clean**: XML-only outputs, no markdown pollution in fields
- **OSS-safe**: no fake precision, no numeric trust scores, hashing optional in v1
- **Portable**: works as a prompt-spec in any chat environment that supports long-form system instructions

This repo ships an **SRX ACE v2 agent prompt-spec** (not an executable binary compiler yet). It is intended to be used as a canonical "front door" for generating structured build prompts and packages.

---

## Official Links

- **PlatXP Creative**: https://platxpcreative.com  
- **SROS**: https://sros.cloud  
- **FlowXP**: https://flowxp.org  
- **SROS v2 Repo**: https://github.com/skrikx/SROS_v2  

---

## What it does

You type:

`compile: build a 10 page enterprise AI agency website for PlatXP (USA), cobalt blue aesthetic, include sitemap + copy brief, stack SvelteKit + Tailwind + Motion One`

You get back exactly one XML artifact:

`<promptunit_package xmlns="https://srx.sros/schema/package/v2"> ... </promptunit_package>`

That package contains:
- `replay_capsule` (normalized intent + versioning hints)
- adapter selection receipt (what modalities were detected)
- model routing receipt (abstract stages, not provider-specific)
- MirrorOS lens set (no numeric scores in OSS mode)
- governance receipt (allow, gate, refuse)
- `sr8_prompt` artifact(s) inside `sr8_prompts` (the build payload)
- compile report (what happened)

---

## Quick start

### Fast mode
Prefix any request with `compile:`.

Example:
`compile: build a 10 page agency site, cobalt blue style, USA market, stack SvelteKit + Tailwind + Motion One`

Expected response root:
- `promptunit_package`

### Refine mode
If your request is vague, the compiler returns a short form (`compiler_input_form`) asking for:
- goal
- deliverables
- constraints
- optional style preferences
- runtime capabilities flags

You reply with the filled `<compiler_input>` block.

---

## Output rules

The compiler always outputs exactly one XML document per response:
- `compiler_input_form` (intake mode), or
- `promptunit_package` (compile mode)

No markdown is emitted. No prose outside XML.

---

## Repository contents

- `SRX.ACE.SelfCompiler.OSS.ChatFriendly.Apex.v1.xml`  
  The public entrypoint agent prompt-spec.

- `examples/01-fast-compile.txt`  
  Example using `compile:` fast mode.

- `examples/02-refine-then-compile.txt`  
  Example showing refine form then compile.

- `LICENSE`  
  Open source license.

---

## OSS hygiene guarantees (v1)

### No fake precision
This OSS release does not output numeric trust scores or numeric lens scores.
Scoring uses `score_class` only (high, medium, low) when needed.

### Hashing is optional in v1
Hash fields may appear as placeholders:
- `status="optional" kind="placeholder"`

This is intentional for early OSS release. Future versions can add canonical byte serialization and real hashing.

### URI sanitization
The agent refuses or sanitizes link-wrapped URIs.
Disallowed patterns include:
- `google.com/search?q=`
- markdown link shapes like `](...)` or `[...]`

---

## Governance behavior

The compiler classifies each request and emits:
- `decision=ALLOW` for safe compilation
- `decision=GATE_REQUIRED` for high-risk requests (emits an approval artifact contract)
- `decision=REFUSE` for disallowed requests (emits a safe alternative `sr8_prompt` instead)

---

## Non-goals (v1)

This release is not:
- a cryptographically deterministic compiler
- a guarantee of correctness
- a runtime engine that executes tools or deploys apps
- a registry-backed model router with provider enforcement (routing is abstract in OSS v1)

---

## Credits and authorship

### Creator
- **Muqeet ul Hassan** (Skrikx Kyōten) - original author, system architect, and primary maintainer.

### Project lineage
This compiler is part of the broader SROS ecosystem:
- **SR8** - compiler discipline and prompt rendering
- **SRX ACE v2** - agent container format and packaging
- **SR9** - orchestration receipts (DAG-level compilation), bounded tighten loops
- **MirrorOS** - lens arbitration and constraint locking

### Attribution request
If you use this project in public content, demos, or derivative repos, please include:
- “Built with SROS Self-Compiler (OSS) by Muqeet ul Hassan.”

---

## Branding and naming

- **SROS** - Sovereign Recursive Operating System  
- **Skrikx Kyōten** - operator identity used for continuity across artifacts  
- **PlatXP** - the public-facing studio and empire node through which SROS artifacts are shipped  

---

## Roadmap (optional)

If you want to contribute, the highest-leverage next steps:
1) Add JSON and YAML output modes (same semantics, different serialization)
2) Add a CLI validator (lint for URI wrapping, numeric scores, single-root output)
3) Add registry-backed model IDs (optional, behind a config file)
4) Add canonical hashing and sealing (v2)

---

## Contact / updates

Official:
- PlatXP: https://platxpcreative.com
- SROS: https://sros.cloud
