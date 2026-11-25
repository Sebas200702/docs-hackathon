# Criterios de Aceptación

Formato: Dado / Cuando / Entonces. Los valores usan el seed de `01-product/personas.md` (Valentina: ingreso 900.000, fijos 520.000, saldo 450.000, fijos pendientes 200.000, saldo protegido 100.000, meta portátil 1.800.000 con 300.000 ahorrados). Montos en COP enteros.

## Autenticación

- **AC-001** Dado un usuario registrado, cuando inicia sesión con credenciales válidas, entonces recibe sesión y `GET /dashboard` responde 200; sin sesión responde 401.
- **AC-002** Dado el usuario A autenticado, cuando pide `GET /goals/:id` de una meta de B, entonces recibe 404 y no se filtra información.

## Onboarding

- **AC-010** Cuando envía el onboarding de Valentina, entonces se guarda el perfil y la respuesta incluye el presupuesto calculado. El formulario no tiene más de 6 campos obligatorios. Ingresos, gastos o saldos negativos responden 400 con el campo inválido.

## Presupuesto

- **AC-020** Dado el perfil de Valentina, entonces: `margin = 380.000`, `recommendedSavings = 76.000`, `variableBudget = 304.000`, `netAvailable = 250.000`, `safeCapacity = 150.000`.
- **AC-020b** Dado fijos > ingreso (ingreso 500.000, fijos 600.000), entonces `margin = -100.000`, `recommendedSavings = 0`, `variableBudget = 0`, y el dashboard muestra mensaje de prioridad de liquidez, sin recomendación de ahorro.
- **AC-021** La explicación contiene al menos el monto comprometido y la capacidad segura del usuario.
- **AC-022** Al ajustar ahorro a 30 %, `recommendedSavings = 114.000`; valores fuera de 0–50 % responden 400.

## Recomendación

- **AC-030** Dado Valentina, cuando pide recomendación, entonces recibe tipo `goal_contribution`, monto 76.000 a la meta portátil y una razón no vacía.
- **AC-031** Al modificar el monto a 50.000 se acepta; a 200.000 (> capacidad segura 150.000) responde 422 `EXCEEDS_SAFE_CAPACITY`. Al rechazar, el estado queda `rejected` y no se crea movimiento.
- **AC-032** Si el proveedor de IA propone 300.000, el Policy Engine la bloquea o la recorta a ≤150.000 y registra `policyOutcome` en `DecisionLog`.
- **AC-033** Si la IA responde JSON inválido, hace timeout (>1,5 s) o 429, la recomendación proviene de `rules` y el usuario ve una recomendación válida.

## Chequeo de compra

- **AC-034** Compra de 180.000 → `recommended: false`, `shortfall: 30.000`. Compra de 120.000 → `recommended: true`, `remainingSafeCapacity: 30.000`.

## Metas

- **AC-040** Crear meta con objetivo ≤0 o fecha pasada responde 400. La meta portátil muestra 16,7 % (300.000 / 1.800.000).
- **AC-041** Con 1.500.000 restantes y 10 meses a la fecha, aporte mensual necesario = 150.000.

## Movimiento

- **AC-050** Dada la recomendación aceptada de 76.000, cuando se prepara, entonces la vista previa muestra monto, origen "Disponible", destino "Meta: Portátil" y razón; sin `POST /payments/confirm` no cambia ningún saldo. Al confirmar con ledger simulado: Disponible −76.000, Meta +76.000, meta = 376.000 (20,9 %).
- **AC-051** Si el proveedor responde rechazo o error, la meta no cambia y el intento queda `rejected` o `failed` en auditoría. Un timeout deja `pending_reconciliation`, nunca `completed`.
- **AC-052** Dos `POST /payments/confirm` con la misma idempotency key producen un único movimiento; la segunda respuesta devuelve el mismo `paymentIntentId` y estado.
- **AC-053** (opcional) Con `PAYMENTS_PROVIDER=open_payments` y wallets de prueba configuradas, el mismo flujo completa un movimiento; si no hay configuración, el sistema arranca en `simulated` y lo indica en `GET /health`.

## Gamificación

- **AC-060** Al confirmar el primer aporte, se otorga el badge "Primer paso" y aumentan los puntos; no hay ranking entre usuarios.
- **AC-061** Una semana con capacidad segura 0 y revisión hecha no rompe la racha (caso Andrés).

## Meta grupal

- **AC-080** Porcentajes 40/30/30 permiten activar; 40/30/20 responde 422 `PERCENTAGES_NOT_100`. Responsabilidades: 360.000 / 270.000 / 270.000 sobre 900.000.
- **AC-081** Si Luis tiene capacidad segura 20.000 y un aporte de recuperación de 90.000, la recomendación es 20.000 y su porcentaje sigue en 30 %. Un aporte mayor a su responsabilidad restante responde 422.

## Insights

- **AC-090** Una cohorte con menos de 20 usuarios con consentimiento no aparece en la respuesta. Ninguna respuesta contiene ids, emails ni montos individuales. La vista muestra la etiqueta "Datos sintéticos" cuando proviene del seed.
- **AC-091** Al revocar consentimiento, el usuario deja de contar en el siguiente cálculo de insights.

## Demo

- **AC-100** `POST /demo/reset` deja los valores de AC-020 y AC-040 exactamente como en el seed en <5 s.
