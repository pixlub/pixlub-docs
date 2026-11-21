# Levels: API reference

Adjusts the black and white points, gamma and output range, per channel

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/levels` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `in` (One image or several) | yes | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image whose levels are adjusted. |

## Settings

### General

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `space` | `string` | `"rgb"` | `rgb` RGB<br />`gray` Gray<br />`cmyk` CMYK<br />`lab` LAB | **Space**<br />Color space in which the channels are adjusted |

### RGB space

> These settings only count when `space` = `rgb` (RGB).

#### Master

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackRgbMaster` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteRgbMaster` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaRgbMaster` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackRgbMaster` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteRgbMaster` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Red

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackRgbR` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteRgbR` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaRgbR` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackRgbR` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteRgbR` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Green

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackRgbG` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteRgbG` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaRgbG` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackRgbG` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteRgbG` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Blue

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackRgbB` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteRgbB` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaRgbB` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackRgbB` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteRgbB` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Alpha

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackRgbAlpha` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteRgbAlpha` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaRgbAlpha` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackRgbAlpha` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteRgbAlpha` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

### Gray space

> These settings only count when `space` = `gray` (Gray).

#### Master

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackGrayMaster` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteGrayMaster` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaGrayMaster` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackGrayMaster` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteGrayMaster` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Intensity

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackGrayI` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteGrayI` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaGrayI` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackGrayI` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteGrayI` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Alpha

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackGrayAlpha` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteGrayAlpha` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaGrayAlpha` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackGrayAlpha` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteGrayAlpha` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

### CMYK space

> These settings only count when `space` = `cmyk` (CMYK).

#### Master

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackCmykMaster` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteCmykMaster` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaCmykMaster` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackCmykMaster` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteCmykMaster` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Cyan

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackCmykC` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteCmykC` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaCmykC` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackCmykC` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteCmykC` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Magenta

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackCmykM` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteCmykM` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaCmykM` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackCmykM` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteCmykM` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Yellow

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackCmykY` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteCmykY` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaCmykY` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackCmykY` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteCmykY` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Black

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackCmykK` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteCmykK` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaCmykK` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackCmykK` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteCmykK` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Alpha

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackCmykAlpha` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteCmykAlpha` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaCmykAlpha` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackCmykAlpha` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteCmykAlpha` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

### LAB space

> These settings only count when `space` = `lab` (LAB).

#### Master

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackLabMaster` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteLabMaster` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaLabMaster` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackLabMaster` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteLabMaster` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Lightness

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackLabL` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteLabL` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaLabL` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackLabL` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteLabL` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Chroma A

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackLabA` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteLabA` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaLabA` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackLabA` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteLabA` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Chroma B

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackLabB` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteLabB` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaLabB` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackLabB` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteLabB` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

#### Alpha

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `blackLabAlpha` | `number` | `0` | min 0 · max 254 · step 1 | **Black level**<br />Anything darker becomes black. Raising it deepens the shadows and crushes the detail sitting there. |
| `whiteLabAlpha` | `number` | `255` | min 1 · max 255 · step 1 | **White level**<br />Anything lighter becomes white. Lowering it brightens the picture and burns the highlights. |
| `gammaLabAlpha` | `number` | `1` | min 0.1 · max 4 · step 0.05 | **Gamma**<br />Bends the midtones without moving either end. Below 1 the channel darkens, above it brightens. |
| `outBlackLabAlpha` | `number` | `0` | min 0 · max 255 · step 1 | **Output black level**<br />Value black takes on output. Raising it washes out the shadows. |
| `outWhiteLabAlpha` | `number` | `255` | min 0 · max 255 · step 1 | **Output white level**<br />Value white takes on output. Lowering it dulls the highlights. |

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
curl -X POST https://api.pixlub.com/v1/modules/levels \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"space":"rgb","blackRgbMaster":0,"whiteRgbMaster":255}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"space":"rgb","blackRgbMaster":0,"whiteRgbMaster":255}))

const res = await fetch('https://api.pixlub.com/v1/modules/levels', {
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
    "https://api.pixlub.com/v1/modules/levels",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"space": "rgb", "blackRgbMaster": 0, "whiteRgbMaster": 255})},
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
result = client.tools.run("levels", image="photo.png", params={"space": "rgb", "blackRgbMaster": 0, "whiteRgbMaster": 255})
result.save(f"levels{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "levels", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"space": "rgb", "blackRgbMaster": 0, "whiteRgbMaster": 255},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("levels"+result.Extension(), false)
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
  "module": "levels",
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

`GET /v1/modules/levels/schema`

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
    "blackRgbMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbR": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbR": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbR": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbR": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbR": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbG": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbG": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbG": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbG": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbG": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbB": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbB": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbB": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbB": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbB": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackGrayMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteGrayMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaGrayMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackGrayMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteGrayMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackGrayI": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteGrayI": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaGrayI": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackGrayI": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteGrayI": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackGrayAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteGrayAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaGrayAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackGrayAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteGrayAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykC": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykC": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykC": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykC": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykC": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykM": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykM": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykM": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykM": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykM": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykY": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykY": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykY": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykY": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykY": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykK": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykK": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykK": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykK": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykK": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabL": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabL": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabL": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabL": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabL": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabA": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabA": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabA": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabA": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabA": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabB": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabB": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabB": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabB": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabB": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
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
