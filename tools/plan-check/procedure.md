# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

### What to read first

1. In live mode, first follow the scope and voice-guide gates in `SKILL.md`. In either mode, read the complete candidate plan and plan comment once without grading; note where the diagnosis, scope, proposed changes, test plan, risks or unknowns, and comment appear.
2. Read the issue context and the reproduction evidence. In live mode, use the issue thread and the student's accepted repro comment; for the house issue, use the house repro pack quoted in the drafts, and record if none is quoted. In eval mode, use only those sections in the package. Record the reported and reproduced behavior, expected result, actual result, and any control runs or limitations.
3. Read the repo-facts block, including relevant contribution guidance, test conventions, and disclosure requirements. In live mode, consult the corresponding repository documentation as directed by `SKILL.md` and the evidence guide.
4. Read every check and the verdict rule in `rubric.md`, then consult the matching evidence-guide section. Do not add checks or change pass conditions while grading.

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

## Evidence gathering

### How to gather the evidence

1. For each rubric row, identify the exact plan or package section named in its Evidence cell. Use the evidence guide to locate the equivalent source in live mode; in eval mode, do not fetch or use evidence outside the package.
2. For Diagnosis, extract the plan's cause and proposed fix. Compare them with the reproduced steps, actual and expected results, and controls; record evidence that supports or contradicts the cause and whether the fix targets that cause or only a symptom.
3. For Bounded scope and Executable approach, extract the in-scope work, exclusions, named files or areas, and implementation actions and order. Compare them with the diagnosis and repo facts; record unrelated work, open-ended scope, or material decisions left for the author.
4. For Observable test plan and Automated regression test, extract each proposed test or check and its expected result. Compare it with the reproduced behavior and the repository's stated test conventions; record whether the result would distinguish the reported failure from correct behavior and whether an automated regression test is proposed.
5. For Uncertainty and risks, collect the plan's assumptions, stated unknowns, risks, and deviation notes. Compare factual claims with the issue, repro, and repo facts; record any unsupported claim or unresolved uncertainty that could change the diagnosis or implementation, and whether a way to resolve it is given.
6. For Thread and repository fit, compare the plan comment with explicit requests or direction in the thread and applicable contribution, communication, and AI-disclosure requirements in the repo facts. In eval mode, treat every package as AI-assisted; when its repo policy requires disclosure, verify the comment names the AI tool and extent of assistance. In live mode, assess disclosure against actual AI use and repository policy. Record the specific request or requirement and whether the comment addresses it.
7. Keep a brief source-based note for each check. If a source is explicitly empty (for example, no thread comments), record that fact; do not invent a request or requirement.

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

## Check execution

### How to grade each check

1. Grade every rubric row once, using its stated Evidence and Pass condition and the evidence gathered above. Use the check name exactly as written in the table.
2. Mark a check `pass` only when the evidence shows its pass condition is met. Mark it `fail` when the evidence shows the condition is not met; missing plan content that the condition requires is a fail. For Automated regression test, mark `fail` when no automated regression test is proposed.
3. Mark a check `unclear` only when relevant evidence is genuinely unavailable, ambiguous, or conflicting and does not establish either pass or fail. Do not fill gaps with assumptions. An explicitly empty source is not by itself unclear: assess what the rubric requires from the sources that do exist.
4. Judge outcomes, not length, headings, or polish. Do not grade whether the plan is a good idea beyond the rubric's conditions, and do not advise how to implement or rewrite it.
5. For each grade, keep one concise evidence note naming the observed fact or quoting the decisive text and its source. Ensure the note supports that grade.

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

## Verdict assembly

### How to reach the verdict

1. Confirm that every rubric check has exactly one grade and an evidence note, and that each check name matches the table.
2. Apply the rubric's verdict rule: accept (ready) only when every required check passes. Reject (hold) if any required check fails or is unclear. Preferred checks do not change the verdict; retain their grades, including `unclear`, in the results.
3. Return the item identifier, every check's exact name, grade (`pass`, `fail`, or `unclear`), and concise evidence note in the JSON format required by `SKILL.md`. Set verdict to `accept` or `reject` according to step 2, and end with the fenced JSON block.

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->
