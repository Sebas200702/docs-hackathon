# Seguridad

## Autenticación

Login obligatorio. Contraseñas con hash (argon2/bcrypt). Cookie httpOnly, `SameSite=Lax`.

## Autorización

- `student`: solo sus datos y los grupos de los que es miembro.
- `institution_analyst`: solo `GET /insights/aggregate`; nunca datos individuales.

## Datos financieros y privacidad

- Minimizar: no se piden credenciales bancarias ni movimientos detallados.
- Ley 1581 de 2012 (habeas data): consentimiento explícito y revocable para insights (FR-091), finalidad informada en onboarding.
- Insights con k ≥ 20 y sin identificadores (BR-040, BR-041).
- Al LLM solo se envía estado numérico, sin nombre, email ni institución.

## Movimientos

- Confirmación explícita.
- Idempotencia.
- Auditoría.
- La IA no ejecuta movimientos.
- Credenciales de Open Payments (si se integra) solo en variables de entorno, nunca en el frontend.

## API

- Validación Zod.
- Rate limiting en login y pagos.
- Secrets fuera del repositorio.
- Logs sin montos asociados a email ni datos sensibles.
- `POST /demo/reset` deshabilitado salvo `DEMO_MODE=true`.

## Auditoría

Registrar decisiones y operaciones relevantes (`decision_logs`, `audit_logs`).
