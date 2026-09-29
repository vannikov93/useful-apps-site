# 13 — CONTINUOUS LEARNING & SELF-IMPROVEMENT ENGINE v2
## Evidence-calibrated learning system for the AI app workshop

### Назначение

Этот стандарт превращает опыт мастерской приложений в проверяемое, контекстное и повторно используемое инженерное знание.

Цель — не «самопереписывающаяся система», не бесконечный аудит и не накопление заметок.  
Цель — чтобы после существенных ошибок, near-miss, переделок, экспериментов, удачных решений, релизов и пользовательских сигналов мастерская:

- реже повторяла известные ошибки;
- быстрее распознавала знакомые классы проблем;
- переиспользовала проверенные решения только там, где они применимы;
- превращала серьёзные ошибки в guardrails;
- быстрее исправляла знакомые failures;
- уменьшала rework и ручную работу;
- не выучивала ложные причинные связи;
- не применяла устаревшее знание;
- не превращала прошлые успехи в догму;
- прекращала оптимизацию после достаточного результата.

Система **не переобучает веса модели** и не даёт AI права бесконтрольно менять authoritative rules.

Главный принцип:

> **FEEDBACK LOOP ALLOWED. AUTHORITY LOOP FORBIDDEN.**

AI может:
- наблюдать;
- диагностировать;
- формулировать hypothesis;
- извлекать прошлый опыт;
- предлагать изменение;
- выполнять разрешённое изменение;
- проверять результат;
- записывать candidate lesson.

Но сила нового правила не может быть выше силы evidence, а изменение authoritative/global rules не должно происходить молча.

---

# 1. GOAL CONTRACT BEFORE LEARNING

Самоулучшение существует ради цели продукта, а не ради собственного совершенства.

Перед существенным improvement cycle определить только необходимое:

```text
PRIMARY_OUTCOME
DONE_CRITERIA
MINIMUM_QUALITY_FLOOR
HARD_CONSTRAINTS
CURRENT_BOTTLENECK
NON_GOALS
RESOURCE_BUDGET
RISK_TOLERANCE
REVERSIBILITY_REQUIREMENTS
```

Правило:

```text
IMPROVEMENT
must materially support
CURRENT PRODUCT GOAL
```

Если предлагаемое улучшение не влияет на текущую цель, реальный повторяемый риск или будущую стоимость работы — BACKLOG / REJECT.

---

# 2. MASTER CORE LOOP

```text
GOAL CONTRACT
→ OBSERVE
→ CLASSIFY LEARNING SIGNAL
→ BUILD EVIDENCE PACKET
→ SEPARATE TRIGGER / CONTRIBUTING FACTORS / CAUSAL HYPOTHESIS
→ RECALL RELEVANT LESSONS
→ FILTER BY APPLICABILITY / STALENESS / CONFLICT
→ CHECK EXISTING EQUIVALENT
→ SELECT DECISIVE QUESTION OR HIGHEST-LEVERAGE CHANGE
→ MAKE MINIMUM REVERSIBLE CHANGE
→ VALIDATE
→ COMPARE BEFORE / AFTER
→ ACCEPT / REJECT / ROLLBACK
→ CLOSE ACTION
→ CAPTURE LESSON
→ PROMOTION GATE
→ REUSABLE PATTERN / ANTI-PATTERN / GUARDRAIL
→ MONITOR REAL EFFECT
→ STALE / SUPERSEDE / REOPEN WHEN REALITY CHANGES
↺
```

Система должна учиться на **подтверждённых последствиях**, а не на уверенности объяснения.

---

# 3. CORE LAWS

