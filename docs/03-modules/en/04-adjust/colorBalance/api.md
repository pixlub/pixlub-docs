# Color balance: API reference

Adjusts hues per tonal range (highlights, midtones, shadows), maskable

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/colorBalance` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (Single image) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Image whose tints are adjusted. |
| `mask` (Single image) | no | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Mask**<br />Optional mask: the adjustment follows its lightness, white = full effect, black = none. When missing, the whole image is adjusted. |

## Settings

### General

#### Highlights

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `highsCR` | `number`<br />*Color axis* | `0` | min -100 · max 100 | **Cyan ↔ Red**<br />*Color axis* : From -100 (first hue) to 100 (second hue); 0 changes nothing. |
| `highsMG` | `number`<br />*Color axis* | `0` | min -100 · max 100 | **Magenta ↔ Green**<br />*Color axis* : From -100 (first hue) to 100 (second hue); 0 changes nothing. |
| `highsYB` | `number`<br />*Color axis* | `0` | min -100 · max 100 | **Yellow ↔ Blue**<br />*Color axis* : From -100 (first hue) to 100 (second hue); 0 changes nothing. |

#### Midtones

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `midsCR` | `number`<br />*Color axis* | `0` | min -100 · max 100 | **Cyan ↔ Red**<br />*Color axis* : From -100 (first hue) to 100 (second hue); 0 changes nothing. |
| `midsMG` | `number`<br />*Color axis* | `0` | min -100 · max 100 | **Magenta ↔ Green**<br />*Color axis* : From -100 (first hue) to 100 (second hue); 0 changes nothing. |
| `midsYB` | `number`<br />*Color axis* | `0` | min -100 · max 100 | **Yellow ↔ Blue**<br />*Color axis* : From -100 (first hue) to 100 (second hue); 0 changes nothing. |

#### Shadows

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `shadowsCR` | `number`<br />*Color axis* | `0` | min -100 · max 100 | **Cyan ↔ Red**<br />*Color axis* : From -100 (first hue) to 100 (second hue); 0 changes nothing. |
| `shadowsMG` | `number`<br />*Color axis* | `0` | min -100 · max 100 | **Magenta ↔ Green**<br />*Color axis* : From -100 (first hue) to 100 (second hue); 0 changes nothing. |
| `shadowsYB` | `number`<br />*Color axis* | `0` | min -100 · max 100 | **Yellow ↔ Blue**<br />*Color axis* : From -100 (first hue) to 100 (second hue); 0 changes nothing. |

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `preserveLum` | `boolean` | `true` |  | **Preserve brightness**<br />Keeps the picture's lightness as it is: only the hue moves, never the overall brightness. |

### Blending

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blendMode` | `string`<br />*Blend mode* | `"normal"` | `normal` Normal : The layer simply covers what is below.<br />`multiply` Multiply : Darkens: white disappears.<br />`screen` Screen : Lightens: black disappears.<br />`overlay` Overlay : Boosts the contrast below.<br />`darken` Darken : Keeps the darker of the two.<br />`color-burn` Color burn : Darkens and deepens colors.<br />`lighten` Lighten : Keeps the lighter of the two.<br />`color-dodge` Color dodge : Brightens up to a glow.<br />`soft-light` Soft light : Gentle contrast, like diffused light.<br />`hard-light` Hard light : Strong contrast, like a spotlight.<br />`difference` Difference : Inverts where the layer is bright.<br />`exclusion` Exclusion : Like Difference, but softer.<br />`hue` Hue : Takes only the layer's hue.<br />`saturation` Saturation : Takes only the layer's saturation.<br />`color` Color : Takes hue and saturation, keeps the lightness.<br />`luminosity` Luminosity : Takes only the layer's lightness. | **Blend mode**<br />How the adjustment sits on the original picture. |
| `blendOpacity` | `number` | `100` | min 0 % · max 100 % · step 1 | **Opacity**<br />How much of the adjustment is applied. |

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
curl -X POST https://api.pixlub.com/v1/modules/colorBalance \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"highsCR":0,"highsMG":0,"highsYB":0}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"highsCR":0,"highsMG":0,"highsYB":0}))

const res = await fetch('https://api.pixlub.com/v1/modules/colorBalance', {
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
    "https://api.pixlub.com/v1/modules/colorBalance",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"highsCR": 0, "highsMG": 0, "highsYB": 0})},
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
result = client.tools.run("colorBalance", image="photo.png", params={"highsCR": 0, "highsMG": 0, "highsYB": 0})
result.save(f"colorBalance{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "colorBalance", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"highsCR": 0, "highsMG": 0, "highsYB": 0},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("colorBalance"+result.Extension(), false)
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
  "module": "colorBalance",
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

`GET /v1/modules/colorBalance/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "highsCR": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "highsMG": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "highsYB": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "midsCR": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "midsMG": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "midsYB": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "shadowsCR": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "shadowsMG": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "shadowsYB": {
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "default": 0
    },
    "preserveLum": {
      "title": "Preserve brightness",
      "default": true,
      "type": "boolean"
    },
    "blendMode": {
      "title": "Blend mode",
      "default": "normal",
      "type": "string",
      "enum": [
        "normal",
        "multiply",
        "screen",
        "overlay",
        "darken",
        "color-burn",
        "lighten",
        "color-dodge",
        "soft-light",
        "hard-light",
        "difference",
        "exclusion",
        "hue",
        "saturation",
        "color",
        "luminosity"
      ]
    },
    "blendOpacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
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
