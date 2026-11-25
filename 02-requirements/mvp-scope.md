# Alcance MVP

Dimensionado para QuiJAM: ≈19,5 h de reloj (jue 14:00 → vie 09:30), 5 personas. Plan horario en `00-quijam/plan-48h.md`.

## Regla de alcance

No entra nada que no mejore directamente el loop:

Entender → decidir → aprobar → actuar → progresar.

## P0 — Imprescindible (listo en la noche del jueves)

| # | Funcionalidad | FR | Dueño | Real / Simulado |
|---|---|---|---|---|
| 1 | Login + usuario seed | FR-001 … FR-003 | Backend + Frontend | Real |
| 2 | Onboarding (≤6 campos) + plantillas de meta | FR-010 … FR-015 | Frontend | Real |
| 3 | Modelo financiero y dashboard | FR-020 … FR-022 | Backend + Frontend | Real (cálculo); datos ingresados a mano |
| 4 | Recomendación explicada | FR-030 … FR-033 | AI Specialist | Real: LLM + RulesProvider de fallback |
| 5 | Policy Engine | FR-033 | Backend | Real |
| 6 | Meta con progreso | FR-040 … FR-043 | Frontend + Backend | Real |
| 7 | Confirmación y movimiento | FR-050 … FR-054 | Backend + Frontend | **Simulado:** ledger interno; no se mueve dinero real |
| 8 | Auditoría (DecisionLog, AuditLog) | FR-053 | Backend | Real |
| 9 | Seed + reset de demo | FR-100 | Backend | Real |

## P1 — Si P0 está verde al punto de control

| # | Funcionalidad | FR | Dueño | Real / Simulado |
|---|---|---|---|---|
| 1 | Chequeo "¿me alcanza?" | FR-034 | Backend + Frontend | Real |
| 2 | Gamificación básica (puntos, racha, 3 retos, 3 badges) | FR-060 … FR-063 | Frontend + UI/UX | Real |
| 3 | Vista de insights de ciudad | FR-090, FR-091 | AI Specialist + Frontend | **Simulado:** cohorte sintética en seed, etiquetada |
| 4 | Meta grupal | FR-080 … FR-083 | Backend | Real sobre ledger simulado |
| 5 | Ajuste de % de ahorro | FR-023 | Frontend | Real |

## P2 — Posterior / opcional

1. Open Payments con wallets de prueba (FR-055, ADR-007) — solo si sobra tiempo y no amenaza P0.
2. Revisión semanal (FR-070, FR-071).
3. Distribución de ingresos extra.
4. Clasificación avanzada y perfil financiero.
5. Integraciones bancarias o con billeteras comerciales (no en hackatón).

## Qué es real y qué es simulado (decirlo así en la demo)

- **Real:** cálculos, reglas de protección, recomendación con IA y fallback, persistencia, idempotencia, auditoría, gamificación.
- **Simulado:** el dinero (ledger interno con bolsillos), los insights de ciudad (datos sintéticos), el usuario de la demo (seed).
- **Opcional:** Open Payments en entorno de pruebas.

## Fuera de alcance

Ver `01-product/prd.md` §12.
