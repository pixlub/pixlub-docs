# Face blur: API reference

Blurs hand-drawn zones, or detects faces via AI (our services). Zones can be edited in the preview: create, move, resize, delete.

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/faceBlurApi` | 10 credits per file when `mode` is `auto`; 1 credit per file with any other `mode` value |

> This module only calls the remote service when mode is "auto". With any other setting, the API computes it itself, at the price of a standard module.

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `image` (Single image) | yes | `PNG`, `JPEG`, `WebP` | **Image**<br />Image whose zones are blurred. In automatic mode, it is sent to the server to detect the faces. |

## Settings

### Detection

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `mode` | `string` | `"manual"` | `manual` Manual : You draw the zones to blur.<br />`auto` Automatic : Our services detect the faces. | **Mode**<br />Mode of detection of the zones to blur. |

### Blur

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `radius` | `number` | `18` | min 1 px · max 60 px | **Intensity**<br />Intensity of the blur applied to the zones. |

### Zones

> These settings only count when `mode` = `manual` (Manual).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `zones` | [`BlurZone[]`](#type-blurzone)<br />*List of objects* | `[]` |  | **Zones**<br />List of zones to blur.<br />*List of objects* : List of `BlurZone` objects, detailed below; an omitted member keeps its default value.<br />BlurZone[] structure and example : [`BlurZone`](#type-blurzone) |

## Examples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/faceBlurApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F image=@image.png \
  -F 'params={"zones":[{"x":0.42,"y":0.18,"w":0.16,"h":0.24,"shape":"circle"},{"x":0.05,"y":0.8,"w":0.3,"h":0.12}],"mode":"manual","radius":18}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('image', await openAsBlob('image.png'), 'image.png')
form.append('params', JSON.stringify({"zones":[{"x":0.42,"y":0.18,"w":0.16,"h":0.24,"shape":"circle"},{"x":0.05,"y":0.8,"w":0.3,"h":0.12}],"mode":"manual","radius":18}))

const res = await fetch('https://api.pixlub.com/v1/modules/faceBlurApi', {
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
    "https://api.pixlub.com/v1/modules/faceBlurApi",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("image", open("image.png", "rb"))],
    data={"params": json.dumps({"zones": [{"x": 0.42, "y": 0.18, "w": 0.16, "h": 0.24, "shape": "circle"}, {"x": 0.05, "y": 0.8, "w": 0.3, "h": 0.12}], "mode": "manual", "radius": 18})},
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
result = client.tools.run("faceBlurApi", inputs={"image": "image.png"}, params={"zones": [{"x": 0.42, "y": 0.18, "w": 0.16, "h": 0.24, "shape": "circle"}, {"x": 0.05, "y": 0.8, "w": 0.3, "h": 0.12}], "mode": "manual", "radius": 18})
result.save(f"faceBlurApi{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "faceBlurApi", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "image": pixlub.FromPath("image.png"),
    },
    Params: map[string]any{"zones": []any{map[string]any{"x": 0.42, "y": 0.18, "w": 0.16, "h": 0.24, "shape": "circle"}, map[string]any{"x": 0.05, "y": 0.8, "w": 0.3, "h": 0.12}}, "mode": "manual", "radius": 18},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("faceBlurApi"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image produced by the module. |
| `data` | [`FaceDetection`](#type-facedetection) | `JSON` | **Data**<br />Data detected by the remote service, as JSON.<br />File content: a `FaceDetection` object.<br />Returned only when `mode` = `auto`. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "faceBlurApi",
  "outputs": [
    {
      "key": "out",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.png?exp=1767268800&sig=…",
      "content_type": "image/png",
      "bytes": 184203
    },
    {
      "key": "data",
      "name": "data",
      "url": "https://files.pixlub.com/r/5f0c2a91-8d3e-4b7a-a1c4-6e2d9b0f3a58_result.json?exp=1767268800&sig=…",
      "content_type": "application/json",
      "bytes": 82
    }
  ],
  "expires_at": "2026-01-01T12:00:00Z",
  "credits": {
    "cost": 10,
    "balance": 190
  }
}
```

## Types

The structured values of the settings, detailed like classes: each member with its type, then an example.

**BlurZone[] example**

```json
[
  {
    "x": 0.42,
    "y": 0.18,
    "w": 0.16,
    "h": 0.24,
    "shape": "circle"
  },
  {
    "x": 0.05,
    "y": 0.8,
    "w": 0.3,
    "h": 0.12
  }
]
```

<a name="type-blurzone"></a>

### BlurZone

*Object*. Blurred zone: a rectangle, or the ellipse it holds, placed from 0 to 1 within the image.

