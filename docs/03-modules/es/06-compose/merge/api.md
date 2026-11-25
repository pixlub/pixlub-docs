# Fusión: referencia de la API

Superpone una o varias imágenes (capas) sobre otra

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/merge` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `base` (Una sola imagen) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Base**<br />Imagen de fondo sobre la que se colocan las capas. |
| `overlay` (Imagen o lote) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Capa(s)**<br />Capa o lote de capas superpuestas a la base, en orden.<br />Envíe una imagen, o un lote repitiendo el campo una vez por imagen: hasta 7 imágenes por llamada. |

## Ajustes

### Colocación

> **1 archivo** : Una sola imagen en `overlay`.

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `scale` | `number` | `100` | mín. 1 % · máx. 800 % · paso de 1 | **Escala**<br />Escala de la capa. |
| `rotation` | `number` | `0` | mín. -180 ° · máx. 180 ° · paso de 1 | **Rotación**<br />Rotación de la capa. |
| `offsetX` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 0.1 | **X**<br />Desplazamiento horizontal de la capa desde el centro, en % del ancho de la base. |
| `offsetY` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 0.1 | **Y**<br />Desplazamiento vertical de la capa desde el centro, en % del alto de la base. |

### Capa

> **1 archivo** : Una sola imagen en `overlay`.

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `opacity` | `number` | `100` | mín. 0 % · máx. 100 % · paso de 1 | **Opacidad**<br />Opacidad de la capa. |
| `blendMode` | `string`<br />*Modo de fusión* | `"normal"` | `normal` Normal : La capa cubre lo que está debajo.<br />`multiply` Multiplicar : Oscurece: el blanco desaparece.<br />`screen` Trama : Aclara: el negro desaparece.<br />`overlay` Superponer : Refuerza el contraste de lo que está debajo.<br />`darken` Oscurecer : Conserva el más oscuro de los dos.<br />`color-burn` Subexponer color : Oscurece saturando los colores.<br />`lighten` Aclarar : Conserva el más claro de los dos.<br />`color-dodge` Sobreexponer color : Aclara hasta el destello.<br />`soft-light` Luz suave : Contraste suave, como una luz difusa.<br />`hard-light` Luz fuerte : Contraste marcado, como un foco.<br />`difference` Diferencia : Invierte donde la capa es clara.<br />`exclusion` Exclusión : Como Diferencia, pero más suave.<br />`hue` Tono : Toma solo el tono de la capa.<br />`saturation` Saturación : Toma solo la saturación de la capa.<br />`color` Color : Toma el tono y la saturación, conserva la luminosidad.<br />`luminosity` Luminosidad : Toma solo la luminosidad de la capa. | **Modo de fusión**<br />Modo de fusión de la capa. |

### Composición

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `overlayOnTop` | `boolean` | `true` |  | **Capa por encima de la base**<br />Coloca la capa o las capas por encima de la base; si no, la base las cubre. |

### Capas

> **Varios archivos** : Varias imágenes en `overlay`, hasta 7: su número se deduce de los archivos enviados, usted no lo envía.

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `layers` | [`MergeLayer[]`](#type-mergelayer)<br />*Lista de objetos* | `[]` |  | **Capas**<br />Lista de las capas con su colocación y su modo de fusión.<br />*Lista de objetos* : Un elemento por cada archivo `overlay`, en el orden de envío; como máximo 7. Lista de objetos `MergeLayer`, detallados a continuación; un miembro omitido conserva su valor por defecto.<br />Estructura de MergeLayer[] y ejemplo : [`MergeLayer`](#type-mergelayer) |

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
curl -X POST https://api.pixlub.com/v1/modules/merge \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F base=@base.png \
  -F overlay=@overlay-1.png \
  -F overlay=@overlay-2.png \
  -F 'params={"layers":[{"scale":60,"offsetX":-25,"offsetY":0},{"scale":40,"rotation":15,"offsetX":25,"opacity":80,"blendMode":"multiply"}],"overlayOnTop":true}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('base', await openAsBlob('base.png'), 'base.png')
form.append('overlay', await openAsBlob('overlay-1.png'), 'overlay-1.png')
form.append('overlay', await openAsBlob('overlay-2.png'), 'overlay-2.png')
form.append('params', JSON.stringify({"layers":[{"scale":60,"offsetX":-25,"offsetY":0},{"scale":40,"rotation":15,"offsetX":25,"opacity":80,"blendMode":"multiply"}],"overlayOnTop":true}))

const res = await fetch('https://api.pixlub.com/v1/modules/merge', {
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
    "https://api.pixlub.com/v1/modules/merge",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("base", open("base.png", "rb")), ("overlay", open("overlay-1.png", "rb")), ("overlay", open("overlay-2.png", "rb"))],
    data={"params": json.dumps({"layers": [{"scale": 60, "offsetX": -25, "offsetY": 0}, {"scale": 40, "rotation": 15, "offsetX": 25, "opacity": 80, "blendMode": "multiply"}], "overlayOnTop": True})},
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
result = client.tools.run("merge", inputs={"base": "base.png", "overlay": "overlay.png"}, params={"layers": [{"scale": 60, "offsetX": -25, "offsetY": 0}, {"scale": 40, "rotation": 15, "offsetX": 25, "opacity": 80, "blendMode": "multiply"}], "overlayOnTop": True})
result.save(f"merge{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "merge", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "base": pixlub.FromPath("base.png"),
        "overlay": pixlub.FromPath("overlay.png"),
    },
    Params: map[string]any{"layers": []any{map[string]any{"scale": 60, "offsetX": -25, "offsetY": 0}, map[string]any{"scale": 40, "rotation": 15, "offsetX": 25, "opacity": 80, "blendMode": "multiply"}}, "overlayOnTop": true},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("merge"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Imagen(es)**<br />Base y capas fusionadas en una imagen. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "merge",
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

**Ejemplo de MergeLayer[]**

```json
[
  {
    "scale": 60,
    "offsetX": -25,
    "offsetY": 0
  },
  {
    "scale": 40,
    "rotation": 15,
    "offsetX": 25,
    "opacity": 80,
    "blendMode": "multiply"
  }
]
```

<a name="type-mergelayer"></a>

### MergeLayer

*Objeto*. Colocación y aspecto de una capa, situada en el centro de la base y luego desplazada.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `scale` | `number` | *opcional* · Escala de la capa. De 1 a 800 %. `100` por defecto. |
| `rotation` | `number` | *opcional* · Rotación de la capa. De -180 a 180 °. `0` por defecto. |
| `offsetX` | `number` | *opcional* · Desplazamiento horizontal de la capa desde el centro, en % del ancho de la base. De -100 a 100 %. `0` por defecto. |
| `offsetY` | `number` | *opcional* · Desplazamiento vertical de la capa desde el centro, en % del alto de la base. De -100 a 100 %. `0` por defecto. |
| `opacity` | `number` | *opcional* · Opacidad de la capa. De 0 a 100 %. `100` por defecto. |
| `blendMode` | `string` | *opcional* · Modo de fusión de la capa. `"normal"` por defecto.<br />`normal` Normal : La capa cubre lo que está debajo.<br />`multiply` Multiplicar : Oscurece: el blanco desaparece.<br />`screen` Trama : Aclara: el negro desaparece.<br />`overlay` Superponer : Refuerza el contraste de lo que está debajo.<br />`darken` Oscurecer : Conserva el más oscuro de los dos.<br />`color-burn` Subexponer color : Oscurece saturando los colores.<br />`lighten` Aclarar : Conserva el más claro de los dos.<br />`color-dodge` Sobreexponer color : Aclara hasta el destello.<br />`soft-light` Luz suave : Contraste suave, como una luz difusa.<br />`hard-light` Luz fuerte : Contraste marcado, como un foco.<br />`difference` Diferencia : Invierte donde la capa es clara.<br />`exclusion` Exclusión : Como Diferencia, pero más suave.<br />`hue` Tono : Toma solo el tono de la capa.<br />`saturation` Saturación : Toma solo la saturación de la capa.<br />`color` Color : Toma el tono y la saturación, conserva la luminosidad.<br />`luminosity` Luminosidad : Toma solo la luminosidad de la capa. |

**Ejemplo**

```json
{
  "scale": 60,
  "offsetX": -25,
  "offsetY": 0
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/merge/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "scale": {
      "title": "Scale",
      "default": 100,
      "type": "number",
      "minimum": 1,
      "maximum": 800,
      "multipleOf": 1
    },
    "rotation": {
      "title": "Rotation",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
    },
    "offsetX": {
      "title": "X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "offsetY": {
      "title": "Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "opacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
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
    "overlayOnTop": {
      "title": "Layer above the base",
      "default": true,
      "type": "boolean"
    },
    "layers": {
      "title": "Layers",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "scale": {
            "title": "Scale",
            "default": 100,
            "type": "number",
            "minimum": 1,
            "maximum": 800,
            "multipleOf": 1
          },
          "rotation": {
            "title": "Rotation",
            "default": 0,
            "type": "number",
            "minimum": -180,
            "maximum": 180,
            "multipleOf": 1
          },
          "offsetX": {
            "title": "X",
            "default": 0,
            "type": "number",
            "minimum": -100,
            "maximum": 100,
            "multipleOf": 0.1
          },
          "offsetY": {
            "title": "Y",
            "default": 0,
            "type": "number",
            "minimum": -100,
            "maximum": 100,
            "multipleOf": 0.1
          },
          "opacity": {
            "title": "Opacity",
            "default": 100,
            "type": "number",
            "minimum": 0,
            "maximum": 100,
            "multipleOf": 1
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
          }
        }
      },
      "maxItems": 16
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
