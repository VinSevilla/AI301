# Procedure: how this tool grades a PR package

## Read order

1. In live mode, first apply the scope and voice gates in `SKILL.md` (read `scope.md`, then `voice-guide.md`). In eval mode skip both.
2. Read the plan first, before the diff and before the description. Note: the files the plan names, its steps and deliverables, its "not in scope" list, its test plan, and any deviation notes (live: `plan.md` and its `## Deviations`; eval: the plan-context block). The plan is the yardstick, so it must be fixed in mind before anything is measured against it; reading the description first would let its claims colour how the diff is read.
3. Read the issue and the reproduction evidence (live: the issue thread; eval: the Issue, Thread highlights, and the repro evidence in the plan context). Note the reported behavior, the repro steps, and the expected result.
4. Read the repo facts: the PR template's sections and checklist, the contribution guide's asks, and any AI-use policy (live: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`; eval: the Repo facts block).
5. Read the diff next, on its own. List every changed file and, for each, what its hunks do. Note any hunk that looks like debris. Do not yet compare to the description.
6. Read the description last, then the test evidence. Note every claim the description makes about the change, and each outcome the test evidence shows.
7. Read every check and the verdict rule in `rubric.md`, then the matching section of the evidence guide. Do not add checks or change pass conditions.

## Evidence gathering

1. Diff within plan: put the diff's changed files next to the plan's named files and "not in scope" list. For each changed file, and each hunk within it, record whether the plan or a deviation note covers it. Record every uncovered hunk with its file and what it does.
2. Plan delivered and claims match: put the plan's deliverables next to the diff, and record any that the diff lacks. Then list the description's claims (Summary, Changes bullets, statements like "exactly as planned" or "docs updated") and look for each in the diff. Record each claim with no matching hunk and each plan deliverable that is missing. For each missing item, record whether the plan's deviations or the description discloses it.
3. Decisive test evidence: take the plan's test plan and the repro steps, and find the matching run in the test evidence. Record the command run, the before result, the after result, and whether the run exercises the plan's repro or a different path. Record each failure mode the test plan names and whether the evidence covers it. Note any test the diff adds and whether it exercises the changed behavior.
4. Repo checks run: list the checks the template and contribution guide name. For each, find its outcome in the test evidence or Testing section. Record the outcome, or that none is shown. Record honest failures with their stated reasons.
5. Clean diff: scan every hunk for debug prints or logging, commented-out code, unused functions or imports, added TODOs, and whitespace or re-indent or reformatting hunks on untouched logic. Record file and line for each. Read the commit list for "wip"-style messages.
6. Template and stated asks: put the description next to the template. Record each section and whether it has real content, each checkbox and whether it is ticked truthfully, and each stated ask (issue reference, tests, changelog entry, annotations) with where it is met in the description or diff.
7. AI disclosure: find the repo's AI-use policy. If one exists, find the disclosure in the description and record whether it names the tool and the extent of use. If no policy exists, record that.
8. Reviewable commits: read the commit messages and record whether each says what changed.
9. If a source is explicitly empty (for example no thread comments, or no stated AI policy), record that fact; never invent a request or requirement.

## Check execution

1. Grade every rubric row once, in rubric order, using the row's Evidence and Pass condition. Use the check name exactly as written.
2. Mark `pass` only when the gathered evidence shows the pass condition is met. Mark `fail` when it shows the condition is not met; content the condition requires that is absent from the package is a fail, not an unclear.
3. Mark `unclear` only when the relevant evidence is genuinely unavailable, ambiguous, or conflicting. Do not fill gaps with assumptions, and do not mark unclear to avoid a hard call.
4. Compare, don't trust: a check that depends on a claim (the description says "no changes outside the plan", the evidence says "all checks passed") is graded on the diff or output that backs the claim, never on the claim.
5. Honest disclosure re-ties a mismatch: if a gap between plan and PR is stated in the deviations note or the description, grade against what the PR says it delivers.
6. Judge outcomes, not length or polish. A short PR with thin prose can pass; a long, confident one can fail. Do not advise on how to rewrite the change.
7. Keep one concise evidence line per check naming the fact or quote that decided it, with its source. When a check's evidence is already fully gathered, grade it without re-reading the whole package.

## Verdict assembly

1. Confirm every rubric check has exactly one grade and one evidence line, with names matching the table.
2. Apply the verdict rule: accept only if every required check passes; reject if any required check fails or is unclear. Unclear on a required check counts as fail. Preferred checks never change the verdict; keep their grades in the output.
3. In the readable summary, quote the deciding check: the first failing (or unclear) required check in rubric order, with its evidence line. List the other failures after it.
4. In live mode, add any voice-guide rules the PR title or description breaks, and any procedure gaps found.
5. End with the fenced JSON block from `SKILL.md`: the item identifier (PR URL or bundle id), every check with its exact name, grade, and evidence line, and the verdict. Nothing follows the block.