| Member | Type | Description |
| --- | --- | --- |
| `x` | `number` | Left edge, from 0 (left) to 1 (right) of the image. From 0 to 1. |
| `y` | `number` | Top edge, from 0 (top) to 1 (bottom) of the image. From 0 to 1. |
| `w` | `number` | Width, as a fraction of the image width. From 0 to 1. |
| `h` | `number` | Height, as a fraction of the image height. From 0 to 1. |
| `shape` | `"square" \| "circle"` | *optional* · Rectangle, or ellipse inscribed in the rectangle. `"square"` by default. |

**Example**

```json
{
  "x": 0.42,
  "y": 0.18,
  "w": 0.16,
  "h": 0.24,
  "shape": "circle"
}
```

<a name="type-facedetection"></a>

### FaceDetection

*Object*. Faces detected in the image sent, in pixels of that image.

| Member | Type | Description |
| --- | --- | --- |
| `image_width` | `integer` | Width of the analyzed image, in pixels. |
| `image_height` | `integer` | Height of the analyzed image, in pixels. |
| `faces_count` | `integer` | Number of faces found, whatever their confidence. |
| `faces` | `DetectedFace[]` | The faces found. Only those with a confidence of `0.6` or more are blurred. |

**Example**

```json
{
  "image_width": 1280,
  "image_height": 853,
  "faces_count": 1,
  "faces": [
    {
      "bbox": {
        "x": 512.4,
        "y": 188.9,
        "width": 164.2,
        "height": 211.7
      },
      "landmarks": {
        "right_eye": [
          561.3,
          268.1
        ],
        "left_eye": [
          628.8,
          266.4
        ],
        "nose_tip": [
          596.2,
          307.5
        ],
        "right_mouth": [
          567.9,
          345.2
        ],
        "left_mouth": [
          622.4,
          343.8
        ]
      },
      "confidence": 0.9731
    }
  ]
}
```

<a name="type-detectedface"></a>

### DetectedFace

*Object*. One detected face.

| Member | Type | Description |
| --- | --- | --- |
| `bbox` | `FaceBox` | Box of the face, clamped to the image. |
| `landmarks` | `FaceLandmarks` | Five face landmarks, each `[x, y]` in pixels. |
| `confidence` | `number` | Detection confidence, from 0 to 1. |

**Example**

```json
{
  "bbox": {
    "x": 512.4,
    "y": 188.9,
    "width": 164.2,
    "height": 211.7
  },
  "confidence": 0.9731
}
```

<a name="type-facebox"></a>

### FaceBox

*Object*. Rectangle in pixels, from the top-left corner of the image.

| Member | Type | Description |
| --- | --- | --- |
| `x` | `number` | Left edge. |
| `y` | `number` | Top edge. |
| `width` | `number` | Width. |
| `height` | `number` | Height. |

**Example**

```json
{
  "x": 512.4,
  "y": 188.9,
  "width": 164.2,
  "height": 211.7
}
```

<a name="type-facelandmarks"></a>

### FaceLandmarks

*Object*. Landmarks of a face, from the photographed person's point of view.

| Member | Type | Description |
| --- | --- | --- |
| `right_eye` | `[number, number]` | Right eye. |
| `left_eye` | `[number, number]` | Left eye. |
| `nose_tip` | `[number, number]` | Tip of the nose. |
| `right_mouth` | `[number, number]` | Right corner of the mouth. |
| `left_mouth` | `[number, number]` | Left corner of the mouth. |

**Example**

```json
{
  "right_eye": [
    561.3,
    268.1
  ],
  "left_eye": [
    628.8,
    266.4
  ],
  "nose_tip": [
    596.2,
    307.5
  ],
  "right_mouth": [
    567.9,
    345.2
  ],
  "left_mouth": [
    622.4,
    343.8
  ]
}
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

`GET /v1/modules/faceBlurApi/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "mode": {
      "title": "Mode",
      "default": "manual",
      "type": "string",
      "enum": [
        "manual",
        "auto"
      ]
    },
    "radius": {
      "title": "Intensity",
      "default": 18,
      "type": "number",
      "minimum": 1,
      "maximum": 60
    },
    "zones": {
      "title": "Zones",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "x": {
            "title": "X",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "y": {
            "title": "Y",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "w": {
            "title": "W",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "h": {
            "title": "H",
            "type": "number",
            "minimum": 0,
            "maximum": 1
          },
          "shape": {
            "title": "Shape",
            "default": "square",
            "type": "string",
            "enum": [
              "square",
              "circle"
            ]
          }
        },
        "required": [
          "x",
          "y",
          "w",
          "h"
        ]
      }
    }
  }
}
```

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
