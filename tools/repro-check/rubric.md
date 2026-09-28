# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | The repro report's environment record (tool version, OS, install method), read against the issue's stated version/OS. | The report names the tool version, OS, and install method, and if the tested version differs from the issue's, the report says so explicitly rather than silently substituting it. | required |
| Steps followable | The repro report's input/setup and the exact command run. | The starting input and the command are unambiguous: shown verbatim in a code block, OR explicitly identified as the issue's own input used unchanged (restating its specific parameters), OR a self-constructed minimal input where the report names the exact structural property that triggers the bug (not just "a config file," but the specific field/shape that matters, matching what the issue names as the cause) — needed when the issue's own input isn't reproducible as given (e.g. it points to an external file or URL). Fails if the input is paraphrased or summarized without confirming it is unchanged and without naming the essential trigger, or the exact command is not shown. | required |
| Behavior matches the issue | The output/error artifact in the report's execution section, read against the issue's actual-behavior description. | Passes if either (a) the artifact shows the same failure class and root cause the issue describes, or (b) the report documents a good-faith attempt under the issue's real conditions and transparently states the behavior did not occur, naming what was tried and what differed from the reporter's setup. Fails if the artifact shows a different or unrelated failure that the report nonetheless treats as confirming the issue, or if no real attempt or artifact is shown at all. | required |
| Outcome stated honestly | The report's stated conclusion (Analysis/Actual), read against what the artifact it quotes actually shows. | The conclusion matches the artifact: no claim of confirming/reproducing the issue when the artifact shows a different or unrelated failure. An honest, evidenced cannot-reproduce passes this check. | required |
| Claim doesn't overcommit | The claim comment's text, read against the repro report when one is included alongside it. | The claim never promises a fix or a date. Any stated result ("reproduced," "could not reproduce," a suspected cause) is hedged in proportion to what's shown and consistent with the accompanying report, not asserted as unqualified certainty about root cause. | required |
| Conventions respected | The repo-facts block's contribution policy (especially any AI-disclosure requirement) and any comment-specific rules it states, read against the comment text. | If the repo's policy requires disclosing AI assistance, the comment discloses it; silence on a repo that requires disclosure fails this check. If the policy states other comment-specific rules (e.g. own-words requirement), the comment follows them. The intake bug-report template's fields (title, duplicate search, etc.) are for filing a new issue and are not required of a reproduction comment on an already-open one. | required |

## Verdict rule

Accept only if every required check passes. Any required check graded
`fail` or `unclear` yields reject. There are no `preferred` checks in
this rubric yet; if added later, they never change the verdict.
