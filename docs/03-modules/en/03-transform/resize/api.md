# Resize: API reference

Changes the image dimensions

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/resize` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (One image or several) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image to resize. |

## Settings

### Dimensions

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `size` | [`Size`](#type-size)<br />*Size* | `{"width":0,"height":0,"unit":"px"}` | `px` Pixels : From 0 px to 8000 px.<br />`%` Percentage : From 0 % to 800 %. As a percentage of the image width and height.<br />`centimeters` Centimeters : From 0 cm to 500 cm. Converted to pixels by `dpi`.<br />`inches` Inches : From 0 in to 200 in. Converted to pixels by `dpi`. | **Size**<br />Target width and height, in a single unit. A side at 0 ("Auto") keeps the image one, or follows the proportions when they are locked.<br />*Size* : `Size` object: `{ "width": 1280, "height": 720, "unit": "px" }`. The bounds of `width` and `height` depend on `unit`: see the allowed values. Without `unit`, `px`.<br />Size structure and example : [`Size`](#type-size) |
| `lockAspect` | `boolean`<br />*Proportions* | `true` |  | **Keep proportions**<br />*Proportions* : When only one of the `size.width`, `size.height` dimensions is given, the other follows the image proportions; unlocked, it keeps the image one. |
| `dpi` | `number`<br />*Resolution* | `300` | min 1 dpi · max 2400 dpi | **Resolution**<br />*Resolution* : Dots per inch that convert the `centimeters` and `inches` of `size` to pixels; no effect in `px` and `%`. |

### Algorithm

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `algorithm` | `string` | `"bilinear"` | `bilinear` Bilinear<br />`nearest` Nearest neighbor<br />`bicubic` Bicubic | **Algorithm** |

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
curl -X POST https://api.pixlub.com/v1/modules/resize \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"size":{"width":50,"unit":"%"},"lockAspect":true,"dpi":300}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"size":{"width":50,"unit":"%"},"lockAspect":true,"dpi":300}))

const res = await fetch('https://api.pixlub.com/v1/modules/resize', {
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
    "https://api.pixlub.com/v1/modules/resize",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"size": {"width": 50, "unit": "%"}, "lockAspect": True, "dpi": 300})},
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
result = client.tools.run("resize", image="photo.png", params={"size": {"width": 50, "unit": "%"}, "lockAspect": True, "dpi": 300})
result.save(f"resize{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "resize", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"size": map[string]any{"width": 50, "unit": "%"}, "lockAspect": true, "dpi": 300},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("resize"+result.Extension(), false)
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
  "module": "resize",
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

**Size example**

```json
{
  "width": 50,
  "unit": "%"
}
```

<a name="type-size"></a>

### Size

*Object*. Target width and height, in a single unit.

| Member | Type | Description |
| --- | --- | --- |
| `width` | `number` | *optional* · Width, in the `unit` unit. `0` or omitted: the image width, or the one that keeps the proportions when they are locked and only `height` is given. |
| `height` | `number` | *optional* · Height, in the `unit` unit. `0` or omitted: the image height, or the one that keeps the proportions when they are locked and only `width` is given. |
| `unit` | `"px" \| "%" \| "centimeters" \| "inches"` | *optional* · `px`: in pixels; `%`: as a percentage of the image width (for `width`) and height (for `height`); `centimeters` and `inches`: print lengths, converted to pixels by the resolution. Each setting lists the units it accepts; the first one by default. |

**Example**

```json
{
  "width": 1280,
  "height": 720,
  "unit": "px"
}
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

`GET /v1/modules/resize/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "size": {
      "title": "Size",
      "default": {
        "width": 0,
        "height": 0,
        "unit": "px"
      },
      "anyOf": [
        {
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "width": {
              "type": "number",
              "minimum": 0,
              "maximum": 8000
            },
            "height": {
              "type": "number",
              "minimum": 0,
              "maximum": 8000
            },
            "unit": {
              "const": "px"
            }
          }
        },
        {
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "width": {
              "type": "number",
              "minimum": 0,
              "maximum": 800
            },
            "height": {
              "type": "number",
              "minimum": 0,
              "maximum": 800
            },
            "unit": {
              "const": "%"
            }
          },
          "required": [
            "unit"
          ]
        },
        {
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "width": {
              "type": "number",
              "minimum": 0,
              "maximum": 500
            },
            "height": {
              "type": "number",
              "minimum": 0,
              "maximum": 500
            },
            "unit": {
              "const": "centimeters"
            }
          },
          "required": [
            "unit"
          ]
        },
        {
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "width": {
              "type": "number",
              "minimum": 0,
              "maximum": 200
            },
            "height": {
              "type": "number",
              "minimum": 0,
              "maximum": 200
            },
            "unit": {
              "const": "inches"
            }
          },
          "required": [
            "unit"
          ]
        }
      ]
    },
    "lockAspect": {
      "type": "boolean",
      "default": true
    },
    "dpi": {
      "type": "number",
      "minimum": 1,
      "maximum": 2400,
      "default": 300
    },
    "algorithm": {
      "title": "Algorithm",
      "default": "bilinear",
      "type": "string",
      "enum": [
        "bilinear",
        "nearest",
        "bicubic"
      ]
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
