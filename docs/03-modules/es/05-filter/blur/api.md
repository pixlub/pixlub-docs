# Desenfoque: referencia de la API

Desenfoque gaussiano, de movimiento, de rotación o de zoom (centro interactivo)

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/blur` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una imagen o varias) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen(es)**<br />Imagen que se va a desenfocar. |

## Ajustes

### General

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `type` | `string` | `"gaussian"` | `gaussian` Gaussiano<br />`motion` Movimiento<br />`radial` Rotación<br />`zoom` Zoom | **Tipo**<br />Tipo de desenfoque |

### Gaussiano

> Estos ajustes solo cuentan cuando `type` = `gaussian` (Gaussiano).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `radius` | `number` | `4` | mín. 0 px · máx. 40 px | **Radio**<br />Radio del desenfoque gaussiano. |

### Movimiento

> Estos ajustes solo cuentan cuando `type` = `motion` (Movimiento).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `angle` | `number` | `0` | mín. -180 ° · máx. 180 ° | **Ángulo**<br />Ángulo de la dirección del movimiento. |
| `distance` | `number` | `24` | mín. 0 px · máx. 500 px · paso de 1 | **Distancia**<br />Distancia del movimiento. |

### Rotación

> Estos ajustes solo cuentan cuando `type` = `radial` (Rotación).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `spin` | `number` | `15` | mín. 0 ° · máx. 90 ° | **Ángulo de rotación**<br />Ángulo de rotación del desenfoque radial. |

### Zoom

> Estos ajustes solo cuentan cuando `type` = `zoom` (Zoom).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `amount` | `number` | `30` | mín. 0 % · máx. 100 % | **Intensidad**<br />Intensidad del desenfoque de zoom. |

### Centro

> Estos ajustes solo cuentan cuando `type` = `radial` (Rotación) o `zoom` (Zoom).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `centerX` | `number` | `50` | mín. 0 % · máx. 100 % · paso de 0.1 | **X**<br />Posición horizontal del centro del desenfoque, en % del ancho |
| `centerY` | `number` | `50` | mín. 0 % · máx. 100 % · paso de 0.1 | **Y**<br />Posición vertical del centro del desenfoque, en % del alto |

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
curl -X POST https://api.pixlub.com/v1/modules/blur \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"type":"gaussian","radius":4}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"type":"gaussian","radius":4}))

const res = await fetch('https://api.pixlub.com/v1/modules/blur', {
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
    "https://api.pixlub.com/v1/modules/blur",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"type": "gaussian", "radius": 4})},
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
result = client.tools.run("blur", image="photo.png", params={"type": "gaussian", "radius": 4})
result.save(f"blur{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "blur", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"type": "gaussian", "radius": 4},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("blur"+result.Extension(), false)
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
  "module": "blur",
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

`GET /v1/modules/blur/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "type": {
      "title": "Type",
      "default": "gaussian",
      "type": "string",
      "enum": [
        "gaussian",
        "motion",
        "radial",
        "zoom"
      ]
    },
    "radius": {
      "title": "Radius",
      "default": 4,
      "type": "number",
      "minimum": 0,
      "maximum": 40
    },
    "angle": {
      "title": "Angle",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180
    },
    "distance": {
      "title": "Distance",
      "default": 24,
      "type": "number",
      "minimum": 0,
      "maximum": 500,
      "multipleOf": 1
    },
    "spin": {
      "title": "Spin angle",
      "default": 15,
      "type": "number",
      "minimum": 0,
      "maximum": 90
    },
    "amount": {
      "title": "Intensity",
      "default": 30,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "centerX": {
      "title": "X",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "centerY": {
      "title": "Y",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
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