```text
OUTPUT != PROOF

OBSERVATION != CAUSE

CORRELATION != ROOT CAUSE

AI SELF-CRITIQUE != INDEPENDENT VALIDATION

CLAIM_STRENGTH <= EVIDENCE_STRENGTH

NEW != BETTER

MORE COMPLEX != MORE CAPABLE

IMPROVEMENT != MORE FEATURES

AUTOMATION != VALUE
unless it removes proven repeated work.

REUSE BEFORE BUILD

BUT:
REUSE ONLY IF APPLICABLE

ROOT CAUSE BEFORE SYSTEMIC PATCH

MEASURE BEFORE OPTIMIZE

VALIDATE BEFORE PROMOTE

ACTION BEFORE CLAIMING LEARNING

VERIFY EFFECT BEFORE CALLING IMPROVEMENT PROVEN

REVERSIBLE BEFORE IRREVERSIBLE

LOCAL FIX > SYSTEM REDESIGN
unless evidence shows a systemic defect.

FAILED ATTEMPT != USELESS
if it prevents repetition of the same mistake.

SUCCESS != GENERAL PATTERN
without applicability evidence.

METRIC = SENSOR
METRIC != TARGET

DONE = ACCEPTANCE CRITERIA MET
```

---

# 4. LEARNING SIGNALS ≠ KNOWLEDGE

Система сначала получает **сигнал**, а уже затем может сформировать знание.

## 4.1 Learning signals

```text
INCIDENT
NEAR_MISS
SUCCESS
FRICTION
REWORK
FAILED_TEST
EXPERIMENT_RESULT
USER_FEEDBACK_PATTERN
METRIC_SHIFT
DEPENDENCY_CHANGE
POLICY_CHANGE
COST_SPIKE
MANUAL_REPEAT
```

### INCIDENT
Реальный failure.

### NEAR_MISS
Сбой почти произошёл, но вред был предотвращён случайностью, ручным вмешательством или удачным условием.

Near-miss высокого риска рассматривается почти как реальный incident.

### SUCCESS
Решение сработало.

Успех не становится pattern автоматически: нужно понять механизм и область применимости.

### FRICTION / MANUAL_REPEAT
Работа выполняется, но с ненужной повторяемостью, задержкой, handoff или стоимостью.

---

# 5. KNOWLEDGE ARTIFACTS

Из learning signals могут появляться следующие типы знания.

## A. LESSON
Проверяемый вывод о том, что учитывать в будущем.

## B. REUSABLE PATTERN
Проверенное решение, которое имеет чёткую область применимости.

## C. ANTI-PATTERN
Подход, который при определённых условиях создаёт failure, лишнюю сложность или стоимость.

## D. GUARDRAIL
Механизм, который предотвращает повторение класса ошибки или делает failure видимым раньше.

Примеры:

```text
automated test
validator
type/schema constraint
permission gate
release gate
lint/static check
runtime invariant
monitor/alert
checklist
explicit approval
```

## E. OPEN UNKNOWN
Существенный вопрос, для которого evidence пока недостаточно.

Не закрывать UNKNOWN правдоподобной догадкой.

---

# 6. EPISTEMIC CLASSIFICATION

Каждый material вывод помечается по типу.

```text
FACT
OBSERVATION
EVIDENCE
INFERENCE
ASSUMPTION
HYPOTHESIS
UNKNOWN
CONFLICT
```

И отдельно по уровню validation:

```text
REASONED
EVIDENCE_SUPPORTED
TESTED
INDEPENDENTLY_VALIDATED
```

### REASONED
Есть логическое основание, но нет достаточного внешнего/исполняемого подтверждения.

### EVIDENCE_SUPPORTED
Есть релевантные логи, документация, метрики, воспроизводимые наблюдения или сильное внешнее evidence.

### TESTED
Claim проверен реальным тестом/экспериментом в релевантной среде.

### INDEPENDENTLY_VALIDATED
Критический claim подтверждён другим failure domain:
- deterministic executable test;
- официальный внешний источник;
- другой независимый инструмент;
- human expert review;
- иной evaluator с действительно отличающимся источником ошибки.

Повторная оценка тем же AI в том же контексте не считается независимой.

---

# 7. EVIDENCE PACKET

Для material learning signal сохранять достаточный пакет:

