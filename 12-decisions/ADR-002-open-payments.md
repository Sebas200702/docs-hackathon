# ADR-002 — Open Payments como capacidad central

## Estado

**Reemplazada por ADR-007** (2026-11-24). Se conserva como registro histórico.

## Decisión original

Open Payments forma parte del MVP de la hackathon.

## Razón original

Se asumía que la hackathon estaba orientada a Interledger y que la propuesta debía demostrar una aplicación sustantiva de esa tecnología.

## Consecuencia original

La demo debía mostrar una recomendación transformada en una distribución aprobada mediante Open Payments.

## Por qué se reemplaza

La competencia es QuiJAM 2026, cuyo reto se centra en la calidad de vida de los ciudadanos de Barranquilla y en el talento joven, no en Interledger. Open Payments pasa a ser una capa de ejecución opcional detrás de `PaymentProvider`; el MVP usa un ledger simulado. Ver ADR-007.
