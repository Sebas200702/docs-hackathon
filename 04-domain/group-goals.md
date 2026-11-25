# Metas Grupales

## Concepto

Una meta grupal separa:

**Responsabilidad final** ≠ **Contribución periódica**

Caso de uso en Barranquilla: tres estudiantes ahorran para un stand en una feria de emprendimiento (persona P3).

## Responsabilidad

`responsibilityTarget = target * finalPercentage`

Los porcentajes deben sumar exactamente 100 % (BR-030).

Ejemplo (montos ilustrativos): meta 900.000, 6 meses → Mariana 40 % = 360.000; Luis 30 % = 270.000; Sofía 30 % = 270.000.

## Aporte adaptativo

El sistema considera responsabilidad, progreso esperado, aportes acumulados, capacidad segura y contribución mínima:

```
remainingResponsibility = responsibilityTarget - contributedAmount
expectedByNow = responsibilityTarget * elapsedMonths / totalMonths
catchUpAmount = max(0, expectedByNow - contributedAmount)
recommended = min(remainingResponsibility, safeCapacity, max(catchUpAmount, minimumMonthlyContribution))
```

Ejemplo Luis, mes 3 de 6: responsabilidad 270.000, aportado 45.000 → esperado 135.000 → catch-up 90.000. Capacidad segura 20.000 → recomendado **20.000**. Su 30 % no cambia (BR-034).

## Privacidad dentro del grupo

Los miembros ven el progreso del grupo y el aporte acumulado de cada uno, no el saldo ni la capacidad de los demás.

## Regla

Un periodo difícil puede reducir el aporte recomendado sin cambiar la responsabilidad final acordada.
