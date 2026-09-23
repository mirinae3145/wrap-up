---
name: wrap-up
description: >
  Closes out the current task: reconciles it with the actual project state,
  cleans up, re-verifies, reviews instruction adherence and workflow friction,
  and writes a closeout summary for resuming or handing off.
  Use only when the user asks to finish the work.
  Triggers
  include "wrap up", "마무리해", "정리하고 끝내자", "작업 마무리", "commit 전에 정리해".
metadata:
  version: "0.3"
---

# Wrap Up

Close the work already done; do not continue it. Anything outside the
original objective becomes a **follow-up** in the summary, not an edit.

**Scope**: the whole task, or for an orchestrator the integrated result. A
worker in a larger task closes only its own slice and leaves other workers'
files, repo-wide cleanup, and the "done" call to the orchestrator.

## Flow

1. **Inspect** — in every repository or location the task touched (not only
   the working directory): `git status`, `git diff` staged and unstaged,
   untracked files, outputs outside git, and external state changed (links,
   task trackers, services). Earlier "done"/"tested" claims are context; this
   state is evidence. Done when every change is accounted for.

1. **Reconcile** — objective vs. evidence: met, missing, and unrequested
   changes. Report missing work rather than completing it; list unrequested
   changes for the user to keep or revert.
   Review adherence and workflow friction using **Instruction and workflow review** below; keep these judgments separate from task completion.

1. **Clean** — only in the area the task worked in; classify each leftover:
   - **SAFE**: created during this task *and* disposable (scratch scripts,
     debug prints, temp or regenerable output). Remove it.
   - **REVIEW**: probably unneeded but not provably yours or disposable
     (older results, duplicates, pre-existing untracked files). Check
     references and provenance; recommend, let the user decide.
   - **PROTECTED**: raw or measurement data, hand-written or received files,
     unclear origin, anything another worker may use. Keep it.
   When unsure, pick the safer class.

1. **Update** — fix only documentation this task's diff made inaccurate, in
   existing documents. Inaccuracies that predate the task are follow-ups.

1. **Validate** — after cleanup, run the project's own checks covering the
   change and read `git status` again.

1. **Handoff** — write the summary below. Write a persistent handoff only
   when work continues later or changes hands, following the project's
   convention or else suggesting `/handoff`. Offer to record follow-ups via
   `todoist-task`.

Commit only when asked or by repository convention. Push, merge, release,
and remote branch deletion need explicit go-ahead in this session.

## Instruction and workflow review

Perform a retrospective within the closeout turn using the available conversation, tool results, and artifacts.
Do not introduce continuous logging, monitoring agents, or a separate audit workflow.
Review the applicable global instructions, repository rules, loaded skills (explicitly including this `wrap-up` skill), and other user-provided workflow requirements, including relevant instructions that should have been consulted but were missed.
Keep two independent judgments: whether the agent followed the applicable instructions, and whether those instructions supported the work effectively.
A compliant execution can still expose poor guidance; an execution failure does not by itself establish a guidance defect.
The boundary against continuing the task limits additional execution, not retrospective analysis or improvement proposals.

### Adherence

Evaluate actions against the instructions applicable at the time, accounting for scope, instruction priority, and authorized exceptions.
Do not classify following a higher-priority instruction as a violation of a lower-priority one.
Do not assume a conflicting request automatically authorized an exception where the applicable rules require more.
Distinguish confirmed adherence, noncompliance, authorized exceptions, and cases that cannot be determined from the available evidence.
Record material procedural violations even if later corrected, distinguishing the original event, recovery, and any remaining impact.

Current files and diffs establish present state, not the complete history of execution.
Do not infer adherence from a successful final result or missing evidence.
If earlier conversation, tool results, or the instruction version in effect are unavailable, state the resulting review limitation instead of reconstructing events or applying later rules retroactively.
Keep findings grounded in observable actions and results rather than an assumed account of internal reasoning.

### Workflow friction

Look for problems encountered in interpreting or following guidance and avoidable friction in the agent's working method, rather than difficulties intrinsic to the task.
Before deciding that there are no material findings, examine observed corrections of misunderstandings, failed approaches, and avoidable rework for their cause, impact, and possible improvement.
These incidents warrant consideration, not an automatic finding or a new rule.
Use categories only when they help explain an observed incident; do not fill a mandatory checklist or invent findings.
Consider, for example:

- Conflicting requirements, ambiguous or misleading wording, and mismatches between documented and actual behavior.
- Repeated exception requests as possible evidence that a default does not fit the user's work, rather than fault on the user's part.
  Limit frequency claims to the history actually available; a single exception does not establish a recurring pattern.
- Failed tool calls, distinguishing agent misuse, stale examples, unavailable tools, and transient environment failures before attributing a cause.
- Procedural overhead supported by observed duplicate lookups, redundant checks, or unnecessary confirmation requests, assessed against their benefit.
- Outdated guidance supported by a concrete incompatibility with the current environment or interface, rather than age alone.

For each material finding, identify the source or tool, the observed event and evidence, its impact, the confirmed or suspected cause, and a minimal improvement or further check.
Name the likely feedback recipient when known; do not invent ownership.
Separate observations from hypotheses and consolidate related incidents rather than listing every failed attempt.
Suggestions may clarify, simplify, or remove guidance; do not turn every isolated failure into a new universal rule.
When evidence points to agent execution rather than defective guidance, propose an improvement to the working method without attributing it to an instruction defect.

### Reporting boundary

Keep routine review brief and expand only material findings.
Assess materiality before compressing the report; retain enough of the event, impact, and improvement to explain a useful lesson even when the mistake was corrected.
Report adherence findings and workflow feedback separately from each other and from unfinished task work.
When no material findings exist, omit those sections; if the review was incomplete or could not be performed, report its scope and limitations instead of implying a clean review.
Avoid blanket compliance claims unsupported by the evidence.

The review may produce a feedback draft for the user or a maintainer, but does not itself authorize changing governing instructions, contacting maintainers, or filing external feedback.
Leave improvements outside the original task as follow-ups.
Do not automatically create a separate report or persistent incident log; use the closeout summary or an otherwise warranted handoff.

## Closeout summary

Markdown, not a code block (narrow panes break fixed-width columns).
Use one short finding per bullet, with enough evidence to make it actionable.
Leave out empty sections except required review limitations; keep table cells to a few words.
If a handoff document already exists, name it under **Artifacts** and list only what it does not already record.

```markdown
**Wrap-up** — <goal in one line>

**Done**

- <what is actually done, per the evidence>

**Changed / Artifacts**

- `<path>` — <what changed or is kept>

**Cleaned / Docs**

- <removed artifact> · <updated document>

**Validation**

| Check | Result |
|---|---|
| <check> | ✅ passed / ❌ failed / ⚠️ not run — <reason> |

**Instruction adherence**

- <material deviation or exception> — <applicable source, evidence, recovery or remaining impact>
- Review limits: <unavailable evidence and what could not be determined; omit if none>

**Workflow feedback**

- <source or tool> — <observed friction and evidence>; <impact>; <cause or uncertainty>; <minimal suggestion and recipient if known>

**Needs your decision**

- <REVIEW item, unrequested change, or open question> — <recommendation>

**Decisions**

- <choice that constrains later work>

**Remaining → Next**

- <unfinished item or follow-up>
- Next: <where the next session or colleague starts>
```
