# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

VinSevilla

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5874933341

Hi, I'd like to take this one as my first contribution. I'll compare README.md,
.env.example, and core/config.py to confirm exactly where the two docs disagree
on OPENROUTER_API_KEY and the LLM_PROVIDER options, and report back with what I
find before proposing the fix.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5875444891

### Environment

macOS (Darwin 24.6.0), fork `VinSevilla/pathreview-ai301-fa26-s1` at commit
`f89c06f` (`main`). This is a static docs/config comparison, not a version- or
platform-specific runtime bug, so no app boot is required to confirm it — the
same grep below reproduces identically on any OS with the repo checked out.

### Reproduction Steps

```
grep -n "OPENROUTER_API_KEY\|OPENAI_API_KEY\|LLM_PROVIDER" README.md docs/SETUP.md .env.example core/config.py
```

Output:

```
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
.env.example:18:LLM_PROVIDER=mock
.env.example:19:OPENAI_API_KEY=sk-your-key-here
docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
```

`core/config.py` doesn't use the uppercase env-var spelling directly (pydantic
lowercases field names), so a second grep confirms what the app itself actually
supports:

```
grep -n "openrouter_api_key\|openai_api_key\|llm_provider" core/config.py
```

```
18:    llm_provider: str = Field(default="mock")
19:    openai_api_key: str = Field(default="")
20:    openrouter_api_key: str = Field(default="")
```

### Actual behavior

Both `README.md` and `docs/SETUP.md` instruct the reader to set
`OPENROUTER_API_KEY` in `.env`. `.env.example` — the file a new contributor
actually copies via `cp .env.example .env` — only defines `LLM_PROVIDER` and
`OPENAI_API_KEY`; there's no `OPENROUTER_API_KEY` line to fill in. `core/config.py`
confirms the app does define an `openrouter_api_key` settings field, so this
isn't a stale reference to a removed option — it's a real gap in the env
template relative to what the app supports.

### Analysis

This confirms the issue as filed: README and `.env.example` disagree on which
key name to set, and `.env.example` is incomplete relative to what
`core/config.py` actually supports.

I didn't attempt to boot the full app for this — I hit two unrelated
environment failures partway through `make setup`/`make run` (ChromaDB 0.4.22
is incompatible with NumPy 2.0, and `libcst` needs a Rust toolchain to build on
Python 3.13 instead of the documented 3.11) — but neither is needed to confirm
this issue, since the disagreement is fully visible in the files themselves and
rerunnable with the grep above on a fresh checkout.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Final full run (committed as `eval-run.txt`): `agreement: 20/20 scored items (bar: 18/20:
PASS)`. Earlier iteration passes happened in a prior session; their intermediate scores
weren't retained, so this is the run I'm recording.

**Package analysis**

Package: `pkg-20` (`ghostty-org/ghostty#13604`, the `disclosure` category). Gold label:
`reject` ("ghostty's stated AI policy requires disclosing all AI usage and the comments do
not disclose"). My rubric's verdict: `reject`, failed on `conventions-respected`. The repro
report itself is excellent — real environment (Fedora 42, GTK/Wayland), an exact repeatable
trigger (`theme = Kitty Default` vs a conditional pair), and matching output artifacts for
both the broken and control case. But the repo's `AI_POLICY.md` requires disclosing any AI
assistance, and neither the claim nor the report comment discloses it. My `Conventions
respected` check reads the repo-facts block's policy against the comment text regardless of
how strong the technical proof is, so it fails the package on that basis alone — matching
the gold label exactly.

**Check rationale**

`Conventions respected`, as currently written in `rubric.md`: "If the repo's policy requires
disclosing AI assistance, the comment discloses it; silence on a repo that requires
disclosure fails this check. If the policy states other comment-specific rules (e.g.
own-words requirement), the comment follows them. The intake bug-report template's fields
(title, duplicate search, etc.) are for filing a new issue and are not required of a
reproduction comment on an already-open one."

It reads this way because `pkg-20` is otherwise a flawless reproduction — every proof-quality
check (environment, steps, behavior, honesty) would pass it — and a rubric without a
conventions check would wrongly accept it. The check is written to fail only on the
disclosure silence itself, not on the intake template's fields (title, duplicate search),
since those describe filing a new issue, not commenting on one already open — an earlier
draft that didn't carve that out risked failing reproduction comments for not following a
template they were never answering.

**Trade-offs**

Nothing changed on the confirming run — all 20 scored packages agreed, including the
single-item `disclosure` category (`pkg-20`), which is exactly the category the course flags
as the one "a rubric with no conventions check cannot buy back on volume." I know the floor
holds because the run's category line reads `disclosure 1/1`, not because I assume the check
generalizes.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
