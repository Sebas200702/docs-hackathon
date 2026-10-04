# Criterios de Aceptación

## Presupuesto

- El sistema no acepta ingresos negativos.
- Si los gastos fijos superan los ingresos, la prioridad es preservar liquidez.
- La distribución no puede producir valores financieros negativos.

## Recomendación

- Toda recomendación muestra su acción y contexto.
- Una recomendación inválida no puede avanzar.
- Una respuesta de IA inválida activa fallback.

## Distribución

- Debe existir confirmación explícita.
- La cantidad no puede superar la capacidad segura.
- La operación debe ser idempotente.
- El resultado debe registrarse.

## Open Payments

- El usuario puede revisar cantidad y destino antes de confirmar.
- El sistema registra éxito, rechazo o error.
- Un retry no debe crear una segunda operación.

## Meta grupal

- Las responsabilidades deben sumar exactamente 100%.
- El aporte recomendado no puede superar la responsabilidad restante.
- La capacidad segura limita el aporte.
- El motor no puede modificar porcentajes de responsabilidad.
