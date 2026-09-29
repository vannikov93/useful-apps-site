# REUSABLE PATTERNS

Сюда попадают только `PROMOTED` patterns.

Для каждого pattern обязательно указать:

```yaml
id:
title:
scope:
validation_level:
applies_when:
do_not_apply_when:
dependencies:
version_range:
pattern:
guardrails:
known_tradeoffs:
stale_triggers:
supersedes:
last_validated:
```

Правила:
- `IT WORKED ONCE` не является reusable pattern.
- Semantic similarity не заменяет applicability.
- При material изменении создавать новый record и `SUPERSEDE`, а не переписывать историю.

---

## PATTERN-PUBLIC-DOCS-PRIVATE-OPS

```yaml
id: PATTERN-PUBLIC-DOCS-PRIVATE-OPS
title: Public documentation, private operational memory
scope: GLOBAL
validation_level: EVIDENCE_SUPPORTED
applies_when: a public repository contains workshop standards or reusable documentation
do_not_apply_when: the repository itself is intentionally private and access-controlled for operational use
dependencies:
  - repository visibility classification
version_range: current
pattern:
  - keep standards and sanitized templates public
  - keep real incidents, raw logs, auth/payment/security findings and unpublished blockers private
  - promote only sanitized reusable lessons to public documentation
guardrails:
  - classify storage destination before recording a material incident
  - never store secrets or raw sensitive evidence in public memory
known_tradeoffs:
  - requires a private operational source of truth in addition to public documentation
stale_triggers:
  - repository visibility or access-control model changes
supersedes:
last_validated: 2026-09-29
```
