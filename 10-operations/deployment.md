# Deployment

## Objetivo

Aplicación + API + PostgreSQL en infraestructura controlada, con copia local idéntica para la demo.

## Flujo

Git → Build → Docker → VPS/Dokploy → Health check → Seed/demo verification.

## Variables

`DATABASE_URL`, `SESSION_SECRET`, `DEMO_MODE`, `DECISION_PROVIDER` (`llm`/`rules`), `LLM_API_KEY` (si aplica), `PAYMENTS_PROVIDER` (default `simulated`), credenciales de Open Payments (solo si se integra).

## Checklist (vie 08:00)

- Variables configuradas.
- DB migrada.
- `GET /health` 200 con `paymentsProvider: simulated`.
- Login funcional con usuario seed.
- Demo seed cargado y `POST /demo/reset` probado.
- Fallback de IA probado (AI-01).
- Copia local funcionando sin internet.
- Open Payments: solo si se integró y pasó PY-01 … PY-07; si no, se omite.
