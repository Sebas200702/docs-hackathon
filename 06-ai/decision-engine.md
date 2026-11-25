# Decision Engine

## Propósito

Interpretar contexto financiero y producir decisiones estructuradas que después valida el Policy Engine.

## Flujo

Financial state → `DecisionRequest` → `DecisionProvider` → `DecisionResponse` (validada con Zod) → Policy Engine → `Recommendation` + `DecisionLog`.

## Providers

| Provider | Rol | Nota |
|---|---|---|
| `LlmProvider` (Gemini API) | Selecciona y explica | Modelo de clase Flash; la versión exacta la fija el AI Specialist en el evento (`GEMINI_MODEL`). Timeout 1,5 s. Llave solo en el servidor (ADR-006). |
| `RulesProvider` | Fallback determinista | Implementa `04-domain/financial-model.md`. Debe existir antes que el LLM. |

Ambos cumplen la misma interfaz `DecisionProvider`; cambiar Gemini por otro proveedor no toca el dominio.

## Entrada a Gemini (sin datos personales)

```json
{
  "state": { "monthlyIncome": 900000, "fixedExpenses": 520000, "safeCapacity": 150000,
             "recommendedSavings": 76000, "savedThisPeriod": 0,
             "goals": [{ "id": "g1", "category": "herramienta_estudio", "targetAmount": 1800000, "savedAmount": 300000, "monthsLeft": 10 }] },
  "allowedTypes": ["goal_contribution"],
  "questionVersion": "v1"
}
```

## Salida esperada

```json
{ "type": "goal_contribution", "goalId": "g1", "amount": 76000, "confidence": 0.82,
  "reason": "Te quedan $150.000 que puedes mover sin tocar pasajes, almuerzos ni tus $100.000 protegidos. Con $76.000 tu portátil pasa al 20,9 %." }
```

## Fallback

Se usa ante timeout, error HTTP, 429, JSON inválido, `confidence < 0,6` o contexto incompleto. Se registra `fallbackReason` en `DecisionLog`.

## Límite

El Decision Engine no ejecuta movimientos.
