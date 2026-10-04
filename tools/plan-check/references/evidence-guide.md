# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

**Where it lives:** In an eval package, read the candidate plan's `Diagnosis` or cause statement and proposed change against `## Issue` and `## Repro evidence`, including the steps, expected and actual results, and control runs. In live mode, read the draft plan's diagnosis against the issue description and the student's posted repro comment; use the house repro pack quoted in the drafts for the house issue, as directed by `SKILL.md`.

**What good looks like:** The proposed cause explains the reproduced behavior and is not ruled out by a control or other package evidence. The planned fix addresses that cause, rather than a symptom or a different issue.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

**Where it lives:** In an eval package, read the candidate plan's `Scope`, named files or areas, and proposed changes; compare them with `## Issue`, the diagnosis, and `## Repo facts`. In live mode, read those parts of the draft plan against the issue and the repository facts gathered per `SKILL.md`.

**What good looks like:** The work is a bounded response to the reported problem. The affected files or areas and meaningful exclusions are clear, and unrelated rewrites or extra initiatives are not bundled into the fix.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

**Where it lives:** In an eval package, read the candidate plan's named files or areas, `Approach` or `Changes`, and their stated order, along with relevant facts in `## Repo facts`. In live mode, use the corresponding draft-plan details and repository documentation or conventions identified by `SKILL.md`.

**What good looks like:** A contributor can identify a concrete first action and proceed without asking the author to choose among material alternatives. Exact files or functions may be pinned down during work when the plan bounds the area and names an evidence-gathering action and decision that will resolve them; open-ended investigation with no decision path is not executable.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

**Where it lives:** In an eval package, read the candidate plan's `Test plan` against the exact steps, expected and actual results, and artifacts in `## Repro evidence`; use `## Repo facts` for stated test commands or conventions. In live mode, use the draft plan's test details against the student's posted repro evidence (or quoted house repro pack) and repository test guidance.

**What good looks like:** The proposed check exercises the reported behavior and names an observable result that distinguishes failure from success. “Run the full test suite” alone is not decisive; a manual repro can be decisive even when no automated regression test is proposed.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

**Where it lives:** In an eval package, read the candidate plan's cause, scope, assumptions, `Risks` or `Unknowns`, and any `Deviations` note against `## Issue`, `## Repro evidence`, and `## Repo facts`. In live mode, use the same draft-plan content and the issue, repro comment or quoted house repro pack, and repository facts. A deviation is relevant when one is recorded; its absence before implementation is not itself a problem.

**What good looks like:** Factual claims are supported by the available evidence. Any unresolved uncertainty that could change the diagnosis or implementation is acknowledged and paired with a reasonable way to resolve it; the plan does not present a contradicted assumption as certain.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

**Where it lives:** In an eval package, read `## Candidate plan comment` against `## Thread highlights` and the contribution policy, bug-report asks, and disclosure requirements in `## Repo facts`. In live mode, read the draft `comment.md` against the current issue thread and the repository's contribution documentation, templates, and AI-use policy.

**What good looks like:** The comment accurately summarizes the plan and responds to explicit maintainer or reporter direction instead of posting boilerplate past it. It follows applicable repository asks and disclosure rules; when no thread direction or policy requirement exists, do not invent one. In eval mode, treat every package as AI-assisted and require the comment to name the AI tool and extent of assistance when the repo policy requires disclosure. In live mode, assess disclosure against actual AI use and repository policy.
