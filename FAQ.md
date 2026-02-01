# File: FAQ.md

## FAQ - SROS Self-Compiler (OSS)

### What is this repo?
A chat-first compiler prompt-spec that turns short intent into a sealed XML `promptunit_package` containing `sr8_prompt` artifacts and receipts.

### Is this an executable program?
No. OSS v1 is a prompt-spec designed to run in normal LLM chats. It is not a binary compiler.

### What do I paste into a chat?
Option A: Paste the compiler agent XML in `agents/` as your first message in a new chat, then use:
- `compile: ...`
- `refine: ...`

Option B: Paste one of the demo agents in `agents/demo/` as your first message, then give it a normal instruction.

### Why is everything XML-only?
XML-only keeps outputs deterministic in structure, easy to lint, easy to diff, and hard to “accidentally” contaminate with markdown.

### Why are hashes optional?
OSS v1 prioritizes portability and cleanliness. If a hash is not computed, the spec uses placeholder nodes marked:
- `status="optional" kind="placeholder"`

### What’s the difference between compile and refine?
- `compile:` goes straight to packaging using minimal inferred constraints.
- `refine:` returns a minimal intake form when your intent is missing key details.

### Can I compile multi-domain work in one run?
Yes. Put deliverables as a list and lock constraints as hard rules. See `examples/03-multidomain-sros-run.txt`.

### Does this support multimodal inputs?
The spec supports adapter selection for multimodal, but actual capability depends on your chat environment. See `examples/04-multimodal-adapters.txt`.

### What is governance gating?
If a request is unsafe or disallowed, the compiler will refuse and compile a safe alternative.  
If a request is high-risk but not disallowed, the compiler can return `GATE_REQUIRED` with an approval artifact contract. See `examples/05-governance-gate-required.txt`.

### Can I change the output format to JSON/YAML?
Not in OSS v1. This repo is intentionally XML-only to stay schema-clean and portable.

### What do I do after I get a promptunit_package?
Extract the active `sr8_prompt` from CDATA, paste it into a new chat, and tell the model to execute it and produce the deliverables. Full steps are in `USAGE_GUIDE_SOVEREIGN.md`.

### How do I iterate without drift?
Re-run `compile:` with deltas. Do not manually rewrite the spec. Keep constraints stable.

### Is this “SROS” or just a prompt?
This repo is the OSS “front door” compiler spec aligned to SROS concepts:
- adapters
- receipts
- constraint arbitration
- governance gates
- SR8 compilation artifacts
- SR9 compile receipt stubs (OSS-friendly)

It’s designed to be portable, not to require the full SROS runtime to be useful.