```text
SIGNAL_ID
TIMESTAMP
APP
ENVIRONMENT
VERSION
OBSERVED_BEHAVIOR
EXPECTED_BEHAVIOR
IMPACT
SOURCE
LOGS / TESTS / METRICS / USER_SIGNAL
LIMITATIONS
KNOWN_MISSING_EVIDENCE
```

Для material causal claim добавить:

```text
TRIGGER
CONTRIBUTING_FACTORS
CAUSAL_HYPOTHESIS
ALTERNATIVE_EXPLANATIONS
DECISIVE_TEST
VALIDATION_LEVEL
```

Не заставлять каждый маленький bug проходить тяжёлую научную процедуру.

Чем выше:
- severity;
- scope;
- irreversibility;
- security/payment/privacy impact;
- вероятность превращения вывода в GLOBAL rule,

тем сильнее должна быть validation.

---

# 8. CAUSAL LEARNING — НЕ ВЫУЧИВАТЬ ЛОЖНУЮ ПРИЧИНУ

Запрещено автоматически превращать:

```text
A happened
then
B happened
```

в:

```text
A caused B
```

Для material root-cause claim проверить, насколько применимо:

```text
WHAT EXACTLY FAILED?
WHAT TRIGGERED IT?
WHAT CONDITIONS MADE IT POSSIBLE?
IS THERE ONE CAUSE OR MULTIPLE CONTRIBUTING FACTORS?
DID THE PROPOSED CAUSE PRECEDE THE EFFECT?
IS THERE A PLAUSIBLE MECHANISM?
WHAT OTHER EXPLANATION FITS THE SAME DATA?
CAN WE REPRODUCE THE FAILURE?
DOES REMOVING / CHANGING THE CAUSE CHANGE THE RESULT?
IS THERE A COUNTEREXAMPLE?
WHAT TEST WOULD DISCRIMINATE BETWEEN EXPLANATIONS?
```

Допустимые результаты:

```text
SUPPORTED_CAUSE
MULTI_FACTOR_CAUSE
LIKELY_CAUSE
CAUSE_UNCONFIRMED
UNKNOWN
```

Не форсировать `ROOT_CAUSE`, если реальность не даёт достаточных оснований.

---

# 9. ROOT-CAUSE CONTRACT

Перед material change:

```text
WHAT FAILED?
WHAT EVIDENCE DO WE HAVE?
TRIGGER?
CONTRIBUTING FACTORS?
CAUSE OR SYMPTOM?
HOW OFTEN?
WHAT DOES IT COST?
DOES IT BLOCK THE GOAL?
DO WE ALREADY HAVE A SOLUTION?
WHAT IS THE SMALLEST CHANGE THAT REMOVES OR CONTAINS THE CAUSE?
HOW WILL WE KNOW IT WORKED?
WHAT WOULD FALSIFY OUR EXPLANATION?
```

Если причина неизвестна:
- не строить сложную architecture на догадке;
- выбрать самый дешёвый decisive test;
- либо сделать безопасное containment/mitigation отдельно от causal conclusion.

---

# 10. CONTEXT FINGERPRINT

Каждый validated/promoted lesson получает контекст применимости.

```text
DOMAIN
TASK_TYPE
APP_FAMILY
COMPONENT
STACK
ENVIRONMENT
SYMPTOM_OR_FAILURE_CLASS
DEPENDENCIES
VERSION_RANGE
PRECONDITIONS
APPLIES_WHEN
DO_NOT_APPLY_WHEN
```

Пример:

```text
DOMAIN: payments
TASK_TYPE: entitlement recovery
APP_FAMILY: Android digital-goods apps
COMPONENT: EntitlementService
STACK: Floot + Android + Google Play Billing
APPLIES_WHEN: digital purchase distributed through Google Play
DO_NOT_APPLY_WHEN: physical goods / external service checkout
DEPENDENCIES: Google Play Billing
```

Правило:

