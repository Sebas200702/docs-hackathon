# Decision Engine

## Propósito

Interpretar contexto financiero y producir decisiones estructuradas que posteriormente serán validadas por reglas deterministas.

## Flujo

Financial state → DecisionRequest → DecisionProvider → DecisionResponse → Policy Engine → Recommendation.

## Providers

- OpenJEV.
- RulesProvider.
- Futuros proveedores desacoplados mediante la misma interfaz.

## Fallback

Se utiliza cuando hay timeout, error HTTP, respuesta inválida, baja confianza o contexto incompleto.

## Límite

El Decision Engine no ejecuta movimientos financieros.
