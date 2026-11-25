# Product Brief — Copiloto de Salud Financiera

## Reto

QuiJAM 2026: "¿cómo usar tecnología, innovación y talento joven para mejorar la calidad de vida de los ciudadanos de Barranquilla?" — eje **Economía y oportunidades**. Ver `00-quijam/reto-y-alineacion.md`.

## Problema

Los jóvenes de Barranquilla con ingresos limitados e irregulares (universitarios que trabajan, aprendices SENA) necesitan gestionar dinero, pero las herramientas tradicionales les trasladan demasiada carga: registro, categorización, revisión y ejecución manual. El resultado: metas que abren oportunidades (portátil, curso, emprendimiento) no avanzan y el fin de mes llega sin margen.

## Usuario

Universitarios y aprendices SENA en Barranquilla y su área metropolitana con ingresos limitados (personas en `personas.md`). Usuario secundario: instituciones que consultan insights agregados.

## Solución

Un copiloto que convierte cinco datos en una lectura comprensible (comprometido / disponible / capacidad segura), una recomendación explicada y, si el usuario la aprueba, una separación de dinero hacia su meta.

## Diferenciadores

1. **Protección antes que optimización:** ninguna recomendación supera la capacidad segura (saldo − fijos pendientes − saldo protegido).
2. **De la recomendación a la acción:** el usuario aprueba y el dinero se separa en un bolsillo de meta (ledger simulado en el MVP).
3. **Metas de oportunidad y grupales:** plantillas de herramienta de estudio, curso, emprendimiento y fondo de emergencia; metas compartidas con responsabilidad justa.
4. **Impacto de ciudad:** insights agregados y anónimos para la Alcaldía, universidades y SENA.
5. **Técnico, opcional:** adaptador de pagos listo para Open Payments (Interledger) cuando exista una wallet compatible (ADR-007).

## Propuesta de valor

> Gestiona tu dinero sin convertirlo en otra tarea.

## Principio de autonomía

El sistema interpreta y propone. Las reglas deterministas protegen al usuario. El usuario mantiene la aprobación. El proveedor de pagos (ledger simulado u Open Payments) materializa el movimiento.

## Objetivo en la hackatón

Demostrar, con un prototipo funcional, que un joven barranquillero pasa de información financiera mínima a una acción aprobada y segura que hace avanzar una meta de oportunidad, y que la ciudad puede aprender de ello sin vulnerar su privacidad.

## MVP

Login, onboarding, estado financiero, presupuesto, recomendación explicada, meta, confirmación, separación en ledger simulado, registro/auditoría. P1: chequeo de compra, gamificación básica, insights sintéticos, meta grupal. Detalle en `02-requirements/mvp-scope.md`.
