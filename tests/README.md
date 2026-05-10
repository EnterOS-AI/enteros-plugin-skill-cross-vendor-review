# Test Rationale — molecule-skill-cross-vendor-review

## What this plugin does

`molecule-skill-cross-vendor-review` is a prose-only skill: its logic lives entirely
in `skills/cross-vendor-review/SKILL.md` (when to invoke, which PR types qualify,
how to run adversarial review). The adapter (`adapters/claude_code.py`) is a thin
re-export of `AgentskillsAdaptor` from `plugins_registry.builtins` — no business
logic, no network calls, no side effects.

## What is tested

- `plugin.yaml` is valid YAML with required fields (name, version, runtimes, skills)
- `skills/cross-vendor-review/SKILL.md` has valid YAML frontmatter and a body with
  required sections (When to Use, How to invoke)
- `adapters/claude_code.py` exists and re-exports `AgentskillsAdaptor`
- `validate-plugin.py` (`.molecule-ci/scripts/`) exits zero

## What is NOT unit-tested (and why)

The cross-vendor review logic requires calling an external LLM API (Claude + GPT/Gemini)
and comparing results — testing it requires integration with a real workspace runtime.
Smoke tests cover the artifact structure; full evaluation requires integration tests.

## Running tests

```bash
python -m pytest tests/ -v
```
