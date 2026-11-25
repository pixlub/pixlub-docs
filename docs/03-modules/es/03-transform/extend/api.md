# Ampliar: referencia de la API

Amplía la zona de la imagen sin deformar el contenido

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/extend` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una imagen o varias) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen(es)**<br />Imagen cuya zona se amplía, sin deformar su contenido. |

## Ajustes

### Ampliación

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `addWidth` | [`Dimension`](#type-dimension)<br />*Dimensión* | `{"value":0,"unit":"px"}` | `px` Pixels : De 0 px a 8000 px.<br />`%` Porcentaje : De 0 % a 400 %. En porcentaje de el ancho de la imagen. | **Ancho +**<br />Ancho que se añade alrededor del contenido de la imagen<br />*Dimensión* : Objeto `Dimension`: `{ "value": 50, "unit": "%" }`. Los límites de `value` dependen de `unit`: consulte los valores permitidos. Sin `unit`, o para un número solo, `px`.<br />Estructura de Dimension y ejemplo : [`Dimension`](#type-dimension) |
| `addHeight` | [`Dimension`](#type-dimension)<br />*Dimensión* | `{"value":0,"unit":"px"}` | `px` Pixels : De 0 px a 8000 px.<br />`%` Porcentaje : De 0 % a 400 %. En porcentaje de el alto de la imagen. | **Alto +**<br />Alto que se añade alrededor del contenido de la imagen<br />*Dimensión* : Objeto `Dimension`: `{ "value": 50, "unit": "%" }`. Los límites de `value` dependen de `unit`: consulte los valores permitidos. Sin `unit`, o para un número solo, `px`.<br />Estructura de Dimension y ejemplo : [`Dimension`](#type-dimension) |

### Origen

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `anchor` | `string`<br />*Anclaje* | `"center"` | [cuadrícula de abajo](#anchor-anchor) | **Origen**<br />Posición de la ampliación respecto al contenido de la imagen<br />*Anclaje* : Punto de una cuadrícula de 3 × 3, desde la esquina superior izquierda hasta la esquina inferior derecha. |

<a name="anchor-anchor"></a>

**Posiciones de `anchor`**

| | Izquierda | Centro | Derecha |
| --- | --- | --- | --- |
| **Arriba** | `top-left`<br />Arriba a la izquierda | `top`<br />Arriba | `top-right`<br />Arriba a la derecha |
| **Medio** | `left`<br />A la izquierda | **`center`**<br />**En el centro** | `right`<br />A la derecha |
| **Abajo** | `bottom-left`<br />Abajo a la izquierda | `bottom`<br />Abajo | `bottom-right`<br />Abajo a la derecha |

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
curl -X POST https://api.pixlub.com/v1/modules/extend \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"addWidth":{"value":0,"unit":"px"},"addHeight":{"value":0,"unit":"px"},"anchor":"center"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"addWidth":{"value":0,"unit":"px"},"addHeight":{"value":0,"unit":"px"},"anchor":"center"}))

const res = await fetch('https://api.pixlub.com/v1/modules/extend', {
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
    "https://api.pixlub.com/v1/modules/extend",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"addWidth": {"value": 0, "unit": "px"}, "addHeight": {"value": 0, "unit": "px"}, "anchor": "center"})},
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
result = client.tools.run("extend", image="photo.png", params={"addWidth": {"value": 0, "unit": "px"}, "addHeight": {"value": 0, "unit": "px"}, "anchor": "center"})
result.save(f"extend{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "extend", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"addWidth": map[string]any{"value": 0, "unit": "px"}, "addHeight": map[string]any{"value": 0, "unit": "px"}, "anchor": "center"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("extend"+result.Extension(), false)
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
  "module": "extend",
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

<a name="type-dimension"></a>

### Dimension

*Objeto*. Longitud y su unidad.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `value` | `number` | Longitud, en la unidad `unit`. |
| `unit` | `"px" \| "%"` | *opcional* · `px`: en píxeles; `%`: en porcentaje del ancho (o del alto) de la imagen. Cada ajuste indica las unidades que admite; la primera, por defecto. |

**Ejemplo**

```json
{
  "value": 50,
  "unit": "%"
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/extend/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "addWidth": {
      "title": "Width +",
      "default": {
        "value": 0,
        "unit": "px"
      },
      "anyOf": [
        {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "value"
          ],
          "properties": {
            "value": {
              "type": "number",
              "minimum": 0,
              "maximum": 8000
            },
            "unit": {
              "const": "px"
            }
          }
        },
        {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "value",
            "unit"
          ],
          "properties": {
            "value": {
              "type": "number",
              "minimum": 0,
              "maximum": 400
            },
            "unit": {
              "const": "%"
            }
          }
        }
      ]
    },
    "addHeight": {
      "title": "Height +",
      "default": {
        "value": 0,
        "unit": "px"
      },
      "anyOf": [
        {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "value"
          ],
          "properties": {
            "value": {
              "type": "number",
              "minimum": 0,
              "maximum": 8000
            },
            "unit": {
              "const": "px"
            }
          }
        },
        {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "value",
            "unit"
          ],
          "properties": {
            "value": {
              "type": "number",
              "minimum": 0,
              "maximum": 400
            },
            "unit": {
              "const": "%"
            }
          }
        }
      ]
    },
    "anchor": {
      "title": "Origin",
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
