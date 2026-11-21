# Palette from image: API reference

Extracts the dominant colors of an image (median cut)

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/paletteFromImage` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (One image or several) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image whose dominant colors are extracted. |

## Settings

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `count` | `number` | `6` | min 2 · max 32 · step 1 | **Number of colors**<br />Number of colors extracted from the image. |
| `sortBy` | `string` | `"luminance"` | `luminance` Brightness : Sort by brightness.<br />`hue` Hue : Sort by hue.<br />`frequency` Frequency : Sort by frequency. | **Sort by**<br />Sorting criterion for the extracted colors. |

## Examples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/paletteFromImage \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"count":6,"sortBy":"luminance"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"count":6,"sortBy":"luminance"}))

const res = await fetch('https://api.pixlub.com/v1/modules/paletteFromImage', {
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
    "https://api.pixlub.com/v1/modules/paletteFromImage",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"count": 6, "sortBy": "luminance"})},
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
result = client.tools.run("paletteFromImage", image="photo.png", params={"count": 6, "sortBy": "luminance"})
result.save(f"paletteFromImage{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "paletteFromImage", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"count": 6, "sortBy": "luminance"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("paletteFromImage"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

### 1 file

> **1 file** : A single image in `in`.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Palette**<br />Dominant colors, as color swatches.<br />A single image sent: the file keeps the `out` key. |

### Several files

> **Several files** : Several images in `in`, up to 64: their number comes from the files sent, you do not send it.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG` | **Palette**<br />Dominant colors, as color swatches.<br />Several images sent in `in`: one file per image, under the keys `out#0`, `out#1`…, in upload order. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "paletteFromImage",
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

`GET /v1/modules/paletteFromImage/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "count": {
      "title": "Number of colors",
      "default": 6,
      "type": "number",
      "minimum": 2,
      "maximum": 32,
      "multipleOf": 1
    },
    "sortBy": {
      "title": "Sort by",
      "default": "luminance",
      "type": "string",
      "enum": [
        "luminance",
        "hue",
        "frequency"
      ]
    }
  }
}
```

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
