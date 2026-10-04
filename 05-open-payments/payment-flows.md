# Open Payments — Payment Flows

## Flujo aprobado

Recommendation → Policy validation → User confirmation → Payment preparation → Open Payments → Result → Domain update → Audit.

## Éxito

Actualizar meta/estado y registrar operación.

## Rechazo

Mantener estado financiero y registrar rechazo.

## Error

Mostrar estado recuperable y evitar duplicación.

## Timeout

No asumir éxito. Consultar/reconciliar según el mecanismo disponible o mantener estado pendiente.

## Duplicado

La idempotency key debe impedir doble movimiento.
