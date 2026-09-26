# Wrap Up

Wrap Up is an agent skill for closing a task with an evidence-based account of what changed, what was verified, and what remains.
Invoke it with `wrap up`, `마무리해`, or another explicit request to finish the work.
The execution rules live in [SKILL.md](SKILL.md).

## What to expect

The skill checks the actual project state, reconciles it with the task, removes disposable leftovers, updates documentation made inaccurate by the task, and runs relevant checks.
It reports missing work as follow-ups rather than continuing implementation during closeout.
Instruction adherence and workflow feedback are assessed separately from whether the task succeeded.

A useful retrospective describes observable behavior, its impact, and a concrete improvement or further check.
It should not end with self-blame or assume that one failure proves a defect in the user, environment, guidance, or model.
Recovered mistakes can still contain useful evidence.

When automatic context compaction hides earlier conversation or tool calls, the skill first tries to recover the relevant task history from existing local session records.
For Codex, it looks under `CODEX_HOME` (or `~/.codex`) and confirms the session identity before reviewing the omitted messages and tool results in manageable chunks.
This read-only review is independent of optional case recording and does not modify session logs.
If records are missing or incomplete, the summary states the remaining review limitations.

## Set up case accumulation

Persistent recording is optional.
Provide the arrangement in your request, applicable global instructions, project `CONTRIBUTING.md`, or an existing configuration available to the agent.
The skill does not prescribe storage paths or create repository-local instruction files.

Specify:

- Which stores are enabled: local, global, or both, with their locations and an explicit base for relative paths.
- Whether the agent should automatically record material cases during closeout or only propose entries.
- Whether each store is personal or shared, and any content restrictions.
- Any existing record format and Git tracking preference.

| Store | Purpose | Typical content |
|---|---|---|
| Local | Preserve project context | Relevant project guidance, expected and observed behavior, evidence, impact, recovery |
| Global | Compare across projects | Related case references, common conditions, hypotheses, mitigations, counterexamples |

Either store can be used alone.
Keep the original incident in one place and reference it elsewhere when useful.
Global relevance does not require copying private project details into the global store.

Once the arrangement authorizes recording, the agent can reuse it on later closeouts where that context is available.
Without a resolved arrangement, closeout still completes and leaves the candidate finding in its summary, with any storage limitation stated.
A conversation summary alone does not guarantee that a future session will retrieve it.

## Best practices

- Record material incidents and useful outcomes, not every tool call or routine success.
- Keep observations distinct from explanations; include model identity or version only when known and relevant.
- Search related records before adding a case, and update the same incident instead of counting a later review as another occurrence.
- Connect proposed mitigations to their subsequently observed results, including successful cases and counterexamples.
- Revisit hypotheses when evidence changes; preserve the original observation and explain the revised interpretation.
- Use stable case identifiers and durable evidence references, minimizing copied conversation text and private information.
- Treat repeated observations as grounds for comparison, not an automatic instruction change or proof of a model-wide tendency.

Recording happens during closeout, without background monitoring or a separate experiment workflow.
Selective records can support learning but cannot establish an overall failure rate.

## Optional Git exclusion

For personal records inside repositories, you can choose a common directory convention and exclude it through your global Git ignore configuration.
This avoids requiring a `.gitignore` edit in every repository.
If paths vary by project, a single global pattern may not be suitable; team-owned records may instead belong in Git.

Ask explicitly if you want the agent to configure exclusions.
It should inspect the existing configuration, preserve its contents, derive a pattern from your chosen record location, and check what the pattern excludes.
No global Git settings are changed merely by invoking this skill.
Ignore rules do not affect already tracked files and are not a privacy or access-control mechanism.

## AI disclosure

This skill is developed with AI assistance and is intended for use by AI agents.
Its reviews and cause analyses may be incomplete or mistaken; case records preserve evidence for later evaluation rather than certify a diagnosis.
