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

---

# ACTIVE LEARNING RECORDS

## CONTEXT CORRECTION — Nexora Cleaner

### NXR-20260929-000 — Cross-project context contamination corrected

```yaml
id: NXR-20260929-000
date: 2026-09-29
app: Nexora Cleaner
signal_type: CONTEXT_CORRECTION
context: Project identity / source-of-truth correction
observation: Earlier NXR records were created by renaming records that originated from a different Bolt/Cleana project. Those records are not valid evidence for Nexora Cleaner and must not be used for recall, diagnosis, or promotion.
evidence_link:
  - user correction: Nexora Cleaner was not developed in Bolt
  - Floot project lookup confirms a separate project named Nexora Cleaner
impact: Prevents false transfer of payment/auth/publication conclusions between unrelated projects.
status: VALIDATED
```

Knowledge rule:

```text
PROJECT NAME MATCH
!=
SHARED IMPLEMENTATION HISTORY

Before transferring a lesson or incident between projects:
verify project identity + platform + implementation context.
```

---

## VERIFIED CURRENT STATE — Nexora Cleaner

### NXR-20260929-001 — Floot project exists and is pre-publication

```yaml
id: NXR-20260929-001
date: 2026-09-29
status: VALIDATED
scope: PROJECT
app: Nexora Cleaner
signal_type: PROJECT_STATE
severity: INFO

context:
  domain: project-state
  task_type: release readiness
  app_family: Android utility / cleaner
  component: Floot project
  stack: Floot
  environment: pre-production
  dependencies:
    - Floot project 2daadaa2-40b3-4b9c-bd06-fb4aea955ddf
  version_range: current state on 2026-09-29
  applies_when: reasoning about current Nexora Cleaner release state
  do_not_apply_when: other Bolt/Cleana projects

epistemics:
  claim_type: FACT
  validation_level: TESTED
  evidence:
    - Floot list_projects returned project name Nexora Cleaner
    - Floot get_publish_status returned published=false
    - Floot get_publish_status returned mobileBuild=null
    - Floot get_publish_status returned native builds used=0, remaining=2, limit=2
    - Floot get_publish_status returned plan=free
  limitations:
    - code-level inspection is temporarily unavailable because the current Floot daily build-action budget is exhausted
    - payment/auth implementation details are therefore not revalidated in this record

causality:
  trigger: none
  contributing_factors: none
  hypothesis: none
  alternative_explanations: []
  decisive_test: not applicable

knowledge:
  lesson: Use Floot project state as the source of truth for Nexora Cleaner; do not inherit Bolt project facts.
  reusable_pattern: Verify project identity/platform before reusing cross-project incidents.
  anti_pattern: Renaming an incident from one project and treating it as evidence for another.
  guardrail: Context fingerprint must include project + platform before recall/promotion.

relations:
  supports:
    - NXR-20260929-000
  conflicts_with: []
  supersedes:
    - invalidated prior NXR-20260929-001 payment record
    - invalidated prior NXR-20260929-002 auth record
    - invalidated prior NXR-20260929-003 publication record
  depends_on:
    - workshop/13_CONTINUOUS_LEARNING_SELF_IMPROVEMENT_ENGINE.md

effect:
  expected: future analysis stays attached to the correct Nexora Cleaner implementation.
  actual: project identity and release state corrected.

lifecycle:
  stale_triggers:
    - Nexora Cleaner is published
    - a native mobile build is started/completed
    - project platform changes
  reopen_triggers:
    - conflicting project identity evidence
  last_validated: 2026-09-29

links:
  tests:
    - Floot list_projects
    - Floot get_publish_status
  releases: none
  incidents:
    - NXR-20260929-000
```

---

## OPEN UNKNOWNS — require direct Nexora code inspection

The following are intentionally **not** treated as incidents or facts until the actual Nexora Cleaner code/configuration is inspected:

```text
PAYMENT IMPLEMENTATION STATUS
AUTH IMPLEMENTATION STATUS
GOOGLE SIGN-IN STATUS
REVENUECAT / GOOGLE PLAY BILLING CONFIGURATION
RESTORE PURCHASES STATUS
ANDROID CLEANER NATIVE BRIDGE STATUS
PUBLICATION BLOCKERS BEYOND "not yet published"
```

These must be resolved from Nexora Cleaner itself, not from the separate Bolt project.
