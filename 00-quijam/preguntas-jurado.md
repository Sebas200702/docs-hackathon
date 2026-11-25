# Preguntas probables del jurado

Respuestas cortas (≤30 s). Si una respuesta requiere una cifra, usar solo cifras verificadas; si no, decir "no tenemos el dato verificado".

## Problema e impacto

**¿Por qué esto mejora la calidad de vida en Barranquilla y no en cualquier ciudad?**
Porque está diseñado para el joven barranquillero con ingresos irregulares (turnos, cuota de aprendizaje SENA, encargos) y porque devuelve a la ciudad insights agregados por institución y localidad, con permiso, para dirigir apoyos. La lógica es replicable; los datos y aliados son locales.

**¿Tienen datos del problema?**
Solo citamos cifras verificadas de SPADIES/MEN, DANE GEIH o Banca de las Oportunidades. Lo que no está verificado lo marcamos como pendiente. Además, entrevistamos a estudiantes en el evento (decir cuántos solo si se hizo).

**¿Por qué este eje (Economía y oportunidades)?**
Porque las metas que el producto protege son de oportunidad: herramienta de estudio, curso, emprendimiento. Ahorrar para eso es inclusión y empleabilidad.

## Solución

**¿En qué se diferencia de una app de presupuesto o de la app del banco?**
No pide registrar cada gasto: con cinco datos calcula capacidad segura, propone una sola acción explicada y, si la apruebas, separa el dinero. Y nunca recomienda algo que te deje sin transporte o comida.

**¿Qué hace la IA y qué no?**
Interpreta la situación y explica en lenguaje cotidiano. No mueve dinero, no cambia reglas, no salta la confirmación. Si falla o responde mal, un motor de reglas da una recomendación conservadora (ADR-003, ADR-004).

**¿Qué pasa si la IA recomienda algo peligroso?**
El Policy Engine lo bloquea antes de mostrarlo: ninguna recomendación puede superar la capacidad segura. Tenemos tests para eso (FS-01 … FS-10).

**¿Mueven dinero real?**
No en el MVP. Usamos un ledger simulado con bolsillos. La arquitectura tiene un adaptador de pagos; Open Payments (estándar abierto de Interledger) es una opción futura para mover dinero entre wallets compatibles. Hoy no conectamos bancos.

**¿Por qué no se conectan con Nequi, Daviplata o bancos?**
Requiere acuerdos y regulación que no caben en 48 h. Por eso el adaptador de pagos está desacoplado. [DATO POR VERIFICAR — fuente sugerida: Superintendencia Financiera / Banco de la República, sobre APIs abiertas y finanzas abiertas en Colombia].

## Datos y privacidad

**¿Qué datos guardan?**
Mínimos: ingresos, gastos fijos, saldo, metas. No pedimos credenciales bancarias. Cumplimiento con Ley 1581 de 2012; insights solo agregados con grupos de ≥20 usuarios y con opt-in.

**¿Los insights de la Alcaldía son reales?**
No; en la demo son sintéticos y lo decimos. Mostramos qué tipo de decisión permitirían.

## Viabilidad

**¿Quién paga esto?**
Hipótesis a validar: universidades, SENA o programas de la Alcaldía lo ofrecen gratis a sus estudiantes como herramienta de bienestar e inclusión; ellos reciben los insights agregados. No tenemos acuerdos hoy.

**¿Cómo lo escalan después de la hackatón?**
Piloto con una cohorte de una institución aliada, medir si las metas avanzan y si baja la proporción de usuarios con capacidad cero a fin de mes.

**¿Cuánto se construyó aquí?**
Responder con la verdad según Q1 de `plan-48h.md`: qué existía antes (documentación) y qué se codificó en el evento.

## Técnica

**¿Qué pasa si se cae internet en la demo?**
Demo local con fallback de reglas y seed reproducible (`10-operations/contingency.md`).

**¿Por qué metas grupales?**
Porque los jóvenes ahorran juntos (viaje, stand de feria, equipo compartido) y la pelea es quién pone cuánto. Separamos responsabilidad final de aporte del mes (ADR-005).
