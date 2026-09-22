# Rubric: is this a good first issue?

<!--

THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where.
   - Pass condition: a condition someone else could apply and get your answer.
   - Weight: `required` or `preferred`.

-->

## Checks

| Check            | Evidence                                                                                                              | Pass condition                                                                                                                                                                                            | Weight   |
| ---------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| maintainer-alive | Last 5 default-branch commits, including author usernames and commit dates                                            | At least one non-bot commit is within the last 90 days.                                                                                                                                                   | required |
| repo-in-use      | Repository archived status, latest release date, and recent non-bot development activity                              | Repository is not archived and has either a release or non-bot development activity within the last 90 days.                                                                                              | required |
| newcomer-scope   | Issue title/body, requested changes, affected components, linked sub-issues, maintainer comments clarifying scope, and any linked/attempted pull requests or implementation discussion on the issue | Issue has a settled spec: a defined outcome and a fully specified set of concrete steps to reach it, even if that spec names several files or several causes to fix. Fails only if the issue is a self-described tracking issue or codebase-wide umbrella, requires an unresolved architecture/design/product decision (including a one-line feature request with no spec), or shows a history of unresolved debate or repeated unsuccessful implementation attempts (e.g., abandoned PRs) indicating substantially greater complexity than the issue description suggests. | required |
| unclaimed        | Issue assignees, issue comments, and linked/open pull requests                                                        | No current assignee, no clear active claim in the comments, and no open pull request addressing the issue.                                                                                                | required |
| contribution-policy | Repository contribution guidelines, CONTRIBUTING file, and any documented AI-use policy | Repository does not explicitly prohibit AI-generated or AI-assisted code/documentation required for the contribution workflow. | required |

## Verdict rule

Accept only if 100 percent of required checks pass. Preferred checks do not affect the verdict but may be used to rank accepted issues. `unclear` counts as a fail.
