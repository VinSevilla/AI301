# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check                     | Evidence                                                                                                                                             | Pass condition                                                                                                                                                                                                                                                                                                                                                                  | Weight    |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| Diagnosis                 | The plan's stated cause and proposed fix, read against the issue context and the repro-evidence steps and results.                                   | The cause explains the reproduced behavior without contradicting it, and the proposed change addresses that cause rather than only suppressing a symptom.                                                                                                                                                                                                                       | required  |
| Bounded scope             | The plan's scope statement and named files or areas, read against its diagnosis and the repo-facts block.                                            | The work is one bounded change; the affected files or areas and meaningful exclusions are clear, with no unrelated or open-ended work included.                                                                                                                                                                                                                                 | required  |
| Executable approach       | The plan's implementation approach and order of work, read with its named files or areas and repo-facts block.                                       | A contributor unfamiliar with the issue can identify a concrete first action and proceed without asking the author to choose among material alternatives. Exact files or functions may be pinned down during work if the plan bounds the area and names an evidence-gathering action and decision that will resolve them; open-ended investigation with no decision path fails. | required  |
| Observable test plan      | The plan's test plan, read against the repro-evidence steps and results and the repo-facts block.                                                    | The plan names a check and an observable expected result that would distinguish the reported faulty behavior from correct behavior; it does not rely only on an unrelated or non-discriminating test.                                                                                                                                                                           | required  |
| Automated regression test | The plan's test plan and proposed test changes.                                                                                                      | The plan adds or updates an automated test that would catch the reproduced behavior regressing.                                                                                                                                                                                                                                                                                 | preferred |
| Uncertainty and risks     | The plan's stated cause, assumptions, risks, unknowns, and any deviation note, read against the issue context, repro evidence, and repo-facts block. | Claims are supported by the available evidence. Any unresolved uncertainty that could change the diagnosis or implementation is labeled and paired with a reasonable way to resolve it; pass when no such uncertainty is apparent.                                                                                                                                              | required  |
| Thread and repository fit | The plan comment, read against the issue thread or thread highlights and the repo-facts block's contribution guidance and conventions.               | The comment addresses relevant maintainer or reporter requests and accurately describes the plan. It follows applicable repository requirements, including explicitly naming the AI tool and extent of assistance when disclosure is required; in eval mode, treat every package as AI-assisted. In live mode, assess disclosure against actual AI use and repository policy. | required  |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept (ready) only if every required check passes. Reject (hold) if any required check fails or is unclear. Preferred checks never change the verdict; an unclear preferred check is recorded as unclear but does not block acceptance.
