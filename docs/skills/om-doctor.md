# `om-doctor`

Interactive, read-only diagnosis. It returns text in the conversation and waits
for your next request. It does not change files or tracker items.

## Parameters

- `now-what` — the default. Suggests the next action and work that can run in
  parallel. Shows the evidence, prerequisites, and completion conditions.
- `loose-ends` — checks whether code, specs, backlog, and delivery records agree
  with the repository's rules. Separates confirmed mismatches from questions.
- `{scope}` — optional path, issue id, PR reference, or named area.

Examples:

```text
om-doctor now-what
om-doctor loose-ends
om-doctor loose-ends <spec-path>
```

Reports use STE-inspired English: short sentences, consistent terms, and clear
actions. Each report states its coverage and limits. An unscoped scan examines
up to 30 issues and 30 PRs. Missing configuration or tracker access does not
trigger setup; the report uses local evidence and states what it could not check.
The skill reads existing test results but does not execute tests or builds.

## Works with

Unlike `om-help`, which routes a question to an installed skill, `om-doctor`
compares repository state and linked work records before recommending action.
It never starts recommended work or emits an automatic dispatch marker.

After `loose-ends`, you can ask to file selected findings. That separate action
uses `om-prepare-issue --no-spec`, with its normal duplicate check and tracker
guards. It does not implement fixes or generate specs. If the companion skill
is not installed, you receive an issue draft in the reply instead.

---
*Source: [`skills/om-doctor/SKILL.md`](../../skills/om-doctor/SKILL.md)*
