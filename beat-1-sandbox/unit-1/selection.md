# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73

**Verdict output**

```
I have all the evidence needed. Let me grade each check.

---

**Grading Summary for https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73**

**Issue:** "README and `.env.example` disagree about which LLM API key to set"
Labels: `bug`, `docs`, `good first issue`, `tier-1` — Estimated effort: 1–2 hours

---

**maintainer-alive** — PASS
`Aburke225` committed on September 16, 2026 (6 days ago), well within the 90-day window.

**repo-in-use** — PASS
Repo is not archived; `Aburke225` made at least 3 commits on September 16, 2026 and additional commits on August 24 and August 20, 2026.

**newcomer-scope** — PASS
The issue asks for one bounded task: align `README.md` and `.env.example` so that `OPENROUTER_API_KEY` and `LLM_PROVIDER` options are consistent. No architectural decisions needed, no megaissue structure. Marked `good first issue` and `tier-1` by the maintainer.

**unclaimed** — PASS
No assignees, no comments, no open PRs. (House rule applied: student claim comments would not block in any case.)

**contribution-policy** — PASS
No `CONTRIBUTING.md`, `AI_POLICY.md`, or `AGENTS.md` found. The repo's own commit history shows a `claude` collaborator on recent commits alongside `Aburke225`, signaling AI-assisted work is already the norm. Silence passes per rubric guidance.

---

All 5 required checks pass → **ACCEPT**

> **Note on fit profile:** `scope.md` still has the placeholder text. The skill cannot rank by fit without it — you may want to fill that in for future multi-candidate evaluations.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73",
  "checks": [
    {
      "name": "maintainer-alive",
      "grade": "pass",
      "evidence": "Aburke225 committed on 2026-09-16 (6 days ago), within 90-day window"
    },
    {
      "name": "repo-in-use",
      "grade": "pass",
      "evidence": "Repo not archived; Aburke225 has commits on 2026-09-16, 2026-08-24, and 2026-08-20"
    },
    {
      "name": "newcomer-scope",
      "grade": "pass",
      "evidence": "Single bounded task: align README.md and .env.example on OPENROUTER_API_KEY and LLM_PROVIDER; labeled good-first-issue and tier-1, 1-2 hr estimate"
    },
    {
      "name": "unclaimed",
      "grade": "pass",
      "evidence": "No assignees, no comments, no open PRs against this issue"
    },
    {
      "name": "contribution-policy",
      "grade": "pass",
      "evidence": "No CONTRIBUTING.md, AI_POLICY.md, or AGENTS.md found; repo's own commits include a 'claude' collaborator, indicating AI-assisted work is accepted"
    }
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Smoke run, `--limit 3`, initial rubric: `agreement: 3/3 scored items`
2. Full run, initial rubric (5 checks, including `contribution-policy`): `agreement: 18/20 scored items  (bar: 18/20: PASS)`
3. Partial re-check after tightening the `newcomer-scope` pass condition, `--only issue-01,issue-19,issue-15,issue-20`: `agreement: 3/4 scored items`
4. Partial re-check on the remaining `scope`-category rejects, `--only issue-05,issue-10`: `agreement: 2/2 scored items`
5. Final full run (committed as `eval-run.txt`): `agreement: 19/20 scored items  (bar: 18/20: PASS)`

**Issue analysis**

Issue: `issue-19`. Gold label: `accept` ("maintainer-diagnosed performance bug with named causes, unclaimed"). My rubric's verdict: `reject`, failed on `newcomer-scope`, with evidence: "Two causes are listed as 'potential' (unconfirmed hypotheses); additional suggestions include multi-processing and threading — no settled spec, unresolved architecture/concurrency decisions required."

The issue lists two possible causes for a UI freeze plus three "additional suggestions" for how to fix it, without committing to one approach. My rubric's `newcomer-scope` check requires a settled spec, so it read the unpicked-among suggestions as an open architecture decision. The gold label treats the maintainer's diagnosis of the causes as enough scoping on its own, even though the exact implementation approach isn't chosen yet. That's a real, defensible difference in where the two readings draw the "settled enough" line, not a bug in either one.

**Check rationale**

`newcomer-scope`, as currently written in `rubric.md`: "Issue has a settled spec: a defined outcome and a fully specified set of concrete steps to reach it, even if that spec names several files or several causes to fix. Fails only if the issue is a self-described tracking issue or codebase-wide umbrella, requires an unresolved architecture/design/product decision (including a one-line feature request with no spec), or shows a history of unresolved debate or repeated unsuccessful implementation attempts (e.g., abandoned PRs) indicating substantially greater complexity than the issue description suggests."

It's written this way because an earlier version failed two `clear-accept` issues that touched multiple files or named multiple causes (a docs task updating four pages, and issue-19's two-cause bug) even though each had a fully specified plan. The rewrite draws the line at whether the spec is settled, not at how many files or causes it touches, so multi-part-but-fully-defined work stops reading as "broad" while genuine megaissues, no-spec wishes, and abandoned-PR history still fail.

**Trade-offs**

The rewrite fixed the docs-task false reject (`issue-01`) and left the four `scope`-category true rejects (`issue-05`, `issue-10`, `issue-15`, `issue-20`, all re-checked with `--only` after the change) unaffected. The case it still gives up is `issue-19`: an issue where causes are diagnosed but not yet committed to one fix approach reads as "unresolved" under my check's settled-spec wording, even though the gold label treats that level of diagnosis as sufficient. I'm accepting that miss rather than loosening the wording further, since loosening it enough to catch issue-19 risks pulling in issues that are genuinely still undecided.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. This is a docs/config fix touching two files with no logic changes, so it fits the time I actually have and lines up with wanting an efficient, low-risk first issue rather than something that eats a weekend figuring out unfamiliar code.
2. The verdict correctly caught that it's unclaimed and bounded to two named files. What it can't weigh is that I'd rather spend my first issue building confidence in the whole workflow (claim, fix, PR) than in debugging tricky logic, so a low-risk pick is the right call for me right now even though the skill only ranks by scope/effort, not by that kind of personal reasoning.
3. Low difficulty: it's a matter of confirming which environment variable name is actually correct in the code and making the README and `.env.example` agree with it. The main risk is just making sure I pick the right source of truth, not any unfamiliar tooling or setup.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
