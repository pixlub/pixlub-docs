# Solid: API reference

Generates a shape filled with a solid color or a gradient

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/solid` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `background` (Single image) | no | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Background**<br />Optional image placed under the shape; when connected, it also sets the size of the result. |
| `fill` (Single image) | no | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Media**<br />Optional image seen through the shape, instead of its colour; the outline stays on top. |

## Settings

### Shape

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `shape` | `string` | `"rectangle"` | `rectangle` Rectangle<br />`circle` Circle<br />`ellipse` Ellipse<br />`ring` Ring<br />`triangle` Triangle<br />`diamond` Diamond<br />`polygon` Polygon<br />`star` Star | **Shape**<br />Shape to generate. |

### Color

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `color` | [`Color | ColorGradient`](#type-colorgradient)<br />*Color or gradient* | `"#4c9caf"` |  | **Color**<br />Solid color or gradient of the shape.<br />*Color or gradient* : A CSS color (`"#ff8800"`) for a flat fill, or a `ColorGradient` object for a gradient.<br />Color \| ColorGradient structure and example : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |
| `innerFill` | `number` | `100` | min 0 % · max 100 % · step 1 | **Inner filling**<br />The edge of the shape that is attenuated from the center. |

### Background

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `backgroundOpacity` | `number` | `100` | min 0 % · max 100 % · step 1 | **Opacity**<br />Opacity of the image connected to the Background input, painted under the shape. |

### Media in the shape

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `fillFit` | `string` | `"cover"` | `cover` Fill : The media covers the whole shape, cropped if needed.<br />`contain` Whole : The whole media fits in the shape; its colour shows around it. | **Fit**<br />How the media connected to the Media input fits the shape. |
| `fillScale` | `number` | `100` | min 10 % · max 1000 % · step 0.1 | **Scale**<br />Scale of the media once fitted; 100% = fitted. |
| `fillX` | `number` | `0` | min -100 % · max 100 % · step 0.1 | **Offset X**<br />Horizontal shift of the media, as a share of half the shape width. |
| `fillY` | `number` | `0` | min -100 % · max 100 % · step 0.1 | **Offset Y**<br />Vertical shift of the media, as a share of half the shape height. |

### Outline

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `strokeWidth` | `number` | `0` | min 0 px · max 200 px · step 1 | **Thickness**<br />Thickness of the shape outline. |
| `strokeColor` | `Color`<br />*Solid color* | `"#1c2535"` |  | **Color**<br />Color of the shape outline.<br />*Solid color* : CSS color: `#rrggbb`, `#rrggbbaa`, `rgb()` or `hsl()`. |

### Rotation

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `rotation` | `number` | `0` | min -180 ° · max 180 ° | **Angle**<br />Rotation angle of the shape. |

### Dimensions

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `width` | `number` | `512` | min 1 px · max 8000 px · step 1 | **Width**<br />Zone width. Ignored when an image is connected to the Background input: the zone then takes its dimensions. |
| `height` | `number` | `512` | min 1 px · max 8000 px · step 1 | **Height**<br />Zone height. Ignored when an image is connected to the Background input: the zone then takes its dimensions. |
| `scale` | `number` | `100` | min 1 % · max 400 % · step 1 | **Scale**<br />Scale of the shape relative to the zone width. |
| `relativeWidth` | `number` | `100` | min 1 % · max 100 % · step 1 | **Relative width**<br />Width of the shape relative to the zone width. |

### Position

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `offsetX` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset X**<br />Horizontal shift of the shape from the center. |
| `offsetY` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset Y**<br />Vertical shift of the shape from the center. |

### Corners

> These settings only count when `shape` = `rectangle` (Rectangle).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `cornerRadius` | `number` | `0` | min 0 % · max 100 % · step 1 | **Roundness**<br />Corner roundness, as a share of half the shorter side: 100% makes a pill. |

### Ring

