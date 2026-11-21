# Eraser: API reference

Erases parts of the image by hand, with a palette of adjustable tips

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/eraser` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (Single image) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image to erase. |

## Settings

### Strokes

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `strokes` | [`BrushStroke[]`](#type-brushstroke)<br />*List of objects* | `[]` |  | **Strokes**<br />Eraser strokes, removed from the image in order; each one keeps its own tip. With no stroke, the image stays as it is.<br />*List of objects* : List of `BrushStroke` objects, detailed below; an omitted member keeps its default value.<br />BrushStroke[] structure and example : [`BrushStroke`](#type-brushstroke), [`StrokePoint`](#type-strokepoint) |

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
curl -X POST https://api.pixlub.com/v1/modules/eraser \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"strokes":[{"points":[[0.1,0.2],[0.3,0.25],[0.5,0.2]],"size":40,"hardness":100},{"points":[[0.8,0.8]],"size":120,"hardness":0,"opacity":50},{"points":[[0.25,0.2],[0.35,0.22]],"size":30,"mode":"restore"}]}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"strokes":[{"points":[[0.1,0.2],[0.3,0.25],[0.5,0.2]],"size":40,"hardness":100},{"points":[[0.8,0.8]],"size":120,"hardness":0,"opacity":50},{"points":[[0.25,0.2],[0.35,0.22]],"size":30,"mode":"restore"}]}))

const res = await fetch('https://api.pixlub.com/v1/modules/eraser', {
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
    "https://api.pixlub.com/v1/modules/eraser",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"strokes": [{"points": [[0.1, 0.2], [0.3, 0.25], [0.5, 0.2]], "size": 40, "hardness": 100}, {"points": [[0.8, 0.8]], "size": 120, "hardness": 0, "opacity": 50}, {"points": [[0.25, 0.2], [0.35, 0.22]], "size": 30, "mode": "restore"}]})},
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
result = client.tools.run("eraser", image="photo.png", params={"strokes": [{"points": [[0.1, 0.2], [0.3, 0.25], [0.5, 0.2]], "size": 40, "hardness": 100}, {"points": [[0.8, 0.8]], "size": 120, "hardness": 0, "opacity": 50}, {"points": [[0.25, 0.2], [0.35, 0.22]], "size": 30, "mode": "restore"}]})
result.save(f"eraser{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "eraser", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"strokes": []any{map[string]any{"points": []any{[]any{0.1, 0.2}, []any{0.3, 0.25}, []any{0.5, 0.2}}, "size": 40, "hardness": 100}, map[string]any{"points": []any{[]any{0.8, 0.8}}, "size": 120, "hardness": 0, "opacity": 50}, map[string]any{"points": []any{[]any{0.25, 0.2}, []any{0.35, 0.22}}, "size": 30, "mode": "restore"}}},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("eraser"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image whose erased parts have turned transparent. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "eraser",
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

**BrushStroke[] example**

```json
[
  {
    "points": [
      [
        0.1,
        0.2
      ],
      [
        0.3,
        0.25
      ],
      [
        0.5,
        0.2
      ]
    ],
    "size": 40,
    "hardness": 100
  },
  {
    "points": [
      [
        0.8,
        0.8
      ]
    ],
    "size": 120,
    "hardness": 0,
    "opacity": 50
  },
  {
    "points": [
      [
        0.25,
        0.2
      ],
      [
        0.35,
        0.22
      ]
    ],
    "size": 30,
    "mode": "restore"
  }
]
```

<a name="type-brushstroke"></a>

### BrushStroke

*Object*. Brush stroke: the points it runs through, from 0 to 1 within the image, and the tip that followed them.

| Member | Type | Description |
| --- | --- | --- |
| `points` | `StrokePoint[]` | Points of the stroke, in order; a single point lays one dab. |
| `size` | `number` | *optional* · Tip diameter, in image pixels. From 1 to 500 px. `20` by default. |
| `hardness` | `number` | *optional* · Edge sharpness, from 0 (soft) to 100 (crisp). From 0 to 100 %. `100` by default. |
| `flow` | `number` | *optional* · Strength of each dab. From 1 to 100 %. `100` by default. |
| `opacity` | `number` | *optional* · Ceiling of the whole stroke. From 1 to 100 %. `100` by default. |
| `mode` | `"erase" \| "restore"` | *optional* · Remove, or bring back a part already erased. `"erase"` by default. |

**Example**

```json
{
  "points": [
    [
      0.1,
      0.2
    ],
    [
      0.3,
      0.25
    ],
    [
      0.5,
      0.2
    ]
  ],
  "size": 40,
  "hardness": 100
}
```

<a name="type-strokepoint"></a>

### StrokePoint

*Array of 2 items, in this order*. Point of a brush stroke.

| Member | Type | Description |
| --- | --- | --- |
| `[0]` | `number` | Horizontal position, from 0 (left) to 1 (right) of the image; beyond, the tip runs over the edge. |
| `[1]` | `number` | Vertical position, from 0 (top) to 1 (bottom) of the image. |

**Example**

```json
[
  0.5,
  0.3
]
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

`GET /v1/modules/eraser/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "strokes": {
      "title": "Strokes",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "points": {
            "title": "Points",
            "type": "array",
            "items": {
              "type": "array",
              "items": {
                "type": "number"
              },
              "minItems": 2,
              "maxItems": 2
            },
            "minItems": 1
          },
          "size": {
            "title": "Size",
            "default": 20,
            "type": "number",
            "minimum": 1,
            "maximum": 500
          },
          "hardness": {
            "title": "Hardness",
            "default": 100,
            "type": "number",
            "minimum": 0,
            "maximum": 100
          },
          "flow": {
            "title": "Flow",
            "default": 100,
            "type": "number",
            "minimum": 1,
            "maximum": 100
          },
          "opacity": {
            "title": "Opacity",
            "default": 100,
            "type": "number",
            "minimum": 1,
            "maximum": 100
          },
          "mode": {
            "title": "Mode",
            "default": "erase",
            "type": "string",
            "enum": [
              "erase",
              "restore"
            ]
          }
        },
        "required": [
          "points"
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
