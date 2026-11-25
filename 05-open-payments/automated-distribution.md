# Distribución Automatizada

## Objetivo

Convertir una recomendación aprobada en una separación de dinero hacia una meta.

## Ejemplo (seed, ledger simulado)

Valentina: capacidad segura 150.000 → recomendación 76.000 a "Portátil" → aprueba → `SimulatedLedgerProvider` registra:

| Cuenta | Antes | Entrada | Después |
|---|---|---|---|
| Disponible | 450.000 | −76.000 | 374.000 |
| Meta · Portátil | 300.000 | +76.000 | 376.000 |

Meta al 20,9 %, +10 puntos, badge "Primer paso".

Nota: el saldo "Disponible" del ledger y `liquidBalance` del perfil se mantienen iguales; tras el movimiento la capacidad segura pasa a 74.000.

## Controles

- Monto ≤ capacidad segura (BR-001).
- Destino perteneciente al usuario o a un grupo del que es miembro.
- Confirmación explícita (BR-020).
- Idempotencia (BR-021).
- Auditoría (BR-022).

## Futuro

Aportes recurrentes y reglas de separación programada, siempre con consentimiento revocable; con Open Payments, mediante autorizaciones explícitas del usuario.
