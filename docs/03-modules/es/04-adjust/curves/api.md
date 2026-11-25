# Curvas: referencia de la API

Ajusta la tonalidad con una curva editable, por canal o global

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/curves` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una imagen o varias) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen(es)**<br />Imagen cuya tonalidad se ajusta con las curvas. |

## Ajustes

### General

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `space` | `string` | `"rgb"` | `rgb` RGB<br />`gray` Gris<br />`cmyk` CMYK<br />`lab` LAB | **Espacio**<br />Espacio de color en el que se ajustan los canales |

### Espacio RGB

> Estos ajustes solo cuentan cuando `space` = `rgb` (RGB).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `curveRgbMaster` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Maestro**<br />Curva aplicada a todos los canales de color a la vez: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveRgbR` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Rojo**<br />Curva del canal Rojo: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveRgbG` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Verde**<br />Curva del canal Verde: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveRgbB` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Azul**<br />Curva del canal Azul: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveRgbAlpha` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Alfa**<br />Curva del canal Alfa: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |

### Espacio Gris

> Estos ajustes solo cuentan cuando `space` = `gray` (Gris).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `curveGrayMaster` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Maestro**<br />Curva aplicada a todos los canales de color a la vez: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveGrayI` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Intensidad**<br />Curva del canal Intensidad: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveGrayAlpha` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Alfa**<br />Curva del canal Alfa: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |

### Espacio CMYK

> Estos ajustes solo cuentan cuando `space` = `cmyk` (CMYK).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `curveCmykMaster` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Maestro**<br />Curva aplicada a todos los canales de color a la vez: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveCmykC` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Cian**<br />Curva del canal Cian: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveCmykM` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Magenta**<br />Curva del canal Magenta: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveCmykY` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Amarillo**<br />Curva del canal Amarillo: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveCmykK` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Negro**<br />Curva del canal Negro: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveCmykAlpha` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Alfa**<br />Curva del canal Alfa: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |

### Espacio LAB

> Estos ajustes solo cuentan cuando `space` = `lab` (LAB).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `curveLabMaster` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Maestro**<br />Curva aplicada a todos los canales de color a la vez: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveLabL` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Luminosidad**<br />Curva del canal Luminosidad: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveLabA` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Crominancia A**<br />Curva del canal Crominancia A: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveLabB` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Crominancia B**<br />Curva del canal Crominancia B: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `curveLabAlpha` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Alfa**<br />Curva del canal Alfa: el eje horizontal es el valor original y el vertical, el valor que toma.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |

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
curl -X POST https://api.pixlub.com/v1/modules/curves \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"space":"rgb","blendMode":"normal","blendOpacity":100}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"space":"rgb","blendMode":"normal","blendOpacity":100}))

const res = await fetch('https://api.pixlub.com/v1/modules/curves', {
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
    "https://api.pixlub.com/v1/modules/curves",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"space": "rgb", "blendMode": "normal", "blendOpacity": 100})},
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
result = client.tools.run("curves", image="photo.png", params={"space": "rgb", "blendMode": "normal", "blendOpacity": 100})
result.save(f"curves{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "curves", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"space": "rgb", "blendMode": "normal", "blendOpacity": 100},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("curves"+result.Extension(), false)
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
  "module": "curves",
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

`GET /v1/modules/curves/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "space": {
      "title": "Space",
      "default": "rgb",
      "type": "string",
      "enum": [
        "rgb",
        "gray",
        "cmyk",
        "lab"
      ]
    },
    "curveRgbMaster": {
      "title": "Master",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveRgbR": {
      "title": "Red",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveRgbG": {
      "title": "Green",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveRgbB": {
      "title": "Blue",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveRgbAlpha": {
      "title": "Alpha",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveGrayMaster": {
      "title": "Master",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveGrayI": {
      "title": "Intensity",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveGrayAlpha": {
      "title": "Alpha",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveCmykMaster": {
      "title": "Master",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveCmykC": {
      "title": "Cyan",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveCmykM": {
      "title": "Magenta",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveCmykY": {
      "title": "Yellow",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveCmykK": {
      "title": "Black",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveCmykAlpha": {
      "title": "Alpha",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveLabMaster": {
      "title": "Master",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveLabL": {
      "title": "Lightness",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveLabA": {
      "title": "Chroma A",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveLabB": {
      "title": "Chroma B",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
    "curveLabAlpha": {
      "title": "Alpha",
      "default": [
        {
          "x": 0,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
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
