# Extend: API reference

Enlarges the image area without distorting the content

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/extend` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (One image or several) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image whose canvas is enlarged, without distorting its content. |

## Settings

### Add

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `addWidth` | [`Dimension`](#type-dimension)<br />*Dimension* | `{"value":0,"unit":"px"}` | `px` Pixels : From 0 px to 8000 px.<br />`%` Percentage : From 0 % to 400 %. As a percentage of the image width. | **Width +**<br />Width to add around the image content<br />*Dimension* : `Dimension` object: `{ "value": 50, "unit": "%" }`. The bounds of `value` depend on `unit`: see the allowed values. Without `unit`, or for a bare number, `px`.<br />Dimension structure and example : [`Dimension`](#type-dimension) |
| `addHeight` | [`Dimension`](#type-dimension)<br />*Dimension* | `{"value":0,"unit":"px"}` | `px` Pixels : From 0 px to 8000 px.<br />`%` Percentage : From 0 % to 400 %. As a percentage of the image height. | **Height +**<br />Height to add around the image content<br />*Dimension* : `Dimension` object: `{ "value": 50, "unit": "%" }`. The bounds of `value` depend on `unit`: see the allowed values. Without `unit`, or for a bare number, `px`.<br />Dimension structure and example : [`Dimension`](#type-dimension) |

### Origin

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `anchor` | `string`<br />*Anchor* | `"center"` | [grid below](#anchor-anchor) | **Origin**<br />Position of the addition relative to the image content<br />*Anchor* : Point of a 3 × 3 grid, from the top-left to the bottom-right corner. |

<a name="anchor-anchor"></a>

**Positions of `anchor`**

| | Left | Center | Right |
| --- | --- | --- | --- |
| **Top** | `top-left`<br />Top left | `top`<br />Top | `top-right`<br />Top right |
| **Middle** | `left`<br />Left | **`center`**<br />**Center** | `right`<br />Right |
| **Bottom** | `bottom-left`<br />Bottom left | `bottom`<br />Bottom | `bottom-right`<br />Bottom right |

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
curl -X POST https://api.pixlub.com/v1/modules/extend \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"addWidth":{"value":0,"unit":"px"},"addHeight":{"value":0,"unit":"px"},"anchor":"center"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"addWidth":{"value":0,"unit":"px"},"addHeight":{"value":0,"unit":"px"},"anchor":"center"}))

const res = await fetch('https://api.pixlub.com/v1/modules/extend', {
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
    "https://api.pixlub.com/v1/modules/extend",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"addWidth": {"value": 0, "unit": "px"}, "addHeight": {"value": 0, "unit": "px"}, "anchor": "center"})},
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
result = client.tools.run("extend", image="photo.png", params={"addWidth": {"value": 0, "unit": "px"}, "addHeight": {"value": 0, "unit": "px"}, "anchor": "center"})
result.save(f"extend{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "extend", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"addWidth": map[string]any{"value": 0, "unit": "px"}, "addHeight": map[string]any{"value": 0, "unit": "px"}, "anchor": "center"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("extend"+result.Extension(), false)
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
  "module": "extend",
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

<a name="type-dimension"></a>

### Dimension

*Object*. Length and its unit.

| Member | Type | Description |
| --- | --- | --- |
| `value` | `number` | Length, in the `unit` unit. |
| `unit` | `"px" \| "%"` | *optional* · `px`: in pixels; `%`: as a percentage of the image width (or height). Each setting lists the units it accepts; the first one by default. |

**Example**

```json
{
  "value": 50,
  "unit": "%"
}
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

`GET /v1/modules/extend/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "addWidth": {
      "title": "Width +",
      "default": {
        "value": 0,
        "unit": "px"
      },
      "anyOf": [
        {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "value"
          ],
          "properties": {
            "value": {
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
          "required": [
            "value",
            "unit"
          ],
          "properties": {
            "value": {
              "type": "number",
              "minimum": 0,
              "maximum": 400
            },
            "unit": {
              "const": "%"
            }
          }
        }
      ]
    },
    "addHeight": {
      "title": "Height +",
      "default": {
        "value": 0,
        "unit": "px"
      },
      "anyOf": [
        {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "value"
          ],
          "properties": {
            "value": {
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
          "required": [
            "value",
            "unit"
          ],
          "properties": {
            "value": {
              "type": "number",
              "minimum": 0,
              "maximum": 400
            },
            "unit": {
              "const": "%"
            }
          }
        }
      ]
    },
    "anchor": {
      "title": "Origin",
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
