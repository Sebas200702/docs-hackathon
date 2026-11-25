# Reglas de Negocio

Todas las aplica el Policy Engine (`06-ai/policy-engine.md`). Montos en COP enteros.

## Protección financiera

BR-001: Nunca recomendar ni ejecutar una contribución mayor que la capacidad segura (`safeCapacity`). Ejemplo: Valentina, capacidad 150.000 → máximo 150.000.

BR-002: Una compra mayor que la capacidad segura es "no recomendable" y se informa el faltante. Ejemplo: 180.000 → faltan 30.000.

BR-003: Capacidad segura ≤ 0 produce recomendación 0 con mensaje sin culpa.

BR-004: Ingresos, gastos y saldos no pueden ser negativos en la entrada.

BR-005: Montos recomendados se redondean hacia abajo al múltiplo de 1.000.

## IA

BR-010: La IA no puede ejecutar movimientos.

BR-011: La IA no puede cambiar responsabilidades ni reglas.

BR-012: Respuesta inválida, timeout, 429 o baja confianza (<0,6) activan el RulesProvider.

## Movimientos (cualquier PaymentProvider)

BR-020: Todo movimiento requiere confirmación explícita del usuario.

BR-021: Toda operación lleva idempotency key única; repetirla devuelve el mismo resultado.

BR-022: El resultado se registra; la meta solo cambia con estado `completed`.

BR-023: Timeout nunca equivale a éxito: queda `pending_reconciliation`.

## Metas grupales

BR-030: Las responsabilidades suman exactamente 100 %.

BR-031: El porcentaje representa responsabilidad final, no cuota periódica.

BR-032: El aporte periódico se adapta a la capacidad.

BR-033: El aporte no puede superar la responsabilidad restante.

BR-034: El motor no puede redistribuir porcentajes.

## Insights de ciudad

BR-040: Solo se publican cohortes con al menos 20 usuarios con consentimiento (k-anonimato).

BR-041: Ningún insight contiene identificadores, montos individuales ni texto libre del usuario.

BR-042: Solo cuentan usuarios con `insightsConsent = true` en el momento del cálculo.
