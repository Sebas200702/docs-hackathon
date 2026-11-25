# UX — Dashboard

## Objetivo

Responder en 5 segundos:

1. ¿Cómo estoy?
2. ¿Qué puedo hacer?
3. ¿Qué estoy intentando conseguir?

## Bloques (orden en móvil)

| Bloque | Contenido con el seed de Valentina | FR |
|---|---|---|
| Estado | "Vas bien este mes" / "Mes ajustado" / "Prioridad: liquidez" | FR-020 |
| Tu mes | Comprometido $520.000 · Para gastar $304.000 · Para ahorrar $76.000 | FR-021 |
| Puedes mover con seguridad | $150.000 (capacidad segura) con tooltip de cálculo | FR-020, FR-022 |
| Recomendación prioritaria | "Separa $76.000 para tu portátil" + botón Revisar | FR-030 |
| Meta principal | Portátil 16,7 % · $300.000 de $1.800.000 | FR-041 |
| ¿Me alcanza? | Campo de monto + botón | FR-034 (P1) |
| Progreso | Nivel, racha, reto actual | FR-060 … FR-063 (P1) |

## Estados

- **Vacío:** sin onboarding → CTA "Cuéntame tu mes en 2 minutos".
- **Mes ajustado:** capacidad segura 0 → sin recomendación de ahorro; mensaje "Este mes cuidamos lo básico. Tu meta sigue ahí."
- **Error:** dato no cargado → reintentar, sin perder lo que el usuario escribió.

## Vista institucional (P1)

Pantalla separada para el usuario institucional (FR-090): tarjetas por cohorte con proporción de usuarios con capacidad segura cero por semana del mes y categorías de meta más comunes. Etiqueta visible "Datos sintéticos — demo" mientras use seed. Nunca muestra individuos.

## Regla

El dashboard no es una colección de gráficos. Cada bloque ayuda a comprender o actuar.
