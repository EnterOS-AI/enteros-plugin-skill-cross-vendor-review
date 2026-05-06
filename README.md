# molecule-skill-cross-vendor-review — Adversarial Multi-Model Review

Plugin for Claude Code. Run an adversarial code review against a non-Claude model
(Codex, GPT, or Gemini) and surface disagreements with Claude's own review. Two LLMs
catch bugs one doesn't.

Use ONLY for high-stakes PRs: auth, billing, data-deletion, irreversible migrations,
large blast-radius changes.

## When to use

Install on workspaces that review high-stakes PRs. The skill is invoked on-demand
via the `Skill` tool after Claude has completed its own review.

## What it does

1. Presents the PR diff to a second-model reviewer (configurable: Codex, GPT, Gemini)
2. Asks the second model to flag concerns independently
3. Surfaces disagreements with Claude's own review
4. Highlights where Claude may have missed something the second model caught

## Installation

### In org template (org.yaml)
```yaml
plugins:
  - molecule-skill-cross-vendor-review
```

### From URL
```
github://Molecule-AI/molecule-ai-plugin-molecule-skill-cross-vendor-review
```

## License
Business Source License 1.1 — © Molecule AI.
