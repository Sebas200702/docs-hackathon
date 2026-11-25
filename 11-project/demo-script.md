# Guion de demo

Duración base: **5:00**. Versión corta de 3:00 al final. La duración oficial del turno está por confirmar (Q2 en `00-quijam/plan-48h.md`).

Roles en escena: **Pitch Lead** habla; **Frontend** maneja el celular proyectado; **AI Specialist** y **Backend** listos para la revisión técnica; **UI/UX** controla el cronómetro y las diapositivas.

Antes de empezar: `POST /demo/reset`, sesión de Valentina abierta en onboarding, wifi indiferente (RulesProvider listo), video de respaldo abierto en otra pestaña.

| Tiempo | Qué se dice (Pitch Lead) | Qué se muestra |
|---|---|---|
| 0:00–0:30 | "Esta es Valentina. Estudia en Barranquilla, vive en Soledad y trabaja los fines de semana. Este mes le entran $900.000 y $520.000 ya se le van en pasajes, almuerzos, celular y fotocopias. Quiere un portátil para la carrera y cada mes algo se atraviesa." | Diapositiva con la persona y su mes (montos ilustrativos). |
| 0:30–0:50 | "El reto de QuiJAM pregunta cómo mejorar la calidad de vida de los barranquilleros con talento joven. Nosotros atacamos Economía y oportunidades: que el dinero de los jóvenes alcance para lo que les abre caminos." | Diapositiva: reto + eje (texto oficial). Cifra de contexto solo si está verificada; si no, se omite. |
| 0:50–1:30 | "Valentina no llena una hoja de cálculo. Responde cinco preguntas." | Onboarding en el celular: ingresos 600.000 + 300.000, fijos 520.000, saldo 450.000, pendientes 200.000, protegido 100.000, meta Portátil 1.800.000 (pre-rellenado; se avanza tocando "Siguiente"). |
| 1:30–2:00 | "En segundos sabe lo que ninguna app le decía: de su plata, $150.000 los puede mover sin tocar lo básico." | Dashboard: Comprometido 520.000 · Para gastar 304.000 · Para ahorrar 76.000 · Capacidad segura 150.000. Meta 16,7 %. |
| 2:00–2:40 | "El copiloto le propone una sola acción y le explica por qué, con sus números. Lo redacta la IA, pero un motor de reglas decide el límite: nunca le va a proponer algo que la deje sin pasaje." | Recomendación "Separa $76.000 para tu portátil" con razón. |
| 2:40–3:10 | "Ella revisa: cuánto, de dónde, a dónde. Aprueba. Y el dinero queda separado." | Pantalla de confirmación → Aprobar → "Listo. Tu portátil va en 20,9 %." +10 puntos, badge "Primer paso". Decir: "En la demo el movimiento es simulado." |
| 3:10–3:40 | "Viernes. Ve unos tenis de $180.000. Pregunta: ¿me alcanza?" | ¿Me alcanza? → 180.000 → "Hoy no es recomendable: te faltarían $30.000 para no tocar lo básico." |
| 3:40–4:15 | "Y la ciudad aprende. Con permiso y sin datos individuales, la Alcaldía, el SENA o una universidad pueden ver en qué semana del mes sus jóvenes se quedan sin margen y qué metas persiguen." | Vista `/insights` con etiqueta **"Datos sintéticos — demo"**. Leer en voz alta que son sintéticos. |
| 4:15–4:40 | "Por dentro: la IA explica, las reglas protegen, el usuario aprueba y un adaptador de pagos ejecuta. Hoy es un ledger simulado; mañana puede ser una billetera real o un estándar abierto como Open Payments, sin cambiar el producto." | Diagrama de arquitectura (una diapositiva). Si se integró Open Payments, mencionar en una frase que funciona en entorno de pruebas. |
| 4:40–5:00 | "No queremos que los jóvenes administren mejor una app. Queremos que administren menos su dinero y avancen más hacia sus oportunidades. Somos [nombres], cinco jóvenes construyendo para jóvenes de Barranquilla." | Diapositiva de cierre con los 5 roles. |

## Versión corta (3:00)

0:00–0:30 Valentina → 0:30–1:00 dashboard (onboarding ya hecho) → 1:00–1:50 recomendación + aprobación → 1:50–2:20 ¿me alcanza? → 2:20–2:45 insights sintéticos → 2:45–3:00 cierre. Se omite la arquitectura.

## Si algo falla en vivo

- IA no responde: no se menciona; RulesProvider da la misma recomendación.
- La app no carga: Pitch Lead dice "les muestro la grabación de esta mañana" y continúa el guion sobre el video.
- Pregunta técnica durante la demo: "Lo mostramos en la revisión técnica" (o responde el AI Specialist / Backend en ≤20 s).

## Checklist de ensayo

- 3 ensayos cronometrados el viernes antes de las 09:30.
- Todos los montos en pantalla coinciden con este guion (seed v1).
- Ninguna cifra estadística sin verificar en las diapositivas.
