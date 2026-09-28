# Voice guide: how I talk upstream

## Who I am in threads

I'm a first time contributor to this project. I haven't touched this
codebase before this issue, so I'm not going to speak like I know its
history or its maintainers' preferences. Readers should expect someone
careful and a little slow, not someone fast or authoritative. I'd
rather undersell what I've done than have a maintainer catch me
overselling it.

## Rules I write by

### Rule: promise the work, not the outcome

A claim comment says what I'm about to do, not what I already know the
answer is. I haven't reproduced anything yet when I post it, so it
can't sound like I have.

- Wrong: "I've looked into this and it's clearly an issue with the
  decoder."
- Right: "I'd like to look into this. I'll reply here once I've tried
  to reproduce it."

### Rule: say exactly what I tested, not what I assume

If I only tested one version, one OS, or one install method, I say
that and stop. I don't round up to "this happens on all versions"
because it would be convenient for the maintainer to hear that.

- Wrong: "This is broken across all recent versions."
- Right: "I tested on 4.53.3 via Homebrew on macOS. I haven't tried
  other versions or install methods."

### Rule: a failed reproduction is still a real update

If I can't reproduce it, I say so plainly instead of going quiet or
padding the comment to look more useful than it is.

- Wrong: "Still looking into this, will update soon" (when what
  actually happened is it didn't reproduce).
- Right: "I wasn't able to reproduce this with the steps in the issue.
  Here's exactly what I ran and what happened instead."

### Rule: no timelines I don't control

I don't know how long a fix will take before I've even confirmed the
bug, so I don't name one.

- Wrong: "I'll have a fix up by this weekend."
- Right: "I'll follow up here once I've reproduced it and know more."

### Rule: match the repo's own ask before adding my own flourishes

If the repo has a bug report template or a contribution policy, I fill
that in first, in its own terms, before adding anything in my own
words.

- Wrong: skipping the template's fields and writing a narrative
  version instead because it reads better.
- Right: filling in the template's fields, then adding a short note
  underneath if I have more context.

## Things I never post

- A claim that a fix is coming, or a date for one.
- A reproduction result stronger than what my own output actually
  shows.
- "Same as above, can confirm" on someone else's reproduction. If I
  didn't run it myself, I don't post it as mine.
- Confidence about a codebase I'm seeing for the first time.
