# API

Base: `/api`. JSON. Montos enteros en COP. Sesión por cookie httpOnly. Errores: `{ "error": { "code": "STRING", "message": "texto", "field"?: "campo" } }`. Ejemplos con el seed de Valentina.

## Resumen

| Método | Ruta | FR | Prior. |
|---|---|---|---|
| POST | /auth/register, /auth/login, /auth/logout | FR-001, FR-002 | P0 |
| POST | /onboarding | FR-010 … FR-016 | P0 |
| GET | /dashboard | FR-020 … FR-022 | P0 |
| POST / GET | /goals, /goals/:id | FR-040 … FR-043 | P0 |
| POST | /decisions/recommend | FR-030, FR-031, FR-033 | P0 |
| POST | /recommendations/:id/decision | FR-032 | P0 |
| POST | /payments/prepare | FR-050, FR-051 | P0 |
| POST | /payments/confirm | FR-052 … FR-054 | P0 |
| GET | /payments/:id | FR-053 | P0 |
| POST | /demo/reset | FR-100 | P0 |
| GET | /health | NFR-031 | P0 |
| POST | /affordability/check | FR-034 | P1 |
| GET | /progress | FR-060 … FR-063 | P1 |
| POST | /group-goals, /group-goals/:id/members, /group-goals/:id/activate | FR-080, FR-081 | P1 |
| GET | /group-goals/:id | FR-080 | P1 |
| POST | /group-goals/:id/recommend-contribution | FR-082 | P1 |
| POST | /group-goals/:id/contribute | FR-083 | P1 |
| GET | /insights/aggregate | FR-090 | P1 |
| PATCH | /me/consent | FR-091 | P1 |
| GET | /weekly-review | FR-070 | P2 |
| POST | /windfall/allocate | — | P2 |

## Onboarding

`POST /onboarding`

```json
{
  "incomes": [ { "source": "trabajo_parcial", "amount": 600000, "recurrence": "mensual" },
               { "source": "apoyo_familiar", "amount": 300000, "recurrence": "mensual" } ],
  "fixedExpenses": 520000,
  "liquidBalance": 450000,
  "pendingFixedExpenses": 200000,
  "minimumProtectedBalance": 100000,
  "firstGoal": { "name": "Portátil", "category": "herramienta_estudio", "targetAmount": 1800000, "targetDate": "2027-09-30" },
  "userType": "universitario", "locality": "Soledad", "insightsConsent": true
}
```

`201` → `{ "profileId": "…", "budget": { …igual a GET /dashboard.budget… }, "goalId": "g1" }`
`400` → `{ "error": { "code": "VALIDATION", "field": "liquidBalance", "message": "Debe ser mayor o igual a 0" } }`

## Dashboard

`GET /dashboard` → `200`

```json
{
  "status": "ok",
  "budget": { "period": "2026-11", "margin": 380000, "recommendedSavings": 76000, "variableBudget": 304000,
              "netAvailable": 250000, "safeCapacity": 150000,
              "explanation": "De $900.000, $520.000 ya están comprometidos. Puedes mover $150.000 sin tocar lo básico ni tus $100.000 protegidos." },
  "mainGoal": { "id": "g1", "name": "Portátil", "savedAmount": 300000, "targetAmount": 1800000, "progressPct": 16.7 },
  "topRecommendationId": "r1",
  "progress": { "level": 1, "streakWeeks": 0, "points": 0 }
}
```

## Recomendación

`POST /decisions/recommend` → `{ "goalId": "g1" }` (opcional)

`200`

```json
{ "id": "r1", "type": "goal_contribution", "goalId": "g1", "amount": 76000, "provider": "llm",
  "policyOutcome": "allowed", "status": "proposed",
  "reason": "Te quedan $150.000 que puedes mover… Con $76.000 tu portátil pasa al 20,9 %." }
```

`POST /recommendations/r1/decision` → `{ "action": "accept" }` | `{ "action": "modify", "amount": 50000 }` | `{ "action": "reject" }`

`200` → `{ "id": "r1", "status": "accepted", "amount": 76000 }`
`422` → `{ "error": { "code": "EXCEEDS_SAFE_CAPACITY", "message": "Máximo $150.000" } }`

## Movimientos

`POST /payments/prepare` → `{ "recommendationId": "r1" }`

`201`

```json
{ "paymentIntentId": "p1", "status": "pending_confirmation", "provider": "simulated",
  "amount": 76000, "source": { "id": "a-disp", "label": "Disponible" },
  "destination": { "id": "a-g1", "label": "Meta · Portátil" },
  "idempotencyKey": "rec:r1", "reason": "…" }
```

`POST /payments/confirm` → `{ "paymentIntentId": "p1", "idempotencyKey": "rec:r1", "confirmed": true }`

`200` → `{ "paymentIntentId": "p1", "status": "completed", "goal": { "id": "g1", "savedAmount": 376000, "progressPct": 20.9 }, "awarded": { "points": 10, "badges": ["primer_paso"] } }`
Repetición con la misma key → mismo `200`, sin nuevo movimiento.
`409` → `CONFIRMATION_REQUIRED` si `confirmed` ≠ `true`.

## Chequeo de compra

`POST /affordability/check` → `{ "price": 180000, "label": "Tenis" }`
`200` → `{ "recommended": false, "safeCapacity": 150000, "shortfall": 30000, "explanation": "Te faltarían $30.000 para no tocar lo básico ni tus $100.000 protegidos." }`

## Meta grupal

`POST /group-goals` → `{ "name": "Stand feria", "targetAmount": 900000, "targetDate": "2027-05-31" }`
`POST /group-goals/:id/members` → `{ "members": [ { "userId": "u-mariana", "finalPercentage": 40 }, { "userId": "u-luis", "finalPercentage": 30 }, { "userId": "u-sofia", "finalPercentage": 30 } ] }`
`POST /group-goals/:id/activate` → `200` | `422 PERCENTAGES_NOT_100`
`POST /group-goals/:id/recommend-contribution` (como Luis) → `{ "amount": 20000, "remainingResponsibility": 225000, "finalPercentage": 30, "reason": "…" }`
`POST /group-goals/:id/contribute` → `{ "amount": 20000, "idempotencyKey": "grp:…:2027-02", "confirmed": true }`

## Insights (rol `institution_analyst`)

`GET /insights/aggregate?period=2026-11&cohortKey=userType`

```json
{ "synthetic": true, "period": "2026-11", "minCohortSize": 20,
  "cohorts": [ { "cohortValue": "aprendiz_sena", "usersCount": "<entero ≥ 20>",
                 "pctSafeCapacityZeroByWeek": ["<s1>", "<s2>", "<s3>", "<s4>"],
                 "topGoalCategories": ["<categoría>", "<categoría>", "<categoría>"] } ] }
```

Los valores de la demo se generan del seed sintético; este documento no fija cifras. Cohortes con `usersCount < 20` se omiten.

## Demo y salud

`POST /demo/reset` → `200 { "seed": "v1" }` (solo con `DEMO_MODE=true`)
`GET /health` → `200 { "status": "ok", "db": "ok", "decisionProvider": "llm|rules", "paymentsProvider": "simulated" }`
