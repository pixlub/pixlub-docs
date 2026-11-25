# Quitar el fondo: referencia de la API

Detecta el sujeto mediante IA (con nuestros servicios) y vuelve transparente todo lo demás, sea cual sea el fondo.

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/removeBgApi` | 10 créditos por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `image` (Una sola imagen) | sí | `PNG`, `JPEG`, `WebP`, `GIF` | **Imagen**<br />Imagen enviada al servidor, cuyo sujeto se detecta y cuyo fondo se vuelve transparente. |

## Ajustes

Este módulo no tiene ningún ajuste.

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/removeBgApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F image=@image.png \
  -F 'params={}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('image', await openAsBlob('image.png'), 'image.png')
form.append('params', JSON.stringify({}))

const res = await fetch('https://api.pixlub.com/v1/modules/removeBgApi', {
  method: 'POST',
  headers: { 'X-API-Key': process.env.PIXLUB_API_KEY },
  body: form,
})
const result = await res.json()
const output = result.outputs.find((o) => o.key === 'out')
const image = await fetch(output.url) // lien signé, sans clé
```

### Python

```python
import json, os, requests

res = requests.post(
    "https://api.pixlub.com/v1/modules/removeBgApi",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("image", open("image.png", "rb"))],
    data={"params": json.dumps({})},
)
res.raise_for_status()
result = res.json()
output = next(o for o in result["outputs"] if o["key"] == "out")
print(output["url"])
```

### SDK Python

```python
import pixlub

client = pixlub.Client()  # PIXLUB_API_KEY, PIXLUB_BASE_URL
result = client.tools.run("removeBgApi", inputs={"image": "image.png"})
result.save(f"removeBgApi{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "removeBgApi", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "image": pixlub.FromPath("image.png"),
    },
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("removeBgApi"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `WebP` | **Imagen(es)**<br />Imagen recortada sobre fondo transparente, en WebP sin pérdida. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "removeBgApi",
  "outputs": [
    {
      "key": "out",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.webp?exp=1767268800&sig=…",
      "content_type": "image/webp",
      "bytes": 184203
    }
  ],
  "expires_at": "2026-01-01T12:00:00Z",
  "credits": {
    "cost": 10,
    "balance": 190
  }
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/removeBgApi/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {}
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
