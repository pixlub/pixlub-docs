# Gradient map: API reference

Colorizes the image by mapping its luminance onto a gradient

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/gradientMap` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (One image or several) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image whose luminance is colorized by the gradient. |

## Settings

### Gradient

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `color` | [`ColorGradient`](#type-colorgradient)<br />*Gradient* | [JSON](#default-color) |  | **Gradient**<br />Gradient that recolors the image: each pixel takes the gradient color at the position of its luminance, from black (0%) to white (100%). Only the stops matter.<br />ColorGradient structure and example : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |
| `mix` | `number` | `100` | min 0 % · max 100 % · step 1 | **Blend**<br />Percentage of blending of the gradient with the original image. |
| `invert` | `boolean` | `false` |  | **Invert luminance**<br />Invert the image's luminance. |
| `alphaFromGradient` | `boolean` | `true` |  | **Apply the gradient alpha**<br />Apply the gradient's alpha to the image. |

<a name="default-color"></a>

**Default value of `color`**

```json
{
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
curl -X POST https://api.pixlub.com/v1/modules/gradientMap \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"mix":100,"invert":false,"alphaFromGradient":true}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"mix":100,"invert":false,"alphaFromGradient":true}))

const res = await fetch('https://api.pixlub.com/v1/modules/gradientMap', {
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
    "https://api.pixlub.com/v1/modules/gradientMap",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"mix": 100, "invert": False, "alphaFromGradient": True})},
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
result = client.tools.run("gradientMap", image="photo.png", params={"mix": 100, "invert": False, "alphaFromGradient": True})
result.save(f"gradientMap{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "gradientMap", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"mix": 100, "invert": false, "alphaFromGradient": true},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("gradientMap"+result.Extension(), false)
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
  "module": "gradientMap",
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

`GET /v1/modules/gradientMap/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "color": {
      "title": "Gradient",
      "default": {
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
    "mix": {
      "title": "Blend",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "invert": {
      "title": "Invert luminance",
      "default": false,
      "type": "boolean"
    },
    "alphaFromGradient": {
      "title": "Apply the gradient alpha",
      "default": true,
      "type": "boolean"
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
