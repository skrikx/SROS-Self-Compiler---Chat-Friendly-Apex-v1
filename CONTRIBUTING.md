# File: CONTRIBUTING.md

# Contributing

Thanks for taking the time to contribute.

This repo is a public OSS extraction of the SROS Self-Compiler prompt-spec. The core rule is: keep it clean, chat-friendly, and receipts-first.

## Scope

### In scope
- Output formats: JSON and YAML modes that preserve the same semantics as XML
- Validator tooling:
  - single-root output checks
  - URI sanitation checks
  - numeric score bans
- Better examples and docs
- Stronger governance templates and approval contracts
- Adapter registry expansions (still abstract, no provider coupling in OSS v1)

### Out of scope (for v1)
- Claims of cryptographic determinism
- Provider-specific model routing baked into receipts
- Any automation that requires credential harvesting or private data extraction

## How to propose a change

1) Open an issue with:
- Problem statement
- Proposed behavior
- Minimal example input and expected output

2) If accepted, open a PR with:
- The patch
- Updated example(s) if behavior changed
- Updated README if user-facing

## Style rules for PRs

### XML hygiene
- Do not introduce markdown links inside XML fields.
- Do not introduce Google-wrapped URIs or link wrappers.
- Keep exactly one root output per response.

### No fake precision
- Do not add numeric trust scores or numeric lens scores.
- Use `score_class="high|medium|low"` if you need classification.

### Hashing policy (v1)
- Hash fields may remain placeholders:
  - `status="optional" kind="placeholder"`
- If you implement hashing, include:
  - canonical byte serialization definition
  - deterministic test cases
  - a validator script and fixtures

## Testing expectations

At minimum, add or update fixtures that cover:
- Fast mode `compile:` returns `promptunit_package`
- Vague input returns `compiler_input_form`
- XML spec paste triggers intake mode
- URI sanitation blocks link-wrapped URIs
- Numeric scoring strings do not appear in output

## Pull request checklist

- [ ] No markdown links in XML fields
- [ ] No `google.com/search?q=` anywhere
- [ ] No numeric scoring fields
- [ ] Examples updated if behavior changed
- [ ] README updated if user-facing change

## Contributor credits

If you want attribution, add yourself to a `CREDITS.md` section:
- Name
- Handle
- Contribution type

