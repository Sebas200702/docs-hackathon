# Arquitectura

## Capas

Frontend: React + Tailwind + Vite.

Backend: Bun + Hono + TypeScript.

Persistencia: PostgreSQL + Drizzle.

Decision layer: DecisionProvider + OpenJEV + RulesProvider.

Policy layer: reglas deterministas.

Payments: Open Payments sandbox/mock.

Observabilidad: audit logs + decision logs + telemetry.

## Flujo

Frontend → API → Domain → Decision Engine → Policy Engine → User Confirmation → Open Payments → Persistence/Audit.
