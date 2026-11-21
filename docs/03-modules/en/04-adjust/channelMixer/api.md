# Channel mixer: API reference

Rebuilds each channel from the others, in the chosen space

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/channelMixer` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (One image or several) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image whose channels are remixed. |

## Settings

### General

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `space` | `string` | `"rgb"` | `rgb` RGB<br />`gray` Gray<br />`cmyk` CMYK<br />`lab` LAB | **Space**<br />Color space in which the channels are adjusted |

### RGB space

> These settings only count when `space` = `rgb` (RGB).

#### Red output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `rgbRFromRgbR` | `number` | `100` | min -200 % · max 200 % · step 1 | **Red**<br />Share of the Red channel carried into the Red output channel. 100% copies it, a negative value subtracts it. |
| `rgbRFromRgbG` | `number` | `0` | min -200 % · max 200 % · step 1 | **Green**<br />Share of the Green channel carried into the Red output channel. 100% copies it, a negative value subtracts it. |
| `rgbRFromRgbB` | `number` | `0` | min -200 % · max 200 % · step 1 | **Blue**<br />Share of the Blue channel carried into the Red output channel. 100% copies it, a negative value subtracts it. |
| `rgbRFromRgbAlpha` | `number` | `0` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Red output channel. 100% copies it, a negative value subtracts it. |
| `offsetRgbR` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Red output channel, whatever the picture. |

#### Green output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `rgbGFromRgbR` | `number` | `0` | min -200 % · max 200 % · step 1 | **Red**<br />Share of the Red channel carried into the Green output channel. 100% copies it, a negative value subtracts it. |
| `rgbGFromRgbG` | `number` | `100` | min -200 % · max 200 % · step 1 | **Green**<br />Share of the Green channel carried into the Green output channel. 100% copies it, a negative value subtracts it. |
| `rgbGFromRgbB` | `number` | `0` | min -200 % · max 200 % · step 1 | **Blue**<br />Share of the Blue channel carried into the Green output channel. 100% copies it, a negative value subtracts it. |
| `rgbGFromRgbAlpha` | `number` | `0` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Green output channel. 100% copies it, a negative value subtracts it. |
| `offsetRgbG` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Green output channel, whatever the picture. |

#### Blue output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `rgbBFromRgbR` | `number` | `0` | min -200 % · max 200 % · step 1 | **Red**<br />Share of the Red channel carried into the Blue output channel. 100% copies it, a negative value subtracts it. |
| `rgbBFromRgbG` | `number` | `0` | min -200 % · max 200 % · step 1 | **Green**<br />Share of the Green channel carried into the Blue output channel. 100% copies it, a negative value subtracts it. |
| `rgbBFromRgbB` | `number` | `100` | min -200 % · max 200 % · step 1 | **Blue**<br />Share of the Blue channel carried into the Blue output channel. 100% copies it, a negative value subtracts it. |
| `rgbBFromRgbAlpha` | `number` | `0` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Blue output channel. 100% copies it, a negative value subtracts it. |
| `offsetRgbB` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Blue output channel, whatever the picture. |

#### Alpha output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `rgbAlphaFromRgbR` | `number` | `0` | min -200 % · max 200 % · step 1 | **Red**<br />Share of the Red channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `rgbAlphaFromRgbG` | `number` | `0` | min -200 % · max 200 % · step 1 | **Green**<br />Share of the Green channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `rgbAlphaFromRgbB` | `number` | `0` | min -200 % · max 200 % · step 1 | **Blue**<br />Share of the Blue channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `rgbAlphaFromRgbAlpha` | `number` | `100` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `offsetRgbAlpha` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Alpha output channel, whatever the picture. |

### Gray space

> These settings only count when `space` = `gray` (Gray).

#### Intensity output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `grayIFromGrayI` | `number` | `100` | min -200 % · max 200 % · step 1 | **Intensity**<br />Share of the Intensity channel carried into the Intensity output channel. 100% copies it, a negative value subtracts it. |
| `grayIFromGrayAlpha` | `number` | `0` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Intensity output channel. 100% copies it, a negative value subtracts it. |
| `offsetGrayI` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Intensity output channel, whatever the picture. |

#### Alpha output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `grayAlphaFromGrayI` | `number` | `0` | min -200 % · max 200 % · step 1 | **Intensity**<br />Share of the Intensity channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `grayAlphaFromGrayAlpha` | `number` | `100` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `offsetGrayAlpha` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Alpha output channel, whatever the picture. |

### CMYK space

> These settings only count when `space` = `cmyk` (CMYK).

#### Cyan output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `cmykCFromCmykC` | `number` | `100` | min -200 % · max 200 % · step 1 | **Cyan**<br />Share of the Cyan channel carried into the Cyan output channel. 100% copies it, a negative value subtracts it. |
| `cmykCFromCmykM` | `number` | `0` | min -200 % · max 200 % · step 1 | **Magenta**<br />Share of the Magenta channel carried into the Cyan output channel. 100% copies it, a negative value subtracts it. |
| `cmykCFromCmykY` | `number` | `0` | min -200 % · max 200 % · step 1 | **Yellow**<br />Share of the Yellow channel carried into the Cyan output channel. 100% copies it, a negative value subtracts it. |
| `cmykCFromCmykK` | `number` | `0` | min -200 % · max 200 % · step 1 | **Black**<br />Share of the Black channel carried into the Cyan output channel. 100% copies it, a negative value subtracts it. |
| `cmykCFromCmykAlpha` | `number` | `0` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Cyan output channel. 100% copies it, a negative value subtracts it. |
| `offsetCmykC` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Cyan output channel, whatever the picture. |

#### Magenta output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `cmykMFromCmykC` | `number` | `0` | min -200 % · max 200 % · step 1 | **Cyan**<br />Share of the Cyan channel carried into the Magenta output channel. 100% copies it, a negative value subtracts it. |
| `cmykMFromCmykM` | `number` | `100` | min -200 % · max 200 % · step 1 | **Magenta**<br />Share of the Magenta channel carried into the Magenta output channel. 100% copies it, a negative value subtracts it. |
| `cmykMFromCmykY` | `number` | `0` | min -200 % · max 200 % · step 1 | **Yellow**<br />Share of the Yellow channel carried into the Magenta output channel. 100% copies it, a negative value subtracts it. |
| `cmykMFromCmykK` | `number` | `0` | min -200 % · max 200 % · step 1 | **Black**<br />Share of the Black channel carried into the Magenta output channel. 100% copies it, a negative value subtracts it. |
| `cmykMFromCmykAlpha` | `number` | `0` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Magenta output channel. 100% copies it, a negative value subtracts it. |
| `offsetCmykM` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Magenta output channel, whatever the picture. |

#### Yellow output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `cmykYFromCmykC` | `number` | `0` | min -200 % · max 200 % · step 1 | **Cyan**<br />Share of the Cyan channel carried into the Yellow output channel. 100% copies it, a negative value subtracts it. |
| `cmykYFromCmykM` | `number` | `0` | min -200 % · max 200 % · step 1 | **Magenta**<br />Share of the Magenta channel carried into the Yellow output channel. 100% copies it, a negative value subtracts it. |
| `cmykYFromCmykY` | `number` | `100` | min -200 % · max 200 % · step 1 | **Yellow**<br />Share of the Yellow channel carried into the Yellow output channel. 100% copies it, a negative value subtracts it. |
| `cmykYFromCmykK` | `number` | `0` | min -200 % · max 200 % · step 1 | **Black**<br />Share of the Black channel carried into the Yellow output channel. 100% copies it, a negative value subtracts it. |
| `cmykYFromCmykAlpha` | `number` | `0` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Yellow output channel. 100% copies it, a negative value subtracts it. |
| `offsetCmykY` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Yellow output channel, whatever the picture. |

#### Black output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `cmykKFromCmykC` | `number` | `0` | min -200 % · max 200 % · step 1 | **Cyan**<br />Share of the Cyan channel carried into the Black output channel. 100% copies it, a negative value subtracts it. |
| `cmykKFromCmykM` | `number` | `0` | min -200 % · max 200 % · step 1 | **Magenta**<br />Share of the Magenta channel carried into the Black output channel. 100% copies it, a negative value subtracts it. |
| `cmykKFromCmykY` | `number` | `0` | min -200 % · max 200 % · step 1 | **Yellow**<br />Share of the Yellow channel carried into the Black output channel. 100% copies it, a negative value subtracts it. |
| `cmykKFromCmykK` | `number` | `100` | min -200 % · max 200 % · step 1 | **Black**<br />Share of the Black channel carried into the Black output channel. 100% copies it, a negative value subtracts it. |
| `cmykKFromCmykAlpha` | `number` | `0` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Black output channel. 100% copies it, a negative value subtracts it. |
| `offsetCmykK` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Black output channel, whatever the picture. |

#### Alpha output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `cmykAlphaFromCmykC` | `number` | `0` | min -200 % · max 200 % · step 1 | **Cyan**<br />Share of the Cyan channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `cmykAlphaFromCmykM` | `number` | `0` | min -200 % · max 200 % · step 1 | **Magenta**<br />Share of the Magenta channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `cmykAlphaFromCmykY` | `number` | `0` | min -200 % · max 200 % · step 1 | **Yellow**<br />Share of the Yellow channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `cmykAlphaFromCmykK` | `number` | `0` | min -200 % · max 200 % · step 1 | **Black**<br />Share of the Black channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `cmykAlphaFromCmykAlpha` | `number` | `100` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `offsetCmykAlpha` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Alpha output channel, whatever the picture. |

### LAB space

> These settings only count when `space` = `lab` (LAB).

#### Lightness output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `labLFromLabL` | `number` | `100` | min -200 % · max 200 % · step 1 | **Lightness**<br />Share of the Lightness channel carried into the Lightness output channel. 100% copies it, a negative value subtracts it. |
| `labLFromLabA` | `number` | `0` | min -200 % · max 200 % · step 1 | **Chroma A**<br />Share of the Chroma A channel carried into the Lightness output channel. 100% copies it, a negative value subtracts it. |
| `labLFromLabB` | `number` | `0` | min -200 % · max 200 % · step 1 | **Chroma B**<br />Share of the Chroma B channel carried into the Lightness output channel. 100% copies it, a negative value subtracts it. |
| `labLFromLabAlpha` | `number` | `0` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Lightness output channel. 100% copies it, a negative value subtracts it. |
| `offsetLabL` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Lightness output channel, whatever the picture. |

#### Chroma A output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `labAFromLabL` | `number` | `0` | min -200 % · max 200 % · step 1 | **Lightness**<br />Share of the Lightness channel carried into the Chroma A output channel. 100% copies it, a negative value subtracts it. |
| `labAFromLabA` | `number` | `100` | min -200 % · max 200 % · step 1 | **Chroma A**<br />Share of the Chroma A channel carried into the Chroma A output channel. 100% copies it, a negative value subtracts it. |
| `labAFromLabB` | `number` | `0` | min -200 % · max 200 % · step 1 | **Chroma B**<br />Share of the Chroma B channel carried into the Chroma A output channel. 100% copies it, a negative value subtracts it. |
| `labAFromLabAlpha` | `number` | `0` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Chroma A output channel. 100% copies it, a negative value subtracts it. |
| `offsetLabA` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Chroma A output channel, whatever the picture. |

#### Chroma B output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `labBFromLabL` | `number` | `0` | min -200 % · max 200 % · step 1 | **Lightness**<br />Share of the Lightness channel carried into the Chroma B output channel. 100% copies it, a negative value subtracts it. |
| `labBFromLabA` | `number` | `0` | min -200 % · max 200 % · step 1 | **Chroma A**<br />Share of the Chroma A channel carried into the Chroma B output channel. 100% copies it, a negative value subtracts it. |
| `labBFromLabB` | `number` | `100` | min -200 % · max 200 % · step 1 | **Chroma B**<br />Share of the Chroma B channel carried into the Chroma B output channel. 100% copies it, a negative value subtracts it. |
| `labBFromLabAlpha` | `number` | `0` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Chroma B output channel. 100% copies it, a negative value subtracts it. |
| `offsetLabB` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Chroma B output channel, whatever the picture. |

#### Alpha output

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `labAlphaFromLabL` | `number` | `0` | min -200 % · max 200 % · step 1 | **Lightness**<br />Share of the Lightness channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `labAlphaFromLabA` | `number` | `0` | min -200 % · max 200 % · step 1 | **Chroma A**<br />Share of the Chroma A channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `labAlphaFromLabB` | `number` | `0` | min -200 % · max 200 % · step 1 | **Chroma B**<br />Share of the Chroma B channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `labAlphaFromLabAlpha` | `number` | `100` | min -200 % · max 200 % · step 1 | **Alpha**<br />Share of the Alpha channel carried into the Alpha output channel. 100% copies it, a negative value subtracts it. |
| `offsetLabAlpha` | `number` | `0` | min -100 % · max 100 % · step 1 | **Offset**<br />Value added to the Alpha output channel, whatever the picture. |

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
curl -X POST https://api.pixlub.com/v1/modules/channelMixer \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"space":"rgb","rgbRFromRgbR":100,"rgbRFromRgbG":0}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"space":"rgb","rgbRFromRgbR":100,"rgbRFromRgbG":0}))

const res = await fetch('https://api.pixlub.com/v1/modules/channelMixer', {
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
    "https://api.pixlub.com/v1/modules/channelMixer",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"space": "rgb", "rgbRFromRgbR": 100, "rgbRFromRgbG": 0})},
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
result = client.tools.run("channelMixer", image="photo.png", params={"space": "rgb", "rgbRFromRgbR": 100, "rgbRFromRgbG": 0})
result.save(f"channelMixer{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "channelMixer", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"space": "rgb", "rgbRFromRgbR": 100, "rgbRFromRgbG": 0},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("channelMixer"+result.Extension(), false)
```

