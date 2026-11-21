# Mask: API reference

Modulates an image's opacity by the luminance (or alpha) of a mask

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/mask` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `image` (Single image) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image whose opacity is modulated. |
| `mask` (Single image) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Mask**<br />Mask: its luminance (or alpha) sets the image's opacity, white = visible, black = transparent. |

## Settings

### Mask

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `source` | `string` | `"luminance"` | `luminance` Luminance : Use the mask's luminance.<br />`alpha` Alpha : Use the mask's alpha. | **Mask channel**<br />Mask channel used to modulate the image's opacity. |
| `fit` | `string` | `"native"` | `native` Native (actual size)<br />`contain` Contain (ratio preserved) : Adjusts the mask to fit within the image.<br />`cover` Cover (ratio preserved) : Adjusts the mask to cover the entire image.<br />`stretch` Stretch (distorts) : Stretches the mask to fill the available space. | **Adjustment**<br />Adjustment of the mask onto the image. |
| `anchor` | `string`<br />*Anchor* | `"center"` | [grid below](#anchor-anchor) | **Position**<br />Position of the mask onto the image.<br />*Anchor* : Point of a 3 × 3 grid, from the top-left to the bottom-right corner. |
| `offsetX` | `number` | `0` | min -100 % · max 100 % · step 0.1 | **X**<br />Horizontal offset of the mask, in % of the image width. |
| `offsetY` | `number` | `0` | min -100 % · max 100 % · step 0.1 | **Y**<br />Vertical offset of the mask, in % of the image height. |
| `invert` | `boolean` | `false` |  | **Invert the mask**<br />Invert the mask. |

<a name="anchor-anchor"></a>

**Positions of `anchor`**

| | Left | Center | Right |
| --- | --- | --- | --- |
| **Top** | `top-left`<br />Top left | `top`<br />Top | `top-right`<br />Top right |
| **Middle** | `left`<br />Left | **`center`**<br />**Center** | `right`<br />Right |
| **Bottom** | `bottom-left`<br />Bottom left | `bottom`<br />Bottom | `bottom-right`<br />Bottom right |

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
curl -X POST https://api.pixlub.com/v1/modules/mask \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F image=@image.png \
  -F mask=@mask.png \
  -F 'params={"source":"luminance","fit":"native","anchor":"center"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('image', await openAsBlob('image.png'), 'image.png')
form.append('mask', await openAsBlob('mask.png'), 'mask.png')
form.append('params', JSON.stringify({"source":"luminance","fit":"native","anchor":"center"}))

const res = await fetch('https://api.pixlub.com/v1/modules/mask', {
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
    "https://api.pixlub.com/v1/modules/mask",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("image", open("image.png", "rb")), ("mask", open("mask.png", "rb"))],
    data={"params": json.dumps({"source": "luminance", "fit": "native", "anchor": "center"})},
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
result = client.tools.run("mask", inputs={"image": "image.png", "mask": "mask.png"}, params={"source": "luminance", "fit": "native", "anchor": "center"})
result.save(f"mask{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "mask", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "image": pixlub.FromPath("image.png"),
        "mask": pixlub.FromPath("mask.png"),
    },
    Params: map[string]any{"source": "luminance", "fit": "native", "anchor": "center"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("mask"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image whose opacity follows the mask. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "mask",
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

`GET /v1/modules/mask/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "source": {
      "title": "Mask channel",
      "default": "luminance",
      "type": "string",
      "enum": [
        "luminance",
        "alpha"
      ]
    },
    "fit": {
      "title": "Adjustment",
      "default": "native",
      "type": "string",
      "enum": [
        "native",
        "contain",
        "cover",
        "stretch"
      ]
    },
    "anchor": {
      "title": "Position",
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
    },
    "offsetX": {
      "title": "X",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "offsetY": {
      "title": "Y",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "invert": {
      "title": "Invert the mask",
      "default": false,
      "type": "boolean"
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
