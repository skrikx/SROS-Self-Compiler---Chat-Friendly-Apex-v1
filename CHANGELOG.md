# File: CHANGELOG.md

# Changelog

All notable changes to this project will be documented in this file.

This project follows semantic versioning in OSS mode where possible.

## v1.0.0-oss (2026-02-01)

### Added
- SRX ACE v2 agent prompt-spec: `SRX.ACE.SelfCompiler.OSS.ChatFriendly.Apex.v1.xml`
- Chat-friendly modes:
  - Fast mode via `compile:`
  - Refine mode via `refine:`
- XML-only output contract:
  - `compiler_input_form` or `promptunit_package` only
- SR8 artifact format:
  - `sr8_prompt` inside `sr8_prompts`
- Receipts-first pipeline with governance, routing, mirror lens set, and run report
- OSS hygiene rules:
  - no numeric trust scores
  - no numeric lens scores
  - hashing placeholders allowed (optional)
  - URI sanitation against link wrapping

### Notes
- This is a prompt-spec release, not an executable compiler binary.
- Deterministic replay and canonical hashing are intentionally not shipped in v1.