> Lesson без `APPLIES_WHEN` и `DO_NOT_APPLY_WHEN`, если контекст materially ограничивает применимость, не может быть GLOBAL pattern.

---

# 11. CONTEXTUAL MEMORY ROUTER — RECALL BEFORE BUILD

Перед каждой существенной задачей:

```text
NEW TASK
→ BUILD CURRENT CONTEXT FINGERPRINT
→ RETRIEVE CANDIDATE LESSONS
→ HARD FILTER
→ RANK
→ SURFACE ONLY MATERIAL LESSONS
→ REUSE IF FIT
→ BUILD ONLY MISSING PART
```

## 11.1 Hard filter

Сначала исключить:

```text
STALE
SUPERSEDED
DO_NOT_APPLY_WHEN matched
dependency mismatch
version mismatch
hard-constraint mismatch
```

## 11.2 Ranking

После hard filter приоритет:

```text
APPLICABILITY
> VALIDATION STRENGTH
> SPECIFICITY
> FRESHNESS
> TASK RELEVANCE
> SEMANTIC SIMILARITY
```

Semantic similarity не должна побеждать реальную применимость.

## 11.3 Retrieval fallback

Если:
- релевантный promoted lesson не найден;
- найден конфликт;
- matching слабый;
- context materially отличается;

AI возвращается к текущему evidence и не притягивает прошлое правило насильно.

---

# 12. KNOWLEDGE RELATIONSHIPS

Уроки и patterns могут быть связаны:

```text
SUPPORTS
CONFLICTS_WITH
SUPERSEDES
SUPERSEDED_BY
SPECIALIZES
EXCEPTION_TO
DEPENDS_ON
DERIVED_FROM
```

Если два validated lessons конфликтуют:

```text
DO NOT VOTE
DO NOT PICK THE NEWEST AUTOMATICALLY
```

Сначала проверить:

1. различается ли applicability;
2. один ли является special case;
3. изменились ли dependency/version;
4. можно ли найти decisive test;
5. нужно ли сохранить оба как context-dependent patterns.

---

# 13. IMMUTABLE HISTORY + SUPERSESSION

Promoted lesson/pattern не переписывать так, будто старого решения никогда не существовало.

Если materially изменилось решение:

```text
OLD RECORD
status = SUPERSEDED
        ↓
links to
        ↓
NEW RECORD
```

Новый record хранит:
- что изменилось;
- почему;
- какое evidence изменило решение;
- какие dependents требуют revalidation.

Это сохраняет traceability и предотвращает потерю исторической причины решений.

---

# 14. TWO ORTHOGONAL LIFECYCLES

Чтобы не смешивать качество знания и выполнение действия, использовать две отдельные state machines.

## 14.1 Knowledge lifecycle

```text
CAPTURED
→ CANDIDATE
→ VALIDATED
→ PROMOTED
```

Дополнительные состояния:

```text
CONFLICT
STALE
SUPERSEDED
REJECTED
DEPRECATED
ARCHIVED
```

### CAPTURED
Факт/сигнал сохранён без причинного вывода.

### CANDIDATE
Сформулирован потенциальный lesson/hypothesis.

### VALIDATED
Claim имеет достаточное evidence для текущего scope.

### PROMOTED
Разрешено системно переиспользовать в своей области применимости.

### REJECTED
Hypothesis опровергнута или benefit не подтверждён.

### ARCHIVED
Полезно сохранить исторически, но не использовать для normal recall.

## 14.2 Action lifecycle

```text
OPEN
→ IMPLEMENTED
→ VERIFIED
→ MONITORED
→ CLOSED
```

Запрещено:

```text
LESSON WRITTEN
=
PROBLEM SOLVED
```

---

# 15. LESSON → ACTION → EFFECT CONTRACT

Для material validated lesson определить:

```text
LESSON
ACTION
EXPECTED_EFFECT
EXECUTION_SURFACE
VALIDATION_PLAN
ACTUAL_EFFECT
RECURRENCE_CHECK
STATUS
```

Для командной среды также:

