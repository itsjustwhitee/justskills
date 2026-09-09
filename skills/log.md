# Directory Update Log

## 2026-10-08
* **Create**: `delegate-with-handoff` - orchestrator defines each task, dispatches it to a
  context-free agent on the cheapest capable model with a written handoff, then verifies.

## 2026-09-09
* **Create**: Initial pack - `conventional-commits`, `open-knowledge-tracking`,
  `clarify-before-building`, `stop-after-repeated-failure`.
* **Update**: Dissolved `general.md` into skills - added `keep-it-simple`,
  `no-secrets-in-output`, `safe-git`; moved the git guardrails out of
  `conventional-commits` into `safe-git`.
* **Update**: Adopted patterns from public skills (superpowers, ADR skills,
  secret-scanning skills) - added `verify-before-done`; gave
  `no-secrets-in-output` concrete patterns + a pre-commit scan step; added
  green-before-integrate, base-branch confirmation, and typed confirmation to
  `safe-git`; added English-only, `type!:`, and a no-AI-attribution rule to
  `conventional-commits`; added rationalization tables to the discipline skills;
  `open-knowledge-tracking` Decision concepts now follow the Nygard ADR format
  (numbered `decisions/NNNN-*.md`, `status: proposed|accepted|superseded`).
* **Update**: `keep-it-simple` and `clarify-before-building` promoted to
  `stable` after baseline-vs-skill tests; `verify-before-done` and
  `stop-after-repeated-failure` kept `draft`.
