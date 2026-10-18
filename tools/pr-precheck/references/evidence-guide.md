# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives:**
- Eval bundle: the plan is under `## Plan context` (its named files, steps, "Not in scope" list, test plan, and any deviation note). The diff is under `## Candidate PR` → `### Diff`, and the claims to check are in `### Description` and `### Title`.
- Live: the plan is `plan.md` in the working directory, with `## Deviations` for changes made while building. The diff is `git diff main...HEAD` (and `--stat` for the file list); the claims are in `pr_draft.md` (title on line 1, description below).

**What good looks like:** every changed file and hunk falls inside the plan's stated files and scope, or a deviation note covers it, and every deliverable the plan promises appears in the diff or is plainly disclosed as deferred. Silent drift runs two ways: more than the plan (an extra flag or option, a rename pass, a rewrite of a file the plan never names) or less (a promised doc or test missing). The description is read against the diff here too: a description claiming "exactly as planned", "docs updated", or "no changes outside X" that the diff contradicts is drift.

## Test evidence (harness category: not-tested)

**Where it lives:**
- Eval bundle: `## Candidate PR` → `### Test evidence`, read against the repro evidence and test plan in `## Plan context`. The repo's stated checks are in `## Repo facts` (PR template asks).
- Live: `test_evidence.md` (the repro before and after, and the output of `make test-unit`, `make test-integration`, `make lint`, `make typecheck`), and the Testing section of `pr_draft.md`, read against `plan.md`'s test plan and your unit 2 repro steps.

**What good looks like:** the plan's own repro or named check is re-run on the changed code, with the command, a before result and an after result that differ observably. Every failure mode the test plan names is exercised, or its omission is disclosed. The repo's stated checks each show an outcome; a failure or a "no tests ran" shown honestly with its reason counts. "Tested locally" or "tests pass" with no output, a run of a control or unchanged path, and an added test that covers behavior the fix did not touch are not evidence.

## Diff quality (harness category: unreviewable)

**Where it lives:**
- Eval bundle: `## Candidate PR` → `### Diff` (every hunk) and `### Commits`.
- Live: `git diff main...HEAD` (every hunk), `git diff main...HEAD --stat` (the file list), and `git log main..HEAD --oneline`.

**What good looks like:** the fix is visible at a glance and nothing unrelated rides along. Debris tells: added debug prints or logging (`eprintln`, `print`, `console.log`), commented-out code or abandoned first attempts, functions or imports that are never used (including `allow(dead_code)`), added TODOs, and whitespace, re-indent, import-reordering, or reformatting hunks on lines the fix did not need to touch. Commit messages such as "wip", "fix", "misc cleanups while debugging" back up what the diff shows.

## Standards and comms (harness category: standards-wall)

**Where it lives:**
- Eval bundle: the repo's asks are in `## Repo facts` (the `pull requests:` line for PR template sections and checklist, and the `contribution policy` line for contributing rules and any AI-use policy). The PR's response is in `### Description`, and in `### Diff` for asks that must show up as changes (a changelog or whatsnew entry, a test, annotations).
- Live: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` in the repo (including its AI-use rules), read against `pr_draft.md`: every template section, each ticked box, `Closes #N`, and the Notes for Reviewers AI disclosure.

**What good looks like:** every template section has real content for this change, ticked boxes are true, the issue is referenced, and every ask the repo states is met either in the description or by a matching hunk in the diff. Where the repo states an AI policy, the description discloses the AI use in the student's own words, naming the tool and how it was used (in eval mode treat every package as AI-assisted). A section left blank or boilerplate, a false tick, a stated ask with no sign in the PR, or a required disclosure absent is a miss. If the repo states no template or no AI policy, nothing is owed; do not invent one.
