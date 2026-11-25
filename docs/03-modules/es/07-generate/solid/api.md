# Sólido: referencia de la API

Genera una forma rellena de un color sólido o de un degradado

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/solid` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `background` (Una sola imagen) | no | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Fondo**<br />Imagen opcional colocada bajo la forma; si está conectada, también define el tamaño del resultado. |
| `fill` (Una sola imagen) | no | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Medio**<br />Imagen opcional vista a través de la forma, en lugar de su color; el contorno queda por encima. |

## Ajustes

### Forma

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `shape` | `string` | `"rectangle"` | `rectangle` Rectángulo<br />`circle` Círculo<br />`ellipse` Elipse<br />`ring` Anillo<br />`triangle` Triángulo<br />`diamond` Rombo<br />`polygon` Polígono<br />`star` Estrella | **Forma**<br />Forma que se va a generar. |

### Color

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `color` | [`Color | ColorGradient`](#type-colorgradient)<br />*Color o degradado* | `"#4c9caf"` |  | **Color**<br />Color sólido o degradado de la forma.<br />*Color o degradado* : Un color CSS (`"#ff8800"`) para un relleno plano, o un objeto `ColorGradient` para un degradado.<br />Estructura de Color \| ColorGradient y ejemplo : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |
| `innerFill` | `number` | `100` | mín. 0 % · máx. 100 % · paso de 1 | **Relleno interior**<br />Borde de la forma atenuado desde el centro. |

### Fondo

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `backgroundOpacity` | `number` | `100` | mín. 0 % · máx. 100 % · paso de 1 | **Opacidad**<br />Opacidad de la imagen conectada a la entrada Fondo, pintada bajo la forma. |

### Medio dentro de la forma

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `fillFit` | `string` | `"cover"` | `cover` Rellenar : El medio cubre toda la forma, aunque haya que recortarlo.<br />`contain` Entero : El medio cabe entero en la forma; su color queda alrededor. | **Ajuste**<br />Cómo se ajusta en la forma el medio conectado a la entrada Medio. |
| `fillScale` | `number` | `100` | mín. 10 % · máx. 1000 % · paso de 0.1 | **Escala**<br />Escala del medio una vez ajustado; 100 % = ajustado. |
| `fillX` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 0.1 | **Desplazamiento X**<br />Desplazamiento horizontal del medio, como proporción de la mitad del ancho de la forma. |
| `fillY` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 0.1 | **Desplazamiento Y**<br />Desplazamiento vertical del medio, como proporción de la mitad del alto de la forma. |

### Contorno

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `strokeWidth` | `number` | `0` | mín. 0 px · máx. 200 px · paso de 1 | **Grosor**<br />Grosor del contorno de la forma. |
| `strokeColor` | `Color`<br />*Color sólido* | `"#1c2535"` |  | **Color**<br />Color del contorno de la forma.<br />*Color sólido* : Color CSS: `#rrggbb`, `#rrggbbaa`, `rgb()` o `hsl()`. |

### Rotación

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `rotation` | `number` | `0` | mín. -180 ° · máx. 180 ° | **Ángulo**<br />Ángulo de rotación de la forma. |

### Dimensiones

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `width` | `number` | `512` | mín. 1 px · máx. 8000 px · paso de 1 | **Ancho**<br />Ancho de la zona. Se ignora cuando hay una imagen conectada a la entrada Fondo: la zona toma entonces sus dimensiones. |
| `height` | `number` | `512` | mín. 1 px · máx. 8000 px · paso de 1 | **Alto**<br />Alto de la zona. Se ignora cuando hay una imagen conectada a la entrada Fondo: la zona toma entonces sus dimensiones. |
| `scale` | `number` | `100` | mín. 1 % · máx. 400 % · paso de 1 | **Escala**<br />Escala de la forma respecto al ancho de la zona. |
| `relativeWidth` | `number` | `100` | mín. 1 % · máx. 100 % · paso de 1 | **Ancho relativo**<br />Ancho de la forma respecto al ancho de la zona. |

### Posición

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `offsetX` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento X**<br />Desplazamiento horizontal de la forma desde el centro. |
| `offsetY` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 1 | **Desplazamiento Y**<br />Desplazamiento vertical de la forma desde el centro. |

### Esquinas

> Estos ajustes solo cuentan cuando `shape` = `rectangle` (Rectángulo).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `cornerRadius` | `number` | `0` | mín. 0 % · máx. 100 % · paso de 1 | **Redondeo**<br />Redondeo de las esquinas, como proporción de la mitad del lado más corto: 100 % forma una píldora. |

