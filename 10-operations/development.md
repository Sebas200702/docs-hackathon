# Desarrollo Local

## Requisitos

- Bun.
- Node-compatible tooling cuando sea necesario.
- PostgreSQL (local o Docker).
- Variables de entorno (`deployment.md`); `.env` nunca se versiona.

## Flujo

Instalar → configurar env → migrar DB → seed → ejecutar API/frontend → ejecutar tests.

## Trabajo en paralelo (5 roles)

- Contratos Zod (`08-technical/contracts.md`) primero: Frontend trabaja con mocks del contrato mientras Backend implementa.
- RulesProvider antes que el LLM: el loop funciona desde la primera hora.
- Ramas cortas `feat/*`, merge frecuente a la rama principal del evento.

## Demo

Mantener seed reproducible (v1) y comando de reset.
