# Ajuste básico: referencia de la API

Los ajustes esenciales de una foto, reunidos: luz, tonos, balance de blancos y colores

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/baseAdjust` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una imagen o varias) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen(es)**<br />Imagen que se va a revelar. |

## Ajustes

### Luz

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `exposure` | `number` | `0` | mín. -5 IL · máx. 5 IL · paso de 0.05 | **Exposición**<br />En pasos de luz: +1 duplica la luz y -1 la reduce a la mitad. |
| `contrast` | `number` | `0` | mín. -100 · máx. 100 · paso de 1 | **Contraste**<br />Separa los tonos claros de los oscuros alrededor del gris medio, o los acerca. |
| `highlights` | `number` | `0` | mín. -100 · máx. 100 · paso de 1 | **Altas luces**<br />Oscurece o aclara los tonos claros; hacia la izquierda, recupera los detalles de un cielo. |
| `shadows` | `number` | `0` | mín. -100 · máx. 100 · paso de 1 | **Sombras**<br />Aclara o intensifica los tonos oscuros, sin tocar el negro puro. |
| `whites` | `number` | `0` | mín. -100 · máx. 100 · paso de 1 | **Blancos**<br />Mueve el punto blanco: hacia la derecha, los tonos más claros se queman; hacia la izquierda, se apagan. |
| `blacks` | `number` | `0` | mín. -100 · máx. 100 · paso de 1 | **Negros**<br />Mueve el punto negro: hacia la izquierda, los negros se empastan; hacia la derecha, se desvanecen (efecto mate). |

### Color

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `temperature` | `number` | `0` | mín. -100 · máx. 100 · paso de 1 | **Temperatura**<br />Hacia la izquierda, la imagen se enfría (azul); hacia la derecha, se calienta (amarillo anaranjado). |
| `tint` | `number` | `0` | mín. -100 · máx. 100 · paso de 1 | **Matiz**<br />Corrige una dominante: hacia la izquierda, la imagen tira a verde; hacia la derecha, a magenta. |
| `vibrance` | `number` | `0` | mín. -100 · máx. 100 · paso de 1 | **Intensidad**<br />Aviva sobre todo los colores apagados y respeta los que ya son vivos. |
| `saturation` | `number` | `0` | mín. -100 · máx. 100 · paso de 1 | **Saturación**<br />-100 vuelve gris la imagen y +100 duplica la intensidad de todos los colores. |
| `hue` | `number` | `0` | mín. -180 ° · máx. 180 ° · paso de 1 | **Desplazamiento de tono**<br />Hace girar todos los colores en el círculo cromático, conservando la luminosidad. |

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
curl -X POST https://api.pixlub.com/v1/modules/baseAdjust \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"exposure":0,"contrast":0,"highlights":0}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"exposure":0,"contrast":0,"highlights":0}))

const res = await fetch('https://api.pixlub.com/v1/modules/baseAdjust', {
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
    "https://api.pixlub.com/v1/modules/baseAdjust",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"exposure": 0, "contrast": 0, "highlights": 0})},
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
result = client.tools.run("baseAdjust", image="photo.png", params={"exposure": 0, "contrast": 0, "highlights": 0})
result.save(f"baseAdjust{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "baseAdjust", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"exposure": 0, "contrast": 0, "highlights": 0},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("baseAdjust"+result.Extension(), false)
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
  "module": "baseAdjust",
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

`GET /v1/modules/baseAdjust/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "exposure": {
      "title": "Exposure",
      "default": 0,
      "type": "number",
      "minimum": -5,
      "maximum": 5,
      "multipleOf": 0.05
    },
    "contrast": {
      "title": "Contrast",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "highlights": {
      "title": "Highlights",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "shadows": {
      "title": "Shadows",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "whites": {
      "title": "Whites",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "blacks": {
      "title": "Blacks",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "temperature": {
      "title": "Temperature",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "tint": {
      "title": "Tint",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "vibrance": {
      "title": "Vibrance",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "saturation": {
      "title": "Saturation",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "hue": {
      "title": "Hue shift",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
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
