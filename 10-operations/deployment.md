# Deployment

## Objetivo

Aplicación + API + PostgreSQL en infraestructura controlada, con copia local idéntica para la demo.

## Flujo

Git → Build → Docker → VPS/Dokploy → Health check → Seed/demo verification.

## Variables

`DATABASE_URL`, `SESSION_SECRET`, `DEMO_MODE`, `DECISION_PROVIDER` (`llm`/`rules`), `GEMINI_API_KEY` (llave de Google AI Studio; solo en el servidor, nunca en el frontend ni en el repo), `GEMINI_MODEL` (modelo de clase Flash; lo fija el AI Specialist en el evento), `PAYMENTS_PROVIDER` (default `simulated`), credenciales de Open Payments (solo si se integra).

## Checklist (vie 08:00)

- Variables configuradas.
- DB migrada.
- `GET /health` 200 con `paymentsProvider: simulated`.
- Login funcional con usuario seed.
- Demo seed cargado y `POST /demo/reset` probado.
- Fallback de IA probado (AI-01).
- Copia local funcionando sin internet.
- Open Payments: solo si se integró y pasó PY-01 … PY-07; si no, se omite.
