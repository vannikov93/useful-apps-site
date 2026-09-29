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