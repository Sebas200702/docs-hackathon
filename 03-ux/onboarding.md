# UX — Onboarding

## Objetivo

Obtener el mínimo contexto para producir el primer valor en menos de 2 minutos (AC-010).

## Pasos y campos

| Paso | Pregunta en pantalla | Campo | Ejemplo (Valentina) |
|---|---|---|---|
| 1 | "¿Cuánto te entra al mes y de dónde?" | `incomes[]` (monto + fuente) | 600.000 trabajo parcial · 300.000 apoyo familiar |
| 2 | "¿Cuánto se te va sí o sí?" | `fixedExpenses` (total o lista corta) | 520.000 |
| 3 | "¿Cuánto tienes hoy?" | `liquidBalance` | 450.000 |
| 4 | "¿Qué de eso todavía tienes que pagar este mes?" | `pendingFixedExpenses` | 200.000 |
| 5 | "¿Cuánto nunca quieres tocar?" | `minimumProtectedBalance` (sugerido 10 % del ingreso, editable) | 100.000 |
| 6 | "¿Para qué quieres ahorrar?" | Meta desde plantilla (opcional) | Portátil 1.800.000 |
| Opcional | "¿Estudias en universidad o SENA? ¿Nos dejas usar tus datos de forma anónima para ayudar a la ciudad?" | `userType`, `institution`, `locality`, `insightsConsent` (desmarcado) | Universitaria, Soledad, sí |

## Resultado

Pantalla "Tu mes" con:

- comprometido;
- para gastar;
- para ahorrar;
- capacidad segura;
- primera recomendación;
- meta.

## Principios

- Un campo por pantalla, teclado numérico, formato COP mientras se escribe.
- Lenguaje cotidiano, sin términos como "liquidez" o "pasivo".
- Barra de progreso del onboarding.
- Se puede volver atrás sin perder datos.
