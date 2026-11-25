# ADR-006 — Stack

## Decisión

React/Vite, Bun/Hono/TypeScript, PostgreSQL/Drizzle, Zod, Vitest, Decision Providers (LLM + reglas) y Payment Providers (ledger simulado por defecto; Open Payments opcional, ver ADR-007).

- **LLM:** Gemini vía la Gemini API, con llave de Google AI Studio guardada solo en el servidor (`GEMINI_API_KEY`). Modelo de clase Flash; la versión exacta la fija el AI Specialist en el evento (`GEMINI_MODEL`).
- **Fallback:** `RulesProvider` determinista. Ambos implementan la interfaz `DecisionProvider`, así que cambiar de proveedor no toca el dominio.

## Razón

Es el stack establecido en el plan técnico y permite implementar el MVP dentro de la ventana de construcción de QuiJAM.

Gemini es la opción más sencilla de aplicar (decisión del equipo): tiene nivel gratuito y todo el equipo ya lo usó (Gemini Live en Manglara, Gemini API en Alpine-Translate, Gemini en UltraCem).

## Consecuencia

La documentación y contratos deben mantenerse alineados con este stack. Si Gemini falla o no hay red, responde `RulesProvider` y el Policy Engine (ADR-004) sigue aplicando.
