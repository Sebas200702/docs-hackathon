# Policy Engine

## Propósito

Aplicar reglas deterministas de seguridad financiera antes de mostrar una recomendación o ejecutar una acción. Dueño: Backend.

## Responsabilidades

| Validación | Regla | Resultado |
|---|---|---|
| Monto ≤ capacidad segura | BR-001 | Recorta (`capped`) en recomendación; 422 `EXCEEDS_SAFE_CAPACITY` si el usuario modifica |
| Capacidad 0 | BR-003 | Recomendación 0 |
| Redondeo | BR-005 | Múltiplo de 1.000 hacia abajo |
| Responsabilidad restante | BR-033 | 422 `EXCEEDS_REMAINING_RESPONSIBILITY` |
| Porcentajes = 100 % | BR-030 | 422 `PERCENTAGES_NOT_100` |
| Confirmación presente | BR-020 | 409 `CONFIRMATION_REQUIRED` |
| Idempotencia | BR-021 | Devuelve intento existente |
| Destino propio | — | 403 `FORBIDDEN_DESTINATION` |

## Firma

```ts
evaluate(action, context): { outcome: 'allowed' | 'capped' | 'blocked'; amount: number; code?: string }
```

Función pura, sin I/O: fácil de testear (FS-01 … FS-10).

## Principio

Aunque el proveedor de decisiones produzca una respuesta incorrecta, el Policy Engine impide una operación financieramente insegura.
