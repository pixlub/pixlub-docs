# Merge: API reference

Overlays one or more images (layers) on another

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/merge` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `base` (Single image) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Base**<br />Background image the layers are placed on. |
| `overlay` (Image or batch) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Layer(s)**<br />Layer or batch of layers placed over the base, in order.<br />Send one image, or a batch by repeating the field once per image: up to 7 images per call. |

## Settings

### Placement

> **1 file** : A single image in `overlay`.

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `scale` | `number` | `100` | min 1 % · max 800 % · step 1 | **Scale**<br />Scale of the layer. |
| `rotation` | `number` | `0` | min -180 ° · max 180 ° · step 1 | **Rotation**<br />Rotation of the layer. |
| `offsetX` | `number` | `0` | min -100 % · max 100 % · step 0.1 | **X**<br />Horizontal offset of the layer from the center, in % of the base width. |
| `offsetY` | `number` | `0` | min -100 % · max 100 % · step 0.1 | **Y**<br />Vertical offset of the layer from the center, in % of the base height. |

### Layer

> **1 file** : A single image in `overlay`.

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `opacity` | `number` | `100` | min 0 % · max 100 % · step 1 | **Opacity**<br />Opacity of the layer. |
| `blendMode` | `string`<br />*Blend mode* | `"normal"` | `normal` Normal : The layer simply covers what is below.<br />`multiply` Multiply : Darkens: white disappears.<br />`screen` Screen : Lightens: black disappears.<br />`overlay` Overlay : Boosts the contrast below.<br />`darken` Darken : Keeps the darker of the two.<br />`color-burn` Color burn : Darkens and deepens colors.<br />`lighten` Lighten : Keeps the lighter of the two.<br />`color-dodge` Color dodge : Brightens up to a glow.<br />`soft-light` Soft light : Gentle contrast, like diffused light.<br />`hard-light` Hard light : Strong contrast, like a spotlight.<br />`difference` Difference : Inverts where the layer is bright.<br />`exclusion` Exclusion : Like Difference, but softer.<br />`hue` Hue : Takes only the layer's hue.<br />`saturation` Saturation : Takes only the layer's saturation.<br />`color` Color : Takes hue and saturation, keeps the lightness.<br />`luminosity` Luminosity : Takes only the layer's lightness. | **Blend mode**<br />Blend mode of the layer. |

### Composition

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `overlayOnTop` | `boolean` | `true` |  | **Layer above the base**<br />Puts the layer or layers above the base; otherwise, the base covers them. |

### Layers

> **Several files** : Several images in `overlay`, up to 7: their number comes from the files sent, you do not send it.

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `layers` | [`MergeLayer[]`](#type-mergelayer)<br />*List of objects* | `[]` |  | **Layers**<br />List of layers with their placement and blend mode.<br />*List of objects* : One item per `overlay` file, in upload order; 7 at most. List of `MergeLayer` objects, detailed below; an omitted member keeps its default value.<br />MergeLayer[] structure and example : [`MergeLayer`](#type-mergelayer) |

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
curl -X POST https://api.pixlub.com/v1/modules/merge \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F base=@base.png \
  -F overlay=@overlay-1.png \
  -F overlay=@overlay-2.png \
  -F 'params={"layers":[{"scale":60,"offsetX":-25,"offsetY":0},{"scale":40,"rotation":15,"offsetX":25,"opacity":80,"blendMode":"multiply"}],"overlayOnTop":true}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('base', await openAsBlob('base.png'), 'base.png')
form.append('overlay', await openAsBlob('overlay-1.png'), 'overlay-1.png')
form.append('overlay', await openAsBlob('overlay-2.png'), 'overlay-2.png')
form.append('params', JSON.stringify({"layers":[{"scale":60,"offsetX":-25,"offsetY":0},{"scale":40,"rotation":15,"offsetX":25,"opacity":80,"blendMode":"multiply"}],"overlayOnTop":true}))

const res = await fetch('https://api.pixlub.com/v1/modules/merge', {
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
    "https://api.pixlub.com/v1/modules/merge",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("base", open("base.png", "rb")), ("overlay", open("overlay-1.png", "rb")), ("overlay", open("overlay-2.png", "rb"))],
    data={"params": json.dumps({"layers": [{"scale": 60, "offsetX": -25, "offsetY": 0}, {"scale": 40, "rotation": 15, "offsetX": 25, "opacity": 80, "blendMode": "multiply"}], "overlayOnTop": True})},
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
result = client.tools.run("merge", inputs={"base": "base.png", "overlay": "overlay.png"}, params={"layers": [{"scale": 60, "offsetX": -25, "offsetY": 0}, {"scale": 40, "rotation": 15, "offsetX": 25, "opacity": 80, "blendMode": "multiply"}], "overlayOnTop": True})
result.save(f"merge{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "merge", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "base": pixlub.FromPath("base.png"),
        "overlay": pixlub.FromPath("overlay.png"),
    },
    Params: map[string]any{"layers": []any{map[string]any{"scale": 60, "offsetX": -25, "offsetY": 0}, map[string]any{"scale": 40, "rotation": 15, "offsetX": 25, "opacity": 80, "blendMode": "multiply"}}, "overlayOnTop": true},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("merge"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Base and layers merged into one image. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "merge",
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

## Types

The structured values of the settings, detailed like classes: each member with its type, then an example.

**MergeLayer[] example**

```json
[
  {
    "scale": 60,
    "offsetX": -25,
    "offsetY": 0
  },
  {
    "scale": 40,
    "rotation": 15,
    "offsetX": 25,
    "opacity": 80,
    "blendMode": "multiply"
  }
]
```

<a name="type-mergelayer"></a>

### MergeLayer

*Object*. Placement and look of a layer, put at the center of the base then offset.

| Member | Type | Description |
| --- | --- | --- |
| `scale` | `number` | *optional* · Scale of the layer. From 1 to 800 %. `100` by default. |
| `rotation` | `number` | *optional* · Rotation of the layer. From -180 to 180 °. `0` by default. |
| `offsetX` | `number` | *optional* · Horizontal offset of the layer from the center, in % of the base width. From -100 to 100 %. `0` by default. |
| `offsetY` | `number` | *optional* · Vertical offset of the layer from the center, in % of the base height. From -100 to 100 %. `0` by default. |
| `opacity` | `number` | *optional* · Opacity of the layer. From 0 to 100 %. `100` by default. |
| `blendMode` | `string` | *optional* · Blend mode of the layer. `"normal"` by default.<br />`normal` Normal : The layer simply covers what is below.<br />`multiply` Multiply : Darkens: white disappears.<br />`screen` Screen : Lightens: black disappears.<br />`overlay` Overlay : Boosts the contrast below.<br />`darken` Darken : Keeps the darker of the two.<br />`color-burn` Color burn : Darkens and deepens colors.<br />`lighten` Lighten : Keeps the lighter of the two.<br />`color-dodge` Color dodge : Brightens up to a glow.<br />`soft-light` Soft light : Gentle contrast, like diffused light.<br />`hard-light` Hard light : Strong contrast, like a spotlight.<br />`difference` Difference : Inverts where the layer is bright.<br />`exclusion` Exclusion : Like Difference, but softer.<br />`hue` Hue : Takes only the layer's hue.<br />`saturation` Saturation : Takes only the layer's saturation.<br />`color` Color : Takes hue and saturation, keeps the lightness.<br />`luminosity` Luminosity : Takes only the layer's lightness. |

**Example**

```json
{
  "scale": 60,
  "offsetX": -25,
  "offsetY": 0
}
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

`GET /v1/modules/merge/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "scale": {
      "title": "Scale",
      "default": 100,
      "type": "number",
      "minimum": 1,
      "maximum": 800,
      "multipleOf": 1
    },
    "rotation": {
      "title": "Rotation",
      "default": 0,
      "type": "number",
      "minimum": -180,
      "maximum": 180,
      "multipleOf": 1
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
    "opacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
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
    "overlayOnTop": {
      "title": "Layer above the base",
      "default": true,
      "type": "boolean"
    },
    "layers": {
      "title": "Layers",
      "default": [],
      "type": "array",
      "items": {
        "type": "object",
        "additionalProperties": false,
        "properties": {
          "scale": {
            "title": "Scale",
            "default": 100,
            "type": "number",
            "minimum": 1,
            "maximum": 800,
            "multipleOf": 1
          },
          "rotation": {
            "title": "Rotation",
            "default": 0,
            "type": "number",
            "minimum": -180,
            "maximum": 180,
            "multipleOf": 1
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
          "opacity": {
            "title": "Opacity",
            "default": 100,
            "type": "number",
            "minimum": 0,
            "maximum": 100,
            "multipleOf": 1
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
          }
        }
      },
      "maxItems": 16
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
