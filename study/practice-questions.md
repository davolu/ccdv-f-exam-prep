# Original practice questions (unofficial)

These items are original scenario questions written for study. They are **not** official sample questions and they are **not** a live exam. Official sample items stay in the official exam guide.

Each question is followed by the answer and a short explanation of why the other options fail. Try to answer before you read the explanation.

If you sit the exam on or before 6 December 2026, you can still use these for practice, but study the older official weights and guide.


## Applications and Integration (20%)

### Applications and Integration — question 1

A live pharmacy chat must answer a customer in a second or two. A separate job rewrites thousands of catalogue lines over the weekend, and cost matters more than speed. Which workload belongs on the realtime Messages API, and why?

- A. The catalogue rewrite, because more items need a faster API.
- B. The pharmacy chat, because a person is waiting; the catalogue job can use batch.
- C. Both, because batch processing is only for images.
- D. Neither, because all Claude calls must be streamed.

<details>
<summary>Answer: B</summary>

The answer is B. Realtime is for work that cannot wait. Batch processing is the better fit for a large, latency-tolerant job when cost matters. A is backwards. C is wrong: batch is not limited to images. D is wrong: streaming is an option, not a rule for every call.

</details>

### Applications and Integration — question 2

An app retries every failed Claude call immediately, including invalid request errors, and the bill jumps while the same bad payload keeps failing. What is the defect?

- A. Retry faster, so the bad payload eventually succeeds.
- B. Retry invalid requests only at the weekend.
- C. Distinguish error classes: backoff for limits or overload; fix invalid requests.
- D. Ignore errors and return a cached guess.

<details>
<summary>Answer: C</summary>

The answer is C. The December guide expects you to tell Anthropic's error classes apart. A rate limit or an overload may deserve a careful backoff. An invalid request will not heal itself if you just hit it again. A makes the waste worse. B is an arbitrary rule. D hides the failure and can invent answers.

</details>

### Applications and Integration — question 3

A production service uses a floating model alias. Over a weekend, a new version changes tool-calling behaviour, and bookings break. What should the team have done?

- A. Always use the newest alias, so the product stays current.
- B. Pin a model version, version prompts, and upgrade with regression tests.
- C. Put the model name only inside the system prompt.
- D. Turn tools off after every model change.

<details>
<summary>Answer: B</summary>

The answer is B. Pinning and prompt versioning are part of configuration management, and upgrades should be tested, not discovered by customers. A is how the surprise happened. C hides an important setting in the wrong place. D throws away useful tools instead of controlling the change.

</details>

## Agents and Workflows (17%)

### Agents and Workflows — question 1

Every night, a finance team must fetch yesterday's invoices, add the totals, and email a fixed report. The steps never change, and auditors must see the exact path. What fits best?

- A. An open-ended agent that invents a new plan each night.
- B. A workflow with a predetermined, auditable sequence.
- C. Several subagents, because invoices always need specialists.
- D. A managed runtime, which automatically makes any design auditable.

<details>
<summary>Answer: B</summary>

The answer is B. This is a fixed, auditable path, so a workflow is the honest fit. A adds unnecessary freedom. C invents specialists you do not need. D is wrong: a managed runtime is a hosting choice, not a magic audit stamp.

</details>

### Agents and Workflows — question 2

A support agent's trace shows it calling the same search tool again and again, never stopping, until the time limit is hit. What is most likely missing?

- A. A larger model, which would just know when to stop.
- B. More tools, so it has something else to try.
- C. A termination rule for the tool-use loop.
- D. A CLAUDE.md file that only says, please be concise.

<details>
<summary>Answer: C</summary>

The answer is C. The pattern that is missing is loop termination. A bigger model or a polite instruction will not reliably stop a runaway loop. More tools can make the loop worse, not better.

</details>

### Agents and Workflows — question 3

The product must never send email to an address outside the company, even if the model agrees to do it. Where should that rule live?

- A. Only in the system prompt.
- B. In a deterministic pre-tool hook or permission check that blocks the send.
- C. In a log line written after the email has already gone.
- D. In a larger model, which is naturally more obedient.

