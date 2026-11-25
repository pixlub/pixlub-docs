# Ruido: referencia de la API

Genera un ruido procedural (Perlin, simplex, aleatorio, Voronoi, puntos, cubista, esquirlas) con posprocesamiento y fusión

[Ver cómo usarlo en el sitio](./README.md)

| Endpoint | Costo |
| --- | --- |
| `POST /v1/modules/noise` | 1 crédito por archivo |

## Archivos

| Campo | Obligatorio | Formatos | Descripción |
| --- | --- | --- | --- |
| `blend` (Una imagen o varias) | no | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Imagen que se va a fusionar**<br />Imagen opcional fusionada con el ruido; si está conectada, también define su tamaño. |

## Ajustes

### Tipo de ruido

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `type` | `string` | `"perlin"` | `perlin` Perlin<br />`simplex` Simplex<br />`random` Aleatorio<br />`voronoi` Voronoi<br />`spots` Puntos<br />`cubist` Cubista<br />`shard` Esquirlas | **Tipo** |

### Perlin

> Estos ajustes solo cuentan cuando `type` = `perlin` (Perlin).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `ridged` | `boolean` | `false` |  | **Crestas (ridged)**<br />Pliega el ruido sobre sí mismo para convertir los valles en crestas nítidas: da un relieve de montañas o de nervaduras. |

### Aleatorio

> Estos ajustes solo cuentan cuando `type` = `random` (Aleatorio).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `randomGamma` | `number` | `100` | mín. 10 % · máx. 500 % · paso de 1 | **Gamma**<br />Curva la distribución de los valores. Por debajo del 100 %, el ruido se aclara; por encima, se oscurece y los puntos claros escasean. |

### Voronoi

> Estos ajustes solo cuentan cuando `type` = `voronoi` (Voronoi).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `voronoiMode` | `string` | `"f1"` | `f1` Distancia<br />`ridge` Crestas<br />`f2` Grietas<br />`cells` Planos | **Modo**<br />Lo que se mide en cada celda: distancia al centro, aristas entre celdas, grietas o un tono plano uniforme por celda. |
| `voronoiJitter` | `number` | `100` | mín. 0 % · máx. 100 % | **Irregularidad**<br />Desplazamiento aleatorio del centro de cada celda. Al 0 % la cuadrícula es regular; al 100 %, las celdas son totalmente irregulares. |
| `voronoiInvert` | `boolean` | `false` |  | **Invertir**<br />Intercambia lo claro y lo oscuro del motivo celular. |

### Puntos

> Estos ajustes solo cuentan cuando `type` = `spots` (Puntos).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `spotsRadius` | `number` | `40` | mín. 1 % · máx. 100 % | **Radio**<br />Tamaño de los puntos, en proporción a su celda. Por encima del 100 % se superponen y se funden. |
| `spotsSoftness` | `number` | `60` | mín. 0 % · máx. 100 % | **Suavidad**<br />Extensión del degradado en el borde. Al 0 % el borde es nítido; al 100 %, el punto es un halo sin centro sólido. |
| `spotsDensity` | `number` | `70` | mín. 0 % · máx. 100 % | **Densidad**<br />Proporción de celdas que reciben un punto. Cuanto más bajo es el valor, más disperso es el sembrado. |
| `spotsSizeJitter` | `number` | `40` | mín. 0 % · máx. 100 % | **Variación de tamaño**<br />Variación aleatoria del radio de un punto a otro. |
| `spotsInvert` | `boolean` | `false` |  | **Invertir**<br />Puntos oscuros sobre fondo claro en lugar de lo contrario. |

### Cubista

> Estos ajustes solo cuentan cuando `type` = `cubist` (Cubista).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `cubistJitter` | `number` | `90` | mín. 0 % · máx. 100 % | **Irregularidad**<br />Desplazamiento aleatorio del centro de las facetas. Cuanto más alto, menos se parecen las facetas. |
| `cubistShade` | `number` | `60` | mín. 0 % · máx. 100 % | **Inclinación de las facetas**<br />Fuerza de la inclinación del plano de cada faceta: al 0 % cada faceta es un tono plano; más alto, se degrada como iluminada en diagonal. |
| `cubistEdge` | `number` | `30` | mín. 0 % · máx. 100 % | **Aristas**<br />Oscurece las aristas entre facetas para marcar los pliegues. |

