# Blur: API reference

Gaussian, motion, spin or zoom blur (interactive center)

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/blur` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (One image or several) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image to blur. |

## Settings

### General

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `type` | `string` | `"gaussian"` | `gaussian` Gaussian<br />`motion` Motion<br />`radial` Rotation<br />`zoom` Zoom | **Type**<br />Blur type |

### Gaussian

> These settings only count when `type` = `gaussian` (Gaussian).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `radius` | `number` | `4` | min 0 px · max 40 px | **Radius**<br />Radius of the gaussian blur. |

### Motion

> These settings only count when `type` = `motion` (Motion).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `angle` | `number` | `0` | min -180 ° · max 180 ° | **Angle**<br />Angle of the movement direction. |
| `distance` | `number` | `24` | min 0 px · max 500 px · step 1 | **Distance**<br />Distance of the movement. |

### Rotation

> These settings only count when `type` = `radial` (Rotation).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `spin` | `number` | `15` | min 0 ° · max 90 ° | **Spin angle**<br />Spin angle of the radial blur. |

### Zoom

> These settings only count when `type` = `zoom` (Zoom).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `amount` | `number` | `30` | min 0 % · max 100 % | **Intensity**<br />Intensity of the zoom blur. |

### Center

> These settings only count when `type` = `radial` (Rotation) or `zoom` (Zoom).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `centerX` | `number` | `50` | min 0 % · max 100 % · step 0.1 | **X**<br />Horizontal position of the blur center, in % of the width |
| `centerY` | `number` | `50` | min 0 % · max 100 % · step 0.1 | **Y**<br />Vertical position of the blur center, in % of the height |

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
curl -X POST https://api.pixlub.com/v1/modules/blur \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"type":"gaussian","radius":4}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"type":"gaussian","radius":4}))

const res = await fetch('https://api.pixlub.com/v1/modules/blur', {
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
    "https://api.pixlub.com/v1/modules/blur",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"type": "gaussian", "radius": 4})},
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
result = client.tools.run("blur", image="photo.png", params={"type": "gaussian", "radius": 4})
result.save(f"blur{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "blur", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"type": "gaussian", "radius": 4},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("blur"+result.Extension(), false)
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
  "module": "blur",
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

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

`GET /v1/modules/blur/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "type": {
      "title": "Type",
      "default": "gaussian",
      "type": "string",
      "enum": [
        "gaussian",
        "motion",
        "radial",
        "zoom"
      ]
    },
    "radius": {
      "title": "Radius",
      "default": 4,
      "type": "number",
      "minimum": 0,
      "maximum": 40
    },
    "angle": {
      "title": "Angle",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180
    },
    "distance": {
      "title": "Distance",
      "default": 24,
      "type": "number",
      "minimum": 0,
      "maximum": 500,
      "multipleOf": 1
    },
    "spin": {
      "title": "Spin angle",
      "default": 15,
      "type": "number",
      "minimum": 0,
      "maximum": 90
    },
    "amount": {
      "title": "Intensity",
      "default": 30,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "centerX": {
      "title": "X",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "centerY": {
      "title": "Y",
      "default": 50,
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
