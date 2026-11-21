# Sprite sheet: API reference

Assembles several images into a grid (flipbook, VFX atlas)

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/spriteSheet` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `f1` (Image or batch) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image 1**<br />Image (or batch) placed in cell 1 of the grid.<br />Send one image, or a batch by repeating the field once per image: up to 8 images per call. |

## Settings

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `columns` | `number` | `0` | min 0 · max 16 · step 1 | **Columns**<br />Number of columns in the grid (0 = auto). |
| `padding` | `number` | `0` | min 0 px · max 200 px · step 1 | **Spacing**<br />Spacing between the images in the grid. |

## Examples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/spriteSheet \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F f1=@f1-1.png \
  -F f1=@f1-2.png \
  -F 'params={"columns":0,"padding":0}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('f1', await openAsBlob('f1-1.png'), 'f1-1.png')
form.append('f1', await openAsBlob('f1-2.png'), 'f1-2.png')
form.append('params', JSON.stringify({"columns":0,"padding":0}))

const res = await fetch('https://api.pixlub.com/v1/modules/spriteSheet', {
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
    "https://api.pixlub.com/v1/modules/spriteSheet",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("f1", open("f1-1.png", "rb")), ("f1", open("f1-2.png", "rb"))],
    data={"params": json.dumps({"columns": 0, "padding": 0})},
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
result = client.tools.run("spriteSheet", inputs={"f1": "f1.png"}, params={"columns": 0, "padding": 0})
result.save(f"spriteSheet{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "spriteSheet", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "f1": pixlub.FromPath("f1.png"),
    },
    Params: map[string]any{"columns": 0, "padding": 0},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("spriteSheet"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Sheet**<br />Sheet laying out the received images in a grid. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "spriteSheet",
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

`GET /v1/modules/spriteSheet/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "columns": {
      "title": "Columns",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 16,
      "multipleOf": 1
    },
    "padding": {
      "title": "Spacing",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 200,
      "multipleOf": 1
    }
  }
}
```

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