```text
OWNER
DUE / REVIEW CONDITION
```

Для solo-мастерской OWNER может быть:
- ChatGPT;
- Floot task;
- manual user action;
- external service;
- future release.

Action item должен иметь **verifiable end state**.

Плохо:

```text
Improve payments.
```

Хорошо:

```text
Route all premium access through EntitlementService
and pass sandbox purchase + reinstall + restore scenarios.
```

---

# 16. BOUNDED IMPROVEMENT

Предпочитать:

```text
ONE PROBLEM
→ ONE CAUSAL HYPOTHESIS
→ ONE BOUNDED CHANGE
→ TARGETED VALIDATION
```

System redesign допустим, только если:
- несколько independent failures указывают на общий mechanism;
- local fixes систематически повторяются;
- текущая architecture сама создаёт failure class;
- simpler replacement materially уменьшает complexity/risk.

---

# 17. EXPERIMENT CONTRACT

Каждое material improvement:

```text
PROBLEM
EVIDENCE
BASELINE
CAUSAL_HYPOTHESIS
ALTERNATIVE_EXPLANATIONS
EXPECTED_BENEFIT
CHANGE
RISK
REVERSIBILITY
TEST
SUCCESS_CRITERIA
FAILURE_CRITERIA
ROLLBACK
```

Для high-risk изменения по возможности добавить:

```text
REGRESSION_CASES
HOLDOUT_CASE / PRE-EXISTING CRITICAL CASE
```

Не подгонять acceptance criteria после просмотра результата.

Material изменение evaluation criteria создаёт новую версию evaluation и требует targeted revalidation.

---

# 18. PROMOTION GATE

Урок можно PROMOTE только в заявленный scope.

## A. High-severity guardrail
Одна подтверждённая BLOCKER/CRITICAL ошибка может быть достаточна для немедленного локального guardrail, если failure mechanism подтверждён.

## B. Repeated lesson
Один и тот же mechanism проявился в независимых случаях.

## C. Cross-app reuse
Решение успешно применилось в нескольких distinct contexts и сохранило ожидаемый эффект.

## D. Measurable improvement
Before/after evidence показывает material benefit.

## E. Strong external evidence + local fit
Официальное/сильное внешнее evidence подтверждает pattern, а локальная применимость проверена.

### GLOBAL promotion

Для `GLOBAL`, security, privacy, billing, auth, release-policy или другого high-impact authoritative rule:

```text
PROMOTION REQUIRES
strong validation
+
explicit authority / human approval
```

AI не должен молча переписывать hard constraints или authoritative standards.

---

# 19. SUCCESS LEARNING WITHOUT CARGO CULT

Успех тоже может обмануть.

Не делать:

```text
IT WORKED ONCE
→ BEST PRACTICE
```

Для positive pattern спросить:

```text
WHAT MECHANISM CREATED THE BENEFIT?
WHAT CONDITIONS WERE PRESENT?
WHAT ALTERNATIVE EXPLANATION EXISTS?
CAN WE REPEAT IT?
WHERE SHOULD IT NOT BE USED?
WHAT COST / TRADEOFF DID IT ADD?
```

Если mechanism не понятен, можно сохранить:

```text
PROMISING_OBSERVATION
```

но не продвигать как GLOBAL pattern.

---

# 20. FAILURE → GUARDRAIL

После подтверждённого серьёзного incident/near-miss:

> Можно ли сделать так, чтобы этот класс ошибки больше не зависел от памяти человека?

Приоритет по умолчанию:

```text
SYSTEM INVARIANT / SAFE DESIGN
→ AUTOMATED TEST
→ VALIDATOR
→ TYPE / SCHEMA CONSTRAINT
→ RELEASE GATE
→ MONITOR / ALERT
→ CHECKLIST
→ HUMAN MEMORY
```

Порядок не абсолютный: выбирать самый дешёвый надёжный механизм под failure class.

## Пример: payments

Failure:

```text
Premium activated after button click.
```

