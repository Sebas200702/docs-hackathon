# UX — Confirmación de movimientos

El nombre del archivo se conserva por historia. La experiencia es la misma con el ledger simulado (MVP) o con Open Payments (opcional, ADR-007). La interfaz **no** menciona la tecnología: habla de "separar dinero para tu meta".

## Principio

El usuario siempre entiende qué movimiento está aprobando.

## Flujo

Recomendación → Detalle → Monto (editable) → Origen → Destino → Razón → Aprobar / Rechazar → Procesando → Resultado.

## Pantalla de confirmación (seed)

```
Separar para tu meta
$76.000
De: Disponible          A: Meta · Portátil
Por qué: te quedan $150.000 que puedes mover sin tocar
pasajes, almuerzos ni tus $100.000 protegidos.
[ Aprobar ]   [ Cambiar monto ]   [ Ahora no ]
Modo demo: movimiento simulado, no se mueve dinero real.
```

## Estados

| Estado | Mensaje |
|---|---|
| `pending_confirmation` | Pantalla de arriba |
| `processing` | "Separando…" (botón deshabilitado: evita doble toque) |
| `completed` | "Listo. Tu portátil va en 20,9 %." |
| `rejected` | "No se hizo el movimiento. Tu dinero sigue igual." |
| `failed` | "Algo falló. Tu dinero sigue igual. Reintentar." |
| `pending_reconciliation` | "Estamos confirmando el resultado. No lo intentes de nuevo aún." |

## Mensaje UX

La automatización debe sentirse como una ayuda, no como pérdida de control.
