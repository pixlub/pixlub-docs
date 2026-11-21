# Noise: API reference

Generates procedural noise (Perlin, simplex, random, Voronoi, spots, cubist, shards) with post-processing and blending

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/noise` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `blend` (One image or several) | no | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image blending source**<br />Optional image blended with the noise; when connected, it also sets its size. |

## Settings

### Noise type

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `type` | `string` | `"perlin"` | `perlin` Perlin<br />`simplex` Simplex<br />`random` Random<br />`voronoi` Voronoi<br />`spots` Spots<br />`cubist` Cubist<br />`shard` Shards | **Type** |

### Perlin

> These settings only count when `type` = `perlin` (Perlin).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `ridged` | `boolean` | `false` |  | **Ridged**<br />Folds the noise onto itself, turning valleys into sharp ridges: gives a mountain or vein-like relief. |

### Random

> These settings only count when `type` = `random` (Random).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `randomGamma` | `number` | `100` | min 10 % · max 500 % · step 1 | **Gamma**<br />Bends the value distribution. Below 100% the noise brightens; above it darkens and bright specks become rare. |

### Voronoi

> These settings only count when `type` = `voronoi` (Voronoi).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `voronoiMode` | `string` | `"f1"` | `f1` Distance<br />`ridge` Ridges<br />`f2` Cracks<br />`cells` Flat | **Mode**<br />What is measured in each cell: distance to the centre, edges between cells, cracks, or one flat tone per cell. |
| `voronoiJitter` | `number` | `100` | min 0 % · max 100 % | **Irregularity**<br />Random offset of each cell centre. At 0% the grid is regular, at 100% cells are fully irregular. |
| `voronoiInvert` | `boolean` | `false` |  | **Invert**<br />Swaps light and dark in the cellular pattern. |

### Spots

> These settings only count when `type` = `spots` (Spots).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `spotsRadius` | `number` | `40` | min 1 % · max 100 % | **Radius**<br />Spot size, relative to its cell. Past 100% spots overlap and merge. |
| `spotsSoftness` | `number` | `60` | min 0 % · max 100 % | **Softness**<br />Width of the edge gradient. At 0% the edge is hard, at 100% the spot is a halo with no solid centre. |
| `spotsDensity` | `number` | `70` | min 0 % · max 100 % | **Density**<br />Share of cells that get a spot. Lower values give a sparser scatter. |
| `spotsSizeJitter` | `number` | `40` | min 0 % · max 100 % | **Size variation**<br />Random radius variation from one spot to another. |
| `spotsInvert` | `boolean` | `false` |  | **Invert**<br />Dark spots on a light background instead of the reverse. |

### Cubist

> These settings only count when `type` = `cubist` (Cubist).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `cubistJitter` | `number` | `90` | min 0 % · max 100 % | **Irregularity**<br />Random offset of the facet centres. Higher values make facets less alike. |
| `cubistShade` | `number` | `60` | min 0 % · max 100 % | **Facet slope**<br />How steep each facet plane is: at 0% every facet is flat, higher values shade it as if lit from an angle. |
| `cubistEdge` | `number` | `30` | min 0 % · max 100 % | **Edges**<br />Darkens the edges between facets to bring out the folds. |

### Shards

> These settings only count when `type` = `shard` (Shards).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `shardJitter` | `number` | `100` | min 0 % · max 100 % | **Irregularity**<br />How irregular the shard cut-out is. |
| `shardSharpness` | `number` | `50` | min 1 % · max 100 % | **Sharpness**<br />Edge thinness. Low gives wide, diffuse shards; high gives thin filaments. |
| `shardStretch` | `number` | `200` | min 20 % · max 800 % · step 5 | **Stretch**<br />Stretches shards along one direction. At 100% they are compact, beyond that they draw out into splinters. |
| `shardAngle` | `number` | `25` | min -180 ° · max 180 ° · step 1 | **Angle**<br />The direction the shards are stretched along. |
| `shardInvert` | `boolean` | `false` |  | **Invert**<br />Swaps light and dark in the shards. |

### Noise

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `octaves` | `number` | `4` | min 1 · max 8 · step 1 | **Octaves**<br />Number of stacked noise layers, each twice as fine as the previous one. More layers means richer detail, and a longer render. |
| `octaveRamp` | [`CurvePoint[]`](#type-curvepoint)<br />*Curve* | `[{"x":0,"y":1},{"x":1,"y":0}]` |  | **Octave ramp**<br />Weight of each layer, from the coarsest (left) to the finest (right). A steep drop gives soft noise, a flat ramp a grainy one.<br />CurvePoint[] structure and example : [`CurvePoint`](#type-curvepoint) |
| `intensity` | `number` | `100` | min 0 % · max 400 % · step 1 | **Intensity**<br />Contrast around mid-grey. At 0% the image goes flat, past 100% the extremes get clipped. |
| `seed` | `number` | `1` | min 0 | **Seed**<br />Changes the random draw. With the same settings, one seed always reproduces the exact same noise. Between two whole numbers the noise slides from one draw to the next: animated in the timeline, the seed moves the cells instead of making them jump. |

### Framing

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `posX` | `number` | `0` | min -100 % · max 100 % · step 0.1 | **X**<br />Shifts the noise horizontally without changing its shape, in % of the width: useful to frame a region you like. |
| `posY` | `number` | `0` | min -100 % · max 100 % · step 0.1 | **Y**<br />Shifts the noise vertically without changing its shape, in % of the height. |
| `rotation` | `number` | `0` | min -180 ° · max 180 ° · step 1 | **Rotation**<br />Rotates the pattern inside the image. |
| `scale` | `number` | `64` | min 1 px · max 1024 px · step 1 | **Scale**<br />Size of the noise in pixels. |
| `tileOverlap` | `number` | `0` | min 0 % · max 50 % | **Tiling overlap**<br />Blends the right edge into the left (and bottom into top) over this width, so the image repeats without a visible seam. |

### Dimensions

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `width` | `number` | `512` | min 1 px · max 8000 px · step 1 | **Width**<br />Width of the generated image. Ignored when an image is connected to the blending input. |
| `height` | `number` | `512` | min 1 px · max 8000 px · step 1 | **Height**<br />Height of the generated image. Ignored when an image is connected to the blending input. |

### Post-processing

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `autoLevel` | `boolean` | `false` |  | **Auto level**<br />Stretches the noise to span the full black-to-white range. Handy when the result looks washed out. |
| `remap` | [`CurvePoint[]`](#type-curvepoint)<br />*Curve* | `[{"x":0,"y":0},{"x":1,"y":1}]` |  | **Remap**<br />Remaps produced value (horizontal) to displayed value (vertical). Use it to isolate a range or invert the noise.<br />CurvePoint[] structure and example : [`CurvePoint`](#type-curvepoint) |
| `quantize` | `boolean` | `false` |  | **Quantize**<br />Reduces the continuous gradient to a few tones, for a flat-shaded look. |

### Quantization

> These settings only count when `quantize` = `true`.

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `quantizeLevels` | `number` | `4` | min 2 · max 64 · step 1 | **Levels**<br />Number of tones kept, from black to white. |
| `quantizeBias` | `number` | `0` | min -100 % · max 100 % | **Bias**<br />Shifts the thresholds between tones: negative darkens overall, positive brightens. |

### Blending

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blendMode` | `string`<br />*Blend mode* | `"multiply"` | `normal` Normal : The layer simply covers what is below.<br />`multiply` Multiply : Darkens: white disappears.<br />`screen` Screen : Lightens: black disappears.<br />`overlay` Overlay : Boosts the contrast below.<br />`darken` Darken : Keeps the darker of the two.<br />`lighten` Lighten : Keeps the lighter of the two.<br />`color-dodge` Color dodge : Brightens up to a glow.<br />`color-burn` Color burn : Darkens and deepens colors.<br />`hard-light` Hard light : Strong contrast, like a spotlight.<br />`soft-light` Soft light : Gentle contrast, like diffused light.<br />`difference` Difference : Inverts where the layer is bright.<br />`exclusion` Exclusion : Like Difference, but softer.<br />`luminosity` Luminosity : Takes only the layer's lightness. | **Blend mode**<br />How the noise combines with the image connected to the input. With no input connected, this has no effect. |
| `blendOpacity` | `number` | `50` | min 0 % · max 100 % · step 1 | **Opacity**<br />How much noise goes into the blend. At 0% the source image comes through untouched. |

## Examples

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

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

### 1 file

> **1 file** : A single image in `blend`.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Generated noise, blended over the received image.<br />A single image sent: the file keeps the `out` key. |

### Several files

> **Several files** : Several images in `blend`, up to 64: their number comes from the files sent, you do not send it.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG` | **Image(s)**<br />Generated noise, blended over the received image.<br />Several images sent in `blend`: one file per image, under the keys `out#0`, `out#1`…, in upload order. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

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

## Types

The structured values of the settings, detailed like classes: each member with its type, then an example.

**CurvePoint[] example**

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

*Object*. Point of a mapping curve.

| Member | Type | Description |
| --- | --- | --- |
| `x` | `number` | Input value, from 0 to 1. |
| `y` | `number` | Output value, from 0 to 1. |
| `i` | `"smooth" \| "bezier" \| "linear" \| "constant"` | *optional* · Join to the next point. `smooth` by default. |
| `a` | `number` | *optional* · Tangent angle in degrees, from -85 to 85 (`bezier` join). |

**Example**

```json
{
  "x": 0.5,
  "y": 0.6
}
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

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

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
