# Arquitectura Backend

## Módulos

| Módulo | Responsabilidad | Prior. |
|---|---|---|
| auth | Registro, login, sesión, roles (`student`, `institution_analyst`) | P0 |
| onboarding | Perfil financiero, ingresos, gastos | P0 |
| budget | Modelo financiero (`04-domain/financial-model.md`) | P0 |
| goals | Metas y progreso | P0 |
| decisions | Decision Engine + providers | P0 |
| policies | Policy Engine | P0 |
| payments | PaymentIntent, PaymentProvider, ledger simulado | P0 |
| audit | AuditLog, DecisionLog | P0 |
| demo | Seed y reset | P0 |
| affordability | Chequeo de compra | P1 |
| gamification | Puntos, racha, retos, badges | P1 |
| group-goals | Metas grupales | P1 |
| insights | Agregación anónima | P1 |
| weekly-review | Revisión semanal | P2 |

## Estructura sugerida

```
src/
  modules/<módulo>/{routes.ts, service.ts, schema.ts, <módulo>-types.ts}
  providers/decision/{llm-provider.ts, rules-provider.ts}
  providers/payment/{simulated-ledger-provider.ts, open-payments-provider.ts}
  db/{schema.ts, seed.ts}
```

## Principios

- Validación con Zod en el borde.
- Reglas financieras deterministas y puras.
- Servicios pequeños; un archivo, una responsabilidad.
- Contratos explícitos (`08-technical/contracts.md`).
- Auditoría de decisiones e idempotencia en movimientos.
