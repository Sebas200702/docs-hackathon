# Financial Safety Tests

Tests unitarios del Policy Engine y del modelo financiero. Base: seed de Valentina salvo indicación.

| ID | Caso | Datos | Esperado |
|---|---|---|---|
| FS-01 | Saldo insuficiente | Compra 180.000, capacidad 150.000 | `recommended: false`, `shortfall: 30.000` |
| FS-02 | Obligaciones pendientes altas | Saldo 450.000, pendientes 400.000, protegido 100.000 | `safeCapacity = 0` |
| FS-03 | Saldo protegido | Aporte que dejaría saldo < 100.000 + pendientes | Recortado a capacidad segura |
| FS-04 | Capacidad segura cero | `safeCapacity = 0` | Recomendación 0, mensaje sin culpa |
| FS-05 | Aporte > responsabilidad restante | Luis, restante 225.000, aporte 250.000 | 422 `EXCEEDS_REMAINING_RESPONSIBILITY` |
| FS-06 | Porcentajes ≠ 100 % | 40/30/20 | 422 `PERCENTAGES_NOT_100` |
| FS-07 | Duplicación | Dos confirmaciones con la misma key | Un solo `PaymentIntent` y un par de `LedgerEntry` |
| FS-08 | Confirmación ausente | `confirmed: false` | 409, saldos sin cambio |
| FS-09 | Respuesta de IA inválida | Ver AI-03 | Recomendación válida de reglas |
| FS-10 | Proveedor de decisión caído | Ver AI-01/AI-02 | Recomendación válida de reglas |
| FS-11 | Margen negativo | Ingreso 500.000, fijos 600.000 | Ahorro 0, estado "Prioridad: liquidez" |
| FS-12 | Entrada negativa | `liquidBalance: -1` | 400 |

Resultado esperado global: ninguna acción financieramente insegura llega a ejecución.
