# AI Failure Tests

Dueño: AI Specialist. Se ejecutan con un LLM falso (stub) configurable.

| ID | Caso | Entrada del stub | Resultado esperado |
|---|---|---|---|
| AI-01 | Timeout | Responde en 3 s | RulesProvider en ≤1,6 s total; `fallbackReason = timeout` |
| AI-02 | HTTP 429 | 429 | RulesProvider; `fallbackReason = rate_limited` |
| AI-03 | JSON inválido | `"hola"` o campos faltantes | Rechazo Zod; RulesProvider; `fallbackReason = invalid_output` |
| AI-04 | Baja confianza | `confidence: 0.4` | RulesProvider (conservador) |
| AI-05 | Contexto incompleto | Perfil sin `liquidBalance` | Sin acción de movimiento; pide completar perfil |
| AI-06 | Monto peligroso | `amount: 300000` con capacidad 150.000 | Policy Engine recorta a ≤150.000 (`capped`) o bloquea |
| AI-07 | Datos personales | — | El request al LLM no contiene email, nombre ni institución |

## Principio

La IA mejora la experiencia; su caída no rompe las reglas financieras ni la demo.
