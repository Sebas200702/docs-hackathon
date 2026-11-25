# Database

PostgreSQL + Drizzle. Montos `bigint` (COP enteros). Campos detallados en `04-domain/domain-model.md`.

## Core (P0)

| Tabla | Clave / índices |
|---|---|
| users | `id` pk, `email` unique |
| financial_profiles | `user_id` pk/fk |
| incomes, expenses | `user_id` fk |
| goals | `user_id` fk, `wallet_account_id` fk |
| recommendations | `user_id` fk, índice (`user_id`, `created_at`) |

## Movimientos (P0)

| Tabla | Clave / índices |
|---|---|
| wallet_accounts | `owner_type`, `owner_id`; un `disponible` por usuario |
| payment_intents | `idempotency_key` **unique** |
| ledger_entries | `payment_intent_id` fk |

## Gamificación (P1)

progress, user_challenges, achievements (`user_id` + `badge_code` unique).

## Group goals (P1)

savings_groups, savings_group_members (`group_id` + `user_id` unique), group_contributions.

## Decision/audit (P0)

decision_logs, audit_logs.

## Insights (P1)

insight_snapshots (`period` + `cohort_key` + `cohort_value` unique). Sin columnas de usuario.

## Constraints

- Unique user membership per group.
- La activación del grupo valida suma de porcentajes = 100 en una transacción.
- `payment_intents.idempotency_key` único.
- Por cada `payment_intent` completado simulado, suma de `ledger_entries.amount` = 0.
- `CHECK (amount >= 0)` en montos de perfil; `CHECK (amount > 0)` en `payment_intents`.

## Seed (`db/seed.ts`, v1)

Valentina, Andrés, grupo de Mariana (Mariana, Luis, Sofía), 3 retos, 3 badges, y una cohorte **sintética** de usuarios para insights marcada `synthetic = true`.
