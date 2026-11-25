# Paleta a partir de una imagen: referencia de la API

Extrae los colores dominantes de una imagen (median cut)

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/paletteFromImage` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una imagen o varias) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen(es)**<br />Imagen cuyos colores dominantes se extraen. |

## Ajustes

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `count` | `number` | `6` | mín. 2 · máx. 32 · paso de 1 | **Número de colores**<br />Número de colores extraídos de la imagen. |
| `sortBy` | `string` | `"luminance"` | `luminance` Brillo : Ordenar por brillo.<br />`hue` Tono : Ordenar por tono.<br />`frequency` Frecuencia : Ordenar por frecuencia. | **Ordenar por**<br />Criterio de orden de los colores extraídos. |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/paletteFromImage \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"count":6,"sortBy":"luminance"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"count":6,"sortBy":"luminance"}))

const res = await fetch('https://api.pixlub.com/v1/modules/paletteFromImage', {
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
    "https://api.pixlub.com/v1/modules/paletteFromImage",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"count": 6, "sortBy": "luminance"})},
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
result = client.tools.run("paletteFromImage", image="photo.png", params={"count": 6, "sortBy": "luminance"})
result.save(f"paletteFromImage{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "paletteFromImage", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"count": 6, "sortBy": "luminance"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("paletteFromImage"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

### 1 archivo

> **1 archivo** : Una sola imagen en `in`.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Paleta**<br />Colores dominantes, en muestras de color.<br />Una sola imagen enviada: el archivo conserva la clave `out`. |

### Varios archivos

> **Varios archivos** : Varias imágenes en `in`, hasta 64: su número se deduce de los archivos enviados, usted no lo envía.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG` | **Paleta**<br />Colores dominantes, en muestras de color.<br />Varias imágenes enviadas en `in`: un archivo por imagen, con las claves `out#0`, `out#1`…, en el orden de envío. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "paletteFromImage",
  "outputs": [
    {
      "key": "out",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.png?exp=1767268800&sig=…",
      "content_type": "image/png",
      "bytes": 184203
    }
  ],
  "expires_at": "2026-01-01T12:00:00Z",
  "credits": {
    "cost": 1,
    "balance": 190
  }
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/paletteFromImage/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "count": {
      "title": "Number of colors",
      "default": 6,
      "type": "number",
      "minimum": 2,
      "maximum": 32,
      "multipleOf": 1
    },
    "sortBy": {
      "title": "Sort by",
      "default": "luminance",
      "type": "string",
      "enum": [
        "luminance",
        "hue",
        "frequency"
      ]
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
