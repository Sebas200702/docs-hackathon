# Capa de ejecución — Overview

## Posición tras el reanclaje (ADR-007)

Esta sección describe **cómo se materializa** una recomendación aprobada. No es el objetivo del producto ni de QuiJAM. El producto se evalúa por su impacto en jóvenes de Barranquilla; esta capa solo hace que "aprobar" termine en una acción.

## Proveedores

| Proveedor | Estado | Uso |
|---|---|---|
| `SimulatedLedgerProvider` | **MVP, por defecto** | Ledger interno de doble entrada con bolsillos (Disponible, Meta, Grupo). Es lo que se muestra en la demo. |
| `OpenPaymentsProvider` | Opcional (P2) | Movimientos entre wallets de prueba compatibles con Open Payments (estándar abierto del ecosistema Interledger). Se integra solo si P0 está terminado. |
| Billeteras/bancos comerciales | Fuera de alcance | Requiere acuerdos y marco regulatorio: [DATO POR VERIFICAR — fuente sugerida: Superintendencia Financiera de Colombia, regulación de finanzas abiertas]. |

## Interfaz común

```ts
interface PaymentProvider {
  name: 'simulated' | 'open_payments';
  execute(intent: PaymentIntent): Promise<{ status: 'completed' | 'rejected' | 'failed' | 'pending_reconciliation'; externalRef?: string }>;
  getStatus(intent: PaymentIntent): Promise<PaymentIntent['status']>;
}
```

Selección por `PAYMENTS_PROVIDER` (default `simulated`). El dominio, la UI y los tests no cambian entre proveedores.

## Casos

- Aportes a metas individuales (P0).
- Aportes a metas grupales (P1).
- Microahorro y aportes recurrentes (futuro).

## Por qué conservar Open Payments como opción

- Es un estándar abierto que permitiría, en el futuro, mover dinero entre proveedores distintos sin integrar uno por uno.
- Es un diferenciador técnico para la revisión técnica si da el tiempo.
- No se presenta en el pitch como el objetivo; ver reglas del Pitch Lead en `00-quijam/pitch.md`.

## Principio

No se integra un proveedor de pagos solo para demostrar una API. Debe producir una acción relevante dentro del flujo del producto.
