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

---

## ANTI-PATTERN-PUBLIC-OPS-MEMORY

```yaml
id: ANTI-PATTERN-PUBLIC-OPS-MEMORY
title: Store operational incident memory in a public repository
scope: GLOBAL
evidence:
  - public repositories are readable by anyone
  - operational records may accumulate sensitive implementation, auth, payment, security, log, or release details
applies_when: real project incidents/evidence are being recorded
do_not_apply_when: content is intentionally sanitized public documentation
failure_mechanism: private operational context is progressively exposed through otherwise useful learning records
observed_consequence: increased leakage and attack-surface risk; future maintainers may avoid recording useful evidence
safer_alternative: private project ledger + sanitized public promoted patterns
exceptions:
  - intentionally public open-source incident records that have been explicitly reviewed and sanitized
stale_triggers:
  - storage/access model changes
last_validated: 2026-09-29
```


---

## ANTI-PATTERN-CROSS-PROJECT-CONTEXT-COPY

```yaml
id: ANTI-PATTERN-CROSS-PROJECT-CONTEXT-COPY
title: Copy project-specific incidents to another project by name or feature similarity
scope: GLOBAL
evidence:
  - observed real context-contamination incident during workshop operation
applies_when: prior project knowledge is being reused
do_not_apply_when: evidence has been explicitly verified as belonging to the same project/version
failure_mechanism: a plausible prior incident is relabeled and becomes false evidence for a different implementation
observed_consequence: incorrect diagnosis, wrong priorities, and false learning records
safer_alternative: verify project ID + platform + source-of-truth before recall
exceptions: []
stale_triggers:
  - none; revalidate if project identity model changes
last_validated: 2026-09-29
```
