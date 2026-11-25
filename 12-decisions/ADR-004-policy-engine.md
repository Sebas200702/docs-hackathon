# ADR-004 — Policy Engine

## Decisión

Toda recomendación con impacto financiero pasa por reglas deterministas.

## Razón

La seguridad financiera no puede depender exclusivamente de un proveedor probabilístico.

## Consecuencia

El LLM (Gemini, ADR-006) puede fallar o equivocarse sin comprometer la seguridad del flujo: su salida nunca mueve dinero sin pasar por estas reglas.
