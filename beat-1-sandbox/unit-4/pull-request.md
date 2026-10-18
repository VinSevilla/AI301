# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/223

**Branch**

fix/73-openrouter-env-example

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

I only needed one full run. It scored 20/20 and every category matched, and that run is the one saved in `eval-run.txt`. After that I re-graded pkg-17 by itself with `--only` (1/1) so I could read its per-check results for the next section. That partial run doesn't change `eval-run.txt`.

**Package analysis**

I picked pkg-17 (silent-drift, vuejs/core#14893). My rubric said reject and the gold label is reject, so we agree. The check that failed was "Plan delivered and claims match". Its evidence line says: "Plan deliverable #2 (docs page update) is absent from the diff; description claims 'Implements the plan on #14893 in full' and 'the reactivity-core documentation now documents the limitation'". The plan promised two things, a dev warning and a docs update. The diff only has the warning and its tests, but the description says the docs were updated too, and nothing says the docs were skipped. "Diff within plan" passed because both changed files are in the plan, so that check alone would have missed it. That's why I made one check compare the description to the diff instead of only comparing files to the plan.

**Check rationale**

The check I picked is "Plan delivered and claims match". Its pass condition reads: "Every deliverable the plan promises is in the diff, or the plan's deviation note or the description plainly says it was deferred or changed and why. Every claim the description makes about the change is visible in the diff. A promised piece missing with no disclosure, or a description claiming something the diff does not contain, fails. An honestly disclosed deferral passes." I wrote it this way because drift can go two ways: extra work, or missing work with a description that sounds like everything got done. I kept the last sentence about honest deferrals because the assignment says a PR that admits what it left out shouldn't be punished. I also kept it separate from "Diff within plan" so extra hunks and missing promised work can't hide each other.

**Trade-offs**

I didn't change anything after my first full run, so I didn't loosen a check and didn't need canaries. The only extra run was the pkg-17 re-grade to read its results. One case I think my rubric could miss: a hunk inside a file the plan names that does something unrelated to the plan's purpose. "Diff within plan" asks if each file and hunk is covered by the plan, and a model could count that kind of hunk as covered because the file is named. I didn't test for it.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
