# Bend along path: API reference

Warps an image along a path (ribbon / curved trail)

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/warpPath` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (Single image) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image bent along the path: its width follows the path, its height becomes the ribbon thickness. |

## Settings

### Path

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `path` | [`Path`](#type-path)<br />*Path* | [JSON](#default-path) |  | **Path**<br />Draw the path, or connect a Path module to the node input: the connection then takes precedence. The result has the size of the path frame.<br />*Path* : `Path` object: its `points` anchors are placed from 0 to 1 within the frame, detailed below.<br />Path structure and example : [`Path`](#type-path), [`PathPoint`](#type-pathpoint) |

<a name="default-path"></a>

**Default value of `path`**

```json
{
  "points": [
    {
      "x": 0.12,
      "y": 0.68
    },
    {
      "x": 0.5,
      "y": 0.3
    },
    {
      "x": 0.88,
      "y": 0.66
    }
  ],
  "closed": false,
  "smooth": true,
  "rounding": 0.5,
  "curve": "arc",
  "w": 512,
  "h": 512
}
```

### Ribbon

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `thickness` | `number` | `100` | min 10 % · max 200 % · step 1 | **Thickness**<br />At 100%, the image keeps its proportions along the path, without exceeding what the tightest turn allows. Lower thins the ribbon; higher thickens it, at the risk of pinching inside the turns. |
| `side` | `string` | `"center"` | `left` Left : The ribbon runs along the left of the path, in drawing direction.<br />`center` Centered : The path runs through the middle of the ribbon.<br />`right` Right : The ribbon runs along the right of the path. | **Position**<br />Where the ribbon sits relative to the path. The top of the image is always on the left side. |
| `fill` | `string` | `"stretch"` | `stretch` Stretch : The image stretches once over the whole path.<br />`repeat` Repeat : The image keeps its proportions and repeats along the path. | **Fill**<br />How the image covers the length of the path. |

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
curl -X POST https://api.pixlub.com/v1/modules/warpPath \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"thickness":100,"side":"center","fill":"stretch"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"thickness":100,"side":"center","fill":"stretch"}))

const res = await fetch('https://api.pixlub.com/v1/modules/warpPath', {
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
    "https://api.pixlub.com/v1/modules/warpPath",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"thickness": 100, "side": "center", "fill": "stretch"})},
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
result = client.tools.run("warpPath", image="photo.png", params={"thickness": 100, "side": "center", "fill": "stretch"})
result.save(f"warpPath{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "warpPath", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"thickness": 100, "side": "center", "fill": "stretch"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("warpPath"+result.Extension(), false)
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
  "module": "warpPath",
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

<a name="type-path"></a>

### Path

*Object*. Bézier path running through anchors, inside a reference frame.

| Member | Type | Description |
| --- | --- | --- |
| `points` | `PathPoint[]` | Anchors of the path, in order; at least two. |
| `closed` | `boolean` | *optional* · Joins the last anchor to the first. `false` by default. |
| `smooth` | `boolean` | *optional* · Rounds the path between `auto` anchors; `false` joins them with straight lines. `true` by default. |
| `rounding` | `number` | *optional* · Rounding strength, from 0 to 1. `0.5` by default. |
| `curve` | `"arc" \| "spline"` | *optional* · Curvature of `auto` anchors: `arc` as circular arcs (anchors placed in a ring give an exact circle), `spline` as a Catmull-Rom curve. `spline` by default. |
| `w` | `number` | *optional* · Width of the reference frame, in pixels. With `h`, the path keeps its proportions and is centered in the image; without them, it spans the whole image. |
| `h` | `number` | *optional* · Height of the reference frame, in pixels. |

**Example**

```json
{
  "points": [
    {
      "x": 0.1,
      "y": 0.7
    },
    {
      "x": 0.5,
      "y": 0.3
    },
    {
      "x": 0.9,
      "y": 0.7
    }
  ],
  "closed": false,
  "smooth": true
}
```

<a name="type-pathpoint"></a>

### PathPoint

*Object*. Anchor of a path.

| Member | Type | Description |
| --- | --- | --- |
| `x` | `number` | Horizontal position, from 0 (left) to 1 (right) of the frame. |
| `y` | `number` | Vertical position, from 0 (top) to 1 (bottom) of the frame. |
| `k` | `"auto" \| "corner" \| "free"` | *optional* · Anchor type: `auto` rounded, `corner` sharp angle, `free` with the given `i` and `o` handles. `auto` by default. |
| `i` | `{ x, y }` | *optional* · Incoming handle (`free` anchor), relative to the anchor, as a fraction of the frame. |
| `o` | `{ x, y }` | *optional* · Outgoing handle (`free` anchor), relative to the anchor. |
| `w` | `number` | *optional* · Stroke width at this anchor, in % of the set width. `100` by default. |

**Example**

```json
{
  "x": 0.5,
  "y": 0.3
}
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

`GET /v1/modules/warpPath/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "path": {
      "title": "Path",
      "default": {
        "points": [
          {
            "x": 0.12,
            "y": 0.68
          },
          {
            "x": 0.5,
            "y": 0.3
          },
          {
            "x": 0.88,
            "y": 0.66
          }
        ],
        "closed": false,
        "smooth": true,
        "rounding": 0.5,
        "curve": "arc",
        "w": 512,
        "h": 512
      },
      "type": "object",
      "required": [
        "points"
      ],
      "properties": {
        "points": {
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
              "k": {
                "type": "string",
                "enum": [
                  "auto",
                  "corner",
                  "free"
                ]
              },
              "i": {
                "type": "object",
                "required": [
                  "x",
                  "y"
                ],
                "properties": {
                  "x": {
                    "type": "number"
                  },
                  "y": {
                    "type": "number"
                  }
                }
              },
              "o": {
                "type": "object",
                "required": [
                  "x",
                  "y"
                ],
                "properties": {
                  "x": {
                    "type": "number"
                  },
                  "y": {
                    "type": "number"
                  }
                }
              },
              "w": {
                "type": "number",
                "minimum": 0
              }
            }
          },
          "minItems": 2
        },
        "closed": {
          "type": "boolean"
        },
        "smooth": {
          "type": "boolean"
        },
        "rounding": {
          "type": "number",
          "minimum": 0,
          "maximum": 1
        },
        "curve": {
          "type": "string",
          "enum": [
            "arc",
            "spline"
          ]
        },
        "w": {
          "type": "number",
          "minimum": 1
        },
        "h": {
          "type": "number",
          "minimum": 1
        }
      }
    },
    "thickness": {
      "title": "Thickness",
      "default": 100,
      "type": "number",
      "minimum": 10,
      "maximum": 200,
      "multipleOf": 1
    },
    "side": {
      "title": "Position",
      "default": "center",
      "type": "string",
      "enum": [
        "left",
        "center",
        "right"
      ]
    },
    "fill": {
      "title": "Fill",
      "default": "stretch",
      "type": "string",
      "enum": [
        "stretch",
        "repeat"
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
