# Plan de construcción — QuiJAM 2026

> Roles: los 5 oficiales se usan solo como etiqueta formal. El reparto real del equipo está en [`roles-equipo.md`](./roles-equipo.md) y la estrategia en [`estrategia-para-ganar.md`](./estrategia-para-ganar.md).

Plan sobre la agenda oficial. Ventana real de construcción: **jue 14:00 → vie 09:30** (≈19,5 h de reloj). El P0 debe estar funcionando en la noche del jueves (≈9 h de trabajo en paralelo de 5 personas); el resto es P1, pruebas, recorte y ensayo. El alcance está en `02-requirements/mvp-scope.md`.

## Roles (obligatorios) y responsabilidad

| Rol | Dueño de | Entregable verificable |
|---|---|---|
| **Frontend** | Pantallas React mobile-first: onboarding, dashboard, recomendación, confirmación, meta, chequeo de compra | Loop completo navegable en móvil |
| **Backend** | API Hono, Drizzle/PostgreSQL, modelo financiero, Policy Engine, `SimulatedLedgerProvider`, seed/reset | `GET /health` 200 y endpoints P0 con tests de reglas |
| **AI Specialist** | `DecisionProvider` (LLM/OpenJEV) + `RulesProvider` fallback, prompt, validación de salida, explicación en lenguaje cotidiano | Recomendación explicada; fallback probado (AI-01 … AI-05) |
| **UI/UX Designer** | Flujos, wireframes, copy no culpabilizante, componentes de progreso, prueba con 3 usuarios externos | Prototipo validado + visuales del pitch |
| **Pitch Lead** | Pitch, guion de demo, preguntas del jurado, verificación de datos, entrevistas a estudiantes del evento | Pitch ensayado ≥3 veces con cronómetro |

## Día 1 — jueves 26

| Hora | Agenda oficial | Qué hace el equipo |
|---|---|---|
| 08:00 | Registro | Verificar laptops, cargadores, acceso al repo y a la base de datos local. |
| 08:30 | Apertura | Pitch Lead toma nota de criterios de evaluación y duración de la demo. |
| 09:00 | Conformación de equipos | Confirmar roles de esta tabla. |
| 09:45 | Comprender el reto | Pitch Lead + UI/UX: validar `reto-y-alineacion.md` con lo que digan mentores/Alcaldía. Ajustar eje si cambia. |
| 11:00 | Ideación | Congelar alcance P0 (máx. 30 min). UI/UX: wireframes de 6 pantallas. Backend: esquema DB. AI: contrato `DecisionRequest/Response`. |
| 12:30 | Almuerzo | Pitch Lead entrevista a 3–5 estudiantes asistentes (3 preguntas: ¿cómo te alcanza el mes?, ¿para qué ahorras?, ¿usarías esto?). |
| 13:30 | Impulso técnico | Preguntar a mentores si se permite código base previo (pregunta abierta Q1). |
| 14:00 | Construcción del prototipo | **Bloque A (14:00–18:00):** Backend: modelo financiero + `POST /onboarding` + `GET /dashboard` + seed. Frontend: onboarding + dashboard con datos mock. AI: RulesProvider + endpoint `/decisions/recommend`. UI/UX: copy y estados (loading/error/vacío). Pitch Lead: primera versión del pitch. |
| 18:00 | Punto de control | Debe funcionar: onboarding → dashboard → recomendación (aunque sea solo RulesProvider). Si no, recortar P1 completo. |
| 18:30 | Noche de construcción | **Bloque B (18:30–23:00):** Ledger simulado + `prepare/confirm` + idempotencia (Backend); confirmación + meta actualizada (Frontend); LLM con fallback (AI); prueba con 3 externos (UI/UX). **Bloque C (23:00–03:00), por turnos:** P1 (chequeo de compra, gamificación básica, insights sintéticos). Open Payments testnet **solo si** P0 está verde y probado (ADR-007). |

## Día 2 — viernes 27

| Hora | Agenda oficial | Qué hace el equipo |
|---|---|---|
| 08:00 | Construcción final | Congelar código a las 09:00. Solo bugs del happy path. Ensayo de demo ×2 con `POST /demo/reset`. |
| 09:30 | Revisión técnica | Mostrar: repo, tests de reglas (FS-01 … FS-10), fallback IA, qué es real y qué simulado. |
| 10:00 | Día de demostraciones | Pitch + demo según `11-project/demo-script.md`. Plan B: video grabado a las 08:30 + demo local. |
| 12:30 | Evaluación | Responder con `preguntas-jurado.md`. |

## Regla de recorte

Si a las 18:00 o 02:00 algo de P0 no funciona, se elimina P1 de ese frente y el dueño del P1 ayuda al P0. Nunca se recorta: saldo protegido, confirmación explícita, fallback IA.

## Preguntas abiertas (a resolver en el evento)

- Q1: ¿Se permite traer código o plantillas preparadas antes del evento?
- Q2: ¿Cuánto dura el turno de demostración y si hay proyector/pantalla?
- Q3: ¿Cuáles son los criterios y ponderación de evaluación?
- Q4: ¿El equipo debe ser asignado en "Conformación de equipos" o puede llegar armado?
- Q5: ¿Hay wifi estable para un LLM en la nube, o se requiere modelo/fallback local?
