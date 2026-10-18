# Plan: Add the documented OpenRouter key to the environment template

## Reproduction evidence

From my Unit 2 reproduction at commit `f89c06f`:

> Both `README.md` and `docs/SETUP.md` instruct readers to set `OPENROUTER_API_KEY` in `.env`. `.env.example` only defines `LLM_PROVIDER` and `OPENAI_API_KEY`; there is no `OPENROUTER_API_KEY` line to fill in. `core/config.py` confirms the app defines an `openrouter_api_key` settings field.

The documented `cp .env.example .env` step therefore creates a file with no entry for the key named by both setup guides. My reproduction establishes this template mismatch, not successful OpenRouter runtime support.

## Diagnosis

The setup template omits `OPENROUTER_API_KEY` even though both setup guides tell users to add that key and `core/config.py` declares the corresponding setting. The field declaration does not establish that the application currently wires an OpenRouter provider into review generation; I found no Python reference to the setting outside `core/config.py`.

## Scope

Make the copied environment template include the key named by the setup instructions, and add one small unit test that fails if the template loses that key again (`docs/CONTRIBUTING.md`: "Every code change should include or update relevant tests"). Do not change the documented `LLM_PROVIDER` options, README or `docs/SETUP.md`, provider behavior, or any other environment defaults. In particular, do not advertise `openrouter` as a selectable provider without evidence that the runtime supports it.

## Files

- `.env.example` (add the key)
- `tests/unit/test_env_example.py` (new; reads `.env.example` as text and asserts it has an `OPENROUTER_API_KEY=` line)

## Approach

1. Write `tests/unit/test_env_example.py` first and run `python -m pytest tests/unit/test_env_example.py`; it should fail against the current template (the before).
2. Add an empty `OPENROUTER_API_KEY=` entry directly after `OPENAI_API_KEY` in `.env.example`, matching the empty default in `core/config.py` and avoiding a fake credential.
3. Re-run the test (it should pass), then `make test-unit` and `make lint`.

Leave the existing provider options unchanged: the reproduction proves the missing key entry, but the tracked source does not establish that `LLM_PROVIDER=openrouter` is supported.

## Test plan

1. Run `grep -nE 'OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER' README.md docs/SETUP.md .env.example`. The setup guides should still name `OPENROUTER_API_KEY`, and `.env.example` should contain exactly one `OPENROUTER_API_KEY=` entry.
2. Copy `.env.example` to a temporary `.env` and run `grep -n '^OPENROUTER_API_KEY=' <temporary-file>`. It should print the new empty entry, demonstrating that the documented copy step gives users a place to set the key.
3. Confirm the `LLM_PROVIDER` options remain `mock` and `openai`; this change must not claim that OpenRouter is a supported provider.
4. Run `python -m pytest tests/unit/test_env_example.py`: it fails before the fix (no `OPENROUTER_API_KEY=` line) and passes after, so it would catch the template regressing.
5. Run `git diff --check` and confirm the diff changes only `.env.example` and the new test file.

## Risks and unknowns

The issue thread includes PR #77, which takes a broader approach and adds `openrouter` to the provider options. I have not found runtime wiring for that selector, so this plan does not adopt that claim. Whether the project intends to expose OpenRouter as a provider remains a maintainer question and is outside this one-line template fix; if maintainers require a runtime/provider change, this plan should be revised before implementation.

## Deviations

The build matched the plan: `.env.example` gained an empty `OPENROUTER_API_KEY=` line after `OPENAI_API_KEY`, `tests/unit/test_env_example.py` was added, and nothing else changed (`git diff --check` clean, no provider options touched). The test failed before the fix and passed after it.

One thing differed from my first pass: I originally could not run `make test-unit` or `make lint` because the dependencies (`structlog`, `ruff`) were not installed. I then installed them (`libcst` needed `--only-binary` because it has no Rust toolchain here) and ran all four template checks. Results are in `test_evidence.md`: `make test-unit`, `make lint` and `make typecheck` pass, and `make test-integration` stops with "no tests ran" because Path Review has no integration tests yet. CI has not run, because the PR is not open yet.
