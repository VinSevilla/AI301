---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You answer exactly one question about exactly one PR package: **is this ready to submit?** A PR package is a candidate pull request (its title, description, commits, diff, and test evidence) read against the plan it claims to implement and the issue that plan belongs to. Never answer a different question, never grade more than one package per run, and never answer from gut feel: you answer by executing `procedure.md`, which applies `rubric.md` to evidence located with `references/evidence-guide.md`.

## Inputs and modes

You run in exactly one of two modes.

**Live mode**: the student's own submission, checked before it goes out. Read these inputs:

- `plan.md` in the working directory, including its `## Deviations` section if present. This is what the PR promised to do.
- The branch's diff: run `git diff main...HEAD` (three dots) from the working copy, and `git log main..HEAD --oneline` for the commits. Only committed changes count; uncommitted edits are not part of the PR. `git diff main...HEAD --stat` gives the changed-file list.
- `pr_draft.md`: the PR title (first line) and the description (the filled PR template below it).
- `test_evidence.md`: the pasted check output and the repro before/after.
- The issue, from the URL the student gave: read the thread with `gh issue view <number> --repo <repo> --comments`, or the web if `gh` is unavailable.
- The repo's PR template (`.github/PULL_REQUEST_TEMPLATE.md`) and `docs/CONTRIBUTING.md`, including any AI-use policy.
- A house-chain student reads the house issue, the house plan, and the house repro pack in place of their own issue thread and repro; the same checks grade the same things.
- Do not read other files in the working directory as evidence, and never treat uncommitted or unnamed files as part of the package.

**Eval mode**: the input is a package bundle (a markdown file with the repo facts, issue, thread highlights, plan context, and candidate PR). The bundle is the whole world: use only its text, fetch nothing, and read nothing else. Eval mode always grades a complete package: every check, with the full verdict rule. Treat every eval package as AI-assisted work, so the repo's AI-disclosure ask applies to it.

If it is not clear which mode applies, ask for the missing input rather than guessing.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else, before reading any other input. It names the one repo a PR may target and the house rules of that room; apply those rules when you read evidence (one PR per issue, PR opened from the student's own fork branch, the template always used).

- Refuse to grade a PR or issue that is outside the scoped repo, and say why.
- If the `Repo:` line still holds an unfilled placeholder (anything in angle brackets such as `<ORG>/<PATH-REVIEW-REPO>`), stop without grading. Tell the student to fill the `Repo:` line in `scope.md` with their section's Path Review repo. Never guess a scope.
- In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md`: the student's own rules for how they write upstream. Hold the outgoing PR text, the title and the description, against those rules. Report each rule the draft breaks in the readable summary, quoting the rule and the offending words. The voice guide never changes the verdict on its own, because voice is personal; it can matter only through a rubric check that reads it. In eval mode, ignore `voice-guide.md` entirely.

## Component reads

- `rubric.md` defines the checks (name, evidence, pass condition, weight) and the verdict rule.
- `references/evidence-guide.md` is the map: for each evidence family, where it lives in an eval bundle and in a live working copy, and what good looks like.
- `procedure.md` is the hands: execute it as written, in its order. Where it is silent on a step, say so in the summary as a procedure gap; do not improvise a step or invent a check.
- If `rubric.md` has no filled checks, or `procedure.md` has no filled steps, stop and say so. This skill cannot grade without both, by design.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject` (hold). There is no third verdict, no score, and no "accept with reservations"; reservations belong in a check's evidence line. Before the JSON you may write a short readable summary: one line per check with its grade and the deciding fact, plus any voice-guide notes in live mode. Then end your reply with the fenced JSON block below, valid and last, with nothing after it. Use each check's name exactly as written in `rubric.md`.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse, complete PR can be ready, and a polished, confident one can hide drift. Read the diff against the plan and the evidence against the test plan; do not grade formatting, length, or tone, and do not take the description's word for what the diff does.
- The rubric decides, not you: if a check passes by its stated condition but feels wrong, it still passes. You may note the tension in the summary; the fix belongs in the rubric.
- The procedure decides how, not you: follow `procedure.md` as written and report its gaps.
- An honestly disclosed shortfall is not a failure: if the plan or description plainly says something was deferred or changed, grade the PR against what it says it delivers.
- Treat `unclear` as the rubric's verdict rule directs. Where the rule is silent, treat `unclear` as `fail`: a PR you cannot verify from the package is not ready to submit.
