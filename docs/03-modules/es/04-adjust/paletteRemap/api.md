# Paleta: recolorear: referencia de la API

Genera una variante recoloreada de la imagen por cada color de la paleta (lote)

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/paletteRemap` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una sola imagen) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen**<br />Imagen recoloreada. |

## Ajustes

### Paleta

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `colors` | `Color[]`<br />*Lista de colores* | [JSON](#default-colors) |  | **Colores**<br />Colores de la paleta: una variante de la imagen por color. Se ignoran cuando hay una paleta conectada a la entrada Paleta.<br />*Lista de colores* : Lista de colores CSS, en orden. |

<a name="default-colors"></a>

**Valor por defecto de `colors`**

```json
[
  "#264653",
  "#2a9d8f",
  "#e9c46a",
  "#f4a261",
  "#e76f51"
]
```

### General

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `preserveLum` | `boolean` | `true` |  | **Conservar la luminosidad**<br />Mantiene la luminosidad de la imagen tal cual: solo cambia el tono, nunca el brillo general. |
| `mix` | `number` | `100` | mín. 0 % · máx. 100 % | **Intensidad**<br />Dosis del recoloreado: 0 % deja la imagen intacta y 100 % la recolorea por completo. |

### Correspondencia

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `limitToBase` | `boolean` | `false` |  | **Limitar a un color base**<br />Solo recolorea los píxeles cercanos al color base. |
| `minSaturation` | `number` | `0` | mín. 0 % · máx. 100 % | **Saturación mínima**<br />Solo recolorea los píxeles cuya saturación es, como mínimo, este porcentaje. |
| `feather` | `number` | `25` | mín. 0 % · máx. 100 % | **Suavizado**<br />Suaviza las transiciones entre las zonas recoloreadas y las no recoloreadas. |

### Color base

> Estos ajustes solo cuentan cuando `limitToBase` = `true`.

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `baseColor` | `Color`<br />*Color sólido* | `"#e76f51"` |  | **Color**<br />Color base: los píxeles cercanos a este color se recolorean.<br />*Color sólido* : Color CSS: `#rrggbb`, `#rrggbbaa`, `rgb()` o `hsl()`. |
| `hueTolerance` | `number` | `60` | mín. 1 ° · máx. 180 ° | **Tolerancia de tono**<br />Tolerancia de tono: los píxeles cercanos al color base se recolorean. |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/paletteRemap \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"preserveLum":true,"mix":100,"limitToBase":false}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"preserveLum":true,"mix":100,"limitToBase":false}))

const res = await fetch('https://api.pixlub.com/v1/modules/paletteRemap', {
  method: 'POST',
  headers: { 'X-API-Key': process.env.PIXLUB_API_KEY },
  body: form,
})
const result = await res.json()
const output = result.outputs.find((o) => o.key === 'out#0')
const image = await fetch(output.url) // lien signé, sans clé
```

### Python

```python
import json, os, requests

res = requests.post(
    "https://api.pixlub.com/v1/modules/paletteRemap",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"preserveLum": True, "mix": 100, "limitToBase": False})},
)
res.raise_for_status()
result = res.json()
output = next(o for o in result["outputs"] if o["key"] == "out#0")
print(output["url"])
```

### SDK Python

```python
import pixlub

client = pixlub.Client()  # PIXLUB_API_KEY, PIXLUB_BASE_URL
result = client.tools.run("paletteRemap", image="photo.png", params={"preserveLum": True, "mix": 100, "limitToBase": False})
result.save(f"paletteRemap{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "paletteRemap", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"preserveLum": true, "mix": 100, "limitToBase": false},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("paletteRemap"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image[]` | `PNG` | **Lote**<br />Una variante recoloreada por cada color de la paleta, en el orden de los colores.<br />Un archivo por imagen del lote, con las claves `out#0`, `out#1`… |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "paletteRemap",
  "outputs": [
    {
      "key": "out#0",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.png?exp=1767268800&sig=…",
      "content_type": "image/png",
      "bytes": 184203
    },
    {
      "key": "out#1",
      "name": "image",
      "url": "https://files.pixlub.com/r/5f0c2a91-8d3e-4b7a-a1c4-6e2d9b0f3a58_result.png?exp=1767268800&sig=…",
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

`GET /v1/modules/paletteRemap/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "colors": {
      "title": "Colors",
      "default": [
        "#264653",
        "#2a9d8f",
        "#e9c46a",
        "#f4a261",
        "#e76f51"
      ],
      "type": "array",
      "items": {
        "type": "string",
        "minLength": 1
      },
      "minItems": 1,
      "maxItems": 32
    },
    "preserveLum": {
      "title": "Preserve brightness",
      "default": true,
      "type": "boolean"
    },
    "mix": {
      "title": "Intensity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "limitToBase": {
      "title": "Limit to a base color",
      "default": false,
      "type": "boolean"
    },
    "minSaturation": {
      "title": "Minimum saturation",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "feather": {
      "title": "Softness",
      "default": 25,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "baseColor": {
      "title": "Color",
      "default": "#e76f51",
      "type": "string",
      "minLength": 1
    },
    "hueTolerance": {
      "title": "Hue tolerance",
      "default": 60,
      "type": "number",
      "minimum": 1,
      "maximum": 180
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
