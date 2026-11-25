# Flujos de movimiento

Aplican igual a `simulated` y `open_payments`.

## Flujo aprobado

Recommendation → Policy validation → `POST /payments/prepare` (crea `PaymentIntent` en `pending_confirmation`) → User confirmation → `POST /payments/confirm` (`processing`) → PaymentProvider → Result → Domain update → Audit.

## Éxito (`completed`)

Crear `LedgerEntry` (simulado) o guardar `externalRef` (Open Payments), actualizar meta y progreso, registrar `AuditLog`.

## Rechazo (`rejected`)

Mantener estado financiero y registrar rechazo.

## Error (`failed`)

Mostrar estado recuperable; reintentar con la **misma** idempotency key.

## Timeout (`pending_reconciliation`)

No asumir éxito. Consultar `getStatus` hasta 3 veces; si sigue sin respuesta, mantener pendiente y no permitir un nuevo intento sobre la misma recomendación.

## Duplicado

La idempotency key (`rec:{recommendationId}`) es única en base de datos; una segunda confirmación devuelve el `PaymentIntent` existente.

## Notas para Open Payments (solo si se integra)

Requiere wallets de prueba y credenciales del entorno de pruebas en variables de entorno. Antes de implementarlo, confirmar el flujo vigente de autorizaciones en la documentación oficial de Open Payments; este documento no fija detalles del protocolo.
