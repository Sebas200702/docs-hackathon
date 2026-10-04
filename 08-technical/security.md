# Seguridad

## Autenticación

Login obligatorio para el producto.

## Autorización

El usuario solo puede acceder/modificar sus propios datos y recursos permitidos.

## Datos financieros

Minimizar datos almacenados y registrar únicamente lo necesario.

## Payments

- Confirmación explícita.
- Idempotencia.
- Auditoría.
- No ejecutar desde IA.

## API

- Validación Zod.
- Rate limiting.
- Secrets fuera del repositorio.
- Logs sin exponer información sensible.

## Auditoría

Registrar decisiones y operaciones relevantes.
