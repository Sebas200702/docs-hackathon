# Requisitos No Funcionales

## Rendimiento

- API p95 objetivo: <400 ms para operaciones normales.
- Proveedor de decisión externo: <1.5 s antes de fallback.
- Fallback determinista: <100 ms como objetivo.

## Seguridad

- Validación de entradas.
- Autenticación.
- Autorización.
- Rate limiting.
- Protección de secretos.
- Confirmación explícita para movimientos.
- Idempotencia.
- Auditoría.

## Confiabilidad

- El fallo de IA no debe detener decisiones seguras.
- El fallo de Open Payments debe tener estrategia de demo/contingencia.
- El sistema debe poder restaurarse mediante datos seed/reset.

## UX

- Mobile-first.
- Lectura rápida.
- Lenguaje claro.
- Estados de loading, error y vacío.
- Acciones importantes claramente diferenciadas.

## Trazabilidad

Las decisiones financieras relevantes deben quedar registradas.
