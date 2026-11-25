# ADR-007 — Reanclaje al reto QuiJAM y Open Payments como capa opcional

## Estado

Aceptada (2026-11-24). Reemplaza a ADR-002. Actualiza ADR-001 y ADR-006.

## Contexto

La documentación original presentaba Interledger/Open Payments como el objetivo de la hackathon. El equipo compite en QuiJAM 2026 (Barranquilla, 26–27 de noviembre), cuyo reto es "¿cómo usar tecnología, innovación y talento joven para mejorar la calidad de vida de los ciudadanos de Barranquilla?". Las bases piden mostrar "cómo la solución responde a una necesidad real de la ciudad" y aclaran que no se necesita una aplicación. El jurado, ligado a la Alcaldía y a las universidades, valora impacto, viabilidad y talento joven.

Decisión del equipo: "Pasarlo a secundario y reanclar al reto".

## Decisión

1. El producto se ancla al eje **Economía y oportunidades**, con jóvenes de Barranquilla (universitarios y aprendices SENA) de ingresos limitados como usuarios.
2. Se añade el ángulo de ciudad: insights agregados, anónimos y con consentimiento para Alcaldía, universidades y SENA.
3. La ejecución de movimientos pasa por una interfaz `PaymentProvider`. El MVP usa `SimulatedLedgerProvider`. `OpenPaymentsProvider` es opcional (P2) y solo se implementa si el P0 está terminado.
4. Ningún documento ni el pitch presentan Open Payments como objetivo del concurso.

## Consecuencias

- El loop completo (entender → decidir → aprobar → actuar → progresar) se demuestra sin dependencias externas de pagos.
- El principio rector cambia "Open Payments ejecuta" por "el proveedor de pagos ejecuta".
- `05-open-payments/` se conserva, reencuadrada como capa de ejecución.
- La demo dice explícitamente qué es simulado.
- Riesgo aceptado: se pierde el atractivo para un jurado orientado a Interledger, que no es el de QuiJAM.

## Alternativas descartadas

- Mantener Open Payments como centro: desalineado con el reto y con riesgo en la demo por dependencia externa.
- Eliminar Open Payments: se pierde un diferenciador técnico que no cuesta mantener detrás de una interfaz.
