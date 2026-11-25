# Difuminado de rostros: referencia de la API

Difumina zonas dibujadas a mano o detecta los rostros mediante IA (nuestros servicios). Las zonas se pueden editar en la vista previa: crear, mover, redimensionar, eliminar.

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/faceBlurApi` | 10 créditos por archivo cuando `mode` vale `auto`; 1 crédito por archivo con otro valor de `mode` |

> Este módulo solo llama al servicio remoto cuando mode vale «auto». Con cualquier otro ajuste, la API lo calcula ella misma, al precio de un módulo estándar.

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `image` (Una sola imagen) | sí | `PNG`, `JPEG`, `WebP` | **Imagen**<br />Imagen cuyas zonas se difuminan. En modo automático, se envía al servidor para detectar los rostros. |

## Ajustes

### Detección

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `mode` | `string` | `"manual"` | `manual` Manual : Usted dibuja las zonas que se van a difuminar.<br />`auto` Automático : Nuestros servicios detectan los rostros. | **Modo**<br />Modo de detección de las zonas que se van a difuminar. |

### Desenfoque

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `radius` | `number` | `18` | mín. 1 px · máx. 60 px | **Intensidad**<br />Intensidad del difuminado aplicado a las zonas. |

### Zonas

> Estos ajustes solo cuentan cuando `mode` = `manual` (Manual).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `zones` | [`BlurZone[]`](#type-blurzone)<br />*Lista de objetos* | `[]` |  | **Zonas**<br />Lista de las zonas que se van a difuminar.<br />*Lista de objetos* : Lista de objetos `BlurZone`, detallados a continuación; un miembro omitido conserva su valor por defecto.<br />Estructura de BlurZone[] y ejemplo : [`BlurZone`](#type-blurzone) |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/faceBlurApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F image=@image.png \
  -F 'params={"zones":[{"x":0.42,"y":0.18,"w":0.16,"h":0.24,"shape":"circle"},{"x":0.05,"y":0.8,"w":0.3,"h":0.12}],"mode":"manual","radius":18}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('image', await openAsBlob('image.png'), 'image.png')
form.append('params', JSON.stringify({"zones":[{"x":0.42,"y":0.18,"w":0.16,"h":0.24,"shape":"circle"},{"x":0.05,"y":0.8,"w":0.3,"h":0.12}],"mode":"manual","radius":18}))

const res = await fetch('https://api.pixlub.com/v1/modules/faceBlurApi', {
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
    "https://api.pixlub.com/v1/modules/faceBlurApi",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("image", open("image.png", "rb"))],
    data={"params": json.dumps({"zones": [{"x": 0.42, "y": 0.18, "w": 0.16, "h": 0.24, "shape": "circle"}, {"x": 0.05, "y": 0.8, "w": 0.3, "h": 0.12}], "mode": "manual", "radius": 18})},
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
result = client.tools.run("faceBlurApi", inputs={"image": "image.png"}, params={"zones": [{"x": 0.42, "y": 0.18, "w": 0.16, "h": 0.24, "shape": "circle"}, {"x": 0.05, "y": 0.8, "w": 0.3, "h": 0.12}], "mode": "manual", "radius": 18})
result.save(f"faceBlurApi{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "faceBlurApi", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "image": pixlub.FromPath("image.png"),
    },
    Params: map[string]any{"zones": []any{map[string]any{"x": 0.42, "y": 0.18, "w": 0.16, "h": 0.24, "shape": "circle"}, map[string]any{"x": 0.05, "y": 0.8, "w": 0.3, "h": 0.12}}, "mode": "manual", "radius": 18},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("faceBlurApi"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Imagen(es)**<br />Imagen generada por el módulo. |
| `data` | [`FaceDetection`](#type-facedetection) | `JSON` | **Datos**<br />Datos detectados por el servicio remoto, en JSON.<br />Contenido del archivo: un objeto `FaceDetection`.<br />Se devuelve solo cuando `mode` = `auto`. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "faceBlurApi",
  "outputs": [
    {
      "key": "out",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.png?exp=1767268800&sig=…",
      "content_type": "image/png",
      "bytes": 184203
    },
    {
      "key": "data",
      "name": "data",
      "url": "https://files.pixlub.com/r/5f0c2a91-8d3e-4b7a-a1c4-6e2d9b0f3a58_result.json?exp=1767268800&sig=…",
      "content_type": "application/json",
      "bytes": 82
    }
  ],
  "expires_at": "2026-01-01T12:00:00Z",
  "credits": {
    "cost": 10,
    "balance": 190
  }
}
```

## Tipos

Los valores estructurados de los ajustes, detallados como clases: cada miembro con su tipo y, después, un ejemplo.

**Ejemplo de BlurZone[]**

```json
[
  {
    "x": 0.42,
    "y": 0.18,
    "w": 0.16,
    "h": 0.24,
    "shape": "circle"
  },
  {
    "x": 0.05,
    "y": 0.8,
    "w": 0.3,
    "h": 0.12
  }
]
```

