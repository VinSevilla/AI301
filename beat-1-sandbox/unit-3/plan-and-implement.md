# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

VinSevilla

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5985284662

> I reproduced this at `f89c06f`: both setup guides name `OPENROUTER_API_KEY`, but `.env.example` has no entry for it; `core/config.py` declares the setting. My source check did not find application code wiring that setting into review generation, so I am not treating it as proof that `LLM_PROVIDER=openrouter` works.
>
> My plan is to add an empty `OPENROUTER_API_KEY=` entry to `.env.example` and leave its provider options and runtime code unchanged. I will also add a small unit test that fails when the template lacks that key (it should fail before the change and pass after), and verify the key is present after copying the template to a temporary `.env`. I saw PR #77's broader proposal; this plan is based on my own reproduction and does not assume that provider option is supported. If maintainers intend OpenRouter to be selectable, I would want that runtime direction confirmed before expanding the change.
>
> AI disclosure: I used Claude Code to help draft this plan and will use it to help write the change; I reproduced the issue myself and review every diff before keeping it.

---

## Your branch

**Branch**

fix/73-openrouter-env-example

**Evidence**

Before = the fix absent (branch `fix/73-openrouter-env-example` at the plan's start); after = commit `e82b608`. My Unit 2 repro grep, then the template copy check and the new regression test:

```
$ grep -nE "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" README.md docs/SETUP.md .env.example
docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
.env.example:18:LLM_PROVIDER=mock
.env.example:19:OPENAI_API_KEY=sk-your-key-here

$ python -m pytest tests/unit/test_env_example.py -q
F                                                                        [100%]
=================================== FAILURES ===================================
___________________ test_env_example_has_openrouter_api_key ____________________

    def test_env_example_has_openrouter_api_key():
        """README.md and docs/SETUP.md tell users to set OPENROUTER_API_KEY in .env."""
>       assert "OPENROUTER_API_KEY" in _template_keys()
E       AssertionError: assert 'OPENROUTER_API_KEY' in {'APP_ENV', 'DATABASE_URL', 'GITHUB_TOKEN', 'LLM_PROVIDER', 'LOG_LEVEL', 'OPENAI_API_KEY', ...}
E        +  where {'APP_ENV', 'DATABASE_URL', 'GITHUB_TOKEN', 'LLM_PROVIDER', 'LOG_LEVEL', 'OPENAI_API_KEY', ...} = _template_keys()

tests/unit/test_env_example.py:19: AssertionError
=========================== short test summary info ============================
FAILED tests/unit/test_env_example.py::test_env_example_has_openrouter_api_key
1 failed in 0.08s

=== AFTER the fix ===
$ grep -nE "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" README.md docs/SETUP.md .env.example
.env.example:18:LLM_PROVIDER=mock
.env.example:19:OPENAI_API_KEY=sk-your-key-here
.env.example:20:OPENROUTER_API_KEY=
docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)

$ cp .env.example <tmp> && grep -n "^OPENROUTER_API_KEY=" <tmp>
20:OPENROUTER_API_KEY=

$ python -m pytest tests/unit/test_env_example.py -q
.                                                                        [100%]
1 passed in 0.02s

$ git diff --check; echo "exit $?"
exit 0
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Run 1 (only full run): `agreement: 20/20 scored items (bar: 18/20: PASS)`. This matches the `agreement:` line in `eval-run.txt`, whose category line reads `clear-accept 7/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4`. I made no revisions after it, so there is no second score.

**Package analysis**

Package: `pkg-04` (`junegunn/fzf#4260`, category thread-convention). Gold label: `reject`, with the note "docs-only workaround plan whose comment never engages the owner's explicit direction in-thread: culprit isolated in src/tui/light_windows.go, patched test binary posted, testing requested". My rubric's verdict: `reject`, so it agrees. I re-graded just this package with `--only pkg-04` to see the per-check results; four checks failed:
- Diagnosis: "the proposed fix (documenting '> /dev/tty' workaround) does not address the identified cause (console input loop in src/tui/light_windows.go); it documents symptom bypass."
- Uncertainty and risks: the plan never says the owner already named the culprit and posted patch 8916cbc, or that a docs-only PR could be made obsolete by that fix.
- Thread and repository fit: the comment says "since the behavior has a reliable workaround, I plan to document it properly" with no acknowledgment of the owner's active code fix or request for testing.
- Automated regression test (preferred): no test proposed.
The reject is driven by the three required failures. Bounded scope, Executable approach and Observable test plan all passed, so the plan is tidy but built on the wrong response to the thread. My rubric reads the thread highlights against the comment, which is what catches it.

**Check rationale**

`Thread and repository fit`, as it reads in the uploaded `rubric.md`:

| Thread and repository fit | The plan comment, read against the issue thread or thread highlights and the repo-facts block's contribution guidance and conventions. | The comment addresses relevant maintainer or reporter requests and accurately describes the plan. It follows applicable repository requirements, including explicitly naming the AI tool and extent of assistance when disclosure is required; in eval mode, treat every package as AI-assisted. In live mode, assess disclosure against actual AI use and repository policy. | required |

It reads this way because the thread-and-convention category has only two packages (`pkg-04` and `pkg-20`), so a rubric that never compares the comment with the maintainers' own words would miss both. The Evidence cell names both sources, the thread and the repo-facts block, so the grader cannot grade the comment in isolation. The pass condition requires the comment to "address relevant maintainer or reporter requests", which is what `pkg-04` fails. The disclosure sentence says to treat every package as AI-assisted in eval mode, and in live mode to judge against actual AI use and repo policy, because the eval packages never say whether AI was used. I rejected a check on tone and politeness, since it would not distinguish the failing packages.

**Trade-offs**

This check gives up leniency toward a comment that is accurate but skips something a maintainer said in passing, and toward plans that do not cite the thread. It also depends on the thread highlights being faithful, because it can only fail a comment against what the package shows. In live mode it is judged against the real thread, so a missed late comment would not be caught. A case it will miss: a comment that acknowledges the thread in words but still plans the opposite action. Nothing else changed in my rubric after the first run: all 20 packages agreed and every category matched at least once (thread-convention 2/2), and I confirmed `pkg-04` again with `--only pkg-04`, which still rejected on this check, so I had no reason to loosen or tighten anything.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
