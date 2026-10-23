# Text reports

Use these shapes for `om-doctor` replies. Omit empty optional sections. Keep all
material findings and coverage limits; do not write a separate full report.

## om-doctor specifics

## now-what

Lead with the recommended action and why it comes first.

- **Start now:** Target and action. Cite the evidence. State any satisfied
  prerequisite and what completion will look like.
- **Can run in parallel:** Name the actions that can run together and explain
  why they do not depend on or conflict with each other. Include ownership and
  shared-resource constraints. If none qualify, say so in one sentence.
- **Blocked:** Name the target, blocker, and smallest action or decision that
  removes it. Do not present a blocked action as ready to start.
- **Coverage:** Revision, examined scope and counts, missing or stale sources,
  and any checks not run. End with “No files or tracker items were changed.”

Do not fill a list with generic maintenance suggestions when the evidence shows
no useful next action. Say what was checked and what is still unknown.

## loose-ends

Lead with the most consequential mismatch, or “No confirmed mismatches found
in the inspected scope.” This is not a certification of repository health.

For each finding:

**LE-01 — Short, concrete title.** Mark it **Confirmed mismatch** or
**Needs verification**. State the repository rule or recorded expectation and
the observed state, with evidence links for both. Explain the consequence.
Give the smallest corrective action or verification step and a clear completion
condition. Link any existing issue or PR that already tracks it.

Put policy or scope choices under **Decision needed**, not in the defect list.
Include the conflicting evidence and the choice the user must make.

Finish with coverage as above. Offer to draft or file selected findings only
when useful. Wait for an explicit request; an offer does not start issue creation.

## STE-inspired English

- Use short sentences, normally no more than 20 words. Put one instruction in
  each sentence. Keep one term for each concept.
- Prefer active voice, common words, and concrete verbs: “Review PR 42” rather
  than “Perform a review activity.” Name the actor when it matters.
- Use “must” for a repository requirement, “can” for an available action, and
  “may” for uncertainty. Do not turn a recommendation into a requirement.
- Keep identifiers, paths, quotes, and technical terms exact. Explain an
  unfamiliar abbreviation once. Do not shorten away evidence or uncertainty.
- Avoid idioms, rhetorical questions, vague pronouns, and claims such as
  “everything is healthy.” Say what you inspected and what it shows.

This style is inspired by Simplified Technical English. Do not claim formal
ASD-STE100 compliance or impose its dictionary on repository identifiers.
