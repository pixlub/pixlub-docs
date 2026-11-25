# Curvas de saturación / tono: referencia de la API

Ajusta la saturación o el tono según la luminancia, la saturación o el tono de cada color

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/hueSatCurves` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una imagen o varias) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen(es)**<br />Imagen cuyo tono o saturación se ajusta con las curvas. |

## Ajustes

### General

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `curveLumSat` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0.5},{"x":1,"y":0.5}]` |  | **Luminancia / Saturación**<br />La saturación de cada color se ajusta según su luminancia. Una curva plana a media altura (y = 0,5) no cambia nada; por encima, el valor sube; por debajo, baja.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveSatSat` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0.5},{"x":1,"y":0.5}]` |  | **Saturación / Saturación**<br />La saturación de cada color se ajusta según su saturación. Una curva plana a media altura (y = 0,5) no cambia nada; por encima, el valor sube; por debajo, baja.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveHueSat` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0.5},{"x":1,"y":0.5}]` |  | **Tono / Saturación**<br />La saturación de cada color se ajusta según su tono. Una curva plana a media altura (y = 0,5) no cambia nada; por encima, el valor sube; por debajo, baja.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveHueHue` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0.5},{"x":1,"y":0.5}]` |  | **Tono / Tono**<br />El tono de cada color se ajusta según su tono. Una curva plana a media altura (y = 0,5) no cambia nada; por encima, el valor sube; por debajo, baja.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |

### Fusión

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blendMode` | `string`<br />*Modo de fusión* | `"normal"` | `normal` Normal : La capa cubre lo que está debajo.<br />`multiply` Multiplicar : Oscurece: el blanco desaparece.<br />`screen` Trama : Aclara: el negro desaparece.<br />`overlay` Superponer : Refuerza el contraste de lo que está debajo.<br />`darken` Oscurecer : Conserva el más oscuro de los dos.<br />`color-burn` Subexponer color : Oscurece saturando los colores.<br />`lighten` Aclarar : Conserva el más claro de los dos.<br />`color-dodge` Sobreexponer color : Aclara hasta el destello.<br />`soft-light` Luz suave : Contraste suave, como una luz difusa.<br />`hard-light` Luz fuerte : Contraste marcado, como un foco.<br />`difference` Diferencia : Invierte donde la capa es clara.<br />`exclusion` Exclusión : Como Diferencia, pero más suave.<br />`hue` Tono : Toma solo el tono de la capa.<br />`saturation` Saturación : Toma solo la saturación de la capa.<br />`color` Color : Toma el tono y la saturación, conserva la luminosidad.<br />`luminosity` Luminosidad : Toma solo la luminosidad de la capa. | **Modo de fusión**<br />Cómo se aplica el ajuste sobre la imagen original. |
| `blendOpacity` | `number` | `100` | mín. 0 % · máx. 100 % · paso de 1 | **Opacidad**<br />Dosis del ajuste. |

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
curl -X POST https://api.pixlub.com/v1/modules/hueSatCurves \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"blendMode":"normal","blendOpacity":100}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"blendMode":"normal","blendOpacity":100}))

const res = await fetch('https://api.pixlub.com/v1/modules/hueSatCurves', {
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
    "https://api.pixlub.com/v1/modules/hueSatCurves",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"blendMode": "normal", "blendOpacity": 100})},
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
result = client.tools.run("hueSatCurves", image="photo.png", params={"blendMode": "normal", "blendOpacity": 100})
result.save(f"hueSatCurves{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "hueSatCurves", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"blendMode": "normal", "blendOpacity": 100},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("hueSatCurves"+result.Extension(), false)
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
  "module": "hueSatCurves",
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

**Ejemplo de CurvePoint[]**

```json
[
  {
    "x": 0,
    "y": 0
  },
  {
    "x": 0.5,
    "y": 0.65
  },
  {
    "x": 1,
    "y": 1
  }
]
```

<a name="type-curvepoint"></a>

### CurvePoint

*Objeto*. Punto de una curva de correspondencia.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `x` | `number` | Valor de entrada, de 0 a 1. |
| `y` | `number` | Valor de salida, de 0 a 1. |
| `i` | `"smooth" \| "bezier" \| "linear" \| "constant"` | *opcional* · Unión con el punto siguiente. `smooth` por defecto. |
| `a` | `number` | *opcional* · Ángulo de la tangente en grados, de -85 a 85 (unión `bezier`). |

**Ejemplo**

```json
{
  "x": 0.5,
  "y": 0.6
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/hueSatCurves/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "curveLumSat": {
      "title": "Luminance / Saturation",
      "default": [
        {
          "x": 0,
          "y": 0.5
        },
        {
          "x": 1,
          "y": 0.5
        }
      ],
      "type": "array",
      "items": {
        "type": "object",
        "required": [
          "x",
          "y"
        ],
        "properties": {
          "x": {
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "y": {
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "i": {
            "type": "string",
            "enum": [
              "smooth",
              "bezier",
              "linear",
              "constant"
            ]
          },
          "a": {
            "type": "number",
            "minimum": -85,
            "maximum": 85
          }
        }
      },
      "minItems": 2
    },
    "curveSatSat": {
      "title": "Saturation / Saturation",
      "default": [
        {
          "x": 0,
          "y": 0.5
        },
        {
          "x": 1,
          "y": 0.5
        }
      ],
      "type": "array",
      "items": {
        "type": "object",
        "required": [
          "x",
          "y"
        ],
        "properties": {
          "x": {
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "y": {
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "i": {
            "type": "string",
            "enum": [
              "smooth",
              "bezier",
              "linear",
              "constant"
            ]
          },
          "a": {
            "type": "number",
            "minimum": -85,
            "maximum": 85
          }
        }
      },
      "minItems": 2
    },
    "curveHueSat": {
      "title": "Hue / Saturation",
      "default": [
        {
          "x": 0,
          "y": 0.5
        },
        {
          "x": 1,
          "y": 0.5
        }
      ],
      "type": "array",
      "items": {
        "type": "object",
        "required": [
          "x",
          "y"
        ],
        "properties": {
          "x": {
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "y": {
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "i": {
            "type": "string",
            "enum": [
              "smooth",
              "bezier",
              "linear",
              "constant"
            ]
          },
          "a": {
            "type": "number",
            "minimum": -85,
            "maximum": 85
          }
        }
      },
      "minItems": 2
    },
    "curveHueHue": {
      "title": "Hue / Hue",
      "default": [
        {
          "x": 0,
          "y": 0.5
        },
        {
          "x": 1,
          "y": 0.5
        }
      ],
      "type": "array",
      "items": {
        "type": "object",
        "required": [
          "x",
          "y"
        ],
        "properties": {
          "x": {
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "y": {
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "i": {
            "type": "string",
            "enum": [
              "smooth",
              "bezier",
              "linear",
              "constant"
            ]
          },
          "a": {
            "type": "number",
            "minimum": -85,
            "maximum": 85
          }
        }
      },
      "minItems": 2
    },
    "blendMode": {
      "title": "Blend mode",
      "default": "normal",
      "type": "string",
      "enum": [
        "normal",
        "multiply",
        "screen",
        "overlay",
        "darken",
        "color-burn",
        "lighten",
        "color-dodge",
        "soft-light",
        "hard-light",
        "difference",
        "exclusion",
        "hue",
        "saturation",
        "color",
        "luminosity"
      ]
    },
    "blendOpacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
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
