# Sticker peel: API reference

Peels the image off like a sticker, curling it in a chosen direction

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/sticker` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (One image or several) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image peeled like a sticker; its transparency gives the sticker its shape. |

## Settings

### Peel

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `progress` | `number` | `35` | min 0 % · max 100 % · step 0.1 | **Progress**<br />At 0 the sticker lies flat, at 100 it is fully turned over. |
| `angle` | `number` | `-135` | min -180 ° · max 180 ° | **Direction**<br />Direction the fold travels in. |
| `radius` | `number` | `12` | min 0 % · max 50 % | **Curl radius**<br />How round the curling part is. |
| `frame` | `string` | `"keep"` | `keep` Unchanged<br />`extend` Extended | **Frame**<br />Extended grows the image so the fully turned sticker stays visible. |

### Back side

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `back` | `string` | `"paper"` | `paper` Paper : The back takes a solid color<br />`image` Image : The picture shows through, mirrored | **Back**<br />Type of texture on the back of the sticker. |
| `backColor` | [`Color | ColorGradient`](#type-colorgradient)<br />*Color or gradient* | `"#f4f4f0"` |  | **Back color**<br />Solid color of the back of the sticker.<br />*Applies when `back` = `paper` (Paper).*<br />*Color or gradient* : A CSS color (`"#ff8800"`) for a flat fill, or a `ColorGradient` object for a gradient.<br />Color \| ColorGradient structure and example : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |

### Lighting

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `shading` | `number` | `60` | min 0 % · max 100 % | **Shading**<br />Intensity of the shading on the sticker |
| `shadow` | `number` | `45` | min 0 % · max 100 % | **Drop shadow**<br />Intensity of the drop shadow cast by the sticker |

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
curl -X POST https://api.pixlub.com/v1/modules/sticker \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"progress":35,"angle":-135,"radius":12}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"progress":35,"angle":-135,"radius":12}))

const res = await fetch('https://api.pixlub.com/v1/modules/sticker', {
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
    "https://api.pixlub.com/v1/modules/sticker",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"progress": 35, "angle": -135, "radius": 12})},
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
result = client.tools.run("sticker", image="photo.png", params={"progress": 35, "angle": -135, "radius": 12})
result.save(f"sticker{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "sticker", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"progress": 35, "angle": -135, "radius": 12},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("sticker"+result.Extension(), false)
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
  "module": "sticker",
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

`GET /v1/modules/sticker/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "progress": {
      "title": "Progress",
      "default": 35,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "angle": {
      "title": "Direction",
      "default": -135,
      "type": "number",
      "minimum": -180,
      "maximum": 180
    },
    "radius": {
      "title": "Curl radius",
      "default": 12,
      "type": "number",
      "minimum": 0,
      "maximum": 50
    },
    "frame": {
      "title": "Frame",
      "default": "keep",
      "type": "string",
      "enum": [
        "keep",
        "extend"
      ]
    },
    "back": {
      "title": "Back",
      "default": "paper",
      "type": "string",
      "enum": [
        "paper",
        "image"
      ]
    },
    "backColor": {
      "title": "Back color",
      "default": "#f4f4f0",
      "anyOf": [
        {
          "type": "string",
          "minLength": 1
        },
        {
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
            },
            "type": {
              "type": "string",
              "enum": [
                "linear",
                "radial"
              ]
            },
            "angle": {
              "type": "number"
            }
          }
        }
      ]
    },
    "shading": {
      "title": "Shading",
      "default": 60,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "shadow": {
      "title": "Drop shadow",
      "default": 45,
      "type": "number",
      "minimum": 0,
      "maximum": 100
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