### Anillo

> Estos ajustes solo cuentan cuando `shape` = `ring` (Anillo).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `ringThickness` | `number` | `40` | mín. 1 % · máx. 99 % · paso de 1 | **Grosor**<br />Grosor del anillo. |

### Polígono

> Estos ajustes solo cuentan cuando `shape` = `polygon` (Polígono).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `sides` | `number` | `6` | mín. 3 · máx. 12 · paso de 1 | **Lados**<br />Número de lados del polígono. |

### Estrella

> Estos ajustes solo cuentan cuando `shape` = `star` (Estrella).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `starPoints` | `number` | `5` | mín. 3 · máx. 12 · paso de 1 | **Ramas**<br />Número de puntas de la estrella. |
| `innerRatio` | `number` | `50` | mín. 5 % · máx. 95 % · paso de 1 | **Hendidura**<br />Profundidad de la hendidura de la estrella, como proporción del radio exterior. |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/solid \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F background=@background.png \
  -F 'params={"shape":"rectangle","color":"#4c9caf","innerFill":100}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('background', await openAsBlob('background.png'), 'background.png')
form.append('params', JSON.stringify({"shape":"rectangle","color":"#4c9caf","innerFill":100}))

const res = await fetch('https://api.pixlub.com/v1/modules/solid', {
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
    "https://api.pixlub.com/v1/modules/solid",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("background", open("background.png", "rb"))],
    data={"params": json.dumps({"shape": "rectangle", "color": "#4c9caf", "innerFill": 100})},
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
result = client.tools.run("solid", inputs={"background": "background.png"}, params={"shape": "rectangle", "color": "#4c9caf", "innerFill": 100})
result.save(f"solid{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "solid", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "background": pixlub.FromPath("background.png"),
    },
    Params: map[string]any{"shape": "rectangle", "color": "#4c9caf", "innerFill": 100},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("solid"+result.Extension(), false)
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
  "module": "solid",
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

`GET /v1/modules/solid/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "shape": {
      "title": "Shape",
      "default": "rectangle",
      "type": "string",
      "enum": [
        "rectangle",
        "circle",
        "ellipse",
        "ring",
        "triangle",
        "diamond",
        "polygon",
        "star"
      ]
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
    "innerFill": {
      "title": "Inner filling",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "backgroundOpacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "fillFit": {
      "title": "Fit",
      "default": "cover",
      "type": "string",
      "enum": [
        "cover",
        "contain"
      ]
    },
    "fillScale": {
      "title": "Scale",
      "default": 100,
      "type": "number",
      "minimum": 10,
      "maximum": 1000,
      "multipleOf": 0.1
    },
    "fillX": {
      "title": "Offset X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "fillY": {
      "title": "Offset Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "strokeWidth": {
      "title": "Thickness",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 200,
      "multipleOf": 1
    },
    "strokeColor": {
      "title": "Color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "rotation": {
      "title": "Angle",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180
    },
    "width": {
      "title": "Width",
      "default": 512,
      "type": "number",
      "minimum": 1,
      "maximum": 8000,
      "multipleOf": 1
    },
    "height": {
      "title": "Height",
      "default": 512,
      "type": "number",
      "minimum": 1,
      "maximum": 8000,
      "multipleOf": 1
    },
    "scale": {
      "title": "Scale",
      "default": 100,
      "type": "number",
      "minimum": 1,
      "maximum": 400,
      "multipleOf": 1
    },
    "relativeWidth": {
      "title": "Relative width",
      "default": 100,
      "type": "number",
      "minimum": 1,
      "maximum": 100,
      "multipleOf": 1
    },
    "offsetX": {
      "title": "Offset X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "offsetY": {
      "title": "Offset Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cornerRadius": {
      "title": "Roundness",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "ringThickness": {
      "title": "Thickness",
      "default": 40,
      "type": "number",
      "minimum": 1,
      "maximum": 99,
      "multipleOf": 1
    },
    "sides": {
      "title": "Sides",
      "default": 6,
      "type": "number",
      "minimum": 3,
      "maximum": 12,
      "multipleOf": 1
    },
    "starPoints": {
      "title": "Branches",
      "default": 5,
      "type": "number",
      "minimum": 3,
      "maximum": 12,
      "multipleOf": 1
    },
    "innerRatio": {
      "title": "Inset",
      "default": 50,
      "type": "number",
      "minimum": 5,
      "maximum": 95,
      "multipleOf": 1
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
