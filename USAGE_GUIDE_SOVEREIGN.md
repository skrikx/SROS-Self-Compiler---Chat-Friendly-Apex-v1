# File: USAGE_GUIDE_SOVEREIGN.md

## SROS Self-Compiler (OSS) - Sovereign Usage Guide

This guide shows how to use the compiler in real chats, across domains, inside popular LLM apps, and what to do after you receive a `promptunit_package`.

### 1) Where to run this
You can paste the agent XML into any LLM app that supports long system prompts or custom instructions, then use it in a normal chat.

Popular options:
- ChatGPT (Custom Instructions or a pinned system prompt)
- Claude (Projects)
- Gemini (Gems)
- Perplexity (Spaces, if long prompt allowed)
- Cursor / Windsurf (as a prompt template, then run in chat)
- Continue (prompt templates)
- OpenWebUI (system prompt per chat)

Note: The output is XML-only. You should copy the full XML response as-is.

### 2) Operating modes
#### Fast mode
Start your message with:
- `compile:`

Use when you already know what you want.

#### Refine mode
Start your message with:
- `refine:`

Use when you want the compiler to ask for minimum missing details.

### 3) Multi-domain compiles
You can ask for cross-domain outputs in one compile. Examples:
- Product: app spec + UI copy + pricing page
- Engineering: SRIR graph outline + CLI commands + receipts expectation
- Marketing: landing page + ICP + offer + outbound scripts
- Research: experiment plan + evaluation rubric + dataset schema
- Visuals: prompt packs for image generation, plus style tokens

Best practice:
- Put deliverables as an explicit list
- Put constraints as hard rules

### 4) Sovereign depth switches (chat-friendly)
If you want the compiler to behave in sovereign discipline, use one line inside your request:

Example:
`compile: ... | depth=sovereign | receipts=enforced | no_fake_scores=true | local_only=true`

Even though OSS v1 is not cryptographically deterministic, you still get:
- receipts per stage
- constraint locking and arbitration
- governance gating behavior

### 5) What you do after you receive the promptunit_package
Your `promptunit_package` contains `sr8_prompt` artifacts. Use them like this:

Step A: Extract the active sr8_prompt
- Find: `<sr8_prompts> ... <active> <![CDATA[ ... <sr8_prompt ...> ... </sr8_prompt> ... ]]> </active>`

Step B: Run the sr8_prompt in your chosen execution environment
Common patterns:
1) Paste the `sr8_prompt` into an LLM and say: "Execute this sr8_prompt. Produce the deliverables in the manifest."
2) If using a coding IDE assistant (Cursor/Windsurf), paste the `sr8_prompt` as the task spec and ask it to generate files.

Step C: Store the package as a receipt
- Save the full `promptunit_package` in a folder like:
  - `./runs/YYYY-MM-DD/<release_or_placeholder>/package.xml`
- That becomes your replay capsule for future improvements.

### 6) How to iterate without drift
Do not rewrite the spec.
Instead:
- compile again with a delta:
  - `compile: take the last package, keep constraints, add 2 case studies, tighten copy, keep stack.`

### 7) Common templates
#### Website
`compile: build a 10 page site | deliverables=sitemap,design_tokens,copy_brief | constraints=stack:SvelteKit+Tailwind`

#### App feature
`compile: add module X | deliverables=ui_spec,api_contract,tests | constraints=local_only`

#### SROS run
`compile: design an SROS run | deliverables=graph_spec,cli_commands,receipts_list | constraints=no_web`

### 8) Minimal troubleshooting
- If you get an intake form but wanted compile: you were too vague. Use `compile:` and include deliverables.
- If XML contains weird link wrapping: remove all `[` and `](` from your input and recompile.
- If you need JSON/YAML output: that is a roadmap item, not in v1.