## Outputs

Each returned file carries its output key (`key`) in `outputs`: look it up to find the file you want rather than relying on its position.

### 1 file

> **1 file** : A single image in `in`.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image produced by the module.<br />A single image sent: the file keeps the `out` key. |

### Several files

> **Several files** : Several images in `in`, up to 64: their number comes from the files sent, you do not send it.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG` | **Image(s)**<br />Image produced by the module.<br />Several images sent in `in`: one file per image, under the keys `out#0`, `out#1`…, in upload order. |

## Response

The response lists the produced files in outputs. Each link is signed and valid for one hour, without an API key; files are deleted after 24 hours.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "channelMixer",
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

`GET /v1/modules/channelMixer/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "space": {
      "title": "Space",
      "default": "rgb",
      "type": "string",
      "enum": [
        "rgb",
        "gray",
        "cmyk",
        "lab"
      ]
    },
    "rgbRFromRgbR": {
      "title": "Red",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbRFromRgbG": {
      "title": "Green",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbRFromRgbB": {
      "title": "Blue",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbRFromRgbAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbR": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "rgbGFromRgbR": {
      "title": "Red",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbGFromRgbG": {
      "title": "Green",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbGFromRgbB": {
      "title": "Blue",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbGFromRgbAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbG": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "rgbBFromRgbR": {
      "title": "Red",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbBFromRgbG": {
      "title": "Green",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbBFromRgbB": {
      "title": "Blue",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbBFromRgbAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbB": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbR": {
      "title": "Red",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbG": {
      "title": "Green",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbB": {
      "title": "Blue",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "grayIFromGrayI": {
      "title": "Intensity",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "grayIFromGrayAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetGrayI": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "grayAlphaFromGrayI": {
      "title": "Intensity",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "grayAlphaFromGrayAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetGrayAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykCFromCmykC": {
      "title": "Cyan",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykC": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykMFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykM": {
      "title": "Magenta",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykM": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykYFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykY": {
      "title": "Yellow",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykY": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykKFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykK": {
      "title": "Black",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykK": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labLFromLabL": {
      "title": "Lightness",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labLFromLabA": {
      "title": "Chroma A",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labLFromLabB": {
      "title": "Chroma B",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labLFromLabAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabL": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labAFromLabL": {
      "title": "Lightness",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAFromLabA": {
      "title": "Chroma A",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAFromLabB": {
      "title": "Chroma B",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAFromLabAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabA": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labBFromLabL": {
      "title": "Lightness",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labBFromLabA": {
      "title": "Chroma A",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labBFromLabB": {
      "title": "Chroma B",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labBFromLabAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabB": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labAlphaFromLabL": {
      "title": "Lightness",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAlphaFromLabA": {
      "title": "Chroma A",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAlphaFromLabB": {
      "title": "Chroma B",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAlphaFromLabAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
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