> These settings only count when `shape` = `ring` (Ring).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `ringThickness` | `number` | `40` | min 1 % · max 99 % · step 1 | **Thickness**<br />Thickness of the ring. |

### Polygon

> These settings only count when `shape` = `polygon` (Polygon).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `sides` | `number` | `6` | min 3 · max 12 · step 1 | **Sides**<br />Number of sides of the polygon. |

### Star

> These settings only count when `shape` = `star` (Star).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `starPoints` | `number` | `5` | min 3 · max 12 · step 1 | **Branches**<br />Number of points of the star. |
| `innerRatio` | `number` | `50` | min 5 % · max 95 % · step 1 | **Inset**<br />Depth of the star inset, as a share of the outer radius. |

## Examples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/solid \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F background=@background.png \
  -F 'params={"shape":"rectangle","color":"#4c9caf","innerFill":100}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('background', await openAsBlob('background.png'), 'background.png')
form.append('params', JSON.stringify({"shape":"rectangle","color":"#4c9caf","innerFill":100}))

const res = await fetch('https://api.pixlub.com/v1/modules/solid', {
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
    "https://api.pixlub.com/v1/modules/solid",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("background", open("background.png", "rb"))],
    data={"params": json.dumps({"shape": "rectangle", "color": "#4c9caf", "innerFill": 100})},
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
result = client.tools.run("solid", inputs={"background": "background.png"}, params={"shape": "rectangle", "color": "#4c9caf", "innerFill": 100})
result.save(f"solid{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "solid", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "background": pixlub.FromPath("background.png"),
    },
    Params: map[string]any{"shape": "rectangle", "color": "#4c9caf", "innerFill": 100},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("solid"+result.Extension(), false)
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
  "module": "solid",
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

`GET /v1/modules/solid/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "shape": {
      "title": "Shape",
      "default": "rectangle",
      "type": "string",
      "enum": [
        "rectangle",
        "circle",
        "ellipse",
        "ring",
        "triangle",
        "diamond",
        "polygon",
        "star"
      ]
    },
    "color": {
      "title": "Color",
      "default": "#4c9caf",
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
    "innerFill": {
      "title": "Inner filling",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "backgroundOpacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "fillFit": {
      "title": "Fit",
      "default": "cover",
      "type": "string",
      "enum": [
        "cover",
        "contain"
      ]
    },
    "fillScale": {
      "title": "Scale",
      "default": 100,
      "type": "number",
      "minimum": 10,
      "maximum": 1000,
      "multipleOf": 0.1
    },
    "fillX": {
      "title": "Offset X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "fillY": {
      "title": "Offset Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "strokeWidth": {
      "title": "Thickness",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 200,
      "multipleOf": 1
    },
    "strokeColor": {
      "title": "Color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "rotation": {
      "title": "Angle",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180
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
    "scale": {
      "title": "Scale",
      "default": 100,
      "type": "number",
      "minimum": 1,
      "maximum": 400,
      "multipleOf": 1
    },
    "relativeWidth": {
      "title": "Relative width",
      "default": 100,
      "type": "number",
      "minimum": 1,
      "maximum": 100,
      "multipleOf": 1
    },
    "offsetX": {
      "title": "Offset X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "offsetY": {
      "title": "Offset Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cornerRadius": {
      "title": "Roundness",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "ringThickness": {
      "title": "Thickness",
      "default": 40,
      "type": "number",
      "minimum": 1,
      "maximum": 99,
      "multipleOf": 1
    },
    "sides": {
      "title": "Sides",
      "default": 6,
      "type": "number",
      "minimum": 3,
      "maximum": 12,
      "multipleOf": 1
    },
    "starPoints": {
      "title": "Branches",
      "default": 5,
      "type": "number",
      "minimum": 3,
      "maximum": 12,
      "multipleOf": 1
    },
    "innerRatio": {
      "title": "Inset",
      "default": 50,
      "type": "number",
      "minimum": 5,
      "maximum": 95,
      "multipleOf": 1
    }
  }
}
```

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
