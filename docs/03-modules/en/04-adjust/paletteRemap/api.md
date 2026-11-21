# Palette: recolor: API reference

Generates a recolored variant of the image for each palette color (batch)

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/paletteRemap` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (Single image) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image to recolor. |

## Settings

### Palette

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `colors` | `Color[]`<br />*List of colors* | [JSON](#default-colors) |  | **Colors**<br />Palette colors: one variant of the image per color. Ignored when a palette is connected to the Palette input.<br />*List of colors* : List of CSS colors, in order. |

<a name="default-colors"></a>

**Default value of `colors`**

```json
[
  "#264653",
  "#2a9d8f",
  "#e9c46a",
  "#f4a261",
  "#e76f51"
]
```

### General

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `preserveLum` | `boolean` | `true` |  | **Preserve brightness**<br />Keeps the picture's lightness as it is: only the hue moves, never the overall brightness. |
| `mix` | `number` | `100` | min 0 % · max 100 % | **Intensity**<br />How much recoloring is applied: 0% keeps the picture as it is, 100% recolors it completely. |

### Mapping

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `limitToBase` | `boolean` | `false` |  | **Limit to a base color**<br />Only recolors pixels close to the base color. |
| `minSaturation` | `number` | `0` | min 0 % · max 100 % | **Minimum saturation**<br />Only recolors pixels whose saturation is at least this percentage. |
| `feather` | `number` | `25` | min 0 % · max 100 % | **Softness**<br />Softens the transitions between the recolored and non-recolored areas. |

### Base color

> These settings only count when `limitToBase` = `true`.

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `baseColor` | `Color`<br />*Solid color* | `"#e76f51"` |  | **Color**<br />Base color: pixels close to this color are recolored.<br />*Solid color* : CSS color: `#rrggbb`, `#rrggbbaa`, `rgb()` or `hsl()`. |
| `hueTolerance` | `number` | `60` | min 1 ° · max 180 ° | **Hue tolerance**<br />Hue tolerance: pixels close to the base color are recolored. |

## Examples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/paletteRemap \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"preserveLum":true,"mix":100,"limitToBase":false}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"preserveLum":true,"mix":100,"limitToBase":false}))

const res = await fetch('https://api.pixlub.com/v1/modules/paletteRemap', {
  method: 'POST',
  headers: { 'X-API-Key': process.env.PIXLUB_API_KEY },
  body: form,
})
const result = await res.json()
const output = result.outputs.find((o) => o.key === 'out#0')
const image = await fetch(output.url) // lien signé, sans clé
```

### Python

```python
import json, os, requests

res = requests.post(
    "https://api.pixlub.com/v1/modules/paletteRemap",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"preserveLum": True, "mix": 100, "limitToBase": False})},
)
res.raise_for_status()
result = res.json()
output = next(o for o in result["outputs"] if o["key"] == "out#0")
print(output["url"])
```

### SDK Python

```python
import pixlub

client = pixlub.Client()  # PIXLUB_API_KEY, PIXLUB_BASE_URL
result = client.tools.run("paletteRemap", image="photo.png", params={"preserveLum": True, "mix": 100, "limitToBase": False})
result.save(f"paletteRemap{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "paletteRemap", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"preserveLum": true, "mix": 100, "limitToBase": false},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("paletteRemap"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image[]` | `PNG` | **Batch**<br />One recolored variant per palette color, in color order.<br />One file per image of the batch, under the keys `out#0`, `out#1`… |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "paletteRemap",
  "outputs": [
    {
      "key": "out#0",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.png?exp=1767268800&sig=…",
      "content_type": "image/png",
      "bytes": 184203
    },
    {
      "key": "out#1",
      "name": "image",
      "url": "https://files.pixlub.com/r/5f0c2a91-8d3e-4b7a-a1c4-6e2d9b0f3a58_result.png?exp=1767268800&sig=…",
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

`GET /v1/modules/paletteRemap/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "colors": {
      "title": "Colors",
      "default": [
        "#264653",
        "#2a9d8f",
        "#e9c46a",
        "#f4a261",
        "#e76f51"
      ],
      "type": "array",
      "items": {
        "type": "string",
        "minLength": 1
      },
      "minItems": 1,
      "maxItems": 32
    },
    "preserveLum": {
      "title": "Preserve brightness",
      "default": true,
      "type": "boolean"
    },
    "mix": {
      "title": "Intensity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "limitToBase": {
      "title": "Limit to a base color",
      "default": false,
      "type": "boolean"
    },
    "minSaturation": {
      "title": "Minimum saturation",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "feather": {
      "title": "Softness",
      "default": 25,
      "type": "number",
      "minimum": 0,
      "maximum": 100
    },
    "baseColor": {
      "title": "Color",
      "default": "#e76f51",
      "type": "string",
      "minLength": 1
    },
    "hueTolerance": {
      "title": "Hue tolerance",
      "default": 60,
      "type": "number",
      "minimum": 1,
      "maximum": 180
    }
  }
}
```

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
