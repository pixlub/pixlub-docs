# Seguir un camino: referencia de la API

Desplaza una imagen a lo largo de un camino, del 0 % al 100 % de su longitud; el camino puede salir del encuadre

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/followPath` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una sola imagen) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen**<br />Objeto que se desplaza a lo largo del camino, centrado en él. |

## Ajustes

### Trazado

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `path` | [`Path`](#type-path)<br />*Trazado* | [JSON](#default-path) |  | **Trazado**<br />Dibuje el camino o conecte un módulo Trazado a la entrada del nodo: la conexión tiene entonces prioridad. El resultado tiene el tamaño del marco del camino; los puntos colocados fuera del marco hacen que el objeto entre en la imagen o salga de ella.<br />*Trazado* : Objeto `Path`: sus anclas `points` se colocan de 0 a 1 dentro del marco, como se detalla a continuación.<br />Estructura de Path y ejemplo : [`Path`](#type-path), [`PathPoint`](#type-pathpoint) |

<a name="default-path"></a>

**Valor por defecto de `path`**

```json
{
  "points": [
    {
      "x": 0.12,
      "y": 0.68
    },
    {
      "x": 0.5,
      "y": 0.3
    },
    {
      "x": 0.88,
      "y": 0.66
    }
  ],
  "closed": false,
  "smooth": true,
  "rounding": 0.5,
  "curve": "arc",
  "w": 512,
  "h": 512
}
```

### Recorrido

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `progress` | `number` | `0` | mín. 0 % · máx. 100 % · paso de 0.1 | **Posición**<br />Posición del objeto en el camino: 0 % en el primer punto y 100 % en el último. Añada fotogramas clave en la línea de tiempo para hacerlo avanzar. |
| `offset` | `number` | `0` | mín. -1000 px · máx. 1000 px · paso de 1 | **Desplazamiento lateral**<br />Separación del objeto a uno u otro lado del camino, perpendicular a él (positivo: a la derecha en el sentido del recorrido). |

### Orientación

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `align` | `boolean` | `true` |  | **Orientar según el camino**<br />El objeto gira para seguir la dirección del camino; su lado derecho mira hacia delante. |
| `upright` | `boolean` | `false` |  | **Mantener derecho**<br />Cuando el camino vuelve hacia la izquierda, el objeto se voltea en espejo en lugar de ponerse cabeza abajo.<br />*Se aplica cuando `align` = `true`.* |
| `angle` | `number` | `0` | mín. -180 ° · máx. 180 ° · paso de 1 | **Rotación**<br />Rotación añadida al objeto. |
| `scale` | `number` | `100` | mín. 1 % · máx. 800 % · paso de 1 | **Escala**<br />Tamaño del objeto, en % de su tamaño original. |

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
curl -X POST https://api.pixlub.com/v1/modules/followPath \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"progress":0,"offset":0,"align":true}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"progress":0,"offset":0,"align":true}))

const res = await fetch('https://api.pixlub.com/v1/modules/followPath', {
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
    "https://api.pixlub.com/v1/modules/followPath",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"progress": 0, "offset": 0, "align": True})},
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
result = client.tools.run("followPath", image="photo.png", params={"progress": 0, "offset": 0, "align": True})
result.save(f"followPath{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "followPath", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"progress": 0, "offset": 0, "align": true},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("followPath"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Imagen(es)**<br />Imagen generada por el módulo. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "followPath",
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

<a name="type-path"></a>

### Path

*Objeto*. Trazado de curvas de Bézier que pasa por anclas, dentro de un marco de referencia.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `points` | `PathPoint[]` | Anclas del trazado, en orden; al menos dos. |
| `closed` | `boolean` | *opcional* · Une la última ancla con la primera. `false` por defecto. |
| `smooth` | `boolean` | *opcional* · Redondea el trazado entre las anclas `auto`; `false` las une con líneas rectas. `true` por defecto. |
| `rounding` | `number` | *opcional* · Fuerza del redondeo, de 0 a 1. `0.5` por defecto. |
| `curve` | `"arc" \| "spline"` | *opcional* · Curvatura de las anclas `auto`: `arc` en arcos de círculo (unas anclas colocadas en redondo dan un círculo exacto), `spline` en curva de Catmull-Rom. `spline` por defecto. |
| `w` | `number` | *opcional* · Ancho del marco de referencia, en píxeles. Con `h`, el trazado conserva sus proporciones y se centra en la imagen; sin ellos, cubre toda la imagen. |
| `h` | `number` | *opcional* · Alto del marco de referencia, en píxeles. |

**Ejemplo**

```json
{
  "points": [
    {
      "x": 0.1,
      "y": 0.7
    },
    {
      "x": 0.5,
      "y": 0.3
    },
    {
      "x": 0.9,
      "y": 0.7
    }
  ],
  "closed": false,
  "smooth": true
}
```

<a name="type-pathpoint"></a>

### PathPoint

*Objeto*. Ancla de un trazado.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `x` | `number` | Posición horizontal, de 0 (izquierda) a 1 (derecha) del marco. |
| `y` | `number` | Posición vertical, de 0 (arriba) a 1 (abajo) del marco. |
| `k` | `"auto" \| "corner" \| "free"` | *opcional* · Tipo de ancla: `auto` redondeada, `corner` ángulo marcado, `free` con los tiradores `i` y `o` indicados. `auto` por defecto. |
| `i` | `{ x, y }` | *opcional* · Tirador de entrada (ancla `free`), relativo al ancla, en fracción del marco. |
| `o` | `{ x, y }` | *opcional* · Tirador de salida (ancla `free`), relativo al ancla. |
| `w` | `number` | *opcional* · Grosor del trazo en esta ancla, en % del grosor ajustado. `100` por defecto. |

**Ejemplo**

```json
{
  "x": 0.5,
  "y": 0.3
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/followPath/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "path": {
      "title": "Path",
      "default": {
        "points": [
          {
            "x": 0.12,
            "y": 0.68
          },
          {
            "x": 0.5,
            "y": 0.3
          },
          {
            "x": 0.88,
            "y": 0.66
          }
        ],
        "closed": false,
        "smooth": true,
        "rounding": 0.5,
        "curve": "arc",
        "w": 512,
        "h": 512
      },
      "type": "object",
      "required": [
        "points"
      ],
      "properties": {
        "points": {
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
              "k": {
                "type": "string",
                "enum": [
                  "auto",
                  "corner",
                  "free"
                ]
              },
              "i": {
                "type": "object",
                "required": [
                  "x",
                  "y"
                ],
                "properties": {
                  "x": {
                    "type": "number"
                  },
                  "y": {
                    "type": "number"
                  }
                }
              },
              "o": {
                "type": "object",
                "required": [
                  "x",
                  "y"
                ],
                "properties": {
                  "x": {
                    "type": "number"
                  },
                  "y": {
                    "type": "number"
                  }
                }
              },
              "w": {
                "type": "number",
                "minimum": 0
              }
            }
          },
          "minItems": 2
        },
        "closed": {
          "type": "boolean"
        },
        "smooth": {
          "type": "boolean"
        },
        "rounding": {
          "type": "number",
          "minimum": 0,
          "maximum": 1
        },
        "curve": {
          "type": "string",
          "enum": [
            "arc",
            "spline"
          ]
        },
        "w": {
          "type": "number",
          "minimum": 1
        },
        "h": {
          "type": "number",
          "minimum": 1
        }
      }
    },
    "progress": {
      "title": "Position",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "offset": {
      "title": "Side offset",
      "default": 0,
      "type": "number",
      "minimum": -1000,
      "maximum": 1000,
      "multipleOf": 1
    },
    "align": {
      "title": "Orient along the path",
      "default": true,
      "type": "boolean"
    },
    "upright": {
      "title": "Keep upright",
      "default": false,
      "type": "boolean"
    },
    "angle": {
      "title": "Rotation",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
    },
    "scale": {
      "title": "Scale",
      "default": 100,
      "type": "number",
      "minimum": 1,
      "maximum": 800,
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