<details>
<summary>Answer: B</summary>

The answer is B. A hook or permission check can stop the tool call itself. A prompt is not an enforcement layer. A log after the fact is too late. A larger model is not a guardrail.

</details>

## Prompt and Context Engineering (15%)

### Prompt and Context Engineering — question 1

A support session has been running for an hour. Old tool dumps fill the context, and the answers start to wander. What should you do first?

- A. Add the same dumps again, so the model can re-read them.
- B. Raise the temperature, so the model becomes more creative.
- C. Prune tool output, compact, or start a fresh session if the task is new.
- D. Disable tools, and ask the model to remember the dumps.

<details>
<summary>Answer: C</summary>

The answer is C. You restore intended behaviour by managing context, not by adding more noise. A makes bloat worse. B does not fix a full window. D throws away useful tools and asks the model to recall data it may already have lost.

</details>

### Prompt and Context Engineering — question 2

A policy assistant must answer only from a twelve-page staff handbook, cite the section it used, and say not found if the handbook is silent. What is the right pattern?

- A. Let the model use general knowledge, then cite if it feels confident.
- B. Ground in the handbook, require a citation, and return not found when it is silent.
- C. Hide the handbook, and hope the model memorised it.
- D. Always retrieve one random paragraph.

<details>
<summary>Answer: B</summary>

The answer is B. That is grounding and source citation, including a not-found path. A allows guessing. C is not grounding. D treats retrieval as a ritual, not a decision based on size, cost, and freshness.

</details>

### Prompt and Context Engineering — question 3

Structured output is turned on, but sometimes the model refuses, or hits a token limit, and the payload is incomplete. What must the application do?

- A. Parse whatever arrived, because structured output cannot fail.
- B. Validate against the schema, and parse defensively.
- C. Lower max tokens further, so failures become shorter.
- D. Ignore stop reasons; they only matter in batch jobs.

<details>
<summary>Answer: B</summary>

The answer is B. A schema is a contract you still have to check. A is the trap. C makes cut-offs more likely. D is false: stop reasons matter in realtime calls too.

</details>

## Model Selection and Optimization (12%)

### Model Selection and Optimization — question 1

You must extract dates from invoices with a two-second latency cap, and you want the cheapest tier that still meets a set quality bar. How should you choose?

- A. Always use the most capable tier.
- B. Always use the smallest tier.
- C. Test tiers against quality, latency, and cost on a regression set.
- D. Switch tiers at random in production.

<details>
<summary>Answer: C</summary>

The answer is C. That is model-tier selection against stated constraints. A ignores cost and latency. B ignores the quality bar. D experiments on live users without a plan.

</details>

### Model Selection and Optimization — question 2

A coding agent writes weaker plans when effort is set very low to save money. What is the right way to talk about this tradeoff?

- A. Effort settings do not change quality, only the font of the reply.
- B. Lower effort can cut cost and latency, but may hurt hard planning; measure it.
- C. Effort should always be set to the maximum.
- D. Effort replaces the need for a golden set.

<details>
<summary>Answer: B</summary>

The answer is B. Effort and thinking options change how much work the model does before it answers. You trade cost and speed against quality, and you prove it with evaluations. A is false. C is a blanket rule. D confuses a setting with a test harness.

</details>

## Eval, Testing, and Debugging (10%)

### Eval, Testing, and Debugging — question 1

You want to know whether a new prompt still answers forty known hospital FAQ cases correctly after every change. What should you build?

- A. Only a live chat window, watched when you remember.
- B. A golden set of those forty cases, run after each change.
- C. A new model; evaluations are only for research teams.
- D. A single manual try, then ship.

<details>
<summary>Answer: B</summary>

The answer is B. That is evaluation design with a golden set and regression. A is informal and incomplete. C is false. D is how regressions escape.

</details>

### Eval, Testing, and Debugging — question 2

An LLM as judge gives high scores to long, fluffy answers, and disagrees with your human labels. What should you do?

