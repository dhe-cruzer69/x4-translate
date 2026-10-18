# Engineering and GitHub Copilot Instructions

Repository: `x4-translate`. Source, tests, manifests, README, and workflows are authoritative; names and roadmaps do not prove implementation.

## Engineering and security
- Inspect relevant code, tests, manifests, configuration, and CI before editing. Preserve architecture, public interfaces, and unrelated work.
- Prefer small, reviewable patches. Avoid speculative abstractions, broad rewrites, and unnecessary lockfile churn.
- Validate input at trust boundaries; use least privilege, safe defaults, parameterized queries, and output encoding. Never commit credentials or secrets.
- Use explicit timeouts, bounded retries, idempotency where appropriate, and safe failure behavior for network, subprocess, model, and storage operations.
- Add deterministic regression tests for behavior changes, edge cases, failure paths, and security boundaries. Never weaken tests to obtain a green build.

## Model-assisted completion
1. Read acceptance criteria, existing implementation/tests, and instructions before coding.
2. Treat generated code and commands as untrusted proposals. Inspect commands before execution; never auto-run deployment, migration, destructive, or privilege-changing operations.
3. Reuse established APIs and patterns; keep diffs focused and avoid replacing entire files unnecessarily.
4. Validate syntax, types, schemas, authorization, injection surfaces, dependency changes, resource bounds, and error handling.
5. Run documented checks, inspect the final diff, and report each check as PASS, FAIL, NOT RUN, or BLOCKED with exact command/evidence. Never fabricate test, coverage, benchmark, security, or deployment results.
6. Bound repair attempts. If uncertainty remains, report UNKNOWN — HUMAN REVIEW REQUIRED.
7. Do not merge, deploy, delete data, change permissions/visibility, or write to the default branch without explicit task-specific authorization.

## Build, test, and CI
- Derive commands from README, CONTRIBUTING, manifests, lockfiles, package scripts, Makefile, and existing workflows; do not guess.
- Prefer reproducible lockfile-respecting installs. Run available lint/format, static/type checks, tests, and build/package validation.
- Keep CI least-privileged (`contents: read` by default), time-bounded, and concurrency-aware. Never mask failures with `|| true`, swallowed exit codes, or unconditional success fallbacks.
- Add workflow steps only for detected tooling and supported commands; pin third-party actions to reviewed immutable SHAs where practical.
- Codecov is opt-in: do not add an uploader or badge unless CI generates coverage and Codecov project/token/public-upload configuration is verified. Otherwise omit it.

## Evidence and review
Use a dedicated branch and reviewable PR; never merge automatically. Separate OBSERVED, VALIDATED, CORRELATED, and HYPOTHESIS. Report branch, PR, commit SHA, changed paths, exact checks/results, and unknowns. Mark unexecuted checks `NOT RUN — HUMAN REVIEW REQUIRED`.
