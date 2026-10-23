# Loose-ends checks

Use these checks in `om-doctor loose-ends` after building the evidence map.
Apply only requirements the repository actually declares. For each suspected
gap, search for an explanation, exception, superseding decision, or existing
follow-up before calling it a mismatch.

| Area | Check | Avoid this false conclusion |
|---|---|---|
| Scope and decisions | Active rules, non-goals, and approved decisions agree with specs and implementation. Changes have the required superseding record and approval. | A proposed decision is binding; an old decision was silently replaced by newer code. |
| Specs and code | Acceptance criteria map to actual behavior and relevant tests. Separate planned, partial, implemented, merged, and released scope. | A spec PR implements the feature; a function name or checkbox proves completion. |
| Backlog identity | Source path plus full `Backlog id:` identify an item. Check `Backlog source:`, `Epic:`, `Story:`, dependencies, and the local map against tracker records. | Two sources using `E01` are duplicates; an older unmarked record is invalid rather than needing verification. |
| Backlog coverage | Active, agreed scope has the tracking required by local rules. Search for duplicate or overlapping issues, work already covered by an open PR, and implemented work still listed as unstarted. | Every future idea needs a ticket now; a closed issue was necessarily completed. |
| Run plans | PR `Tracking plan:` links, Progress checkboxes, and loop Tasks/HANDOFF records agree with the diff and completion evidence. | An unchecked task is missing even though a later plan supersedes it. |
| Delivery gates | Labels, reviews, required CI, QA evidence, and tested head revision agree with the configured process. Check run-level state when individual checks may still be registering. | No failed checks means green; an old QA approval covers a new head commit. |
| Ownership and dependencies | Active claims and dependency links agree with the proposed work. Identify blocked work with no recorded unblock action or follow-up. | Age alone proves abandonment; `ci-monitoring` is an active implementation claim. |

Read source and tests at the relevant revision before asserting a behavior
mismatch. If only the current checkout is accessible, do not use it to prove
what an unmerged PR or a deployed release does. Never checkout or fetch a
different revision for this diagnosis.

When labels are disabled, do not report missing labels as violations. When the
repository has no Definition of Ready, do not impose one. When rules disagree,
quote both and ask for a decision instead of silently choosing a new policy.

Rank findings by consequence: blocked or unsafe delivery first, then incorrect
scope or completion records, then maintenance gaps. Give each finding a stable
reply-local id (`LE-01`, `LE-02`) for follow-up discussion. Preserve those ids
in subsequent replies; do not store them in a file. Combine duplicate symptoms
of the same cause. Keep questions separate from confirmed mismatches.
