# Hoja de sprites: referencia de la API

Reúne varias imágenes en una cuadrícula (flipbook, atlas de VFX)

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/spriteSheet` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `f1` (Imagen o lote) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen 1**<br />Imagen (o lote) colocada en la celda 1 de la cuadrícula.<br />Envíe una imagen, o un lote repitiendo el campo una vez por imagen: hasta 8 imágenes por llamada. |

## Ajustes

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `columns` | `number` | `0` | mín. 0 · máx. 16 · paso de 1 | **Columnas**<br />Número de columnas de la cuadrícula (0 = auto). |
| `padding` | `number` | `0` | mín. 0 px · máx. 200 px · paso de 1 | **Espaciado**<br />Espaciado entre las imágenes de la cuadrícula. |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/spriteSheet \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F f1=@f1-1.png \
  -F f1=@f1-2.png \
  -F 'params={"columns":0,"padding":0}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('f1', await openAsBlob('f1-1.png'), 'f1-1.png')
form.append('f1', await openAsBlob('f1-2.png'), 'f1-2.png')
form.append('params', JSON.stringify({"columns":0,"padding":0}))

const res = await fetch('https://api.pixlub.com/v1/modules/spriteSheet', {
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
    "https://api.pixlub.com/v1/modules/spriteSheet",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("f1", open("f1-1.png", "rb")), ("f1", open("f1-2.png", "rb"))],
    data={"params": json.dumps({"columns": 0, "padding": 0})},
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
result = client.tools.run("spriteSheet", inputs={"f1": "f1.png"}, params={"columns": 0, "padding": 0})
result.save(f"spriteSheet{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "spriteSheet", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "f1": pixlub.FromPath("f1.png"),
    },
    Params: map[string]any{"columns": 0, "padding": 0},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("spriteSheet"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Hoja**<br />Hoja que ordena las imágenes recibidas en una cuadrícula. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "spriteSheet",
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

`GET /v1/modules/spriteSheet/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "columns": {
      "title": "Columns",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 16,
      "multipleOf": 1
    },
    "padding": {
      "title": "Spacing",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 200,
      "multipleOf": 1
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
