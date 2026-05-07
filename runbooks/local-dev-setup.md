# Local Development Setup

This runbook covers setting up a local development environment for
`molecule-skill-cross-vendor-review`.

---

## Prerequisites

- Python 3.11+
- `gh` CLI authenticated
- API key for the non-Claude model (see below)
- Write access to `Molecule-AI/molecule-ai-plugin-molecule-skill-cross-vendor-review`

---

## Clone & Bootstrap

```bash
git clone https://git.moleculesai.app/molecule-ai/molecule-ai-plugin-molecule-skill-cross-vendor-review.git
cd molecule-ai-plugin-molecule-skill-cross-vendor-review
```

---

## Validating Plugin Structure

```bash
python3 -c "import yaml; yaml.safe_load(open('plugin.yaml'))"
echo "plugin.yaml OK"
```

---

## Setting Up API Keys

The plugin calls a non-Claude model. Set the key as a workspace secret:

```bash
# Option A: OpenAI (GPT-4)
curl -X POST http://localhost:8080/workspaces/$WS_ID/secrets \
  -H "Content-Type: application/json" \
  -d '{"key":"OPENAI_API_KEY","value":"sk-..."}'

# Option B: Google (Gemini)
curl -X POST http://localhost:8080/workspaces/$WS_ID/secrets \
  -H "Content-Type: application/json" \
  -d '{"key":"GOOGLE_API_KEY","value":"..."}'
```

---

## Testing the Cross-Vendor Review

1. Install the plugin in a test workspace
2. Configure the non-Claude API key as a workspace secret
3. Open a test PR in a known-safe repo
4. Run the `cross-vendor-review` skill
5. Verify disagreements are surfaced and the final synthesis is coherent

---

## Troubleshooting

### Non-Claude model not called

- Verify the API key is set as a workspace secret (not in config.yaml)
- Check the model is available (e.g., GPT-4 credits, Gemini quota)
- Check the workspace can reach the external API

### Disagreements not surfaced

- The skill requires at least one finding from each model to surface disagreement
- If both models agree on everything, no disagreement section is produced

### API errors from non-Claude model

- Check API key is valid and has quota remaining
- Check the workspace has internet access to the model's endpoint

---

## Related

- `skills/cross-vendor-review/SKILL.md` — adversarial review process
- `molecule-skill-code-review` — the Claude-only code review counterpart
