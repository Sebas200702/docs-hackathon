# Modelo Financiero

Montos enteros en COP. Ejemplo con el seed de Valentina (`01-product/personas.md`).

## Conceptos

| Concepto | Fórmula | Valentina |
|---|---|---|
| Margin | `margin = monthlyIncome - fixedExpenses` | 900.000 − 520.000 = **380.000** |
| Recommended savings | `recommendedSavings = max(0, floor(margin * savingsRate))` (savingsRate por defecto 0,20) | **76.000** |
| Variable budget | `variableBudget = max(0, margin - recommendedSavings)` | **304.000** |
| Net available | `netAvailable = liquidBalance - pendingFixedExpenses` | 450.000 − 200.000 = **250.000** |
| Safe capacity | `safeCapacity = max(0, liquidBalance - pendingFixedExpenses - minimumProtectedBalance)` | 450.000 − 200.000 − 100.000 = **150.000** |

## Recomendación de aporte a meta (RulesProvider)

```
pendingSavingsThisPeriod = max(0, recommendedSavings - savedThisPeriod)
amount = roundDown1000(min(safeCapacity, pendingSavingsThisPeriod))
```

Valentina: `min(150.000, 76.000) = 76.000`. Meta: 300.000 → 376.000 (20,9 %).

## Aporte mensual necesario de una meta

`monthlyNeeded = ceil((targetAmount - savedAmount) / monthsUntil(targetDate))` → (1.800.000 − 300.000) / 10 = 150.000.

Si `monthlyNeeded > recommendedSavings`, la UI lo dice sin culpa y sugiere mover la fecha.

## Chequeo de compra

`recommended = price <= safeCapacity`; `shortfall = max(0, price - safeCapacity)`.

## Casos borde

- `margin < 0` → `recommendedSavings = 0`, `variableBudget = 0`, estado "Prioridad: liquidez".
- `safeCapacity = 0` → recomendación 0 (BR-003).

## Principio

La capacidad segura limita cualquier recomendación de movimiento.