<a name="type-blurzone"></a>

### BlurZone

*Objeto*. Zona difuminada: un rectángulo, o la elipse que contiene, colocado de 0 a 1 dentro de la imagen.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `x` | `number` | Borde izquierdo, de 0 (izquierda) a 1 (derecha) de la imagen. De 0 a 1. |
| `y` | `number` | Borde superior, de 0 (arriba) a 1 (abajo) de la imagen. De 0 a 1. |
| `w` | `number` | Ancho, en fracción del ancho de la imagen. De 0 a 1. |
| `h` | `number` | Alto, en fracción del alto de la imagen. De 0 a 1. |
| `shape` | `"square" \| "circle"` | *opcional* · Rectángulo, o elipse inscrita en el rectángulo. `"square"` por defecto. |

**Ejemplo**

```json
{
  "x": 0.42,
  "y": 0.18,
  "w": 0.16,
  "h": 0.24,
  "shape": "circle"
}
```

<a name="type-facedetection"></a>

### FaceDetection

*Objeto*. Rostros detectados en la imagen enviada, en píxeles de esa imagen.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `image_width` | `integer` | Ancho de la imagen analizada, en píxeles. |
| `image_height` | `integer` | Alto de la imagen analizada, en píxeles. |
| `faces_count` | `integer` | Número de rostros encontrados, sea cual sea su confianza. |
| `faces` | `DetectedFace[]` | Los rostros encontrados. Solo se difuminan los que tienen una confianza de `0.6` o más. |

**Ejemplo**

```json
{
  "image_width": 1280,
  "image_height": 853,
  "faces_count": 1,
  "faces": [
    {
      "bbox": {
        "x": 512.4,
        "y": 188.9,
        "width": 164.2,
        "height": 211.7
      },
      "landmarks": {
        "right_eye": [
          561.3,
          268.1
        ],
        "left_eye": [
          628.8,
          266.4
        ],
        "nose_tip": [
          596.2,
          307.5
        ],
        "right_mouth": [
          567.9,
          345.2
        ],
        "left_mouth": [
          622.4,
          343.8
        ]
      },
      "confidence": 0.9731
    }
  ]
}
```

<a name="type-detectedface"></a>

### DetectedFace

*Objeto*. Un rostro detectado.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `bbox` | `FaceBox` | Recuadro del rostro, limitado a la imagen. |
| `landmarks` | `FaceLandmarks` | Cinco puntos de referencia del rostro, cada uno `[x, y]` en píxeles. |
| `confidence` | `number` | Confianza de la detección, de 0 a 1. |

**Ejemplo**

```json
{
  "bbox": {
    "x": 512.4,
    "y": 188.9,
    "width": 164.2,
    "height": 211.7
  },
  "confidence": 0.9731
}
```

<a name="type-facebox"></a>

### FaceBox

*Objeto*. Rectángulo en píxeles, desde la esquina superior izquierda de la imagen.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `x` | `number` | Borde izquierdo. |
| `y` | `number` | Borde superior. |
| `width` | `number` | Ancho. |
| `height` | `number` | Alto. |

**Ejemplo**

```json
{
  "x": 512.4,
  "y": 188.9,
  "width": 164.2,
  "height": 211.7
}
```

<a name="type-facelandmarks"></a>

### FaceLandmarks

*Objeto*. Puntos de referencia de un rostro, desde el punto de vista de la persona fotografiada.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `right_eye` | `[number, number]` | Ojo derecho. |
| `left_eye` | `[number, number]` | Ojo izquierdo. |
| `nose_tip` | `[number, number]` | Punta de la nariz. |
| `right_mouth` | `[number, number]` | Comisura derecha de la boca. |
| `left_mouth` | `[number, number]` | Comisura izquierda de la boca. |

**Ejemplo**

```json
{
  "right_eye": [
    561.3,
    268.1
  ],
  "left_eye": [
    628.8,
    266.4
  ],
  "nose_tip": [
    596.2,
    307.5
  ],
  "right_mouth": [
    567.9,
    345.2
  ],
  "left_mouth": [
    622.4,
    343.8
  ]
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/faceBlurApi/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "mode": {
      "title": "Mode",
      "default": "manual",
      "type": "string",
      "enum": [
        "manual",
        "auto"
      ]
    },
    "radius": {
      "title": "Intensity",
      "default": 18,
      "type": "number",
      "minimum": 1,
      "maximum": 60
    },
    "zones": {
      "title": "Zones",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "x": {
            "title": "X",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "y": {
            "title": "Y",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "w": {
            "title": "W",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "h": {
            "title": "H",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "shape": {
            "title": "Shape",
            "default": "square",
            "type": "string",
            "enum": [
              "square",
              "circle"
            ]
          }
        },
        "required": [
          "x",
          "y",
          "w",
          "h"
        ]
      }
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
