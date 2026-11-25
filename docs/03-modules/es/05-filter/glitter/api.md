# Purpurina: referencia de la API

Cubre la imagen de purpurina centelleante: escamas irisadas, destellos de estrella y un reflejo que barre, en bucle.

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/glitter` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `in` (Una imagen o varias) | sí | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Imagen a cubrir de purpurina; su transparencia define la forma cubierta. |

## Ajustes

### Escamas

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `shape` | `string` | `"facet"` | `facet` Facetas : Escamas poligonales contiguas, como una lámina de purpurina<br />`round` Redondas : Lentejuelas redondas separadas<br />`diamond` Rombos : Pequeños rombos orientados al azar | **Forma**<br />Dibujo de cada escama. |
| `size` | `number` | `6` | mín. 1 px · máx. 80 px · paso de 0.5 | **Tamaño**<br />Tamaño de una escama, en píxeles de la imagen. |
| `sizeVariation` | `number` | `40` | mín. 0 % · máx. 100 % | **Variación de tamaño**<br />Diferencia de tamaño entre las escamas.<br />*Se aplica cuando `shape` = `round` (Redondas) o `diamond` (Rombos).* |
| `density` | `number` | `65` | mín. 0 % · máx. 100 % | **Densidad**<br />Parte de la superficie cubierta de escamas. |
| `gap` | `number` | `12` | mín. 0 % · máx. 100 % | **Junta**<br />Espacio entre dos facetas.<br />*Se aplica cuando `shape` = `facet` (Facetas).* |
| `seed` | `number` | `1` | mín. 0 | **Semilla**<br />Cambia el sorteo de las escamas; una misma semilla da la misma distribución. |

### Colores

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `colors` | [`ColorGradient`](#type-colorgradient)<br />*Degradado* | [JSON](#default-colors) |  | **Colores**<br />Colores de las escamas, tomados a lo largo de este degradado. Un color transparente deja escamas invisibles.<br />Estructura de ColorGradient y ejemplo : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |
| `colorMode` | `string` | `"iridescent"` | `iridescent` Irisado : Los colores ondulan sobre la superficie y se desplazan con el tiempo, como un holograma<br />`random` Aleatorio : Cada escama conserva su color | **Reparto**<br />Forma de repartir los colores del degradado. |
| `opacity` | `number` | `70` | mín. 0 % · máx. 100 % | **Opacidad**<br />Cuánto cubren las escamas la imagen. |
| `blend` | `string` | `"overlay"` | `normal` Normal<br />`screen` Trama<br />`overlay` Superponer<br />`lighten` Aclarar | **Fusión**<br />Cómo se mezclan las escamas con la imagen: en superponer o trama, el dibujo sigue legible debajo. |

<a name="default-colors"></a>

**Valor por defecto de `colors`**

```json
{
  "stops": [
    {
      "color": "#ffb3e6",
      "at": 0
    },
    {
      "color": "#ffe6a3",
      "at": 20
    },
    {
      "color": "#b5ffd8",
      "at": 40
    },
    {
      "color": "#a6e3ff",
      "at": 60
    },
    {
      "color": "#cdb6ff",
      "at": 80
    },
    {
      "color": "#ffb3e6",
      "at": 100
    }
  ]
}
```

### Brillo

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `brightness` | `number` | `100` | mín. 0 % · máx. 200 % | **Luminosidad**<br />Luminosidad de las escamas y de las estrellas. |
| `twinkle` | `number` | `70` | mín. 0 % · máx. 100 % | **Centelleo**<br />Diferencia entre una escama apagada y una encendida. |
| `glints` | `number` | `35` | mín. 0 % · máx. 100 % | **Estrellas**<br />Cantidad de escamas que lanzan una breve estrella. |
| `glintSize` | `number` | `16` | mín. 0 px · máx. 200 px · paso de 1 | **Tamaño de las estrellas**<br />Longitud de una punta de estrella. |
| `glintsOutside` | `boolean` | `true` |  | **Estrellas fuera de la forma**<br />Las estrellas desbordan la forma, como un reflejo real. |
| `sheen` | `number` | `40` | mín. 0 % · máx. 100 % | **Reflejo**<br />Banda de luz que barre la superficie una vez por ciclo. |
| `sheenAngle` | `number` | `35` | mín. -180 ° · máx. 180 ° | **Ángulo del reflejo**<br />Dirección del barrido. |
| `sheenWidth` | `number` | `25` | mín. 2 % · máx. 100 % | **Ancho del reflejo**<br />Ancho de la banda de luz. |

### Animación

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `animate` | `boolean` | `true` |  | **Animar**<br />La purpurina centellea en la línea de tiempo; desmarcado, la imagen permanece fija. |
| `cycle` | `number` | `2` | mín. 0.2 s · máx. 20 s · paso de 0.1 | **Duración del ciclo**<br />Duración de un bucle completo, sin corte visible.<br />*Se aplica cuando `animate` = `true`.* |
| `area` | `string` | `"shape"` | `shape` Forma : Solo en la parte opaca de la imagen<br />`whole` Toda la imagen : En todas partes, transparencia incluida | **Zona**<br />Dónde se posa la purpurina. |

#### Fase

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `phaseDriven` | `boolean` | `false` |  | **Controlar por fase**<br />El centelleo sigue la fase fijada con fotogramas clave en lugar del tiempo.<br />*Se aplica cuando `animate` = `true`.* |
| `phase` | `number` | `0` | mín. 0 % · máx. 100 % · paso de 0.1 | **Fase**<br />Instante mostrado, de 0 % (inicio) a 100 % (final de la animación).<br />*Se aplica cuando `phaseDriven` = `true`.* |

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
curl -X POST https://api.pixlub.com/v1/modules/glitter \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"shape":"facet","size":6,"density":65}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"shape":"facet","size":6,"density":65}))

const res = await fetch('https://api.pixlub.com/v1/modules/glitter', {
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
    "https://api.pixlub.com/v1/modules/glitter",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"shape": "facet", "size": 6, "density": 65})},
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
result = client.tools.run("glitter", image="photo.png", params={"shape": "facet", "size": 6, "density": 65})
result.save(f"glitter{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "glitter", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"shape": "facet", "size": 6, "density": 65},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("glitter"+result.Extension(), false)
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
  "module": "glitter",
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

`GET /v1/modules/glitter/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "shape": {
      "title": "Shape",
      "default": "facet",
      "type": "string",
      "enum": [
        "facet",
        "round",
        "diamond"
      ]
    },
    "size": {
      "title": "Size",
      "default": 6,
      "type": "number",
      "minimum": 1,
      "maximum": 80,
      "multipleOf": 0.5
    },
    "sizeVariation": {
      "title": "Size variation",
      "default": 40,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "density": {
      "title": "Density",
      "default": 65,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "gap": {
      "title": "Gap",
      "default": 12,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "seed": {
      "title": "Seed",
      "default": 1,
      "type": "number",
      "minimum": 0
    },
    "colors": {
      "title": "Colors",
      "default": {
        "stops": [
          {
            "color": "#ffb3e6",
            "at": 0
          },
          {
            "color": "#ffe6a3",
            "at": 20
          },
          {
            "color": "#b5ffd8",
            "at": 40
          },
          {
            "color": "#a6e3ff",
            "at": 60
          },
          {
            "color": "#cdb6ff",
            "at": 80
          },
          {
            "color": "#ffb3e6",
            "at": 100
          }
        ]
      },
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
        }
      }
    },
    "colorMode": {
      "title": "Distribution",
      "default": "iridescent",
      "type": "string",
      "enum": [
        "iridescent",
        "random"
      ]
    },
    "opacity": {
      "title": "Opacity",
      "default": 70,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "blend": {
      "title": "Blend",
      "default": "overlay",
      "type": "string",
      "enum": [
        "normal",
        "screen",
        "overlay",
        "lighten"
      ]
    },
    "brightness": {
      "title": "Brightness",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 200
    },
    "twinkle": {
      "title": "Twinkle",
      "default": 70,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "glints": {
      "title": "Glints",
      "default": 35,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "glintSize": {
      "title": "Glint size",
      "default": 16,
      "type": "number",
      "minimum": 0,
      "maximum": 200,
      "multipleOf": 1
    },
    "glintsOutside": {
      "title": "Glints past the edge",
      "default": true,
      "type": "boolean"
    },
    "sheen": {
      "title": "Sheen",
      "default": 40,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "sheenAngle": {
      "title": "Sheen angle",
      "default": 35,
      "type": "number",
      "minimum": -180,
      "maximum": 180
    },
    "sheenWidth": {
      "title": "Sheen width",
      "default": 25,
      "type": "number",
      "minimum": 2,
      "maximum": 100
    },
    "animate": {
      "title": "Animate",
      "default": true,
      "type": "boolean"
    },
    "cycle": {
      "title": "Cycle length",
      "default": 2,
      "type": "number",
      "minimum": 0.2,
      "maximum": 20,
      "multipleOf": 0.1
    },
    "area": {
      "title": "Area",
      "default": "shape",
      "type": "string",
      "enum": [
        "shape",
        "whole"
      ]
    },
    "phaseDriven": {
      "title": "Drive by phase",
      "default": false,
      "type": "boolean"
    },
    "phase": {
      "title": "Phase",
      "default": 0,
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
