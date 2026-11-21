# Follow path: API reference

Moves an image along a path, from 0% to 100% of its length; the path may leave the frame

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/followPath` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (Single image) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Object that travels along the path, centered on it. |

## Settings

### Path

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `path` | [`Path`](#type-path)<br />*Path* | [JSON](#default-path) |  | **Path**<br />Draw the path, or connect a Path module to the node input: the connection then takes precedence. The result has the size of the path frame; points placed outside the frame make the object enter or leave the image.<br />*Path* : `Path` object: its `points` anchors are placed from 0 to 1 within the frame, detailed below.<br />Path structure and example : [`Path`](#type-path), [`PathPoint`](#type-pathpoint) |

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

### Travel

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `progress` | `number` | `0` | min 0 % · max 100 % · step 0.1 | **Position**<br />Where the object sits on the path: 0% at the first point, 100% at the last. Key it on the timeline to make it travel. |
| `offset` | `number` | `0` | min -1000 px · max 1000 px · step 1 | **Side offset**<br />Distance of the object to either side of the path, perpendicular to it (positive: to the right of the travel direction). |

### Orientation

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `align` | `boolean` | `true` |  | **Orient along the path**<br />The object turns to follow the path direction; its right side faces forward. |
| `upright` | `boolean` | `false` |  | **Keep upright**<br />When the path heads back left, the object is mirrored rather than turned upside down.<br />*Applies when `align` = `true`.* |
| `angle` | `number` | `0` | min -180 ° · max 180 ° · step 1 | **Rotation**<br />Rotation added to the object. |
| `scale` | `number` | `100` | min 1 % · max 800 % · step 1 | **Scale**<br />Size of the object, in % of its original size. |

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
curl -X POST https://api.pixlub.com/v1/modules/followPath \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"progress":0,"offset":0,"align":true}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"progress":0,"offset":0,"align":true}))

const res = await fetch('https://api.pixlub.com/v1/modules/followPath', {
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
    "https://api.pixlub.com/v1/modules/followPath",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"progress": 0, "offset": 0, "align": True})},
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
result = client.tools.run("followPath", image="photo.png", params={"progress": 0, "offset": 0, "align": True})
result.save(f"followPath{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "followPath", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"progress": 0, "offset": 0, "align": true},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("followPath"+result.Extension(), false)
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
  "module": "followPath",
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

`GET /v1/modules/followPath/schema`

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
    "progress": {
      "title": "Position",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "offset": {
      "title": "Side offset",
      "default": 0,
      "type": "number",
      "minimum": -1000,
      "maximum": 1000,
      "multipleOf": 1
    },
    "align": {
      "title": "Orient along the path",
      "default": true,
      "type": "boolean"
    },
    "upright": {
      "title": "Keep upright",
      "default": false,
      "type": "boolean"
    },
    "angle": {
      "title": "Rotation",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
    },
    "scale": {
      "title": "Scale",
      "default": 100,
      "type": "number",
      "minimum": 1,
      "maximum": 800,
      "multipleOf": 1
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
