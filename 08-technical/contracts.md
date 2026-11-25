# Contracts

Esquemas Zod compartidos (`src/contracts/`). Todo input externo se valida antes de entrar al dominio. Ejemplos completos en `api.md`.

## Decisión

**DecisionRequest**: `state` (FinancialState), `allowedTypes[]`, `questionVersion`.

**DecisionResponse**: `provider`, `model`, `type`, `goalId?`, `amount`, `confidence` (0–1), `reason`, `latencyMs`, `requestId`.

**FinancialState**: `monthlyIncome, fixedExpenses, safeCapacity, recommendedSavings, savedThisPeriod, goals[{ id, category, targetAmount, savedAmount, monthsLeft }]`. Sin datos personales.

## Producto

| Contrato | Campos clave |
|---|---|
| OnboardingRequest | `incomes[]`, `fixedExpenses`, `liquidBalance`, `pendingFixedExpenses`, `minimumProtectedBalance`, `firstGoal?`, `userType?`, `institution?`, `locality?`, `insightsConsent?` |
| BudgetResponse | `period, margin, recommendedSavings, variableBudget, netAvailable, safeCapacity, explanation` |
| Goal | ver `04-domain/domain-model.md` |
| Recommendation | `id, type, goalId?, amount, provider, policyOutcome, status, reason` |
| RecommendationDecision | `action: accept \| modify \| reject`, `amount?` |
| PaymentPrepareRequest / Response | `recommendationId` → `paymentIntentId, status, provider, amount, source, destination, idempotencyKey, reason` |
| PaymentConfirmRequest / Response | `paymentIntentId, idempotencyKey, confirmed: true` → `status, goal?, awarded?` |
| AffordabilityRequest / Response | `price, label?` → `recommended, safeCapacity, shortfall, explanation` |
| GroupContributionRecommendation | `amount, remainingResponsibility, finalPercentage, reason` |
| InsightAggregateResponse | `synthetic, period, minCohortSize, cohorts[]` |
| WeeklyReview (P2) | `period, summary, priorityAction` |

## Reglas de validación comunes

- Montos: enteros ≥ 0 (`amount` de movimientos > 0), máximo 100.000.000.
- Fechas de meta: futuras.
- Porcentajes: enteros 1–100.
- Strings: máx. 80 caracteres, sin HTML.
