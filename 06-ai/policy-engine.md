# Policy Engine

## Propósito

Aplicar reglas deterministas de seguridad financiera antes de permitir una recomendación o acción.

## Responsabilidades

- Validar capacidad.
- Validar responsabilidad restante.
- Validar porcentajes.
- Validar confirmación.
- Validar idempotencia.
- Bloquear acciones inválidas.

## Principio

Aunque el proveedor de decisiones produzca una respuesta incorrecta, el Policy Engine debe impedir una operación financieramente insegura.