Guardrail:

```text
verified purchase
→ EntitlementService
→ sandbox purchase
→ reinstall
→ restore
```

## Пример: cleaner

Failure:

```text
important file became deletion candidate.
```

Guardrail:

```text
protected/exclusion layer
→ preview
→ explicit confirmation
→ recoverability where possible
→ regression case
```

---

# 21. CORRELATED ERROR DEFENSE

Одна модель не должна одновременно:

```text
invent explanation
→ approve explanation
→ declare global rule
```

для high-impact conclusions без дополнительного failure domain.

При material/high-risk claims предпочитать:

```text
REAL RUN
> DETERMINISTIC / EXECUTABLE TEST
> STRONG OFFICIAL EXTERNAL EVIDENCE
> ORTHOGONAL REVIEW
> MODEL OPINION
```

Если всё проверяет один GPT:

```text
ORTHOGONAL_SELF_CHECK
```

а не «independent validation».

---

# 22. STALENESS PROPAGATION

При upstream change:

```text
CHANGE
→ FIND DEPENDENTS
→ MARK AFFECTED KNOWLEDGE STALE
→ REVALIDATE
→ REBUILD ONLY AFFECTED PART
```

Типичные stale triggers:

- Floot guide changed;
- Android API changed;
- Google Play policy changed;
- Billing/Auth provider changed;
- pricing model changed;
- schema changed;
- dependency upgraded;
- environment changed;
- target market changed;
- product scope changed;
- assumption invalidated.

Никогда молча не переиспользовать stale conclusion.

---

# 23. REOPEN TRIGGERS

Даже PROMOTED pattern не является вечной истиной.

Reopen при:

```text
NEW FAILURE
NEW COUNTEREXAMPLE
DEPENDENCY CHANGE
POLICY CHANGE
SCALE CHANGE
COST CHANGE
NEW USE CASE
REPEATED MANUAL OVERRIDE
MATERIAL PERFORMANCE DEGRADATION
BETTER SIMPLER ALTERNATIVE WITH REAL EVIDENCE
```

Старый pattern становится baseline, а не догмой.

---

# 24. ANTI-OSSIFICATION GATE

`REUSE BEFORE BUILD` не должно превращаться в:

```text
WE ALWAYS DO IT THIS WAY
```

Clean-room alternative рассматривать только если есть сигнал:

```text
REPEATED FAILURE
SYSTEMIC COMPLEXITY
MATERIAL ENVIRONMENT CHANGE
CURRENT PATTERN NO LONGER MEETS GOAL
LOCAL PATCHES KEEP ACCUMULATING
NEW ALTERNATIVE REMOVES MATERIAL COMPLEXITY/RISK
```

Не запускать clean-room exploration без такого trigger.

Максимум:
- current baseline;
- один materially different alternative;
- третий candidate только если реально нужен.

---

# 25. LEARNING LEDGER — TWO-STAGE CAPTURE

Чтобы память не превратилась в дневник, использовать два уровня.

## 25.1 FAST CAPTURE

Для любого potentially material signal:

```text
ID
DATE
APP
SIGNAL_TYPE
CONTEXT
OBSERVATION
EVIDENCE_LINK
IMPACT
STATUS
```

Без длинной аналитики.

## 25.2 PROMOTED RECORD

Только для validated/material knowledge:

```text
LESSON_ID
DATE
APP
SCOPE
SEVERITY

CONTEXT_FINGERPRINT

OBSERVATION
EXPECTED_BEHAVIOR
TRIGGER
CONTRIBUTING_FACTORS

CAUSAL_HYPOTHESIS
ALTERNATIVE_EXPLANATIONS
VALIDATION_LEVEL
EVIDENCE

LESSON

APPLIES_WHEN
DO_NOT_APPLY_WHEN

REUSABLE_PATTERN
ANTI_PATTERN
GUARDRAIL

SUPPORTS
CONFLICTS_WITH
SUPERSEDES
DEPENDS_ON