# Requisitos Funcionales

Prioridad: P0 = imprescindible para la demo; P1 = si hay tiempo; P2 = posterior. Criterios en `acceptance-criteria.md`. Historias en `user-stories.md`.

## Autenticación

| ID | Requisito | Prior. | AC |
|---|---|---|---|
| FR-001 | Registro/login con email y contraseña. En la demo existe un usuario seed (Valentina). | P0 | AC-001 |
| FR-002 | Mantener sesión autenticada (cookie httpOnly). | P0 | AC-001 |
| FR-003 | Toda información financiera pertenece al usuario autenticado y solo él la lee o modifica. | P0 | AC-002 |

## Onboarding

| ID | Requisito | Prior. | AC |
|---|---|---|---|
| FR-010 | Capturar ingreso mensual con su fuente (trabajo parcial, práctica, cuota de aprendizaje, beca, apoyo familiar, freelance, ocasional). | P0 | AC-010 |
| FR-011 | Capturar gastos fijos (total o lista corta: transporte, alimentación, celular, materiales, aporte en casa). | P0 | AC-010 |
| FR-012 | Capturar saldo disponible hoy. | P0 | AC-010 |
| FR-013 | Capturar fijos aún pendientes de pago en el mes. | P0 | AC-010 |
| FR-014 | Capturar saldo mínimo protegido (sugerido por defecto, editable). | P0 | AC-010 |
| FR-015 | Crear primera meta desde plantillas: herramienta de estudio, curso/certificación, emprendimiento, fondo de emergencia, otra. | P0 | AC-040 |
| FR-016 | Capturar opcionalmente tipo de usuario (universitario/aprendiz SENA/otro), institución y localidad, y consentimiento para insights agregados (desmarcado por defecto). | P1 | AC-091 |

## Presupuesto

| ID | Requisito | Prior. | AC |
|---|---|---|---|
| FR-020 | Calcular margen, ahorro recomendado, presupuesto variable, disponible neto y capacidad segura (`04-domain/financial-model.md`). | P0 | AC-020 |
| FR-021 | Mostrar la distribución del mes en tres bloques: comprometido, para gastar, para ahorrar. | P0 | AC-020 |
| FR-022 | Explicar la distribución en una frase con los números del usuario. | P0 | AC-021 |
| FR-023 | Permitir ajustar el porcentaje de ahorro (0–50 %). | P1 | AC-022 |

## Recomendaciones

| ID | Requisito | Prior. | AC |
|---|---|---|---|
| FR-030 | Generar una recomendación prioritaria de aporte a meta. | P0 | AC-030 |
| FR-031 | Mostrar la razón de la recomendación. | P0 | AC-030 |
| FR-032 | Permitir aceptar, modificar el monto o rechazar. | P0 | AC-031 |
| FR-033 | Aplicar el Policy Engine antes de mostrar cualquier acción. | P0 | AC-032 |
| FR-034 | Chequeo de compra: dado un monto, responder recomendable / no recomendable con explicación. | P1 | AC-034 |

## Metas

| ID | Requisito | Prior. | AC |
|---|---|---|---|
| FR-040 | Crear meta (nombre, categoría, monto objetivo, fecha). | P0 | AC-040 |
| FR-041 | Mostrar progreso (%), aportado, restante, fecha. | P0 | AC-040 |
| FR-042 | Registrar aportes solo desde un movimiento completado. | P0 | AC-050 |
| FR-043 | Calcular restante y aporte mensual necesario para la fecha. | P0 | AC-041 |

## Ejecución de movimientos (PaymentProvider)

| ID | Requisito | Prior. | AC |
|---|---|---|---|
| FR-050 | Preparar una intención de movimiento desde una recomendación aprobada. | P0 | AC-050 |
| FR-051 | Mostrar monto, origen, destino y razón; requerir confirmación explícita. | P0 | AC-050 |
| FR-052 | Ejecutar en el proveedor configurado (por defecto ledger simulado). | P0 | AC-050 |
| FR-053 | Registrar el resultado (completado, rechazado, error, pendiente). | P0 | AC-051 |
| FR-054 | Evitar duplicados mediante idempotency key. | P0 | AC-052 |
| FR-055 | Proveedor seleccionable por configuración (`simulated` / `open_payments`). | P2 (opcional) | AC-053 |

## Gamificación

| ID | Requisito | Prior. | AC |
|---|---|---|---|
| FR-060 | Registrar progreso (puntos por acción útil). | P1 | AC-060 |
| FR-061 | Retos semanales predefinidos (3 en seed). | P1 | AC-060 |
| FR-062 | Racha semanal (semana con al menos una acción aprobada o revisión hecha). | P1 | AC-061 |
| FR-063 | Niveles de estabilidad y badges. | P1 | AC-060 |

## Revisión

| ID | Requisito | Prior. | AC |
|---|---|---|---|
| FR-070 | Generar revisión semanal. | P2 | — |
| FR-071 | Mostrar una acción prioritaria de la semana. | P2 | — |

## Metas grupales

| ID | Requisito | Prior. | AC |
|---|---|---|---|
| FR-080 | Crear meta grupal con miembros y porcentaje de responsabilidad final. | P1 | AC-080 |
| FR-081 | Activar solo si los porcentajes suman exactamente 100 %. | P1 | AC-080 |
| FR-082 | Recomendar aporte del periodo por miembro según capacidad (`04-domain/group-goals.md`). | P1 | AC-081 |
| FR-083 | Aportar con la misma confirmación e idempotencia de FR-050 … FR-054. | P1 | AC-081 |

## Impacto ciudad

| ID | Requisito | Prior. | AC |
|---|---|---|---|
| FR-090 | Vista de insights agregados por periodo y cohorte (tipo de usuario, institución, localidad). | P1 | AC-090 |
| FR-091 | El usuario puede dar y revocar consentimiento para insights. | P1 | AC-091 |

## Demo

| ID | Requisito | Prior. | AC |
|---|---|---|---|
| FR-100 | `POST /demo/reset` restaura el seed (Valentina, Andrés, grupo de Mariana, cohorte sintética). | P0 | AC-100 |