### Esquirlas

> Estos ajustes solo cuentan cuando `type` = `shard` (Esquirlas).

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `shardJitter` | `number` | `100` | mín. 0 % · máx. 100 % | **Irregularidad**<br />Irregularidad del recorte de las esquirlas. |
| `shardSharpness` | `number` | `50` | mín. 1 % · máx. 100 % | **Nitidez**<br />Finura de las aristas. Bajo, las esquirlas son anchas y difusas; alto, son hilos finos. |
| `shardStretch` | `number` | `200` | mín. 20 % · máx. 800 % · paso de 5 | **Estiramiento**<br />Alarga las esquirlas en una dirección. Al 100 % son compactas; por encima, se estiran en astillas. |
| `shardAngle` | `number` | `25` | mín. -180 ° · máx. 180 ° · paso de 1 | **Ángulo**<br />Dirección en la que se estiran las esquirlas. |
| `shardInvert` | `boolean` | `false` |  | **Invertir**<br />Intercambia lo claro y lo oscuro de las esquirlas. |

### Ruido

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `octaves` | `number` | `4` | mín. 1 · máx. 8 · paso de 1 | **Octavas**<br />Número de capas de ruido superpuestas, cada una el doble de fina que la anterior. Cuantas más haya, más rico es el detalle y más largo el cálculo. |
| `octaveRamp` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":1},{"x":1,"y":0}]` |  | **Rampa de octavas**<br />Peso de cada capa, de la más gruesa (izquierda) a la más fina (derecha). Una bajada marcada da un ruido suave; una rampa plana, un ruido granulado.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `intensity` | `number` | `100` | mín. 0 % · máx. 400 % · paso de 1 | **Intensidad**<br />Contraste alrededor del gris medio. Al 0 % la imagen se vuelve uniforme; por encima del 100 %, los extremos se recortan. |
| `seed` | `number` | `1` | mín. 0 | **Semilla**<br />Cambia la tirada aleatoria. Con ajustes idénticos, una misma semilla vuelve a dar siempre exactamente el mismo ruido. Entre dos enteros, el ruido se desliza de una tirada a otra: animada en la línea de tiempo, la semilla hace que las celdas se muevan en lugar de saltar. |

### Encuadre

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `posX` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 0.1 | **X**<br />Desplaza el ruido horizontalmente sin cambiar su forma, en % del ancho: sirve para encuadrar una zona que le guste. |
| `posY` | `number` | `0` | mín. -100 % · máx. 100 % · paso de 0.1 | **Y**<br />Desplaza el ruido verticalmente sin cambiar su forma, en % del alto. |
| `rotation` | `number` | `0` | mín. -180 ° · máx. 180 ° · paso de 1 | **Rotación**<br />Hace girar el motivo dentro de la imagen. |
| `scale` | `number` | `64` | mín. 1 px · máx. 1024 px · paso de 1 | **Escala**<br />Tamaño del ruido en píxeles. |
| `tileOverlap` | `number` | `0` | mín. 0 % · máx. 50 % | **Solapamiento (mosaico)**<br />Funde el borde derecho con el izquierdo (y el inferior con el superior) en este ancho, para que la imagen se repita sin costuras visibles. |

### Dimensiones

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `width` | `number` | `512` | mín. 1 px · máx. 8000 px · paso de 1 | **Ancho**<br />Ancho de la imagen generada. Se ignora si hay una imagen conectada a la entrada de fusión. |
| `height` | `number` | `512` | mín. 1 px · máx. 8000 px · paso de 1 | **Alto**<br />Alto de la imagen generada. Se ignora si hay una imagen conectada a la entrada de fusión. |

