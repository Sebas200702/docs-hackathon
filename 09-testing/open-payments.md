# Open Payments Tests

## Casos

- Payment success.
- Payment rejection.
- Timeout.
- Provider unavailable.
- Invalid request.
- Duplicate request.
- Reconciliation/pending result.

## Invariantes

- Nunca asumir éxito por timeout.
- Nunca ejecutar dos veces la misma intención.
- Registrar resultado.
- Actualizar dominio solo cuando el estado sea consistente.