- A. Always trust the judge; a model is more consistent than a person.
- B. Calibrate the judge against human-labeled data, and watch for length bias.
- C. Delete the golden set, so the disagreement goes away.
- D. Raise the temperature on the judge.

<details>
<summary>Answer: B</summary>

The answer is B. A judge has to be calibrated, and length bias is a known failure. A is backwards. C hides the problem. D makes the grades noisier, not fairer.

</details>

## Tools and MCP (10%)

### Tools and MCP — question 1

A writing product needs a house-style checker: a set of rules and examples, not a live external API. Which mechanism fits best?

- A. An MCP server, because every capability should be a server.
- B. A Skill: reusable instructions and examples, not an external system.
- C. A built-in web-search tool.
- D. No mechanism is needed, because style cannot be specified.

<details>
<summary>Answer: B</summary>

The answer is B. A Skill is the right shape for packaged instructions. An MCP server is for connecting tools and data sources. Web search is not your house style. D is wrong: you can and should specify the style.

</details>

### Tools and MCP — question 2

A list-open-orders tool returns a twenty-page raw database dump, and the model starts to lose the thread. What should you change first?

- A. Shape the tool response into a short, actionable result.
- B. Raise max tokens, and keep sending the full dump.
- C. Delete the tool, and paste the dump into the system prompt.
- D. Switch MCP transport, which will automatically shorten the data.

<details>
<summary>Answer: A</summary>

The answer is A. Response shaping is part of tool design. B and C push more raw text into the window. D is false: the transport does not tidy your payload for you.

</details>

## Claude Code (8%)

### Claude Code — question 1

A rule must apply to every engineer who clones the repository, not just to you on your laptop. Where should it live?

- A. Only in your personal user settings, which are not checked in.
- B. In a shared project CLAUDE.md, or a committed Rules file in the repo.
- C. In a chat message you sent last month.
- D. In an environment variable that holds your API key.

<details>
<summary>Answer: B</summary>

The answer is B. Shared project files travel with the repo. A stays on one machine. C will be forgotten. D confuses a secret with a team instruction, and keys must not be stored in instructions anyway.

</details>

### Claude Code — question 2

The team wants every changelog written the same way from merged pull requests, and they want to share that method. They also need a separate control that blocks a push when tests have not run. How should those two needs be met?

- A. Use a hook for both, because hooks can also write prose.
- B. A Skill or command for the changelog; a hook for the push rule.
- C. A subagent for the push rule, and a hook for the changelog.
- D. Put both only in a system prompt on claude.ai.

<details>
<summary>Answer: B</summary>

The answer is B. The changelog is a repeatable method, so a Skill or command fits. The push rule must be enforced, so a hook fits. A and C swap the mechanisms. D does not ship with the repo, and is not an enforcement control.

</details>

## Security and Safety (8%)

### Security and Safety — question 1

A ticketing agent can issue refunds. A customer message claims to be the finance team and asks for a refund. A system prompt says never refund from a customer message. What is the most effective extra control?

- A. Rely on the prompt alone.
- B. Treat the ticket as untrusted; least privilege; a hook or human approval for refunds.
- C. Raise the temperature.
- D. Switch to a larger model, which cannot be injected.

<details>
<summary>Answer: B</summary>

The answer is B. Untrusted input plus least privilege plus a deterministic control is the layered defence the exam is pointing at. A is a prompt-only trap. C is irrelevant. D is false: a more capable model can still follow injected instructions.

</details>

### Security and Safety — question 2

A mobile app embeds an Anthropic API key in the client so the phone can call Claude directly. What is wrong, and what should you do instead?

- A. Nothing, if the key is written in a comment.
- B. The key can leak from the client. Proxy through your server; use scoped, rotated keys.
- C. Put the same key in a public CLAUDE.md file.
- D. Disable monitoring, so stolen use is quieter.

<details>
<summary>Answer: B</summary>

The answer is B. Client embedding is the defect named in the official skill. A comment does not hide a secret. C publishes it further. D makes a theft harder to see.

</details>

## Mixed mock quiz (eight questions)

### Mock question 1

