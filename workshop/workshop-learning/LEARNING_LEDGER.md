# LEARNING LEDGER

Использовать двухступенчато.

## FAST CAPTURE

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

## PROMOTED / MATERIAL RECORD

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

Правила:
- Не повышать scope выше evidence.
- Не путать observation и cause.
- Не удалять material failed approaches бесследно.
- Stale/Superseded records не использовать как normal recall.