# Calcomanía: referencia de la API

Reconstruye mediante IA (nuestros servicios) el relieve 3D del objeto y luego drapea sobre él la imagen que usted coloca libremente encima. Solo se envía la foto, una sola vez; la imagen colocada se queda en su equipo.

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/decalApi` | 25 créditos por operación |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `base` (Una sola imagen) | sí | `PNG`, `JPEG`, `WebP`, `GIF` | **Superficie**<br />Foto del objeto cuyo relieve 3D se reconstruye. Es la única imagen que se envía al servidor. |
| `decal` (Una sola imagen) | sí | `PNG`, `JPEG`, `WebP`, `GIF` | **Motivo**<br />Imagen colocada y drapeada sobre el objeto. |

## Ajustes

### Colocación

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `anchorX` | `number` | `50` | mín. 0 % · máx. 100 % · paso de 0.1 | **X**<br />Posición horizontal de la imagen sobre la superficie del objeto. |
| `anchorY` | `number` | `50` | mín. 0 % · máx. 100 % · paso de 0.1 | **Y**<br />Posición vertical de la imagen sobre la superficie del objeto. |
| `size` | `number` | `40` | mín. 1 % · máx. 150 % · paso de 0.1 | **Tamaño**<br />Tamaño de la imagen colocada, en porcentaje del ancho del objeto. |
| `rotation` | `number` | `0` | mín. -180 ° · máx. 180 ° · paso de 1 | **Rotación**<br />Rotación de la imagen colocada, en grados. |
| `reliefDepth` | `number` | `100` | mín. 0 % · máx. 300 % · paso de 1 | **Profundidad del relieve**<br />Acentúa o aplana la forma reconstruida. |

### Iluminación

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `lighting` | `number` | `50` | mín. 0 % · máx. 100 % | **Reflejos y sombras**<br />Intensidad de los reflejos y las sombras sobre la imagen colocada. |
| `folds` | `number` | `0` | mín. 0 % · máx. 100 % | **Pliegues**<br />Intensidad de los pliegues y ondulaciones sobre la imagen colocada. |

### Capa

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `opacity` | `number` | `100` | mín. 0 % · máx. 100 % · paso de 1 | **Opacidad**<br />Opacidad de la capa. |
| `blendMode` | `string`<br />*Modo de fusión* | `"normal"` | `normal` Normal : La capa cubre lo que está debajo.<br />`multiply` Multiplicar : Oscurece: el blanco desaparece.<br />`screen` Trama : Aclara: el negro desaparece.<br />`overlay` Superponer : Refuerza el contraste de lo que está debajo.<br />`darken` Oscurecer : Conserva el más oscuro de los dos.<br />`color-burn` Subexponer color : Oscurece saturando los colores.<br />`lighten` Aclarar : Conserva el más claro de los dos.<br />`color-dodge` Sobreexponer color : Aclara hasta el destello.<br />`soft-light` Luz suave : Contraste suave, como una luz difusa.<br />`hard-light` Luz fuerte : Contraste marcado, como un foco.<br />`difference` Diferencia : Invierte donde la capa es clara.<br />`exclusion` Exclusión : Como Diferencia, pero más suave.<br />`hue` Tono : Toma solo el tono de la capa.<br />`saturation` Saturación : Toma solo la saturación de la capa.<br />`color` Color : Toma el tono y la saturación, conserva la luminosidad.<br />`luminosity` Luminosidad : Toma solo la luminosidad de la capa. | **Modo de fusión**<br />Modo de fusión de la capa. |
| `clipToBase` | `boolean` | `true` |  | **Permanecer sobre el objeto**<br />Si está activado, la imagen colocada no sobrepasa los bordes del objeto. |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/decalApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F base=@base.png \
  -F decal=@decal.png \
  -F 'params={"anchorX":50,"anchorY":50,"size":40}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('base', await openAsBlob('base.png'), 'base.png')
form.append('decal', await openAsBlob('decal.png'), 'decal.png')
form.append('params', JSON.stringify({"anchorX":50,"anchorY":50,"size":40}))

const res = await fetch('https://api.pixlub.com/v1/modules/decalApi', {
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
    "https://api.pixlub.com/v1/modules/decalApi",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("base", open("base.png", "rb")), ("decal", open("decal.png", "rb"))],
    data={"params": json.dumps({"anchorX": 50, "anchorY": 50, "size": 40})},
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
result = client.tools.run("decalApi", inputs={"base": "base.png", "decal": "decal.png"}, params={"anchorX": 50, "anchorY": 50, "size": 40})
result.save(f"decalApi{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "decalApi", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "base": pixlub.FromPath("base.png"),
        "decal": pixlub.FromPath("decal.png"),
    },
    Params: map[string]any{"anchorX": 50, "anchorY": 50, "size": 40},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("decalApi"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Imagen**<br />Foto con la imagen colocada drapeada sobre su relieve. |
| `data` | [`DecalSurface`](#type-decalsurface) | `JSON` | **Datos**<br />Datos detectados por el servicio remoto, en JSON.<br />Contenido del archivo: un objeto `DecalSurface`. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "decalApi",
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
    "cost": 25,
    "balance": 190
  }
}
```

