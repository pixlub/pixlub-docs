# Glitter: API reference

Covers the image with twinkling glitter: iridescent flakes, star glints and a sweeping sheen, looping.

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/glitter` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (One image or several) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image to glitter; its transparency gives the covered shape. |

## Settings

### Flakes

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `shape` | `string` | `"facet"` | `facet` Facets : Adjoining polygonal flakes, like a glitter sheet<br />`round` Round : Separate round sequins<br />`diamond` Diamonds : Small randomly turned diamonds | **Shape**<br />Drawing of each flake. |
| `size` | `number` | `6` | min 1 px · max 80 px · step 0.5 | **Size**<br />Size of one flake, in image pixels. |
| `sizeVariation` | `number` | `40` | min 0 % · max 100 % | **Size variation**<br />Size difference between flakes.<br />*Applies when `shape` = `round` (Round) or `diamond` (Diamonds).* |
| `density` | `number` | `65` | min 0 % · max 100 % | **Density**<br />Share of the surface covered with flakes. |
| `gap` | `number` | `12` | min 0 % · max 100 % | **Gap**<br />Space between two facets.<br />*Applies when `shape` = `facet` (Facets).* |
| `seed` | `number` | `1` | min 0 | **Seed**<br />Changes the flake draw; the same seed gives the same scatter. |

### Colors

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `colors` | [`ColorGradient`](#type-colorgradient)<br />*Gradient* | [JSON](#default-colors) |  | **Colors**<br />Flake colors, picked along this gradient. A transparent color leaves invisible flakes.<br />ColorGradient structure and example : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |
| `colorMode` | `string` | `"iridescent"` | `iridescent` Iridescent : Colors ripple across the surface and drift over time, like a hologram<br />`random` Random : Each flake keeps its color | **Distribution**<br />How the gradient colors are spread. |
| `opacity` | `number` | `70` | min 0 % · max 100 % | **Opacity**<br />How much the flakes cover the image. |
| `blend` | `string` | `"overlay"` | `normal` Normal<br />`screen` Screen<br />`overlay` Overlay<br />`lighten` Lighten | **Blend**<br />How flakes mix with the image: with overlay or screen the picture stays readable underneath. |

<a name="default-colors"></a>

**Default value of `colors`**

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

### Sparkle

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `brightness` | `number` | `100` | min 0 % · max 200 % | **Brightness**<br />Brightness of the flakes and glints. |
| `twinkle` | `number` | `70` | min 0 % · max 100 % | **Twinkle**<br />Difference between a dim and a lit flake. |
| `glints` | `number` | `35` | min 0 % · max 100 % | **Glints**<br />How many flakes flash a brief star. |
| `glintSize` | `number` | `16` | min 0 px · max 200 px · step 1 | **Glint size**<br />Length of one star arm. |
| `glintsOutside` | `boolean` | `true` |  | **Glints past the edge**<br />Glints reach past the shape, like a real reflection. |
| `sheen` | `number` | `40` | min 0 % · max 100 % | **Sheen**<br />Band of light sweeping the surface once per cycle. |
| `sheenAngle` | `number` | `35` | min -180 ° · max 180 ° | **Sheen angle**<br />Direction of the sweep. |
| `sheenWidth` | `number` | `25` | min 2 % · max 100 % | **Sheen width**<br />Width of the light band. |

### Animation

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `animate` | `boolean` | `true` |  | **Animate**<br />The glitter twinkles in the timeline; unchecked, the image stays still. |
| `cycle` | `number` | `2` | min 0.2 s · max 20 s · step 0.1 | **Cycle length**<br />Length of one seamless loop.<br />*Applies when `animate` = `true`.* |
| `area` | `string` | `"shape"` | `shape` Shape : Only on the opaque part of the image<br />`whole` Whole image : Everywhere, transparency included | **Area**<br />Where the glitter lands. |

#### Phase

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `phaseDriven` | `boolean` | `false` |  | **Drive by phase**<br />The twinkle follows the keyed phase instead of time.<br />*Applies when `animate` = `true`.* |
| `phase` | `number` | `0` | min 0 % · max 100 % · step 0.1 | **Phase**<br />Instant shown, from 0% (start) to 100% (end of the animation).<br />*Applies when `phaseDriven` = `true`.* |

### Size

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `frameMethod` | `string` | `"module"` | `module` Module : The module grows or shrinks the image to fit what it produces.<br />`source` Source : The output keeps the size of the incoming image.<br />`custom` Custom : The output takes the chosen width and height. | **Method**<br />Where the output size comes from. |
| `frameWidth` | `number` |  | min 1 px · max 16384 px | **Width**<br />Output width, in pixels.<br />*Applies when `frameMethod` = `custom` (Custom).* |
| `frameHeight` | `number` |  | min 1 px · max 16384 px | **Height**<br />Output height, in pixels.<br />*Applies when `frameMethod` = `custom` (Custom).* |
| `frameFit` | `string` | `"none"` | `none` None (crop) : The output keeps its scale and is cropped.<br />`contain` Contain : The whole output fits in the size.<br />`cover` Cover : The output fills the size, even if it overflows.<br />`stretch` Stretch : The output stretches to the size, ignoring its proportions. | **Fit**<br />How the output is placed in the imposed size.<br />*Applies when `frameMethod` = `source` (Source) or `custom` (Custom).* |
| `frameAnchor` | `string`<br />*Anchor* | `"center"` | [grid below](#anchor-frameanchor) | **Anchor**<br />Side the output sticks to.<br />*Applies when `frameMethod` = `source` (Source) or `custom` (Custom) and `frameFit` = `none` (None (crop)) or `contain` (Contain) or `cover` (Cover).*<br />*Anchor* : Point of a 3 × 3 grid, from the top-left to the bottom-right corner. |

<a name="anchor-frameanchor"></a>

**Positions of `frameAnchor`**

| | Left | Center | Right |
| --- | --- | --- | --- |
| **Top** | `top-left`<br />Top left | `top`<br />Top | `top-right`<br />Top right |
| **Middle** | `left`<br />Left | **`center`**<br />**Center** | `right`<br />Right |
| **Bottom** | `bottom-left`<br />Bottom left | `bottom`<br />Bottom | `bottom-right`<br />Bottom right |

## Examples

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

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

### 1 file

> **1 file** : A single image in `in`.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image produced by the module.<br />A single image sent: the file keeps the `out` key. |

### Several files

> **Several files** : Several images in `in`, up to 64: their number comes from the files sent, you do not send it.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG` | **Image(s)**<br />Image produced by the module.<br />Several images sent in `in`: one file per image, under the keys `out#0`, `out#1`…, in upload order. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

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

## Types

The structured values of the settings, detailed like classes: each member with its type, then an example.

<a name="type-colorgradient"></a>

### ColorGradient

*Object*. Color gradient: stops placed along an axis, and how to spread them.

| Member | Type | Description |
| --- | --- | --- |
| `stops` | `GradientStop[]` | Color stops, at least two, in any order. |
| `type` | `"linear" \| "radial"` | *optional* · Linear along `angle`, or in circles from the center. `linear` by default; no effect when only the color order matters (Gradient map). |
| `angle` | `number` | *optional* · Direction of a linear gradient, in degrees: 0 upwards, 90 to the right. `90` by default. |

**Example**

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

*Object*. Stop of a gradient.

| Member | Type | Description |
| --- | --- | --- |
| `color` | `Color` | CSS color of the stop; alpha (`#rrggbbaa`) is kept. |
| `at` | `number` | Position of the stop, from 0 (start) to 100 (end), in %. |

**Example**

```json
{
  "color": "#c264c2",
  "at": 55
}
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

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

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
