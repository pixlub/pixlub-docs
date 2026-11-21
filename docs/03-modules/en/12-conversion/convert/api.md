# Conversion: API reference

Converts images, animations, videos and sounds to any export format: PNG, JPG, WebP, GIF, MP4, WebM, MP3, FLAC, WAV, PDF…

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/convert` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (One image or several) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image(s) to convert to the chosen format. |

## Settings

### Output format

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `format` | `string` | `"png"` | `png` PNG<br />`jpg` JPG<br />`webp` WebP | **Format**<br />Output format of the images. |

### Quality

> These settings only count when `format` = `jpg` (JPG) or `webp` (WebP).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `quality` | `number` | `90` | min 1 % · max 100 % · step 1 | **Quality**<br />Quality of the compressed image. |

## Examples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/convert \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"format":"png"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"format":"png"}))

const res = await fetch('https://api.pixlub.com/v1/modules/convert', {
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
    "https://api.pixlub.com/v1/modules/convert",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"format": "png"})},
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
result = client.tools.run("convert", image="photo.png", params={"format": "png"})
result.save(f"convert{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "convert", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"format": "png"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("convert"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

### 1 file

> **1 file** : A single image in `in`.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG`, `JPEG`, `WebP` | **Image(s)**<br />Converted image, in the format chosen by `format`.<br />A single image sent: the file keeps the `out` key.<br />The format follows the `format` setting. |

### Several files

> **Several files** : Several images in `in`, up to 64: their number comes from the files sent, you do not send it.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG`, `JPEG`, `WebP` | **Image(s)**<br />Converted image, in the format chosen by `format`.<br />Several images sent in `in`: one file per image, under the keys `out#0`, `out#1`…, in upload order.<br />The format follows the `format` setting. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "convert",
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

`GET /v1/modules/convert/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "format": {
      "title": "Format",
      "default": "png",
      "type": "string",
      "enum": [
        "png",
        "jpg",
        "webp"
      ]
    },
    "quality": {
      "title": "Quality",
      "default": 90,
      "type": "number",
      "minimum": 1,
      "maximum": 100,
      "multipleOf": 1
    }
  }
}
```

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
