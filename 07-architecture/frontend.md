# Arquitectura Frontend

## Pantallas

| Pantalla | Ruta | Prior. |
|---|---|---|
| Login | `/login` | P0 |
| Onboarding (6 pasos) | `/onboarding` | P0 |
| Dashboard "Tu mes" | `/` | P0 |
| Detalle de recomendación | `/recommendations/:id` | P0 |
| Confirmación y resultado | `/payments/:id` | P0 |
| Meta | `/goals/:id` | P0 |
| ¿Me alcanza? | modal en dashboard | P1 |
| Progreso (nivel, racha, retos) | `/progress` | P1 |
| Meta grupal | `/groups/:id` | P1 |
| Insights de ciudad | `/insights` (rol institucional) | P1 |

## Principios

- Componentes orientados a dominio.
- Estados loading/error/empty en todas las pantallas P0.
- Mobile-first (360 px).
- Acciones de movimiento con confirmación explícita y botón deshabilitado mientras procesa.
- Formato COP con `Intl.NumberFormat('es-CO')`.
- Copy centralizado para que UI/UX lo revise en un solo archivo.
