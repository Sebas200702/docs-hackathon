# Límites de IA

Dueño: AI Specialist.

## Puede

- Interpretar el contexto financiero estructurado.
- Seleccionar una recomendación estructurada entre tipos permitidos.
- Explicar la recomendación en lenguaje cotidiano y cercano, con los números del usuario.
- Adaptar el tono (sin culpa, sin infantilizar).
- (P1) Redactar la frase de cada insight agregado a partir de números ya calculados.

## No puede

- Ejecutar movimientos ni llamar al PaymentProvider.
- Modificar saldos.
- Cambiar porcentajes de responsabilidad.
- Saltarse límites del Policy Engine.
- Omitir la confirmación.
- Ser la única fuente de reglas financieras.
- Recibir email, nombre o identificadores del usuario (se envía solo el estado numérico).
- Inventar cifras de contexto (estadísticas de la ciudad).

## Arquitectura

LLM / RulesProvider → Policy Engine → Usuario → PaymentProvider (ledger simulado u Open Payments).
