# docs-hackathon

## Copiloto de Salud Financiera — Documentación (QuiJAM 2026)

Copiloto de presupuesto para **jóvenes de Barranquilla con ingresos limitados** —universitarios y aprendices SENA—. Convierte pocos datos en una lectura clara del dinero, una recomendación segura y una acción aprobada (separar dinero para una meta), con progreso visible.

Responde al reto de QuiJAM 2026: *"¿cómo usar tecnología, innovación y talento joven para mejorar la calidad de vida de los ciudadanos de Barranquilla?"*, en el eje **Economía y oportunidades** ("Impulsa el talento y los negocios locales. Abre caminos hacia el empleo, el emprendimiento y la inclusión.").

Open Payments (Interledger) **no es el objetivo del concurso**: es una capa de ejecución opcional. El MVP funciona y se demuestra con un **ledger simulado** (ver `12-decisions/ADR-007-reanclaje-quijam.md`).

## Fuente documental

Esta documentación consolida el PRD y el Plan Técnico del proyecto, reanclados al reto QuiJAM. Cuando existe una decisión específica del equipo, prevalece la decisión más reciente acordada por el equipo (ver `12-decisions/`).

## Mapa

- `00-quijam/` — reto, alineación, pitch, plan de 48 h, preguntas del jurado, [estrategia para ganar](00-quijam/estrategia-para-ganar.md), [roles del equipo](00-quijam/roles-equipo.md) y [comparativa de ideas](00-quijam/comparativa-ideas.md).
  - `reto-y-alineacion.md`, `pitch.md`, `plan-48h.md`, `preguntas-jurado.md`.
  - `comparativa-ideas.md` — contraste con la idea 2 (Orientación Vocacional).
- `01-product/` — visión, usuario y producto.
- `02-requirements/` — requisitos (FR/NFR), criterios de aceptación y alcance.
- `03-ux/` — experiencia y flujos.
- `04-domain/` — dominio y reglas financieras.
- `05-open-payments/` — capa de ejecución: ledger simulado (MVP) y Open Payments (opcional).
- `06-ai/` — IA, decisiones y protección.
- `07-architecture/` — arquitectura del sistema.
- `08-technical/` — API, datos, contratos y seguridad.
- `09-testing/` — estrategia y casos críticos.
- `10-operations/` — desarrollo, despliegue y contingencia.
- `11-project/` — roadmap, backlog y guion de demo.
- `12-decisions/` — decisiones arquitectónicas (ADR-001 … ADR-007).

## Principio rector

> El sistema propone; las reglas protegen; el usuario confirma; el proveedor de pagos (ledger simulado u Open Payments) ejecuta; el sistema registra.

## Regla de datos

Ninguna cifra estadística se inventa. Toda cifra sin fuente verificada se escribe como `[DATO POR VERIFICAR — fuente sugerida: X]`. Los montos de las personas y de la demo son **escenarios ilustrativos**, no estadísticas.

## Trazabilidad

Problema → Objetivo → Feature → Requisito → Regla → Dominio → API → Implementación → Test.

| Problema | Feature | Requisito | Regla | Dominio | API | Test |
|---|---|---|---|---|---|---|
| No sé cuánto puedo gastar sin quedarme corto | Presupuesto automático | FR-020, FR-021, FR-022 | BR-001 | `Budget`, `FinancialProfile` | `POST /onboarding`, `GET /dashboard` | AC-020, FS-01, FS-03 |
| Ahorrar para algo concreto (portátil, curso, emprendimiento) no se sostiene | Metas de oportunidad | FR-040 … FR-043 | BR-001 | `Goal` | `POST /goals` | AC-040 |
| Sé lo que debería hacer pero no lo hago | Recomendación + aprobación | FR-030 … FR-033 | BR-001, BR-010, BR-012 | `Recommendation`, `DecisionLog` | `POST /decisions/recommend`, `POST /recommendations/:id/decision` | AC-030, AI-01 … AI-05 |
| Mover el dinero es otra tarea | Separación aprobada | FR-050 … FR-054 | BR-020 … BR-022 | `PaymentIntent`, `LedgerEntry` | `POST /payments/prepare`, `POST /payments/confirm` | AC-050, PY-01 … PY-07 |
| "¿Me alcanza para esto?" | Chequeo de compra | FR-034 | BR-002 | `Budget` | `POST /affordability/check` | AC-034, FS-01 |
| Ahorro entre compañeros sin peleas | Meta grupal | FR-080 … FR-083 | BR-030 … BR-034 | `SavingsGroup` | `/group-goals/*` | AC-080, FS-05, FS-06 |
| La ciudad no ve la fragilidad financiera juvenil | Insights agregados | FR-090, FR-091 | BR-040, BR-041 | `InsightSnapshot` | `GET /insights/aggregate` | AC-090 |
