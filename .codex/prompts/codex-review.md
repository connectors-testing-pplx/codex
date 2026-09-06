You are reviewing a pull request in this repository.

Load and follow the reviewer skills under `.codex/skills/` — in particular the
`code-review` orchestrator, which dispatches one sub-skill per review dimension,
and `code-review-runtime-evidence`, the Garnet Runtime Review consumer for this
repository.

Runtime grounding is mandatory for this repo. Before reporting, fetch the
Garnet Runtime Review record for the current PR head from the PR comments (see
`.codex/skills/code-review-runtime-evidence/SKILL.md` for the exact fetch
command and the fail-closed verdict table), bind it to the PR head, and emit the
single `Runtime evidence (Garnet, head <sha7>): ` utterance the skill requires.
Ground every dependency-change finding in that record; if the record is missing
or stale, say so and proceed evidence-blind.

Return findings as raw Markdown, one numbered block per finding, each with a
specific file path and line number where applicable. The runtime-evidence
finding is one block and may be the only finding on a trivial dependency bump —
that is the point: a diff-only reviewer has nothing to say there, and the
runtime record is the thing that can.
