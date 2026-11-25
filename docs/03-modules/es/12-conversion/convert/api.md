# Conversión: referencia de la API

Convierte imágenes, animaciones, videos y audios a cualquier formato de exportación: PNG, JPG, WebP, GIF, MP4, WebM, MP3, FLAC, WAV, PDF…

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/convert` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una imagen o varias) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen(es)**<br />Imagen(es) que se van a convertir al formato elegido. |

## Ajustes

### Formato de salida

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `format` | `string` | `"png"` | `png` PNG<br />`jpg` JPG<br />`webp` WebP | **Formato**<br />Formato de salida de las imágenes. |

### Calidad

> Estos ajustes solo cuentan cuando `format` = `jpg` (JPG) o `webp` (WebP).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `quality` | `number` | `90` | mín. 1 % · máx. 100 % · paso de 1 | **Calidad**<br />Calidad de la imagen comprimida. |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/convert \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"format":"png"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"format":"png"}))

const res = await fetch('https://api.pixlub.com/v1/modules/convert', {
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
    "https://api.pixlub.com/v1/modules/convert",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"format": "png"})},
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
result = client.tools.run("convert", image="photo.png", params={"format": "png"})
result.save(f"convert{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "convert", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"format": "png"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("convert"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

### 1 archivo

> **1 archivo** : Una sola imagen en `in`.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG`, `JPEG`, `WebP` | **Imagen(es)**<br />Imagen convertida, en el formato elegido mediante `format`.<br />Una sola imagen enviada: el archivo conserva la clave `out`.<br />El formato sigue el ajuste `format`. |

### Varios archivos

> **Varios archivos** : Varias imágenes en `in`, hasta 64: su número se deduce de los archivos enviados, usted no lo envía.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG`, `JPEG`, `WebP` | **Imagen(es)**<br />Imagen convertida, en el formato elegido mediante `format`.<br />Varias imágenes enviadas en `in`: un archivo por imagen, con las claves `out#0`, `out#1`…, en el orden de envío.<br />El formato sigue el ajuste `format`. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "convert",
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

`GET /v1/modules/convert/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "format": {
      "title": "Format",
      "default": "png",
      "type": "string",
      "enum": [
        "png",
        "jpg",
        "webp"
      ]
    },
    "quality": {
      "title": "Quality",
      "default": 90,
      "type": "number",
      "minimum": 1,
      "maximum": 100,
      "multipleOf": 1
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
