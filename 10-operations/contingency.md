# Contingencia

| Falla | Respuesta | Quién |
|---|---|---|
| IA falla o no hay internet | RulesProvider automático; la demo sigue igual | AI Specialist |
| Open Payments (si se integró) falla | `PAYMENTS_PROVIDER=simulated`; la demo ya usa el ledger simulado por defecto | Backend |
| VPS falla | Entorno local preparado (laptop del Backend, Postgres local) | Backend |
| Proyector/pantalla falla | Demo en celular + video grabado el viernes 08:30 | Pitch Lead |
| Datos incorrectos | `POST /demo/reset` | Backend |
| Error irrecuperable | Video grabado + explicación con capturas | Pitch Lead |

## Regla

La demo debe poder continuar aunque una dependencia externa falle. Nada de la demo P0 depende de internet.
