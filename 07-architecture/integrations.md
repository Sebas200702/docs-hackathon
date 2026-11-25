# Integraciones

| Integración | Uso | Si falla |
|---|---|---|
| Gemini API (Google AI Studio, llave solo en el servidor) | Selección y explicación de recomendaciones | RulesProvider (AI-01 … AI-05) |
| PaymentProvider · ledger simulado | Movimientos del MVP (interno, sin red) | No depende de terceros |
| PaymentProvider · Open Payments (opcional) | Movimientos entre wallets de prueba | Volver a `simulated` por configuración |
| PostgreSQL | Persistencia | Entorno local con seed |
| Autenticación | Acceso seguro | Usuario seed local para demo |

## Principio

Las integraciones externas no son puntos únicos de fallo del flujo de decisión ni de la demo.
