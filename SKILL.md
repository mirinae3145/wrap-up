---
name: wrap-up
description: >
  Closes out the current task: reconciles it with the actual project state,
  cleans up, re-verifies, and writes a closeout summary for resuming or
  handing off. Use only when the user asks to finish the work. Triggers
  include "wrap up", "마무리해", "정리하고 끝내자", "작업 마무리", "commit 전에 정리해".
metadata:
  version: "0.2"
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

2. **Reconcile** — objective vs. evidence: met, missing, and unrequested
   changes. Report missing work rather than completing it; list unrequested
   changes for the user to keep or revert.

3. **Clean** — only in the area the task worked in; classify each leftover:
   - **SAFE**: created during this task *and* disposable (scratch scripts,
     debug prints, temp or regenerable output). Remove it.
   - **REVIEW**: probably unneeded but not provably yours or disposable
     (older results, duplicates, pre-existing untracked files). Check
     references and provenance; recommend, let the user decide.
   - **PROTECTED**: raw or measurement data, hand-written or received files,
     unclear origin, anything another worker may use. Keep it.
   When unsure, pick the safer class.

4. **Update** — fix only documentation this task's diff made inaccurate, in
   existing documents. Inaccuracies that predate the task are follow-ups.

5. **Validate** — after cleanup, run the project's own checks covering the
   change and read `git status` again.

6. **Handoff** — write the summary below. Write a persistent handoff only
   when work continues later or changes hands, following the project's
   convention or else suggesting `/handoff`. Offer to record follow-ups via
   `todoist-task`.

Commit only when asked or by repository convention. Push, merge, release,
and remote branch deletion need explicit go-ahead in this session.

## Closeout summary

Markdown, not a code block (narrow panes break fixed-width columns). One
short line per bullet; leave out sections with nothing to report; keep table
cells to a few words. If a handoff document already exists, name it under
**Artifacts** and list only what it does not already record.

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

**Needs your decision**
- <REVIEW item, unrequested change, or open question> — <recommendation>

**Decisions**
- <choice that constrains later work>

**Remaining → Next**
- <unfinished item or follow-up>
- Next: <where the next session or colleague starts>
```
