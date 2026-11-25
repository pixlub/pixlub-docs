# SDK de Python y Go

Los clientes oficiales: envío de archivos, descarga de resultados, errores tipados y reintentos seguros.

Dos clientes oficiales envuelven la API: envían los archivos, descargan los resultados y convierten cada rechazo en un error tipado. Leen la clave en `PIXLUB_API_KEY` y la dirección de la API en `PIXLUB_BASE_URL`.

```bash
export PIXLUB_API_KEY="pix.xxxxxxxx.xxxxxxxxxxxxxxxx"
export PIXLUB_BASE_URL="https://api.pixlub.com"
```

## Instalar

**Python**

```bash
pip install pixlub
```

**Go**

```bash
go get github.com/pixlub/pixlub-go
```

Python 3.9 o posterior (una sola dependencia: httpx); Go 1.23 o posterior (solo la biblioteca estándar). Ambos SDK son libres, con licencia MIT.

## Ejecutar un módulo

**Python**

```python
import pixlub

client = pixlub.Client()
result = client.tools.run("removeBgApi", image="photo.jpg")
result.save(f"photo-sin-fondo{result.extension}")
print(result.cost, result.credits_balance)
```

**Go**

```go
client, err := pixlub.NewClient()
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "removeBgApi", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.jpg"),
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("photo-sin-fondo"+result.Extension(), false)
```

El SDK descarga por sí mismo los archivos generados. La extensión sigue al archivo generado: `.webp` para `removeBgApi`, `.png` para la mayoría de los módulos. `save` se niega a sobrescribir un archivo existente, salvo que usted lo pida.

## Ajustes y entradas múltiples

**Python**

```python
client.tools.run("flip", image="photo.jpg", params={"axis": "v"})
client.tools.run("mask", inputs={"image": "photo.png", "mask": "mascara.png"})
```

**Go**

```go
client.Tools.Run(ctx, "flip", pixlub.RunRequest{
    Image:  pixlub.FromPath("photo.jpg"),
    Params: map[string]any{"axis": "v"},
})
client.Tools.Run(ctx, "mask", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "image": pixlub.FromPath("photo.png"),
        "mask":  pixlub.FromPath("mascara.png"),
    },
})
```

`client.tools.list()` y `client.tools.schema(id)` (Python) leen la lista de módulos y el esquema de sus ajustes. En Python, `pixlub.AsyncClient` ofrece los mismos métodos en modo asíncrono.

## Errores

Cada rechazo de la API se convierte en un error específico:

| HTTP | Python | Caso |
| --- | --- | --- |
| `400` | `InvalidRequestError` | Ajustes no válidos; detalle en `details`. |
| `401` | `AuthenticationError` | Clave desconocida o revocada. |
| `402` | `InsufficientCreditsError` | Créditos insuficientes. |
| `403` | `PermissionDeniedError` | Plan gratuito (`code == "plan_required"`), enlace caducado. |
| `429` | `RateLimitError` | Demasiadas solicitudes: 30 ejecuciones por minuto, en ráfagas de 10. Nunca se cobra. |
| `5xx` | `ServerError` | Error por nuestra parte. |

Los errores locales (clave ausente, archivo demasiado grande, entrada desconocida) se lanzan **antes de cualquier envío**: no cuestan nada.

## Reintentos

El SDK **nunca** reintenta una llamada que haya podido cobrarse. Solo reintenta lo que con seguridad no se ejecutó: las respuestas `429`, las conexiones rechazadas antes de cualquier envío, las lecturas (`list`, `schema`) y las descargas de resultados. Tras un tiempo de espera agotado o un error `5xx` en una llamada, compruebe su saldo antes de volver a empezar.

> [!NOTE]
> **Seguridad**
>
> Los SDK solo envían la clave en el encabezado `X-API-Key`, rechazan el HTTP sin cifrar fuera de `localhost`, no siguen ninguna redirección y nunca adjuntan la clave a las descargas.
