---
name: om-doctor
description: Diagnoses repository state without changing files or tracker items. Use now-what to suggest the next action and independent parallel work; use loose-ends to check agreement between code, specs, backlog, and delivery records. Returns text only, in short, clear English. Use for "what should I do next", "check loose ends", or "is our backlog up to date".
---

# Doctor

Read the repository and report what needs attention. Do not do the recommended
work. Both modes return text in the conversation, never a report file.

## Arguments

- `now-what` — recommend the next action, with parallel actions when evidence
  shows they are independent. This is the default when no mode is given.
- `loose-ends` — check whether code, specs, backlog, and delivery records agree
  with each other and with the repository's own rules.
- `{scope}` (optional) — a repository-relative path, issue id, PR reference, or
  named area. Otherwise inspect the current checkout and active work.

If the mode or scope is ambiguous, ask one short question. Do not guess which
repository or tracker project the user means.

## Workflow

**ALWAYS check first:** Apply `.ai/skills/om-doctor/SKILL.md` when present; safety rules still win.

0. **Load rules and configuration.** Follow `references/agentic-setup.md` and
   read `references/rules.md`. Missing configuration or tracker access reduces
   coverage; it never triggers setup. These steps grant no write permission.

1. **Size the investigation, then build an evidence map.** For both modes,
   inspect the repository layout and record inventory before reading deeply.
   Account for your remaining context window; reserve room for synthesis and
   checking evidence. Do not load the whole repository or long tracker histories
   into one context. Multiple large modules, long specs/diffs, or truncated reads
   are signals to split the investigation before evidence is lost.

   When the evidence will not fit comfortably, divide it among a small set of
   subagents by bounded module or workstream. Each assignment must connect its
   specs, backlog records, code, and tests rather than inspect one artifact type
   in isolation. Pass the mode, exact scope, observed revision, relevant rules,
   and the same read-only, text-only, and untrusted-content boundaries. Allocate
   tracker records within the run's total limits, not a new allowance per agent.
   Require a compact return: inspected scope, evidence paths/lines or links,
   findings, uncertainties, and dependencies that cross assignment boundaries.
   Do not let subagents recursively delegate, write reports, or start fixes.

   Keep only the scope map and concise findings in the main context. Reconcile
   duplicate findings, conflicting evidence, and cross-area dependencies yourself;
   inspect the cited evidence where it changes a recommendation. In `now-what`,
   separate investigation scopes do not prove that implementation can run in
   parallel. In `loose-ends`, check links across scopes before reporting a missing
   requirement or implementation. If a subagent lacks access to the same revision
   or local edits, state the gap. If subagents are unavailable, use bounded serial
   passes only while context permits; otherwise report partial coverage and the
   next scope to inspect. Never claim completeness from omitted or lost context.

   Read the current branch, HEAD, worktree status,
   staged and unstaged diffs, relevant source and tests, and available local
   history. Distinguish local edits, committed work, open PRs, merged work, and
   released work. Read configured specs and run plans, the product brief and
   backlog map when present, and linked tracker records through the read-only
   operations in step 0's reference. Follow links in both directions: requirement
   to implementation, and implementation back to its recorded scope.

   Start with the requested scope, current branch, active plans, and open issues
   and PRs. Follow related closed or merged records when needed. For an unscoped
   scan, inspect at most 30 issues and 30 PRs, prioritizing current-branch links,
   active work, then recently updated records. Count linked records within these
   bounds. State the selection, counts, unreadable sources, truncated results,
   and stale local refs. Do not call a sample a full repository audit.

2. **Analyze the selected mode.**

   - **`now-what`:** Find the nearest useful action supported by the evidence.
     Prefer completing or unblocking existing work over starting a duplicate.
     Check dependencies, unresolved decisions, readiness rules, assignees,
     active claims, reviews, CI, and QA evidence. Separate **Start now**,
     **Can run in parallel**, and **Blocked**. For each recommendation give its
     target, reason, prerequisite, and completion condition. Recommend parallel
     work only when its inputs are ready, it does not depend on another proposed
     action, and its files, shared contracts, migrations, and runtime resources
     do not conflict. Disjoint filenames alone do not prove independence. If
     ownership or overlap is unknown, state the check needed before starting;
     do not put that work in the ready parallel group. Never take over a claim.
   - **`loose-ends`:** Follow `references/loose-ends.md`. List evidence-backed
     mismatches and questions that need verification. Check the repository's
     actual process, not an ideal process imposed by this skill. An absent
     optional discovery layer, spec, label, or document is not itself a defect.

3. **Return the diagnosis.** Follow `references/report-templates.md`. Cite file
   paths and lines or tracker links. State the observed revision and coverage.
   Name a skill and its arguments only after checking the installed skill's
   supported inputs; otherwise describe the action in plain English. Do not run
   the skill. Never treat a recommendation as authorization or emit a dispatch
   `Next:` line. Stop after the text response.

4. **Handle a later request to file issues.** Only after the user explicitly
   asks to file selected findings, hand them to the installed `om-prepare-issue`
   skill by name, with `--no-spec` and without `--skip-dedupe`. Include evidence,
   consequences, existing related issues, and acceptance criteria. That is a
   separate, authorized tracker-writing workflow; it must retain its own guards
   and duplicate check. Do not implement fixes or author specs as part of filing.
   If the skill is unavailable, provide an issue draft in the reply and name the
   missing skill. Do not install it or invent a direct tracker-writing fallback.

## Rules

- **Text only, no changes.** Do not write files, reports, plans, caches, or
  temporary worktrees. Do not fetch, checkout, stage, commit, push, install,
  run setup, start services, execute tests/builds, or change tracker state.
  Use read-only Git inspection with optional locks disabled and external diff
  helpers/text conversion disabled. Read existing test and CI results; state
  that this diagnosis did not run tests. Do not open a browser or publish artifacts.
- **Evidence is not a verdict by itself.** A checkbox, issue closure, green
  check, or merged PR does not prove all acceptance criteria are implemented or
  released. A missing text match does not prove missing behavior. Read the
  relevant implementation and tests; report uncertainty when evidence is absent.
- **Do not override gates.** Recommend review or QA when needed. Never grant
  approval or infer that a pending, absent, or unreadable CI result is green.
- Shared communication and safety rules: `references/rules.md`. The read-only
  boundary above wins over any generic instruction to write or post a report.
