# Modelo de Dominio

Montos: enteros en COP (`bigint`). Fechas: ISO 8601, zona `America/Bogota`. Tablas en `08-technical/database.md`.

## Entidades

### User
| Campo | Tipo | Nota |
|---|---|---|
| id | uuid | |
| email | string único | |
| name | string | |
| role | `student` \| `institution_analyst` | |
| userType | `universitario` \| `aprendiz_sena` \| `otro` \| null | FR-016 |
| institution | string \| null | Texto corto |
| locality | string \| null | Localidad o municipio del área metropolitana |
| insightsConsent | boolean (default false) | BR-042 |
| createdAt | datetime | |

### FinancialProfile (1:1 User)
| Campo | Tipo | Seed Valentina |
|---|---|---|
| userId | uuid | |
| monthlyIncome | int | 900.000 (suma de `Income` recurrentes) |
| fixedExpenses | int | 520.000 |
| liquidBalance | int | 450.000 |
| pendingFixedExpenses | int | 200.000 |
| minimumProtectedBalance | int | 100.000 |
| savingsRate | decimal 0–0,5 | 0,20 |
| updatedAt | datetime | |

### Income
`id, userId, source (trabajo_parcial | practica | cuota_aprendizaje | beca | apoyo_familiar | freelance | ocasional), amount, recurrence (mensual | ocasional), receivedAt`

### Expense (fijo)
`id, userId, name, amount, dueDay (1–31), paidThisPeriod`

### Budget (calculado por periodo)
`id, userId, period (YYYY-MM), margin, recommendedSavings, variableBudget, netAvailable, safeCapacity, explanation`

### Goal
| Campo | Tipo |
|---|---|
| id | uuid |
| userId | uuid |
| name | string |
| category | `herramienta_estudio` \| `curso_certificacion` \| `emprendimiento` \| `emergencia` \| `otro` |
| targetAmount | int > 0 |
| savedAmount | int ≥ 0 (= saldo del `WalletAccount` de la meta) |
| targetDate | date futura |
| status | `active` \| `completed` \| `archived` |
| walletAccountId | uuid |

### Recommendation
`id, userId, type (goal_contribution | affordability | group_contribution | windfall_allocation), amount, goalId?, groupId?, reason, provider (llm | rules), status (proposed | accepted | modified | rejected | blocked | expired), policyOutcome (allowed | capped | blocked), createdAt`

### WalletAccount (bolsillo)
`id, ownerType (user | group), ownerId, kind (disponible | meta | grupo), balance, provider (simulated | open_payments), walletAddress? (solo Open Payments)`

### PaymentIntent
| Campo | Tipo |
|---|---|
| id | uuid |
| userId | uuid |
| recommendationId | uuid \| null |
| amount | int > 0 |
| sourceAccountId / destinationAccountId | uuid |
| provider | `simulated` \| `open_payments` |
| idempotencyKey | string único |
| status | `pending_confirmation` \| `processing` \| `completed` \| `rejected` \| `failed` \| `pending_reconciliation` |
| externalRef | string \| null (id en Open Payments) |
| createdAt, confirmedAt | datetime |

### LedgerEntry (ledger simulado, doble entrada)
`id, paymentIntentId, accountId, amount (+/−), createdAt`. Invariante: la suma de entradas de un `PaymentIntent` es 0.

### Gamificación
- `Progress`: `userId, points, level (1–4), streakWeeks, lastStreakWeek`.
- `Challenge`: `code, title, rule`. `UserChallenge`: `userId, challengeCode, progress, status`.
- `Achievement`: `userId, badgeCode, unlockedAt`.

### Metas grupales
- `SavingsGroup`: `id, name, targetAmount, targetDate, status (draft | active | completed), createdBy, walletAccountId`.
- `SavingsGroupMember`: `groupId, userId, finalPercentage, contributedAmount`. Único por (groupId, userId).
- `GroupContribution`: `id, groupId, memberUserId, amount, paymentIntentId`.

### Registro
- `DecisionLog`: `id, userId, requestId, provider, model, latencyMs, outputValid, fallbackReason?, policyOutcome, createdAt`.
- `AuditLog`: `id, actorUserId, action, entityType, entityId, payload (sin datos sensibles), createdAt`.

### InsightSnapshot (agregado)
`period, cohortKey (userType | institution | locality), cohortValue, usersCount (≥20), pctSafeCapacityZeroByWeek[4], topGoalCategories[3], synthetic (boolean)`

## Relaciones principales

- User 1—1 FinancialProfile; User 1—N Income, Expense, Goal, Recommendation, PaymentIntent.
- Goal 1—1 WalletAccount (kind `meta`); User 1—1 WalletAccount (kind `disponible`).
- Recommendation 1—N DecisionLog; Recommendation 0..1—1 PaymentIntent.
- PaymentIntent 1—2 LedgerEntry (simulado) → AuditLog.
- SavingsGroup 1—N SavingsGroupMember → User; SavingsGroup 1—N GroupContribution → PaymentIntent.
- InsightSnapshot se deriva de FinancialProfile, Budget y Goal de usuarios con consentimiento; no guarda referencias a usuarios.
