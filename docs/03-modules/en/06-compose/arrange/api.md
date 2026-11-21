# Layout: API reference

Aligns several images side by side or stacked (banners, comparisons)

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/arrange` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `a1` (Image or batch) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image 1**<br />Image (or batch) placed at position 1 of the layout.<br />Send one image, or a batch by repeating the field once per image: up to 8 images per call. |

## Settings

### General

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `direction` | `string` | `"horizontal"` | `horizontal` Horizontal : Horizontal layout of the images.<br />`vertical` Vertical : Vertical layout of the images. | **Direction**<br />Direction of the layout of the images. |
| `align` | `string` | `"center"` | `start` Start : Align the images to the top of the layout.<br />`center` Center : Align the images to the center of the layout.<br />`end` End : Align the images to the bottom of the layout. | **Alignment**<br />Alignment of the images in the layout. |
| `fit` | `string` | `"none"` | `none` None : Do not adjust the images.<br />`fit` Adjust : Adjust the images to fit the layout.<br />`stretch` Stretch : Stretch the images to fill the available space. | **Adjustment**<br />Adjustment of the images in the layout. |
| `gap` | `number` | `0` | min 0 px · max 500 px · step 1 | **Spacing**<br />Spacing between the images in the layout. |

### Background

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `bgTransparent` | `boolean` | `true` |  | **Transparent** |
| `bgColor` | `Color`<br />*Solid color* | `"#ffffff"` |  | **Color**<br />*Solid color* : CSS color: `#rrggbb`, `#rrggbbaa`, `rgb()` or `hsl()`. |

## Examples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/arrange \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F a1=@a1-1.png \
  -F a1=@a1-2.png \
  -F 'params={"direction":"horizontal","align":"center","fit":"none"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('a1', await openAsBlob('a1-1.png'), 'a1-1.png')
form.append('a1', await openAsBlob('a1-2.png'), 'a1-2.png')
form.append('params', JSON.stringify({"direction":"horizontal","align":"center","fit":"none"}))

const res = await fetch('https://api.pixlub.com/v1/modules/arrange', {
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
    "https://api.pixlub.com/v1/modules/arrange",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("a1", open("a1-1.png", "rb")), ("a1", open("a1-2.png", "rb"))],
    data={"params": json.dumps({"direction": "horizontal", "align": "center", "fit": "none"})},
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
result = client.tools.run("arrange", inputs={"a1": "a1.png"}, params={"direction": "horizontal", "align": "center", "fit": "none"})
result.save(f"arrange{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "arrange", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "a1": pixlub.FromPath("a1.png"),
    },
    Params: map[string]any{"direction": "horizontal", "align": "center", "fit": "none"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("arrange"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Received images laid out on a single image. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "arrange",
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

`GET /v1/modules/arrange/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "direction": {
      "title": "Direction",
      "default": "horizontal",
      "type": "string",
      "enum": [
        "horizontal",
        "vertical"
      ]
    },
    "align": {
      "title": "Alignment",
      "default": "center",
      "type": "string",
      "enum": [
        "start",
        "center",
        "end"
      ]
    },
    "fit": {
      "title": "Adjustment",
      "default": "none",
      "type": "string",
      "enum": [
        "none",
        "fit",
        "stretch"
      ]
    },
    "gap": {
      "title": "Spacing",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 500,
      "multipleOf": 1
    },
    "bgTransparent": {
      "title": "Transparent",
      "default": true,
      "type": "boolean"
    },
    "bgColor": {
      "title": "Color",
      "default": "#ffffff",
      "type": "string",
      "minLength": 1
    }
  }
}
```

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
