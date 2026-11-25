# PRD — Copiloto de Salud Financiera

## 1. Resumen

Copiloto de Salud Financiera es un sistema de presupuesto autónomo para jóvenes de Barranquilla con ingresos limitados. Busca que gestionar dinero sea ligero, comprensible y accionable, y que las metas que abren oportunidades avancen. Se presenta en QuiJAM 2026, eje Economía y oportunidades.

## 2. Problema

La gestión financiera se vuelve una tarea repetitiva: registrar, categorizar, revisar dashboards y decidir manualmente qué hacer con el dinero. Para un joven con ingresos irregulares, el costo de no hacerlo es alto: se quedan sin margen a fin de mes y abandonan metas como un portátil, un curso o un emprendimiento.

Magnitud del problema en Barranquilla: [DATO POR VERIFICAR — fuente sugerida: DANE GEIH (desempleo e informalidad juvenil), SPADIES/MEN (deserción), Banca de las Oportunidades (ahorro e inclusión financiera)].

El producto aborda la fricción entre conocer el estado financiero y actuar sobre él.

## 3. Oportunidad

Una experiencia centrada en decisiones y hábitos, donde el sistema reduzca la carga operativa y convierta la gestión financiera en pequeñas acciones con progreso visible. Para la ciudad: una fuente agregada y anónima sobre la fragilidad financiera juvenil.

## 4. Visión

Un copiloto que organice el presupuesto, detecte oportunidades, recomiende acciones seguras, ayude a construir hábitos y separe dinero hacia metas con aprobación del usuario, mediante un adaptador de pagos (ledger simulado hoy; Open Payments u otros proveedores mañana).

## 5. Objetivos

| ID | Objetivo | Señal verificable en la demo |
|---|---|---|
| O1 | Reducir la fricción de presupuestar | Onboarding en ≤6 campos y <2 min (AC-010) |
| O2 | Claridad sobre el dinero disponible | Dashboard muestra comprometido, disponible y capacidad segura (AC-020) |
| O3 | Ahorrar para metas de oportunidad | Aporte aprobado actualiza la meta (AC-050) |
| O4 | Proteger obligaciones | Ninguna recomendación supera capacidad segura (FS-01 … FS-04) |
| O5 | Motivar sin culpa | Copy revisado sin lenguaje culpabilizante (NFR-021) |
| O6 | Aportar valor a la ciudad | Vista de insights agregados con umbral de anonimato (AC-090) |

## 6. Usuario objetivo

Universitarios y aprendices SENA en Barranquilla y su área metropolitana, con ingresos limitados e irregulares, que usan el celular para todo y quieren avanzar en metas sin mantener sistemas manuales. Ver `personas.md`.

## 7. Propuesta de valor

> Gestiona tu dinero sin convertirlo en otra tarea.

## 8. Principios

Ver `product-principles.md`.

## 9. Casos de uso

| Caso | Prioridad | Persona |
|---|---|---|
| Presupuesto inicial automático | P0 | Valentina |
| Lectura del estado financiero | P0 | Valentina |
| Recomendación de aporte a meta + aprobación + separación | P0 | Valentina |
| Chequeo "¿me alcanza?" | P1 | Valentina |
| Capacidad cero sin culpa | P1 | Andrés |
| Gamificación básica (racha, nivel, reto) | P1 | Todas |
| Insights agregados (datos sintéticos) | P1 | Institucional |
| Meta grupal | P1 | Mariana |
| Distribución de ingreso extra, revisión semanal | P2 | Todas |

## 10. Capa de ejecución de pagos

La recomendación aprobada se materializa a través de un `PaymentProvider`:

- **MVP (real en la demo):** `SimulatedLedgerProvider`, ledger de doble entrada con bolsillos (Disponible, Meta, Grupo).
- **Opcional:** `OpenPaymentsProvider` contra wallets de prueba compatibles con Open Payments. Solo se integra si el P0 está terminado (ADR-007). No es requisito para demostrar el producto ni el objetivo del concurso.

Flujo: Recomendación → Policy Engine → Confirmación → PaymentProvider → Movimiento → Actualización → Registro. Detalle en `05-open-payments/`.

## 11. Gamificación

Refuerza comportamientos útiles mediante niveles, progreso, rachas, retos y badges, sin competencia agresiva ni diseño infantil. Ver `03-ux/gamification.md`.

## 12. MVP

Ver `02-requirements/mvp-scope.md` (fuente única de alcance, con real vs simulado).

### Fuera de alcance

- Trading e inversión.
- Préstamos y scoring crediticio.
- Marketplace financiero.
- Integraciones bancarias o con billeteras comerciales reales.
- Movimiento de dinero real.
- OCR.
- Leaderboards públicos.
- Automatizaciones irreversibles.
- IA ejecutando pagos directamente.

## 13. Éxito

En la demo, un usuario pasa de información financiera mínima a una recomendación explicada, la aprueba y ve la separación aplicada a su meta en el ledger simulado, sin comprometer sus obligaciones. Ante una compra que no le alcanza, recibe una respuesta honesta. La institución ve un insight agregado sin datos individuales.

Después de la hackatón (piloto): proporción de metas con al menos un aporte mensual y proporción de usuarios con capacidad segura cero a fin de mes. Línea base: [DATO POR VERIFICAR — se mide en el piloto; no hay dato previo].

## 14. Riesgos

| Riesgo | Mitigación |
|---|---|
| Exceso de funcionalidades | Regla de alcance y punto de control de las 18:00 (`00-quijam/plan-48h.md`) |
| Gamificación infantil | Revisión de UI/UX; badges ligados a conducta financiera |
| Automatización opaca | Pantalla de confirmación con monto, origen, destino y razón |
| Recomendaciones genéricas | Explicación con números del propio usuario |
| Decisiones financieras incorrectas | Policy Engine + tests FS-01 … FS-10 |
| Fallo de proveedores (IA, pagos, red) | RulesProvider, ledger simulado, demo local |
| Jurado percibe tecnología sin necesidad real | Pitch abre con persona y ciudad; Open Payments queda en segundo plano |

## 15. Definición del producto

> Copiloto de Salud Financiera es un sistema de presupuesto autónomo para jóvenes de Barranquilla con ingresos limitados que reduce la fricción de gestionar dinero mediante recomendaciones seguras, separación aprobada de dinero hacia metas de oportunidad y progreso visible. Su autonomía está controlada: el sistema propone, las reglas protegen, el usuario aprueba y el proveedor de pagos materializa la acción.
