# Puppet: API reference

Warps the image by moving pins on a mesh (puppet warp)

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/puppet` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (Single image) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image warped by the pins. |

## Settings

### Warp

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `rigidity` | `number` | `40` | min 0 % · max 100 % | **Stiffness**<br />Controls how much the rest of the image follows the moved pins |

### Pins

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `pins` | [`PuppetPin[]`](#type-puppetpin)<br />*List of objects* | `[]` |  | **Pins**<br />Pins set in the image then moved: the mesh follows each one from its start position to its target. With no moved pin, the image stays as it is.<br />*List of objects* : List of `PuppetPin` objects, detailed below; an omitted member keeps its default value.<br />PuppetPin[] structure and example : [`PuppetPin`](#type-puppetpin) |

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
curl -X POST https://api.pixlub.com/v1/modules/puppet \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"pins":[{"x0":0.5,"y0":0.3,"x1":0.58,"y1":0.22},{"x0":0.5,"y0":0.8,"x1":0.5,"y1":0.8}],"rigidity":40}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"pins":[{"x0":0.5,"y0":0.3,"x1":0.58,"y1":0.22},{"x0":0.5,"y0":0.8,"x1":0.5,"y1":0.8}],"rigidity":40}))

const res = await fetch('https://api.pixlub.com/v1/modules/puppet', {
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
    "https://api.pixlub.com/v1/modules/puppet",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"pins": [{"x0": 0.5, "y0": 0.3, "x1": 0.58, "y1": 0.22}, {"x0": 0.5, "y0": 0.8, "x1": 0.5, "y1": 0.8}], "rigidity": 40})},
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
result = client.tools.run("puppet", image="photo.png", params={"pins": [{"x0": 0.5, "y0": 0.3, "x1": 0.58, "y1": 0.22}, {"x0": 0.5, "y0": 0.8, "x1": 0.5, "y1": 0.8}], "rigidity": 40})
result.save(f"puppet{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "puppet", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"pins": []any{map[string]any{"x0": 0.5, "y0": 0.3, "x1": 0.58, "y1": 0.22}, map[string]any{"x0": 0.5, "y0": 0.8, "x1": 0.5, "y1": 0.8}}, "rigidity": 40},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("puppet"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image produced by the module. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "puppet",
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

**PuppetPin[] example**

```json
[
  {
    "x0": 0.5,
    "y0": 0.3,
    "x1": 0.58,
    "y1": 0.22
  },
  {
    "x0": 0.5,
    "y0": 0.8,
    "x1": 0.5,
    "y1": 0.8
  }
]
```

<a name="type-puppetpin"></a>

### PuppetPin

*Object*. Pin: the point of the image it holds, then where it takes it, from 0 to 1 within the image.

| Member | Type | Description |
| --- | --- | --- |
| `x0` | `number` | Start, horizontal: from 0 (left) to 1 (right). From 0 to 1. |
| `y0` | `number` | Start, vertical: from 0 (top) to 1 (bottom). From 0 to 1. |
| `x1` | `number` | Target, horizontal. From 0 to 1. |
| `y1` | `number` | Target, vertical. A pin whose target is its start holds the image in place. From 0 to 1. |

**Example**

```json
{
  "x0": 0.5,
  "y0": 0.3,
  "x1": 0.58,
  "y1": 0.22
}
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

`GET /v1/modules/puppet/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "rigidity": {
      "title": "Stiffness",
      "default": 40,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "pins": {
      "title": "Pins",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "x0": {
            "title": "x0",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "y0": {
            "title": "y0",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "x1": {
            "title": "x1",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "y1": {
            "title": "y1",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          }
        },
        "required": [
          "x0",
          "y0",
          "x1",
          "y1"
        ]
      }
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
