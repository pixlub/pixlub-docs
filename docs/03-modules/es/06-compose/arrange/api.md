# Disposición: referencia de la API

Alinea varias imágenes una al lado de otra o apiladas (banners, comparativas)

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/arrange` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `a1` (Imagen o lote) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen 1**<br />Imagen (o lote) colocada en la posición 1 de la disposición.<br />Envíe una imagen, o un lote repitiendo el campo una vez por imagen: hasta 8 imágenes por llamada. |

## Ajustes

### General

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `direction` | `string` | `"horizontal"` | `horizontal` Horizontal : Disposición horizontal de las imágenes.<br />`vertical` Vertical : Disposición vertical de las imágenes. | **Dirección**<br />Dirección de la disposición de las imágenes. |
| `align` | `string` | `"center"` | `start` Inicio : Alinear las imágenes en la parte superior de la disposición.<br />`center` Centro : Alinear las imágenes en el centro de la disposición.<br />`end` Fin : Alinear las imágenes en la parte inferior de la disposición. | **Alineación**<br />Alineación de las imágenes en la disposición. |
| `fit` | `string` | `"none"` | `none` Ninguno : No ajustar las imágenes.<br />`fit` Ajustar : Ajustar las imágenes para que se adapten a la disposición.<br />`stretch` Estirar : Estirar las imágenes para llenar el espacio disponible. | **Ajuste**<br />Ajuste de las imágenes en la disposición. |
| `gap` | `number` | `0` | mín. 0 px · máx. 500 px · paso de 1 | **Espaciado**<br />Espaciado entre las imágenes de la disposición. |

### Fondo

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `bgTransparent` | `boolean` | `true` |  | **Transparente** |
| `bgColor` | `Color`<br />*Color sólido* | `"#ffffff"` |  | **Color**<br />*Color sólido* : Color CSS: `#rrggbb`, `#rrggbbaa`, `rgb()` o `hsl()`. |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/arrange \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F a1=@a1-1.png \
  -F a1=@a1-2.png \
  -F 'params={"direction":"horizontal","align":"center","fit":"none"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('a1', await openAsBlob('a1-1.png'), 'a1-1.png')
form.append('a1', await openAsBlob('a1-2.png'), 'a1-2.png')
form.append('params', JSON.stringify({"direction":"horizontal","align":"center","fit":"none"}))

const res = await fetch('https://api.pixlub.com/v1/modules/arrange', {
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
    "https://api.pixlub.com/v1/modules/arrange",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("a1", open("a1-1.png", "rb")), ("a1", open("a1-2.png", "rb"))],
    data={"params": json.dumps({"direction": "horizontal", "align": "center", "fit": "none"})},
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
result = client.tools.run("arrange", inputs={"a1": "a1.png"}, params={"direction": "horizontal", "align": "center", "fit": "none"})
result.save(f"arrange{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "arrange", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "a1": pixlub.FromPath("a1.png"),
    },
    Params: map[string]any{"direction": "horizontal", "align": "center", "fit": "none"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("arrange"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Imagen(es)**<br />Imágenes recibidas dispuestas en una misma imagen. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "arrange",
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

`GET /v1/modules/arrange/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "direction": {
      "title": "Direction",
      "default": "horizontal",
      "type": "string",
      "enum": [
        "horizontal",
        "vertical"
      ]
    },
    "align": {
      "title": "Alignment",
      "default": "center",
      "type": "string",
      "enum": [
        "start",
        "center",
        "end"
      ]
    },
    "fit": {
      "title": "Adjustment",
      "default": "none",
      "type": "string",
      "enum": [
        "none",
        "fit",
        "stretch"
      ]
    },
    "gap": {
      "title": "Spacing",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 500,
      "multipleOf": 1
    },
    "bgTransparent": {
      "title": "Transparent",
      "default": true,
      "type": "boolean"
    },
    "bgColor": {
      "title": "Color",
      "default": "#ffffff",
      "type": "string",
      "minLength": 1
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
