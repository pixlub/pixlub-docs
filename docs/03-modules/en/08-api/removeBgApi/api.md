# Remove background: API reference

Detects the subject with AI (our services) and makes everything else transparent, whatever the background.

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/removeBgApi` | 10 credits per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `image` (Single image) | yes | `PNG`, `JPEG`, `WebP`, `GIF` | **Image**<br />Image sent to the server, whose subject is detected and background made transparent. |

## Settings

This module has no settings.

## Examples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/removeBgApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F image=@image.png \
  -F 'params={}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('image', await openAsBlob('image.png'), 'image.png')
form.append('params', JSON.stringify({}))

const res = await fetch('https://api.pixlub.com/v1/modules/removeBgApi', {
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
    "https://api.pixlub.com/v1/modules/removeBgApi",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("image", open("image.png", "rb"))],
    data={"params": json.dumps({})},
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
result = client.tools.run("removeBgApi", inputs={"image": "image.png"})
result.save(f"removeBgApi{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "removeBgApi", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "image": pixlub.FromPath("image.png"),
    },
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("removeBgApi"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `WebP` | **Image(s)**<br />Cut-out image on a transparent background, as lossless WebP. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "removeBgApi",
  "outputs": [
    {
      "key": "out",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.webp?exp=1767268800&sig=…",
      "content_type": "image/webp",
      "bytes": 184203
    }
  ],
  "expires_at": "2026-01-01T12:00:00Z",
  "credits": {
    "cost": 10,
    "balance": 190
  }
}
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

`GET /v1/modules/removeBgApi/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {}
}
```

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
