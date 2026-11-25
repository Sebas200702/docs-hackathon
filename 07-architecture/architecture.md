# Arquitectura

## Capas

| Capa | Tecnología | Dueño |
|---|---|---|
| Frontend | React + Tailwind + Vite (mobile-first) | Frontend |
| Backend | Bun + Hono + TypeScript + Zod | Backend |
| Persistencia | PostgreSQL + Drizzle | Backend |
| Decision layer | `DecisionProvider`: LlmProvider (Gemini API) + RulesProvider | AI Specialist |
| Policy layer | Reglas deterministas (función pura) | Backend |
| Payments | `PaymentProvider`: SimulatedLedgerProvider (default) · OpenPaymentsProvider (opcional) | Backend |
| Insights | Job de agregación con k ≥ 20 sobre usuarios con consentimiento | AI Specialist + Backend |
| Observabilidad | AuditLog + DecisionLog + logs estructurados | Backend |

Stack según ADR-006.

## Flujo principal

Frontend → API → Domain → Decision Engine → Policy Engine → User Confirmation → PaymentProvider → Persistence/Audit.

## Flujo de insights

Perfiles con consentimiento → agregación por periodo y cohorte → filtro k ≥ 20 → `InsightSnapshot` → `GET /insights/aggregate` → vista institucional.

## Decisiones clave

- Dependencias externas (Gemini, Open Payments) detrás de interfaces y con alternativa local: la demo funciona offline.
- Policy Engine sin I/O, testeable de forma aislada.
- Un solo repositorio, un despliegue.
