# Contributing to Zuma

Zuma is a personal device mesh built in phases. Every change starts as an issue and lands through a reviewed pull request.

## 1. Where work lives

| Repository | Responsibility |
|---|---|
| `zuma` | Meta repo: project docs and shared process |
| `zuma-protocol` | Wire format, framing and message envelopes |
| `zuma-core` | Engine: transport, identity, membership, replication, rules |
| `zuma-desktop` | Desktop shell (Slint) |
| `zuma-android` | Android client (Kotlin) |
| `zuma-landing` | Public website |

- Issues live in the repository they touch.
- Milestones map to phases: **F0 Seams**, **F1 Sovereign minimum**, **F2 Optimize**, **F3 Empower**.
- Labels describe area and state (`area:*`, `blocked`, `good first issue`). Read the issue for acceptance criteria before starting.

## 2. Claiming work

1. Pick an issue that is **ready**: it states the goal, acceptance criteria, tests and dependencies.
2. Assign yourself. One issue in progress per person (WIP = 1); take a second only if the first is `blocked`, and say so in a comment.
3. If you are blocked, add the `blocked` label, comment what you need, and move to another ready issue.
4. If the issue is unclear, ask in the issue before writing code. Ambiguity is cheaper to fix there than in review.

## 3. Branches and commits

- Branch from `main`: `<type>/<issue-number>-<short-slug>` (e.g. `feat/5-transport-skeleton`).
- Commits follow [Conventional Commits](https://www.conventionalcommits.org/): `feat(protocol): ...`, `fix(core): ...`, `test(...)`, `docs(...)`, `refactor(...)`, `chore(...)`.
- One logical change per commit. Do not mix unrelated work.
- Keep branches short-lived. Rebase on `main` when needed; do not merge `main` into a feature branch just to update it.

## 4. Pull requests

- One PR per issue. Link it with `Closes #<n>`.
- Target **≤ 400 changed lines**. If the change is larger, split it into reviewable PRs that each leave the build green.
- Describe:
  - **What** changed.
  - **Why** (link the issue and any decision).
  - **How it was tested** (commands and new tests).
  - **Risks and out of scope**.
- Self-review before requesting review: read your own diff, remove debug code, run the checks locally.
- Rust checks, from the crate directory:
  - `cargo fmt --check`
  - `cargo clippy --all-targets -- -D warnings`
  - `cargo test`

## 5. Review doctrine

The other developer reviews; **the author never approves their own PR**.

Reviewer checklist:

1. **Scope** — matches the issue and acceptance criteria; no unrelated changes.
2. **Correctness** — edge cases, error paths, invariants; no `unwrap`/`expect` in production code.
3. **Tests** — happy path and failure or rejection paths; a test would fail if the behavior regressed.
4. **Design** — names, ownership, layering; fits the current phase and the project seams.
5. **Docs** — rustdoc or README updated when behavior or public API changes.

Feedback:

- Mark blocking comments as **must**; non-blocking suggestions as **nit**. If it is not blocking, say so.
- Review the code, not the person. Explain the reason, not just the request.
- Approve only when you would be comfortable maintaining the code.

Merge:

- After one approval and green checks. The author merges (squash or rebase; no merge commits on `main`).
- Delete the branch after merge.

## 6. Definition of Done

An issue is done when:

- Acceptance criteria are met.
- Checks are green.
- Tests cover the new behavior and its failure paths.
- Public API or behavior changes are documented.
- Follow-up work discovered along the way is filed as a new issue, not left as a TODO.
- The PR is merged and the issue is closed by it.

## 7. Reporting

"Specified", "implemented" and "verified" are different states. Say which one you are reporting. Numbers come from a run you just did, not from memory.

## 8. Decisions

Decisions that affect both developers (formats, protocols, identity, storage) are written down before implementation — in the issue itself or a short decision note — with context, alternatives and consequences. If a decision changes later, update the note instead of relying on chat history.

## Questions

Open an issue or comment on the relevant one. Keeping questions and decisions in the repository makes them searchable and durable.
