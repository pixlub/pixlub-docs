# Credits

What a call costs, when it is charged, and when it is refunded.

Every module call is paid in **credits**, the same as on the site. A module's cost is shown at the top of the **API** view of its [page](../../03-modules/en/README.md).

## How much a call costs

| Module | Cost |
| --- | --- |
| Module computed by the API (blur, resize, conversion…) | 1 credit |
| AI module (background removal, auto face blur, decal…) | Its own price, 10 credits for most |

The unit is given on each page: **per file**, **per minute** or **per operation**. A module whose AI is optional (Face blur in `manual` mode, for example) costs the price of a standard module as long as it does not call the remote service.

## When the charge happens

1. The request is checked: key, settings, files. An invalid request is refused **without a charge**.
2. The cost is **taken before** computing. Without enough credits, the API answers `402` and nothing is computed.
3. If the computation fails **on our side** (server error, unavailable service), the charge is **refunded** automatically.

The response gives the cost and the remaining balance:

```json
"credits": { "cost": 10, "balance": 190 }
```

Downloading a result costs nothing, even several times while the link is valid.

## Topping up

Credits come from your subscription (monthly credits) and from packs bought separately, which never expire. The balance and history are in [Settings → Payments → Credits](https://pixlub.com/en/settings/payments#credits).

> [!TIP]
> **After a cut**
>
> After a timeout or a `5xx` error on a call, check your balance before running again: the call may have been charged then refunded, or have succeeded without the response reaching you.
