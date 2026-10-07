# Plan for #73: add OPENROUTER_API_KEY to .env.example

## Diagnosis

From my reproduction at f89c06f (posted on #73), the setup docs and the template disagree:

- `README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)`
- `docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)`
- After the Quick Start copy step, `grep -c "OPENROUTER_API_KEY" .env` printed `0`.
- The template's provider block is only:

      16:# LLM provider
      17-# Options: "mock" (default, no API key needed), "openai"
      18-LLM_PROVIDER=mock
      19-OPENAI_API_KEY=sk-your-key-here

- `core/config.py:20: openrouter_api_key: str = Field(default="")`, and `Settings()` resolved `openrouter_api_key -> ''`.

Two setup docs and the config declare the OpenRouter key; `.env.example` is the one file that leaves it out. So the template is the side to fix.

## Scope

In: add one `OPENROUTER_API_KEY=sk-or-your-key-here` line, with a one-line comment above it, directly under `OPENAI_API_KEY` in the `# LLM provider` block of `.env.example`. The placeholder follows the existing `sk-your-key-here` style.

Not in:
- `README.md` and `docs/SETUP.md` (they already name the key).
- `core/config.py` or any Python code.
- The `# Options:` line, the `LLM_PROVIDER=mock` default, and the `OPENAI_API_KEY` line.
- `OPENROUTER_BASE_URL` / `OPENROUTER_MODEL` (config.py already has defaults, and the docs ask only for the key).

## Files to touch

- `.env.example` (only)

## Approach

1. Branch `fix/73-env-example-openrouter-key` from `main` on my fork.
2. Insert these two lines after line 19 of `.env.example`:

       # OpenRouter key named in README Quick Start and docs/SETUP.md
       OPENROUTER_API_KEY=sk-or-your-key-here

3. Check `git diff --stat` shows 1 file changed, 2 insertions, no deletions.

## Test plan

Re-run my unit 2 repro steps unchanged on the branch, from a fresh `cp .env.example .env`:

- `grep -c "OPENROUTER_API_KEY" .env`: before `0`, expected after `1`.
- `grep -n -A5 "# LLM provider" .env`: before lines 16-19 only; expected after, lines 16-19 unchanged plus the comment and `OPENROUTER_API_KEY=sk-or-your-key-here`.
- `Settings()` check in `/tmp/prvenv`: before `openrouter_api_key -> ''`; expected after `openrouter_api_key -> 'sk-or-your-key-here'`.
- Same check: `llm_provider -> 'mock'` and `openai_api_key -> 'sk-your-key-here'` stay unchanged.

## Risks and unknowns

- I haven't confirmed which `LLM_PROVIDER` value, if any, selects OpenRouter at runtime, so I'm not adding `openrouter` to the `# Options:` line. If a maintainer confirms a value, that's a one-line follow-up.
- PR #77 also targets this issue and goes further (it documents `LLM_PROVIDER=openrouter`). My change is narrower; if maintainers prefer #77's direction, mine can be dropped.
- I never started the app or called a provider, so this fixes the setup template only, not runtime behavior.

## Deviations

None. The build matched the plan: one commit (4826698) adds the comment line and `OPENROUTER_API_KEY=sk-or-your-key-here` after line 19 of `.env.example`, 1 file changed, 2 insertions. The re-run repro gave the expected results: grep count 0 -> 1, `openrouter_api_key` '' -> 'sk-or-your-key-here', `llm_provider` and `openai_api_key` unchanged.