## Tipos

Los valores estructurados de los ajustes, detallados como clases: cada miembro con su tipo y, después, un ejemplo.

<a name="type-decalsurface"></a>

### DecalSurface

*Objeto*. Relieve 3D reconstruido del objeto fotografiado, sobre el que se ha drapeado la imagen colocada. Posiciones de 0 a 1 dentro de la imagen enviada.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `relief` | `ReliefGrid` | Altura de la superficie en cada punto de una cuadrícula. |
| `outline` | `[number, number][] \| null` | Silueta del objeto, puntos `[x, y]` en orden; `null` cuando ningún objeto se distingue del fondo. |
| `anchor` | `[number, number]` | Centro del objeto `[x, y]`: la colocación propuesta cuando no se envían `anchorX` ni `anchorY`. |
| `width` | `number` | Tamaño propuesto de la imagen colocada, en fracción del ancho, cuando no se envía `size`. |
| `size` | `[number, number]` | Tamaño `[ancho, alto]` de la imagen analizada, en píxeles (reducido a 768 como máximo). |

**Ejemplo**

```json
{
  "relief": {
    "w": 96,
    "h": 72,
    "depth": 0.18342,
    "data": "AAAAAAAAAAD/f/9//3//f…"
  },
  "outline": [
    [
      0.2141,
      0.1875
    ],
    [
      0.7969,
      0.2031
    ],
    [
      0.8125,
      0.8594
    ],
    [
      0.1953,
      0.8438
    ]
  ],
  "anchor": [
    0.5021,
    0.5234
  ],
  "width": 0.4688,
  "size": [
    768,
    576
  ]
}
```

<a name="type-reliefgrid"></a>

### ReliefGrid

*Objeto*. Cuadrícula de alturas, fila por fila desde arriba.

| Miembro | Tipo | Descripción |
| --- | --- | --- |
| `w` | `integer` | Columnas de la cuadrícula. |
| `h` | `integer` | Filas de la cuadrícula. |
| `depth` | `number` | Profundidad del relieve más alto, en fracción del ancho de la imagen. |
| `data` | `string` | Alturas de 0 (fondo) a 1 (lo más cercano): `w × h` enteros de 16 bits little-endian (0 a 65535), en base64. |

**Ejemplo**

```json
{
  "w": 96,
  "h": 72,
  "depth": 0.18342,
  "data": "AAAAAAAAAAD/f/9//3//f…"
}
```

## JSON Schema

El JSON Schema exacto de los ajustes, el que aplica la API para validar el campo params:

`GET /v1/modules/decalApi/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "anchorX": {
      "title": "X",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "anchorY": {
      "title": "Y",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "size": {
      "title": "Size",
      "default": 40,
      "type": "number",
      "minimum": 1,
      "maximum": 150,
      "multipleOf": 0.1
    },
    "rotation": {
      "title": "Rotation",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
    },
    "reliefDepth": {
      "title": "Relief depth",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 300,
      "multipleOf": 1
    },
    "lighting": {
      "title": "Highlights and shadows",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "folds": {
      "title": "Folds",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100
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
    "clipToBase": {
      "title": "Stay on the object",
      "default": true,
      "type": "boolean"
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
