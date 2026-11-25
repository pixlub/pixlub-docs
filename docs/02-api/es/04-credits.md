# Créditos

Cuánto cuesta una llamada, cuándo se descuenta y cuándo se reembolsa.

Cada llamada a un módulo se paga en **créditos**, los mismos que en el sitio. El costo de un módulo figura al principio de la vista **API** de su [ficha](../../03-modules/es/README.md).

## Cuánto cuesta una llamada

| Módulo | Costo |
| --- | --- |
| Módulo calculado por la API (desenfoque, redimensionado, conversión…) | 1 crédito |
| Módulo de IA (quitar el fondo, desenfoque automático, calcomanía…) | Su propio precio, 10 créditos en la mayoría de los casos |

La unidad se indica en cada ficha: **por archivo**, **por minuto** o **por operación**. Un módulo cuya IA es opcional (Difuminado de rostros en modo `manual`, por ejemplo) cuesta lo mismo que un módulo estándar mientras no llame al servicio remoto.

## Cuándo se descuenta

1. Se verifica la solicitud: clave, ajustes, archivos. Una solicitud no válida se rechaza **sin cargo**.
2. El costo se **descuenta antes** del cálculo. Sin créditos suficientes, la API responde `402` y no se calcula nada.
3. Si el cálculo falla **por nuestra parte** (error del servidor, servicio no disponible), el cargo se **reembolsa** automáticamente.

La respuesta indica el costo y el saldo restante:

```json
"credits": { "cost": 10, "balance": 190 }
```

Descargar un resultado no cuesta nada, aunque sea varias veces mientras el enlace sea válido.

## Recargar

Los créditos proceden de su suscripción (créditos mensuales) y de los paquetes comprados aparte, que no caducan. El saldo y el historial se consultan en [Configuración → Pagos → Créditos](https://pixlub.com/es/settings/payments#credits).

> [!TIP]
> **Tras un corte**
>
> Tras un tiempo de espera agotado o un error `5xx` en una llamada, compruebe su saldo antes de volver a intentarlo: la llamada puede haberse descontado y luego reembolsado, o haberse completado sin que le llegue la respuesta.
