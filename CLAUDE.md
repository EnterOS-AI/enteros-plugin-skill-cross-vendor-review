# molecule-skill-cross-vendor-review — Adversarial Multi-Model Code Review

`molecule-skill-cross-vendor-review` runs an adversarial code review against
a non-Claude model (Codex / GPT / Gemini) and surfaces disagreements with
Claude's own review. Use **only for noteworthy PRs**: auth, billing, data-deletion,
irreversible migration.

**Version:** 1.0.0
**Runtime:** `claude_code`

---

## Repository Layout

```
molecule-skill-cross-vendor-review/
├── plugin.yaml              — Plugin manifest
├── skills/
│   └── cross-vendor-review/
│       └── SKILL.md         — Adversarial review process
└── adapters/               — Harness adaptors (non-Claude model API keys)
```

---

## When to Use

✅ Use for PRs involving:
- Authentication or authorisation changes
- Billing or payment logic
- Data deletion or irreversible migrations
- Large blast-radius refactors

❌ Do NOT use for:
- Documentation-only PRs
- Minor typo fixes
- Mechanical formatting changes

---

## How It Works

1. Claude Code reviews the PR (internal review)
2. A non-Claude model (GPT-4 / Codex / Gemini) reviews the same PR
3. The skill surfaces points of disagreement:
   - Something Claude flagged but the other model missed
   - Something the other model flagged but Claude missed
4. The agent synthesises a final recommendation

### Required API Keys

The non-Claude model is called via its API. Set the key as a workspace secret:

```bash
# GPT-4
OPENAI_API_KEY=sk-...  # set via workspace secret

# Gemini
GOOGLE_API_KEY=...     # set via workspace secret

# Codex
OPENAI_API_KEY=sk-...  # Codex uses the same key
```

---

## Development

### Prerequisites

- Python 3.11+
- `gh` CLI authenticated
- Write access to `Molecule-AI/molecule-ai-plugin-molecule-skill-cross-vendor-review`

### Setup

```bash
git clone https://git.moleculesai.app/molecule-ai/molecule-ai-plugin-molecule-skill-cross-vendor-review.git
cd molecule-ai-plugin-molecule-skill-cross-vendor-review
python3 -c "import yaml; yaml.safe_load(open('plugin.yaml'))"
```

### Pre-Commit Checklist

```bash
python3 -c "import yaml; yaml.safe_load(open('plugin.yaml'))"

python3 -c "
import re, sys
with open('plugin.yaml') as f:
    content = f.read()
patterns = [r'sk.ant', r'ghp.', r'AKIA[A-Z0-9]']
if any(re.search(p, content) for p in patterns):
    print('FAIL: possible credentials found')
    sys.exit(1)
print('No credentials: OK')
"
```

---

## Release Process

1. Review changes: `git log origin/main..HEAD --oneline`
2. Bump `version` in `plugin.yaml` (semver)
3. Commit: `chore: bump version to X.Y.Z`
4. Tag and push: `git tag vX.Y.Z && git push origin main --tags`
5. Create GitHub Release with changelog

---

## Known Issues

See `known-issues.md` at the repo root.
