# Payment Provider Tests

El nombre del archivo se conserva. Estos tests aplican a cualquier `PaymentProvider`; en el MVP se ejecutan contra `SimulatedLedgerProvider` y un stub que fuerza cada resultado. Si se integra Open Payments, se repiten contra wallets de prueba.

## Casos

| ID | Caso | Esperado |
|---|---|---|
| PY-01 | Éxito | `completed`; Disponible −76.000, Meta +76.000; AuditLog |
| PY-02 | Rechazo | `rejected`; saldos y meta sin cambio |
| PY-03 | Timeout | `pending_reconciliation`; nunca `completed`; meta sin cambio |
| PY-04 | Proveedor no disponible | `failed`; reintento con la misma key |
| PY-05 | Request inválido (monto 0 o destino ajeno) | 400 / 403; sin `PaymentIntent` ejecutado |
| PY-06 | Request duplicado | Una sola ejecución (FS-07) |
| PY-07 | Reconciliación | `pending_reconciliation` → `getStatus` = `completed` → meta actualizada una vez |

## Invariantes

- Nunca asumir éxito por timeout.
- Nunca ejecutar dos veces la misma intención.
- Registrar resultado.
- Actualizar dominio solo cuando el estado es consistente.
- En el ledger simulado, la suma de entradas por intento es 0.