A daily sales summary always runs the same three steps, and a research assistant must roam across unknown sources to answer new questions. Which pairing is right?

- A. An agent for the sales summary, and a workflow for the research.
- B. A workflow for the sales summary, and an agent for the open-ended research.
- C. A workflow for both, because agents are never allowed.
- D. An agent for both, because workflows are outdated.

<details>
<summary>Answer: B</summary>

The answer is B. Fixed, repeated steps are a workflow. Open-ended research is a better fit for an agent. A swaps them. C and D are blanket rules the exam will not reward.

</details>

### Mock question 2

After a prompt change, a travel bot still has to stay correct on a fixed set of fare questions that used to pass. What should run before you ship?

- A. No tests, if the new wording sounds clearer.
- B. The golden set, as a regression check.
- C. A production experiment on all customers at once.
- D. A switch to a new MCP transport.

<details>
<summary>Answer: B</summary>

The answer is B. A golden set exists exactly for this moment. A is hope. C is a risky way to discover a regression. D is unrelated.

</details>

### Mock question 3

A model must answer from a contract pack and say not found when the pack is silent. It instead invents a clause that sounds legal. What failed, and what do you require?

- A. Grounding failed; require pack-based answers, citations, and a not-found path.
- B. The model is too small; only Opus can avoid invention.
- C. Caching failed; add a breakpoint anywhere.
- D. Nothing failed; confident wording is a valid legal source.

<details>
<summary>Answer: A</summary>

The answer is A. That is grounding and source citation. B over-claims a tier. C is a different topic. D is dangerous, and wrong.

</details>

### Mock question 4

A client gets a rate-limit error and also, on a bad payload, an invalid request error. The code uses the same instant retry for both. What should change?

- A. Nothing, because all Claude errors are the same.
- B. Back off on rate limits, and fix or reject invalid requests.
- C. Retry invalid requests more quickly than rate limits.
- D. Convert both errors into a successful empty answer.

<details>
<summary>Answer: B</summary>

The answer is B. Distinguishing error classes is the resilience skill. A and C are how bills rise and defects linger. D invents success.

</details>

### Mock question 5

You are starting a brand-new task that has nothing to do with a long, messy session still sitting in the window. What is the cleanest next step?

- A. Keep the old session, even if the memories are irrelevant.
- B. Start a fresh session for the new task.
- C. Paste the entire old dump into the new prompt, twice.
- D. Disable logging, so the mess is harder to see.

<details>
<summary>Answer: B</summary>

The answer is B. A new task is a good reason to start fresh. A and C carry drift into the new work. D is not a context strategy.

</details>

### Mock question 6

An agent can read a catalogue, and it can also delete products. Most users only need to look up items. What is the least-privilege design?

- A. Give every session both tools, and ask the model to be careful.
- B. Lookup by default; reserve delete for a tighter permission, hook, or approval.
- C. Hide the delete tool's name, but leave it enabled.
- D. Put the delete key in the prompt, so only clever users find it.

<details>
<summary>Answer: B</summary>

The answer is B. Least privilege means the dangerous tool is not sitting there for every turn. A and C still leave the power on. D is not a control.

</details>

### Mock question 7

A team is about to move production from one pinned model version to a newer one. What should they do first?

- A. Switch everyone on Friday night, and watch social media.
- B. Run regression evaluations, then decide to move, adjust prompts, or wait.
- C. Delete the pin, and follow the latest alias forever.
- D. Change only the marketing site, not the model.

<details>
<summary>Answer: B</summary>

The answer is B. Release planning uses regression results. A is a gamble. C undoes pinning. D does not address the model change.

</details>

### Mock question 8

A useful internal knowledge base must be available to several Claude apps, and a platform team will maintain it in one place. Which mechanism fits?

- A. Copy the articles into every app's system prompt.
- B. Expose the knowledge base through a shared MCP server.
- C. A built-in calculator tool.
- D. A hook that blocks all reads.

<details>
<summary>Answer: B</summary>

The answer is B. A shared, independently maintained capability is a classic MCP fit. A will drift. C is the wrong built-in. D would prevent the access you need.

</details>

