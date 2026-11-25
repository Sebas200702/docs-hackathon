# Estrategia de Testing

Herramienta: Vitest (unit e integration). Prioridad para la revisión técnica del viernes 09:30: FS-01 … FS-12 en verde.

## Unit

- Cálculos financieros (AC-020 … AC-041).
- Policy Engine (FS-01 … FS-12).
- RulesProvider.
- Agregación de insights con k ≥ 20 (AC-090).

## Integration

- API + DB: onboarding → dashboard → recomendación → prepare → confirm (AC-050).
- Decision Provider + fallback (AI-01 … AI-07).
- Payment flow (PY-01 … PY-07).

## Failure

- IA timeout / 429 / respuesta inválida.
- DB no disponible → 503 con mensaje claro.
- PaymentProvider no disponible.
- Doble click.
- Porcentajes inválidos.
- Capacidad segura cero.

## Manual

- Tres personas externas (idealmente estudiantes asistentes a QuiJAM) completan el loop sin explicación (NFR-024). UI/UX anota dónde dudan.
- Ensayo completo de `11-project/demo-script.md` con wifi apagado (NFR-033).