### Posprocesamiento

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `autoLevel` | `boolean` | `false` |  | **Niveles automáticos**<br />Estira el ruido para que ocupe todo el rango del negro al blanco. Útil cuando el resultado parece apagado. |
| `remap` | [`CurvePoint[]`](#type-curvepoint)<br />*Curva* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Reasignar**<br />Vuelve a trazar la correspondencia entre el valor generado (horizontal) y el valor mostrado (vertical). Sirve para aislar un rango o invertir el ruido.<br />Estructura de CurvePoint[] y ejemplo : [`CurvePoint`](#type-curvepoint) |
| `quantize` | `boolean` | `false` |  | **Cuantizar**<br />Reduce el degradado continuo a un pequeño número de tonos, para un resultado de tonos planos. |

### Cuantización

> Estos ajustes solo cuentan cuando `quantize` = `true`.

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `quantizeLevels` | `number` | `4` | mín. 2 · máx. 64 · paso de 1 | **Niveles**<br />Número de tonos conservados, del negro al blanco. |
| `quantizeBias` | `number` | `0` | mín. -100 % · máx. 100 % | **Sesgo**<br />Desplaza los umbrales entre tonos: negativo oscurece el conjunto y positivo lo aclara. |

### Fusión

| Ajuste | Tipo | Por defecto | Valores permitidos | Descripción |
| --- | --- | --- | --- | --- |
| `blendMode` | `string`<br />*Modo de fusión* | `"multiply"` | `normal` Normal : La capa cubre lo que está debajo.<br />`multiply` Multiplicar : Oscurece: el blanco desaparece.<br />`screen` Trama : Aclara: el negro desaparece.<br />`overlay` Superponer : Refuerza el contraste de lo que está debajo.<br />`darken` Oscurecer : Conserva el más oscuro de los dos.<br />`lighten` Aclarar : Conserva el más claro de los dos.<br />`color-dodge` Sobreexponer color : Aclara hasta el destello.<br />`color-burn` Subexponer color : Oscurece saturando los colores.<br />`hard-light` Luz fuerte : Contraste marcado, como un foco.<br />`soft-light` Luz suave : Contraste suave, como una luz difusa.<br />`difference` Diferencia : Invierte donde la capa es clara.<br />`exclusion` Exclusión : Como Diferencia, pero más suave.<br />`luminosity` Luminosidad : Toma solo la luminosidad de la capa. | **Modo de fusión**<br />Cómo se combina el ruido con la imagen conectada a la entrada. Sin entrada conectada, este ajuste no se aplica. |
| `blendOpacity` | `number` | `50` | mín. 0 % · máx. 100 % · paso de 1 | **Opacidad**<br />Dosis de ruido en la fusión. Al 0 % la imagen de origen sale intacta. |

## Ejemplos

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/noise \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F blend=@blend.png \
  -F 'params={"type":"perlin","ridged":false,"octaves":4}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('blend', await openAsBlob('blend.png'), 'blend.png')
form.append('params', JSON.stringify({"type":"perlin","ridged":false,"octaves":4}))

const res = await fetch('https://api.pixlub.com/v1/modules/noise', {
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
    "https://api.pixlub.com/v1/modules/noise",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("blend", open("blend.png", "rb"))],
    data={"params": json.dumps({"type": "perlin", "ridged": False, "octaves": 4})},
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
result = client.tools.run("noise", inputs={"blend": "blend.png"}, params={"type": "perlin", "ridged": False, "octaves": 4})
result.save(f"noise{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "noise", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "blend": pixlub.FromPath("blend.png"),
    },
    Params: map[string]any{"type": "perlin", "ridged": false, "octaves": 4},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("noise"+result.Extension(), false)
```

## Salidas

Cada archivo devuelto lleva en `outputs` la clave de su salida (`key`): búsquela para encontrar el archivo que quiere en lugar de fiarse de su posición.

### 1 archivo

> **1 archivo** : Una sola imagen en `blend`.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Imagen(es)**<br />Ruido generado, fundido sobre la imagen recibida.<br />Una sola imagen enviada: el archivo conserva la clave `out`. |

### Varios archivos

> **Varios archivos** : Varias imágenes en `blend`, hasta 64: su número se deduce de los archivos enviados, usted no lo envía.

| key | Tipo | Formatos | Descripción |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG` | **Imagen(es)**<br />Ruido generado, fundido sobre la imagen recibida.<br />Varias imágenes enviadas en `blend`: un archivo por imagen, con las claves `out#0`, `out#1`…, en el orden de envío. |

## Respuesta

La respuesta enumera los archivos generados en outputs. Cada enlace está firmado y es válido durante una hora, sin clave de API; los archivos se eliminan al cabo de 24 horas.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "noise",
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

`GET /v1/modules/noise/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "ridged": {
      "title": "Ridged",
      "default": false,
      "type": "boolean"
    },
    "randomGamma": {
      "title": "Gamma",
      "default": 100,
      "type": "number",
      "minimum": 10,
      "maximum": 500,
      "multipleOf": 1
    },
    "voronoiMode": {
      "title": "Mode",
      "default": "f1",
      "type": "string",
      "enum": [
        "f1",
        "ridge",
        "f2",
        "cells"
      ]
    },
    "voronoiJitter": {
      "title": "Irregularity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "voronoiInvert": {
      "title": "Invert",
      "default": false,
      "type": "boolean"
    },
    "spotsRadius": {
      "title": "Radius",
      "default": 40,
      "type": "number",
      "minimum": 1,
      "maximum": 100
    },
    "spotsSoftness": {
      "title": "Softness",
      "default": 60,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "spotsDensity": {
      "title": "Density",
      "default": 70,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "spotsSizeJitter": {
      "title": "Size variation",
      "default": 40,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "spotsInvert": {
      "title": "Invert",
      "default": false,
      "type": "boolean"
    },
    "cubistJitter": {
      "title": "Irregularity",
      "default": 90,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "cubistShade": {
      "title": "Facet slope",
      "default": 60,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "cubistEdge": {
      "title": "Edges",
      "default": 30,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "shardJitter": {
      "title": "Irregularity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "shardSharpness": {
      "title": "Sharpness",
      "default": 50,
      "type": "number",
      "minimum": 1,
      "maximum": 100
    },
    "shardStretch": {
      "title": "Stretch",
      "default": 200,
      "type": "number",
      "minimum": 20,
      "maximum": 800,
      "multipleOf": 5
    },
    "shardAngle": {
      "title": "Angle",
      "default": 25,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
    },
    "shardInvert": {
      "title": "Invert",
      "default": false,
      "type": "boolean"
    },
    "octaves": {
      "title": "Octaves",
      "default": 4,
      "type": "number",
      "minimum": 1,
      "maximum": 8,
      "multipleOf": 1
    },
    "octaveRamp": {
      "title": "Octave ramp",
      "default": [
        {
          "x": 0,
          "y": 1
        },
        {
          "x": 1,
          "y": 0
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
    "intensity": {
      "title": "Intensity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 400,
      "multipleOf": 1
    },
    "seed": {
      "title": "Seed",
      "default": 1,
      "type": "number",
      "minimum": 0
    },
    "posX": {
      "title": "X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "posY": {
      "title": "Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
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
    "scale": {
      "title": "Scale",
      "default": 64,
      "type": "number",
      "minimum": 1,
      "maximum": 1024,
      "multipleOf": 1
    },
    "tileOverlap": {
      "title": "Tiling overlap",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 50
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
    "autoLevel": {
      "title": "Auto level",
      "default": false,
      "type": "boolean"
    },
    "remap": {
      "title": "Remap",
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
    "quantize": {
      "title": "Quantize",
      "default": false,
      "type": "boolean"
    },
    "quantizeLevels": {
      "title": "Levels",
      "default": 4,
      "type": "number",
      "minimum": 2,
      "maximum": 64,
      "multipleOf": 1
    },
    "quantizeBias": {
      "title": "Bias",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100
    },
    "blendMode": {
      "title": "Blend mode",
      "default": "multiply",
      "type": "string",
      "enum": [
        "normal",
        "multiply",
        "screen",
        "overlay",
        "darken",
        "lighten",
        "color-dodge",
        "color-burn",
        "hard-light",
        "soft-light",
        "difference",
        "exclusion",
        "luminosity"
      ]
    },
    "blendOpacity": {
      "title": "Opacity",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "type": {
      "type": "string",
      "default": "perlin"
    }
  }
}
```

## Errores

Ajuste fuera de rango, archivo ausente, créditos insuficientes: cada rechazo tiene su código HTTP.
