# ANTI-PATTERNS

Сюда попадают подтверждённые approaches, которые создают существенную ошибку, сложность, стоимость или fragility в определённых условиях.

```yaml
id:
title:
scope:
evidence:
applies_when:
do_not_apply_when:
failure_mechanism:
observed_consequence:
safer_alternative:
exceptions:
stale_triggers:
last_validated:
```

Правила:
- Не превращать единичную неудачу в вечный запрет.
- Anti-pattern должен описывать mechanism и context.
- При появлении counterexample или нового environment — REOPEN.