# Decision Engine

## Propósito

Interpretar contexto financiero y producir decisiones estructuradas que después valida el Policy Engine.

## Flujo

Financial state → `DecisionRequest` → `DecisionProvider` → `DecisionResponse` (validada con Zod) → Policy Engine → `Recommendation` + `DecisionLog`.

## Providers

| Provider | Rol | Nota |
|---|---|---|
| `LlmProvider` (OpenJEV u otro LLM) | Selecciona y explica | Timeout 1,5 s. Modelo concreto lo fija el AI Specialist en el evento según conectividad. |
| `RulesProvider` | Fallback determinista | Implementa `04-domain/financial-model.md`. Debe existir antes que el LLM. |

Ambos cumplen la misma interfaz; se pueden añadir otros sin cambiar el dominio.

## Entrada al LLM (sin datos personales)

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
