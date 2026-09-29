# LEARNING LEDGER — PUBLIC TEMPLATE

This file is a **public template**, not the operational incident database.

## STORAGE BOUNDARY

```text
PUBLIC REPOSITORY
→ standards
→ sanitized templates
→ non-sensitive reusable patterns

PRIVATE PROJECT STORAGE
→ real incidents
→ auth/payment/security findings
→ internal architecture details
→ logs
→ unpublished release blockers
→ evidence packets
```

Never place secrets, credentials, tokens, private user data, raw sensitive logs, or security-sensitive operational details in this public repository.

Project-specific learning records must live in a private project source of truth. Public promotion is allowed only after sanitization and only when the reusable lesson no longer exposes sensitive implementation details.

---

## FAST CAPTURE TEMPLATE

```yaml
id:
date:
app:
signal_type:
context:
observation:
evidence_link:
impact:
status: CAPTURED
```

---

## PROMOTED / MATERIAL RECORD TEMPLATE

```yaml
id:
date:
status: CANDIDATE
scope:
app:
signal_type:
severity:

context:
  domain:
  task_type:
  app_family:
  component:
  stack:
  environment:
  dependencies:
  version_range:
  applies_when:
  do_not_apply_when:

epistemics:
  claim_type:
  validation_level:
  evidence:
  limitations:

causality:
  trigger:
  contributing_factors:
  hypothesis:
  alternative_explanations:
  decisive_test:

knowledge:
  lesson:
  reusable_pattern:
  anti_pattern:
  guardrail:

relations:
  supports:
  conflicts_with:
  supersedes:
  depends_on:

effect:
  expected:
  actual:

lifecycle:
  stale_triggers:
  reopen_triggers:
  last_validated:

links:
  tests:
  releases:
  incidents:
```

## Public-memory rules

- Do not raise scope above evidence.
- Do not confuse observation with cause.
- Do not delete material failed approaches from the **private** operational history without trace.
- Stale/Superseded records are not used for normal recall.
- Never copy a project-specific incident into another project merely because names/features look similar.
- Sanitize before promoting any operational lesson to this public repository.
