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

---

# ACTIVE LEARNING RECORDS

## FAST CAPTURE — Cleana

### CLN-20260929-001 — Payment flow not verified

```yaml
id: CLN-20260929-001
date: 2026-09-29
app: Cleana
signal_type: INCIDENT
context: Android monetization / Pro purchase flow
observation: User reports that the payment system is not working. No successful official sandbox/test purchase and restore evidence is currently recorded.
evidence_link: pending — code/config/test evidence not yet mirrored into this repository
impact: Release blocker for a monetized production build; Premium entitlement cannot be treated as READY.
status: CAPTURED
```

### CLN-20260929-002 — One-tap Google auth requirement gap

```yaml
id: CLN-20260929-002
date: 2026-09-29
app: Cleana
signal_type: FRICTION
context: Auth / account onboarding
observation: The current build plan explicitly included Bolt Database email/password auth, while the required product standard calls for a fast Google sign-in path when accounts are useful. No verified Google sign-in implementation is currently recorded.
evidence_link: pending — implementation evidence not yet mirrored into this repository
impact: User-friction and requirements gap; may affect onboarding and account recovery/sync design.
status: CAPTURED
```

### CLN-20260929-003 — Publication attempt blocked

```yaml
id: CLN-20260929-003
date: 2026-09-29
app: Cleana
signal_type: INCIDENT
context: Publication / release workflow
observation: User attempted to publish the current app and the publishing flow did not complete. The exact platform error and its cause are not yet captured as repository evidence.
evidence_link: pending — exact error/log/screenshot classification required
impact: Release blocker until the concrete failure is identified.
status: CAPTURED
```

---

## MATERIAL CANDIDATE — CLN-20260929-001

```yaml
id: CLN-20260929-001
date: 2026-09-29
status: CANDIDATE
scope: PROJECT
app: Cleana
signal_type: INCIDENT
severity: BLOCKER

context:
  domain: payments
  task_type: digital premium purchase
  app_family: Android utility / cleaner
  component: payment + entitlement flow
  stack: current Cleana build; exact provider/billing implementation to verify
  environment: pre-production
  dependencies:
    - payment provider / Google Play Billing path to verify
    - entitlement state implementation to verify
  version_range: current build
  applies_when: Cleana monetization flow
  do_not_apply_when: none defined yet

epistemics:
  claim_type: OBSERVATION
  validation_level: REASONED
  evidence:
    - user reports payment flow is not working
    - no recorded successful official test purchase + restore result
  limitations:
    - code has not yet been inspected in this learning cycle
    - provider configuration has not yet been inspected
    - no runtime/payment logs are attached here

causality:
  trigger: unknown
  contributing_factors: unknown
  hypothesis: CAUSE_UNCONFIRMED
  alternative_explanations:
    - payment UI may still be mock or incomplete
    - billing/provider configuration may be missing or invalid
    - product/plan identifiers may not match provider configuration
    - purchase result may not be connected to entitlement activation
    - restore/lifecycle handling may be incomplete
    - publication/runtime environment may not support the current payment route
  decisive_test:
    - inspect actual payment and entitlement implementation
    - identify the authoritative billing route
    - inspect provider/product configuration
    - run an official sandbox/test purchase
    - verify entitlement activation
    - verify Restore Purchases / reinstall path

knowledge:
  lesson: pending — do not infer root cause before implementation/config/test evidence
  reusable_pattern: pending
  anti_pattern: pending
  guardrail: existing workshop rule remains applicable — Payments are not READY without a real official test purchase and restore verification

relations:
  supports: []
  conflicts_with: []
  supersedes: []
  depends_on:
    - workshop/13_CONTINUOUS_LEARNING_SELF_IMPROVEMENT_ENGINE.md

effect:
  expected: identify the real failure mechanism and produce the minimum verified fix
  actual: pending

lifecycle:
  stale_triggers:
    - payment implementation changed
    - billing provider changed
    - product configuration changed
  reopen_triggers:
    - sandbox purchase fails
    - entitlement does not persist
    - restore/reinstall/new-device path fails
  last_validated: 2026-09-29

links:
  tests: pending
  releases: pending
  incidents:
    - CLN-20260929-001
```
