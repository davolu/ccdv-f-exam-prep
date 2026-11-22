# Domain checklists (unofficial)

Use these as a study list for the official 7 December 2026 domains. Tick an item only when you can explain it in your own words and apply it to a short scenario.

Confirm wording and any new skills against the official exam guide for your date.

## Applications and Integration — 20%

- [ ] Choose the Messages API (or the right official API surface) for a workload, versus a batch or offline job
- [ ] Configure a request: model, system prompt, tools, streaming, and token limits
- [ ] Read the stop reason (`end_turn`, `tool_use`, `max_tokens`, `refusal`) before you trust the text
- [ ] Tell error classes apart: rate limit, overloaded, invalid request, timeout — and decide what to retry
- [ ] Design a resilient integration: retries with backoff, idempotency, and timeouts
- [ ] Keep secrets on the server; never ship a key in a mobile or browser client

## Agents and Workflows — 17%

- [ ] Tell a workflow (a path you designed) from an agent (the model chooses the next step)
- [ ] Choose when a thin orchestrator and specialist subagents are worth the extra moving parts
- [ ] Isolate context so one messy task does not pollute another
- [ ] Use a hook when a rule must always fire, including blocking a tool call before it happens
- [ ] Read a trace: loops, missing termination, a tool called with the wrong argument
- [ ] Know when a self-hosted harness is justified (audit, network boundary) versus a managed runtime

## Prompt and Context Engineering — 15%

- [ ] Manage a filling context window: prune, compact, hand a task to a subagent, or start a fresh session
- [ ] Write instructions that state the goal, the constraints, and the output shape
- [ ] Choose zero-shot, one-shot, or few-shot when the format is easier to show than to describe
- [ ] Turn structured output on, then still check the stop reason and validate the result
- [ ] Ground an answer in the supplied documents, cite them, or say the pack does not contain the answer
- [ ] Decide when the full pack belongs in context versus retrieving passages

## Model Selection and Optimization — 12%

- [ ] Choose a model tier (faster/cheaper vs a strong middle vs more capable) against quality, latency, and cost
- [ ] Prove an upgrade with a regression set, not with a hunch
- [ ] Look up current rate and token limits in official docs; do not memorise unofficial numbers
- [ ] Use extended thinking when the task needs it, and know that it costs time and tokens
- [ ] Find the cost driver first (input tokens, output tokens, retries, cache misses)
- [ ] Place a cache breakpoint after a stable prefix; put changing text after the breakpoint

## Eval, Testing, and Debugging — 10%

- [ ] Build a golden set of fixed cases with known good answers, including “must not invent” cases
- [ ] Use an LLM-as-judge carefully: it can grade, but it also needs checks
- [ ] Name a failure mode: hallucination, refusal, under-acting, context loss, format drift, inconsistency
- [ ] Decide whether a defect is in the integration (timeouts, retries, tool wiring) or in the model output
- [ ] Re-run a failing case after a change, and keep the golden set in version control

## Tools and MCP — 10%

- [ ] Write a precise tool description and return a short, useful result (not a 20-page dump)
- [ ] Validate tool arguments before you execute the side effect
- [ ] Explain Model Context Protocol: tools, resources, and prompts, shared by more than one app
- [ ] Know the transports (stdio and HTTP) and that a server still needs authentication
- [ ] Pick the mechanism that matches the job: built-in tool, custom tool, Skill, or MCP server

## Claude Code — 8%

- [ ] Know the surfaces: CLI, desktop, editor/IDE, web, and mobile
- [ ] Use `CLAUDE.md` (the project instructions file) for standing rules the project should remember
- [ ] Choose the right extension: Skill or command, rules file, hook, subagent, or plugin
- [ ] Set permissions so the tool cannot do more than the task needs
- [ ] Do not treat a hook as a Skill, or a Skill as a hook

## Security and Safety — 8%

- [ ] Treat tickets, pages, documents, and tool results as untrusted content
- [ ] Keep untrusted content outside the trusted system instructions
- [ ] Enforce high-risk actions with a hook, a permission, or a human approval — not with a prompt alone
- [ ] Apply least privilege: workspace-scoped keys, not a broad admin key
- [ ] Rotate keys when people leave or a leak is possible, and watch usage
- [ ] Never put a key on a phone, in a repo, or in a screenshot
