# Borrador: referencia de la API

Borra a mano partes de la imagen, con una paleta de puntas ajustables

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/eraser` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una sola imagen) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen**<br />Imagen que se va a borrar. |

## Ajustes

### Trazos

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `strokes` | [`BrushStroke[]`](#type-brushstroke)<br />*Lista de objetos* | `[]` |  | **Trazos**<br />Trazos de borrador, eliminados de la imagen en orden; cada uno conserva su punta. Sin trazos, la imagen se queda tal cual.<br />*Lista de objetos* : Lista de objetos `BrushStroke`, detallados a continuación; un miembro omitido conserva su valor por defecto.<br />Estructura de BrushStroke[] y ejemplo : [`BrushStroke`](#type-brushstroke), [`StrokePoint`](#type-strokepoint) |

### Tamaño

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `frameMethod` | `string` | `"module"` | `module` Módulo : El módulo amplía o reduce la imagen según lo que genera.<br />`source` Origen : El resultado conserva el tamaño de la imagen recibida.<br />`custom` Libre : El resultado toma el ancho y el alto elegidos. | **Método**<br />De dónde procede el tamaño del resultado. |
| `frameWidth` | `number` |  | mín. 1 px · máx. 16384 px | **Ancho**<br />Ancho del resultado, en píxeles.<br />*Se aplica cuando `frameMethod` = `custom` (Libre).* |
| `frameHeight` | `number` |  | mín. 1 px · máx. 16384 px | **Alto**<br />Alto del resultado, en píxeles.<br />*Se aplica cuando `frameMethod` = `custom` (Libre).* |
| `frameFit` | `string` | `"none"` | `none` Ninguno (recorta) : El resultado conserva su escala y se recorta.<br />`contain` Contener : Todo el resultado cabe en el tamaño.<br />`cover` Cubrir : El resultado llena el tamaño, aunque sobresalga.<br />`stretch` Estirar : El resultado se estira hasta el tamaño, sin conservar sus proporciones. | **Ajuste**<br />Cómo se coloca el resultado en el tamaño impuesto.<br />*Se aplica cuando `frameMethod` = `source` (Origen) o `custom` (Libre).* |
| `frameAnchor` | `string`<br />*Anclaje* | `"center"` | [cuadrícula de abajo](#anchor-frameanchor) | **Anclaje**<br />Lado al que se ancla el resultado.<br />*Se aplica cuando `frameMethod` = `source` (Origen) o `custom` (Libre) y `frameFit` = `none` (Ninguno (recorta)) o `contain` (Contener) o `cover` (Cubrir).*<br />*Anclaje* : Punto de una cuadrícula de 3 × 3, desde la esquina superior izquierda hasta la esquina inferior derecha. |

<a name="anchor-frameanchor"></a>

**Posiciones de `frameAnchor`**

| | Izquierda | Centro | Derecha |
| --- | --- | --- | --- |
| **Arriba** | `top-left`<br />Arriba a la izquierda | `top`<br />Arriba | `top-right`<br />Arriba a la derecha |
| **Medio** | `left`<br />A la izquierda | **`center`**<br />**En el centro** | `right`<br />A la derecha |
| **Abajo** | `bottom-left`<br />Abajo a la izquierda | `bottom`<br />Abajo | `bottom-right`<br />Abajo a la derecha |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/eraser \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"strokes":[{"points":[[0.1,0.2],[0.3,0.25],[0.5,0.2]],"size":40,"hardness":100},{"points":[[0.8,0.8]],"size":120,"hardness":0,"opacity":50},{"points":[[0.25,0.2],[0.35,0.22]],"size":30,"mode":"restore"}]}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"strokes":[{"points":[[0.1,0.2],[0.3,0.25],[0.5,0.2]],"size":40,"hardness":100},{"points":[[0.8,0.8]],"size":120,"hardness":0,"opacity":50},{"points":[[0.25,0.2],[0.35,0.22]],"size":30,"mode":"restore"}]}))

const res = await fetch('https://api.pixlub.com/v1/modules/eraser', {
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
    "https://api.pixlub.com/v1/modules/eraser",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"strokes": [{"points": [[0.1, 0.2], [0.3, 0.25], [0.5, 0.2]], "size": 40, "hardness": 100}, {"points": [[0.8, 0.8]], "size": 120, "hardness": 0, "opacity": 50}, {"points": [[0.25, 0.2], [0.35, 0.22]], "size": 30, "mode": "restore"}]})},
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
result = client.tools.run("eraser", image="photo.png", params={"strokes": [{"points": [[0.1, 0.2], [0.3, 0.25], [0.5, 0.2]], "size": 40, "hardness": 100}, {"points": [[0.8, 0.8]], "size": 120, "hardness": 0, "opacity": 50}, {"points": [[0.25, 0.2], [0.35, 0.22]], "size": 30, "mode": "restore"}]})
result.save(f"eraser{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "eraser", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"strokes": []any{map[string]any{"points": []any{[]any{0.1, 0.2}, []any{0.3, 0.25}, []any{0.5, 0.2}}, "size": 40, "hardness": 100}, map[string]any{"points": []any{[]any{0.8, 0.8}}, "size": 120, "hardness": 0, "opacity": 50}, map[string]any{"points": []any{[]any{0.25, 0.2}, []any{0.35, 0.22}}, "size": 30, "mode": "restore"}}},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("eraser"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Imagen(es)**<br />Imagen cuyas partes borradas se han vuelto transparentes. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "eraser",
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

## Tipos

Los valores estructurados de los ajustes, detallados como clases: cada miembro con su tipo y, después, un ejemplo.

**Ejemplo de BrushStroke[]**

```json
[
  {
    "points": [
      [
        0.1,
        0.2
      ],
      [
        0.3,
        0.25
      ],
      [
        0.5,
        0.2
      ]
    ],
    "size": 40,
    "hardness": 100
  },
  {
    "points": [
      [
        0.8,
        0.8
      ]
    ],
    "size": 120,
    "hardness": 0,
    "opacity": 50
  },
  {
    "points": [
      [
        0.25,
        0.2
      ],
      [
        0.35,
        0.22
      ]
    ],
    "size": 30,
    "mode": "restore"
  }
]
```

<a name="type-brushstroke"></a>

### BrushStroke

*Objeto*. Trazo de pincel: los puntos que recorre, de 0 a 1 dentro de la imagen, y la punta que los siguió.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `points` | `StrokePoint[]` | Puntos del trazo, en orden; un solo punto deja una pincelada. |
| `size` | `number` | *opcional* · Diámetro de la punta, en píxeles de la imagen. De 1 a 500 px. `20` por defecto. |
| `hardness` | `number` | *opcional* · Nitidez del borde, de 0 (difuminado) a 100 (marcado). De 0 a 100 %. `100` por defecto. |
| `flow` | `number` | *opcional* · Fuerza de cada pincelada. De 1 a 100 %. `100` por defecto. |
| `opacity` | `number` | *opcional* · Tope de todo el trazo. De 1 a 100 %. `100` por defecto. |
| `mode` | `"erase" \| "restore"` | *opcional* · Quitar, o recuperar una parte ya borrada. `"erase"` por defecto. |

**Ejemplo**

```json
{
  "points": [
    [
      0.1,
      0.2
    ],
    [
      0.3,
      0.25
    ],
    [
      0.5,
      0.2
    ]
  ],
  "size": 40,
  "hardness": 100
}
```

<a name="type-strokepoint"></a>

### StrokePoint

*Array de 2 elementos, en este orden*. Punto de un trazo de pincel.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `[0]` | `number` | Posición horizontal, de 0 (izquierda) a 1 (derecha) de la imagen; más allá, la punta sobresale del borde. |
| `[1]` | `number` | Posición vertical, de 0 (arriba) a 1 (abajo) de la imagen. |

**Ejemplo**

```json
[
  0.5,
  0.3
]
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/eraser/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "strokes": {
      "title": "Strokes",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "points": {
            "title": "Points",
            "type": "array",
            "items": {
              "type": "array",
              "items": {
                "type": "number"
              },
              "minItems": 2,
              "maxItems": 2
            },
            "minItems": 1
          },
          "size": {
            "title": "Size",
            "default": 20,
            "type": "number",
            "minimum": 1,
            "maximum": 500
          },
          "hardness": {
            "title": "Hardness",
            "default": 100,
            "type": "number",
            "minimum": 0,
            "maximum": 100
          },
          "flow": {
            "title": "Flow",
            "default": 100,
            "type": "number",
            "minimum": 1,
            "maximum": 100
          },
          "opacity": {
            "title": "Opacity",
            "default": 100,
            "type": "number",
            "minimum": 1,
            "maximum": 100
          },
          "mode": {
            "title": "Mode",
            "default": "erase",
            "type": "string",
            "enum": [
              "erase",
              "restore"
            ]
          }
        },
        "required": [
          "points"
        ]
      }
    },
    "frameMethod": {
      "title": "Method",
      "default": "module",
      "type": "string",
      "enum": [
        "module",
        "source",
        "custom"
      ]
    },
    "frameWidth": {
      "title": "Width",
      "type": "number",
      "minimum": 1,
      "maximum": 16384
    },
    "frameHeight": {
      "title": "Height",
      "type": "number",
      "minimum": 1,
      "maximum": 16384
    },
    "frameFit": {
      "title": "Fit",
      "default": "none",
      "type": "string",
      "enum": [
        "none",
        "contain",
        "cover",
        "stretch"
      ]
    },
    "frameAnchor": {
      "title": "Anchor",
      "default": "center",
      "type": "string",
      "enum": [
        "top-left",
        "top",
        "top-right",
        "left",
        "center",
        "right",
        "bottom-left",
        "bottom",
        "bottom-right"
      ]
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
