# Requisitos No Funcionales

Cada NFR tiene una verificación concreta para la revisión técnica (vie 09:30).

## Rendimiento

| ID | Requisito | Verificación |
|---|---|---|
| NFR-001 | API p95 <400 ms en operaciones normales (sin IA). | 50 llamadas a `GET /dashboard` en local; medir p95. |
| NFR-002 | Proveedor de IA: timeout 1,5 s, luego fallback. | Test AI-01 con proveedor que tarda 3 s. |
| NFR-003 | Fallback determinista <100 ms. | Test unitario con medición. |

## Seguridad

| ID | Requisito | Verificación |
|---|---|---|
| NFR-010 | Validación Zod de toda entrada externa. | Payload inválido → 400 con campo. |
| NFR-011 | Autenticación y autorización por recurso. | AC-001, AC-002. |
| NFR-012 | Rate limiting en login y endpoints de pagos. | 20 intentos/min → 429. |
| NFR-013 | Secretos solo por variables de entorno. | Búsqueda de claves en el repo vacía. |
| NFR-014 | Confirmación explícita e idempotencia en movimientos. | AC-050, AC-052. |
| NFR-015 | Auditoría de decisiones y movimientos. | Cada confirmación produce un `AuditLog`. |
| NFR-016 | Privacidad: insights solo agregados, k ≥ 20, con consentimiento; Ley 1581 de 2012. | AC-090, AC-091. |

## UX

| ID | Requisito | Verificación |
|---|---|---|
| NFR-020 | Mobile-first (360 px de ancho sin scroll horizontal). | Revisión en celular real. |
| NFR-021 | Lenguaje claro, cotidiano, sin culpa ("aún no", "este mes no alcanza" en vez de "gastaste mal"). | Revisión de copy por UI/UX. |
| NFR-022 | Estados de loading, error y vacío en cada pantalla P0. | Checklist por pantalla. |
| NFR-023 | Montos en COP con separador de miles (`$76.000`). | Revisión visual. |
| NFR-024 | Tres personas externas completan el loop sin ayuda. | Prueba de UI/UX la noche del jueves. |

## Confiabilidad

| ID | Requisito | Verificación |
|---|---|---|
| NFR-030 | El fallo de IA no detiene recomendaciones seguras. | AI-01 … AI-05. |
| NFR-031 | La demo no depende de servicios externos de pagos. | Proveedor por defecto `simulated`. |
| NFR-032 | Restauración por seed/reset en <5 s. | AC-100. |
| NFR-033 | La demo corre en local sin internet (con RulesProvider). | Ensayo con wifi apagado. |

## Trazabilidad

| ID | Requisito | Verificación |
|---|---|---|
| NFR-040 | Toda decisión financiera relevante queda registrada con proveedor, resultado de política y actor. | Consulta a `decision_logs` y `audit_logs` tras la demo. |
