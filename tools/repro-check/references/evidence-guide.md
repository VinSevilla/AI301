# Evidence guide: where proof lives in a reproduction package

## Environment

**Where it lives.** Eval bundle: the repro report's `**Environment.**`
line (or equivalent opening line), read against the issue block's
stated version/OS/install method near the top of the issue. Live mode:
the issue's original post on GitHub (version/OS fields, often from a
bug report template) against the student's draft report.

**What good looks like.** The report names a tool version, OS, and
install method. If the version tested differs from the version the
issue names, the report says so explicitly (e.g. "the issue was filed
against 4.53.2; I tested the current release") rather than silently
substituting a different version and treating it as equivalent.

## Steps

**Where it lives.** Eval bundle: the repro report's preparation/setup
section (the exact input given) and its execution section (the exact
command run). Live mode: the same two things in the student's draft
report.

**What good looks like.** One of three things:

1. The input is shown verbatim in a code block.
2. The report says explicitly that it reused the issue's own
   input/script unchanged (e.g. "the exact 12 lines from the issue,"
   or restating the issue's specific parameters like range offsets or
   file counts) so nothing is left for the reader to guess.
3. When the issue's own input isn't reproducible as given (it points
   to an external file, a URL, or a live service instead of inline
   content), a self-constructed minimal input that names the exact
   structural property causing the trigger — not "a config file" but
   "a `dependencies:` list plus a `category:` section, the section
   conda does not recognize," matching what the issue itself names as
   the cause.

A paraphrase with no confirmation of "unchanged" and no named trigger
property (e.g. "an object with an integer key," or just "a config
file") fails this even if the general shape is right. The command is
always shown verbatim, including any flags the issue itself used.

## Behavior shown

**Where it lives.** Eval bundle: the repro report's execution/output
section (the actual command output or error, usually right after the
command), read against the issue's "actual behavior" description near
the top of the bundle. Live mode: the same report section against the
issue thread's stated behavior on GitHub.

**What good looks like.** Either of two things counts as a pass:

1. The quoted output shows the same failure class and root cause as
   the issue describes (same error type, same underlying code path if
   named), not a superficially similar but different failure. Watch
   for a report whose input deviates from the issue's (wrong syntax,
   different flag, different data shape): a deviated input can produce
   a different error that looks like a "failure" but isn't the one
   being reproduced.
2. An honest cannot-reproduce: the report ran the issue's real
   conditions (or names precisely how its environment differed) and
   plainly states the behavior did not occur, rather than staying
   silent or padding the comment to look more conclusive than it is.
   This is a genuine, valuable result, not a lesser one — it fails
   only the checks that ask for a match to the issue's behavior, not
   this one.

What fails: an artifact showing an unrelated failure that the report's
own words nonetheless describe as confirming the issue (the report's
confidence outruns what it quotes), or no attempt/artifact at all.

## Honesty

**Where it lives.** Eval bundle: the repro report's concluding
analysis (often "Analysis"/"Actual"/"Expected" lines), read against
what its own quoted artifact actually shows. Live mode: the same, in
the student's draft.

**What good looks like.** The stated conclusion is no stronger than
the artifact it points to. A report that says "this confirms the bug"
while its artifact shows an unrelated error is claiming more than its
evidence supports — the mismatch is often invisible unless you reread
the artifact yourself rather than trusting the report's own summary of
it. An honest "I could not reproduce this" backed by a real attempt is
a pass, not a hedge.

## Comms

**Where it lives.** Eval bundle: the candidate claim comment, read
against (a) the issue it's replying to and (b) the repo-facts block's
contribution policy and bug-report template. Live mode: the student's
draft claim/repro comment against the issue thread and the repo's
CONTRIBUTING docs.

**What good looks like.**
- The claim never promises a fix or a date. Within that, it may
  honestly report a completed reproduction ("Reproduced this on
  4.53.3... report below") as long as the confidence is hedged to
  match what the accompanying report actually shows ("seems to be,"
  "my hypothesis is") rather than asserting a certain root cause the
  evidence doesn't support.
- If the repo-facts block states an AI-disclosure policy, the comment
  discloses AI assistance when it was used; silence on a repo that
  requires disclosure is a fail, not an unclear.
- The bug-report template's intake fields (title, duplicate search,
  "output of conda info/conda list") describe what an *original*
  bug report needs. A reproduction comment on an already-open issue is
  answering a different question ("does the bug hold up?") and is not
  scored against that template; its environment/step requirements are
  covered by the Environment and Steps checks instead.
