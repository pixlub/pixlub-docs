# Borde difuminado: referencia de la API

Suaviza los bordes de la transparencia (fundido de la máscara alfa)

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/feather` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una imagen o varias) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen(es)**<br />Imagen cuyos bordes de transparencia se suavizan. |

## Ajustes

### General

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `radius` | `number` | `8` | mín. 1 px · máx. 100 px · paso de 1 | **Radio**<br />Radio del fundido |
| `mode` | `string` | `"both"` | `both` Ambos : Fundido en ambos lados<br />`in` Interior : Fundido hacia el interior<br />`out` Exterior : Fundido hacia el exterior | **Dirección**<br />Dirección del fundido |

### Color

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `tint` | `boolean` | `false` |  | **Colorear el fundido**<br />Colorear el fundido con un color específico |
| `color` | [`Color | ColorGradient`](#type-colorgradient)<br />*Color o degradado* | `"#4c9caf"` |  | **Color**<br />Color del fundido<br />*Color o degradado* : Un color CSS (`"#ff8800"`) para un relleno plano, o un objeto `ColorGradient` para un degradado.<br />Estructura de Color \| ColorGradient y ejemplo : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |

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
curl -X POST https://api.pixlub.com/v1/modules/feather \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"radius":8,"mode":"both","tint":false}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"radius":8,"mode":"both","tint":false}))

const res = await fetch('https://api.pixlub.com/v1/modules/feather', {
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
    "https://api.pixlub.com/v1/modules/feather",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"radius": 8, "mode": "both", "tint": False})},
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
result = client.tools.run("feather", image="photo.png", params={"radius": 8, "mode": "both", "tint": False})
result.save(f"feather{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "feather", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"radius": 8, "mode": "both", "tint": false},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("feather"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

### 1 archivo

> **1 archivo** : Una sola imagen en `in`.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Imagen(es)**<br />Imagen generada por el módulo.<br />Una sola imagen enviada: el archivo conserva la clave `out`. |

### Varios archivos

> **Varios archivos** : Varias imágenes en `in`, hasta 64: su número se deduce de los archivos enviados, usted no lo envía.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG` | **Imagen(es)**<br />Imagen generada por el módulo.<br />Varias imágenes enviadas en `in`: un archivo por imagen, con las claves `out#0`, `out#1`…, en el orden de envío. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "feather",
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

<a name="type-colorgradient"></a>

### ColorGradient

*Objeto*. Degradado de colores: paradas colocadas a lo largo de un eje y la forma de repartirlas.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `stops` | `GradientStop[]` | Paradas de color, al menos dos, en cualquier orden. |
| `type` | `"linear" \| "radial"` | *opcional* · Lineal a lo largo de `angle`, o en círculos desde el centro. `linear` por defecto; sin efecto cuando solo cuenta el orden de los colores (Mapa de degradado). |
| `angle` | `number` | *opcional* · Dirección de un degradado lineal, en grados: 0 hacia arriba, 90 hacia la derecha. `90` por defecto. |

**Ejemplo**

```json
{
  "type": "linear",
  "angle": 90,
  "stops": [
    {
      "color": "#140a2e",
      "at": 0
    },
    {
      "color": "#c264c2",
      "at": 55
    },
    {
      "color": "#ffffff",
      "at": 100
    }
  ]
}
```

<a name="type-gradientstop"></a>

### GradientStop

*Objeto*. Parada de un degradado.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `color` | `Color` | Color CSS de la parada; se conserva el alfa (`#rrggbbaa`). |
| `at` | `number` | Posición de la parada, de 0 (inicio) a 100 (final), en %. |

**Ejemplo**

```json
{
  "color": "#c264c2",
  "at": 55
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/feather/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "radius": {
      "title": "Radius",
      "default": 8,
      "type": "number",
      "minimum": 1,
      "maximum": 100,
      "multipleOf": 1
    },
    "mode": {
      "title": "Direction",
      "default": "both",
      "type": "string",
      "enum": [
        "both",
        "in",
        "out"
      ]
    },
    "tint": {
      "title": "Colorize the fade",
      "default": false,
      "type": "boolean"
    },
    "color": {
      "title": "Color",
      "default": "#4c9caf",
      "anyOf": [
        {
          "type": "string",
          "minLength": 1
        },
        {
          "type": "object",
          "required": [
            "stops"
          ],
          "properties": {
            "stops": {
              "type": "array",
              "items": {
                "type": "object",
                "required": [
                  "color",
                  "at"
                ],
                "properties": {
                  "color": {
                    "type": "string",
                    "minLength": 1
                  },
                  "at": {
                    "type": "number",
                    "minimum": 0,
                    "maximum": 100
                  }
                }
              },
              "minItems": 2
            },
            "type": {
              "type": "string",
              "enum": [
                "linear",
                "radial"
              ]
            },
            "angle": {
              "type": "number"
            }
          }
        }
      ]
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
