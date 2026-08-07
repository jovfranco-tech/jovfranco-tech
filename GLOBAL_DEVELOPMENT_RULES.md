# Global Development Rules

## Purpose
These rules apply to every repository owned by `jovfranco-tech`. They preserve the existing quality, security, evidence, PR, release and deployment controls while making GitHub Actions a scarce certification resource rather than the default development loop.

## Authority and release boundaries
- Work in an isolated branch.
- Prefer one consolidated Draft PR per mission or a clearly ordered stacked PR chain when isolation requires it.
- No auto-merge.
- CI success never authorizes merge, release or production deployment.
- Merge, release and production remain separate human-authorized actions.
- Changes must be small, reversible, backward-compatible where practical and auditable.

## CI cost governance — mandatory
Target: reduce GitHub Actions workflow executions by at least 90% versus the August 1–7, 2026 high-frequency baseline while preserving equivalent technical assurance.

1. **Local-first development loop**
   - Run lint, typecheck, deterministic unit/integration tests, build and focused smoke checks locally before pushing.
   - GitHub Actions is for remote certification/checkpoints, not iterative debugging.
   - Do not push known-red states merely to discover failures in Actions.

2. **One canonical quality workflow per repository**
   - Do not create a new workflow for each gate, workstream, bug fix, roadmap step or temporary experiment.
   - Fold reusable checks into scripts and call them from the canonical quality workflow.
   - Specialized workflows are allowed only when they have a durable operational purpose that cannot reasonably live in the canonical workflow.

3. **No CI on every development push**
   - Full remote CI should run only on explicit certification checkpoints: `pull_request` transition to ready-for-review, a deliberate `workflow_dispatch`, and/or integration to `main` as required by the repository.
   - Draft PR synchronizations are not a certification event.
   - If a ready PR head changes materially, re-certify explicitly rather than enabling unrestricted per-push CI.

4. **Concurrency cancellation is mandatory**
   - Every automatically triggered workflow must define `concurrency` with `cancel-in-progress: true` using a PR/ref-scoped group.

5. **Path filtering is mandatory where safe**
   - Documentation-only, metadata-only and unrelated-path changes must not trigger application CI/E2E suites.
   - Use `paths` / `paths-ignore` conservatively so required security or release checks are never bypassed.

6. **Heavy E2E is checkpoint-only**
   - Browser/Playwright, emulator, live-integration, full regression and other expensive suites run only for a final technical checkpoint or explicit manual dispatch unless a repository has a documented reason for continuous execution.
   - Prefer a small local or deterministic smoke suite during normal development.

7. **Eliminate duplicate work**
   - Do not duplicate `npm ci`, build, lint, Vitest/Jest, Playwright, security audit or packaging across overlapping workflows for the same commit.
   - Prefer a single job when parallelism would only multiply billing/minute-rounding and provides little quality benefit.
   - Reuse cached dependencies/artifacts only when the cache cost and complexity are justified.

8. **Use economical runners and limits**
   - Default to Linux (`ubuntu-latest` or a cheaper supported Linux runner where appropriate).
   - macOS/Windows runners require a technical need.
   - Every job must have a reasonable `timeout-minutes`.
   - Artifacts default to 1–7 day retention; evidence needing long-term retention should be summarized or stored outside Actions artifacts according to repository governance.

9. **No unnecessary schedules**
   - Remove or disable obsolete `schedule`/cron workflows.
   - Recurring workflows require a real operational dependency and the lowest useful frequency.

10. **Retry only what failed**
    - Do not rerun an entire workflow when a single failed job can be retried.
    - Infrastructure/network failures may be retried once after identifying them as external; repeated retries without diagnosis are prohibited.

11. **Legacy/one-off workflow hygiene**
    - One-off, temporary, migration, focused-fix and superseded gate workflows must be removed from the active `.github/workflows/` directory after their purpose is complete, or converted to explicit manual-only execution if they must be retained.
    - Historical workflow source may be archived outside `.github/workflows/` for auditability.

12. **CI change certification**
    - CI optimizations must not weaken the acceptance criteria of the product roadmap.
    - For each optimized repository, document: previous workflow count/triggers, new workflow count/triggers, checks preserved, checks moved local/manual, estimated execution reduction, and any residual risk.

## Standard certification sequence
1. Develop and validate locally.
2. Commit coherent checkpoints rather than microcommits solely to obtain CI feedback.
3. Keep the PR Draft while iterating.
4. Run a deliberate remote certification checkpoint when the increment is technically ready.
5. Record exact HEAD, commands/checks, CI result and preview/runtime evidence where applicable.
6. Do not infer merge/release/production authority from a green gate.

## Audit metric
Primary metric: workflow executions per repository per accepted increment.

Secondary metrics: billed runner minutes, number of active workflow files, duplicate installs/builds/tests, cancelled obsolete runs, and percentage of changes certified locally before remote CI.

Global objective: >=90% fewer GitHub Actions executions without reducing required technical evidence.