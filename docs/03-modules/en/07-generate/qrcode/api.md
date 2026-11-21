# QR code: API reference

Generates a QR code any reader can scan (link, Wi-Fi, contact…), styled, with a logo, or blended into an image

[See how to use it on the site](./README.md)

| Endpoint | Cost |
| --- | --- |
| `POST /v1/modules/qrcode` | 1 credit per file |

## Files

| Field | Required | Formats | Description |
| --- | --- | --- | --- |
| `logo` (Single image) | no | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Logo**<br />Optional image placed in the middle of the QR code; automatic correction rises to H. |
| `image` (Single image) | no | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image**<br />Optional image turned into a QR code pattern the QR code blends into ("In an image" mode); its transparency gives the silhouette. |

## Settings

### Content

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `contentType` | `string` | `"url"` | `url` Link : Web address; `https://` is added when missing.<br />`text` Text : Free text.<br />`wifi` Wi-Fi : Joins a Wi-Fi network in one scan.<br />`email` Email : Prepares an email: recipient, subject, message.<br />`tel` Phone : Calls a number.<br />`sms` SMS : Prepares a text message.<br />`vcard` Contact (vCard) : Contact card to save.<br />`geo` Location : Opens a point on the map. | **Type**<br />What the QR code holds; each type follows the format common readers understand. |
| `url` | `string` | `"https://pixlub.com"` |  | **Link**<br />Address opened on scan.<br />*Applies when `contentType` = `url` (Link).* |
| `text` | `string` | *empty string* |  | **Text**<br />Text carried as is.<br />*Applies when `contentType` = `text` (Text).* |
| `wifiSsid` | `string` | *empty string* |  | **Network name (SSID)**<br />Name of the Wi-Fi network.<br />*Applies when `contentType` = `wifi` (Wi-Fi).* |
| `wifiSecurity` | `string` | `"WPA"` | `WPA` WPA/WPA2/WPA3<br />`WEP` WEP<br />`none` None | **Security**<br />Network encryption.<br />*Applies when `contentType` = `wifi` (Wi-Fi).* |
| `wifiPassword` | `string` | *empty string* |  | **Password**<br />Network password, stored in clear in the QR code.<br />*Applies when `contentType` = `wifi` (Wi-Fi) and `wifiSecurity` = `WPA` (WPA/WPA2/WPA3) or `WEP` (WEP).* |
| `wifiHidden` | `boolean` | `false` |  | **Hidden network**<br />The network does not broadcast its name.<br />*Applies when `contentType` = `wifi` (Wi-Fi).* |
| `vcardFirstName` | `string` | *empty string* |  | **First name**<br />Contact first name.<br />*Applies when `contentType` = `vcard` (Contact (vCard)).* |
| `vcardLastName` | `string` | *empty string* |  | **Last name**<br />Contact last name.<br />*Applies when `contentType` = `vcard` (Contact (vCard)).* |
| `vcardOrg` | `string` | *empty string* |  | **Organization**<br />Company or organization.<br />*Applies when `contentType` = `vcard` (Contact (vCard)).* |
| `vcardTitle` | `string` | *empty string* |  | **Job title**<br />Job title.<br />*Applies when `contentType` = `vcard` (Contact (vCard)).* |
| `emailTo` | `string` | *empty string* |  | **Email**<br />Email address.<br />*Applies when `contentType` = `email` (Email) or `vcard` (Contact (vCard)).* |
| `phone` | `string` | *empty string* |  | **Phone**<br />Number, preferably in international format (+1…).<br />*Applies when `contentType` = `tel` (Phone) or `sms` (SMS) or `vcard` (Contact (vCard)).* |
| `emailSubject` | `string` | *empty string* |  | **Subject**<br />Email subject.<br />*Applies when `contentType` = `email` (Email).* |
| `emailBody` | `string` | *empty string* |  | **Message**<br />Email body.<br />*Applies when `contentType` = `email` (Email).* |
| `smsMessage` | `string` | *empty string* |  | **Message**<br />Text of the message.<br />*Applies when `contentType` = `sms` (SMS).* |
| `vcardUrl` | `string` | *empty string* |  | **Website**<br />Contact website.<br />*Applies when `contentType` = `vcard` (Contact (vCard)).* |
| `vcardStreet` | `string` | *empty string* |  | **Street**<br />Street and number.<br />*Applies when `contentType` = `vcard` (Contact (vCard)).* |
| `vcardZip` | `string` | *empty string* |  | **Postal code**<br />Postal code.<br />*Applies when `contentType` = `vcard` (Contact (vCard)).* |
| `vcardCity` | `string` | *empty string* |  | **City**<br />City.<br />*Applies when `contentType` = `vcard` (Contact (vCard)).* |
| `vcardCountry` | `string` | *empty string* |  | **Country**<br />Country.<br />*Applies when `contentType` = `vcard` (Contact (vCard)).* |
| `geoLat` | `number` | `48.8584` | min -90 ° · max 90 ° | **Latitude**<br />Latitude in decimal degrees.<br />*Applies when `contentType` = `geo` (Location).* |
| `geoLng` | `number` | `2.2945` | min -180 ° · max 180 ° | **Longitude**<br />Longitude in decimal degrees.<br />*Applies when `contentType` = `geo` (Location).* |

### Blending

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `mode` | `string` | `"standard"` | `standard` Standard : QR code alone, on its background.<br />`shape` In a shape : The QR code fills a silhouette (cloche, heart… or that of the connected image), extended by modules of the same design and ringed by an outline.<br />`image` In an image : The connected image becomes a module pattern, tones and colors included, and the QR code blends into it. | **Mode**<br />In a shape: a white outlined silhouette filled with modules like the QR code. In an image: connect an image to the Image input, its tones become the pattern. |

### Silhouette

> These settings only count when `mode` = `shape` (In a shape).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `shape` | `string` | `"cloche"` | `cloche` Cloche<br />`circle` Circle<br />`roundedSquare` Rounded square<br />`heart` Heart<br />`star` Star<br />`diamond` Diamond<br />`hexagon` Hexagon<br />`shield` Shield<br />`house` House<br />`cloud` Cloud<br />`bubble` Speech bubble<br />`pin` Location pin<br />`drop` Drop<br />`leaf` Leaf<br />`cup` Cup<br />`tshirt` T-shirt<br />`gift` Gift<br />`bag` Bag<br />`cat` Cat<br />`paw` Paw<br />`image` From the image : Silhouette of the image connected to the Image input. | **Shape**<br />Silhouette the QR code fills. "From the image" takes that of the connected image: its transparency, or its outline for a line drawing. |
| `outlineWidth` | `number` | `0.8` | min 0 · max 6 · step 0.1 | **Outline thickness**<br />Thickness of the border around the silhouette, in modules; 0 removes it. |
| `outlineCustom` | `boolean` | `false` |  | **Own outline color**<br />Otherwise the outline takes the module color (or gradient). |
| `outlineColor` | `Color`<br />*Solid color* | `"#1c2535"` |  | **Outline color**<br />Outline color.<br />*Applies when `outlineCustom` = `true`.*<br />*Solid color* : CSS color: `#rrggbb`, `#rrggbbaa`, `rgb()` or `hsl()`. |
| `patternDensity` | `number` | `50` | min 20 % · max 80 % · step 1 | **Pattern density**<br />Share of dark modules around the QR code; 50% mimics QR code data. |

### Placement

> These settings only count when `mode` = `image` (In an image) or `shape` (In a shape).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `qrSize` | `number` | `85` | min 20 % · max 150 % · step 1 | **QR code size**<br />Share of the largest square that fits in the shape; the pattern modules follow.<br />*Applies when `mode` = `shape` (In a shape).* |
| `cellSize` | `number` | `12` | min 3 px · max 64 px · step 1 | **Module size**<br />Module side in image pixels: sets the pattern grain and the QR code size.<br />*Applies when `mode` = `image` (In an image).* |
| `qrX` | `number` | `50` | min 0 % · max 100 % · step 0.1 | **Position X**<br />In an image: QR code center, as a share of the width. In a shape: offset from its automatic spot (50% = middle of the shape). It always snaps to the grid. |
| `qrY` | `number` | `50` | min 0 % · max 100 % · step 0.1 | **Position Y**<br />Like position X, along the height. |
| `halo` | `number` | `0` | min 0 · max 6 · step 1 | **Halo**<br />Light modules around the QR code. At 0 the QR code melts into the pattern with no edge. |
| `seed` | `number` | `1` | min 0 · max 9999 | **Variant**<br />Changes the pattern draw.<br />*Applies when `mode` = `shape` (In a shape), or `mode` = `image` (In an image) and `convert` = `qr` (QR pattern).* |
| `finderGuard` | `boolean` | `true` |  | **Clear the eyes**<br />A one-module light rim around the three eyes, on the image side: that is what readers need to find the code; the rest of the edge stays blended. |

### Conversion

> These settings only count when `mode` = `image` (In an image).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `convert` | `string` | `"qr"` | `qr` QR pattern : Random texture like QR code data, denser in dark tones: the QR code melts into it.<br />`threshold` Threshold : Clean flat areas: logos, silhouettes.<br />`dither` Diffusion : Renders gradients and photos.<br />`ordered` Ordered : Regular screen (Bayer). | **Method**<br />How the image tones turn into dark or light modules. |
| `tone` | `number` | `70` | min 0 % · max 100 % · step 1 | **Tone depth**<br />At 0, even density everywhere (silhouette only, pure QR look); higher, the image tones show through the density.<br />*Applies when `convert` = `qr` (QR pattern).* |
| `threshold` | `number` | `50` | min 0 % · max 100 % · step 1 | **Threshold**<br />Higher means more dark modules. |
| `contrast` | `number` | `0` | min -100 % · max 100 % · step 1 | **Contrast**<br />Image contrast before conversion. |
| `invertImage` | `boolean` | `false` |  | **Invert**<br />Light areas turn dark. |
| `silhouette` | `boolean` | `true` |  | **Follow the silhouette**<br />Nothing is drawn outside the opaque areas of the image. |
| `outline` | `boolean` | `true` |  | **Outline**<br />The silhouette edge is drawn with a line of modules.<br />*Applies when `silhouette` = `true`.* |
| `colorSource` | `string` | `"qr"` | `qr` From the QR code<br />`image` From the image | **Module color**<br />Color of every module, pattern and QR code alike: the QR code color, or the image color under each module, darkened to stay readable. |

### Merge

> These settings only count when `mode` = `image` (In an image).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `halftone` | `boolean` | `false` |  | **Image through the QR**<br />Each module is split 3 × 3: the center carries the data, the rest shows the image; the whole pattern takes that grain. |
| `halftoneStrength` | `number` | `50` | min 0 % · max 100 % · step 1 | **QR strength**<br />Share of each module given back to the QR code around its center: higher reads better.<br />*Applies when `halftone` = `true`.* |
| `qrSolidBg` | `boolean` | `true` |  | **Solid background under the QR**<br />The QR code and its halo keep an opaque background, even when the rest is transparent. |
| `backdropOpacity` | `number` | `0` | min 0 % · max 100 % · step 1 | **Original image**<br />Shows the original image under the pattern; lower the background opacity then. |

### Modules

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `moduleShape` | `string` | `"square"` | `square` Squares<br />`rounded` Fluid<br />`dots` Dots<br />`squircle` Rounded squares<br />`diamond` Diamonds<br />`star` Stars<br />`cross` Crosses<br />`heart` Hearts<br />`leaf` Leaves<br />`vbars` Vertical bars<br />`hbars` Horizontal bars<br />`random` Confetti | **Shape**<br />Shape of each module (and of the image modules in blended mode). |
| `moduleScale` | `number` | `100` | min 40 % · max 100 % · step 1 | **Size**<br />Module size within its cell; below 70% scanning gets more fragile.<br />*Applies when `moduleShape` = `square` (Squares) or `dots` (Dots) or `squircle` (Rounded squares) or `diamond` (Diamonds) or `star` (Stars) or `cross` (Crosses) or `heart` (Hearts) or `leaf` (Leaves) or `vbars` (Vertical bars) or `hbars` (Horizontal bars) or `random` (Confetti).* |
| `roundness` | `number` | `50` | min 0 % · max 100 % · step 1 | **Roundness**<br />Corner roundness.<br />*Applies when `moduleShape` = `rounded` (Fluid) or `squircle` (Rounded squares) or `leaf` (Leaves) or `vbars` (Vertical bars) or `hbars` (Horizontal bars).* |

### Eyes

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `eyeFrame` | `string` | `"square"` | `square` Square<br />`rounded` Rounded<br />`circle` Circle<br />`leaf` Leaf<br />`shape` Like the modules | **Frame**<br />Shape of the frame of the three finder eyes and of the small alignment patterns. "Like the modules" with detached shapes (dots…) hinders readers. |
| `eyeBall` | `string` | `"square"` | `square` Square<br />`rounded` Rounded<br />`circle` Round<br />`diamond` Diamond<br />`leaf` Leaf<br />`star` Star<br />`shape` Like the modules | **Center**<br />Shape of the eye centers. For the safest scan, keep the same family as the frame: square or rounded with a square or rounded frame, round or diamond with a round frame. |
| `eyeCustom` | `boolean` | `false` |  | **Own colors**<br />Gives the eyes their own colors. |
| `eyeFrameColor` | `Color`<br />*Solid color* | `"#1c2535"` |  | **Frame color**<br />Color of the eye frames.<br />*Applies when `eyeCustom` = `true`.*<br />*Solid color* : CSS color: `#rrggbb`, `#rrggbbaa`, `rgb()` or `hsl()`. |
| `eyeBallColor` | `Color`<br />*Solid color* | `"#1c2535"` |  | **Center color**<br />Color of the eye centers.<br />*Applies when `eyeCustom` = `true`.*<br />*Solid color* : CSS color: `#rrggbb`, `#rrggbbaa`, `rgb()` or `hsl()`. |

### Colors

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `color` | [`Color | ColorGradient`](#type-colorgradient)<br />*Color or gradient* | `"#000000"` |  | **Modules**<br />Color or gradient of the modules; keep it clearly darker than the background.<br />*Color or gradient* : A CSS color (`"#ff8800"`) for a flat fill, or a `ColorGradient` object for a gradient.<br />Color \| ColorGradient structure and example : [`ColorGradient`](#type-colorgradient), [`GradientStop`](#type-gradientstop) |
| `fgOpacity` | `number` | `100` | min 0 % · max 100 % · step 1 | **Module opacity**<br />Module transparency. |
| `background` | `Color`<br />*Solid color* | `"#ffffff"` |  | **Background**<br />Background color (light cells).<br />*Solid color* : CSS color: `#rrggbb`, `#rrggbbaa`, `rgb()` or `hsl()`. |
| `bgOpacity` | `number` | `100` | min 0 % · max 100 % · step 1 | **Background opacity**<br />At 0% the background is transparent. |
| `bgRadius` | `number` | `0` | min 0 % · max 50 % · step 1 | **Background corners**<br />Roundness of the background corners.<br />*Applies when `mode` = `standard` (Standard).* |

### Dimensions

> These settings only count when `mode` = `standard` (Standard) or `shape` (In a shape).

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `size` | `number` | `1024` | min 64 px · max 4096 px · step 1 | **Size**<br />Side of the image, margin included. |
| `margin` | `number` | `4` | min 0 · max 20 · step 1 | **Margin (modules)**<br />Light zone around the code; the standard asks for 4 modules.<br />*Applies when `mode` = `standard` (Standard).* |

### Logo

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `logoSize` | `number` | `22` | min 5 % · max 40 % · step 1 | **Size**<br />Logo side, as a share of the QR code. With "Safe size" it is brought back to the largest size error correction can repair. |
| `logoSafe` | `boolean` | `true` |  | **Safe size**<br />Counts the codewords hidden by the logo, block by block, and shrinks the logo while it hides too many: the link stays readable. Raise correction to H for a bigger logo. |
| `logoShape` | `string` | `"rounded"` | `none` None<br />`square` Square<br />`rounded` Rounded<br />`circle` Round | **Plate**<br />Shape placed under the logo; the logo is clipped to it. |
| `logoBg` | `Color`<br />*Solid color* | `"#ffffff"` |  | **Plate color**<br />Color of the plate under the logo.<br />*Applies when `logoShape` = `square` (Square) or `rounded` (Rounded) or `circle` (Round).*<br />*Solid color* : CSS color: `#rrggbb`, `#rrggbbaa`, `rgb()` or `hsl()`. |
| `logoPadding` | `number` | `1` | min 0 · max 4 · step 0.5 | **Padding**<br />Space around the logo, in modules. |
| `logoClear` | `boolean` | `true` |  | **Clear the modules**<br />Removes the modules hidden by the logo, for a clean edge. |
| `logoOpacity` | `number` | `100` | min 0 % · max 100 % · step 1 | **Opacity**<br />Logo transparency. |

### Encoding

| Setting | Type | Default | Allowed values | Description |
| --- | --- | --- | --- | --- |
| `ecl` | `string` | `"auto"` | `auto` Auto : M, or H as soon as a logo or halftone hides modules.<br />`L` L · 7% : Smallest code, least robust.<br />`M` M · 15% : Common use.<br />`Q` Q · 25% : Withstands dirt and small logos.<br />`H` H · 30% : Most robust: logo, strong style, blending. | **Error correction**<br />Share of the code that can be lost without breaking the scan; higher means a denser code. It rises by itself while the size stays the same. |
| `minVersion` | `number` | `1` | min 1 · max 40 · step 1 | **Minimum version**<br />Minimum grid size (1 = 21 × 21 modules, +4 per version); useful for a finer pattern or a fixed grid. |
| `mask` | `string` | `"auto"` | `auto` Auto<br />`0` 0<br />`1` 1<br />`2` 2<br />`3` 3<br />`4` 4<br />`5` 5<br />`6` 6<br />`7` 7 | **Mask**<br />Pattern that scrambles the data; Auto keeps the most readable, a fixed number changes how the code looks. |

## Examples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/qrcode \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F logo=@logo.png \
  -F 'params={"contentType":"url","url":"https://pixlub.com","mode":"standard"}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('logo', await openAsBlob('logo.png'), 'logo.png')
form.append('params', JSON.stringify({"contentType":"url","url":"https://pixlub.com","mode":"standard"}))

const res = await fetch('https://api.pixlub.com/v1/modules/qrcode', {
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
    "https://api.pixlub.com/v1/modules/qrcode",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("logo", open("logo.png", "rb"))],
    data={"params": json.dumps({"contentType": "url", "url": "https://pixlub.com", "mode": "standard"})},
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
result = client.tools.run("qrcode", inputs={"logo": "logo.png"}, params={"contentType": "url", "url": "https://pixlub.com", "mode": "standard"})
result.save(f"qrcode{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "qrcode", pixlub.RunRequest{
    Inputs: map[string]pixlub.Source{
        "logo": pixlub.FromPath("logo.png"),
    },
    Params: map[string]any{"contentType": "url", "url": "https://pixlub.com", "mode": "standard"},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("qrcode"+result.Extension(), false)
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
  "module": "qrcode",
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

<a name="type-colorgradient"></a>

### ColorGradient

*Object*. Color gradient: stops placed along an axis, and how to spread them.

| Member | Type | Description |
| --- | --- | --- |
| `stops` | `GradientStop[]` | Color stops, at least two, in any order. |
| `type` | `"linear" \| "radial"` | *optional* · Linear along `angle`, or in circles from the center. `linear` by default; no effect when only the color order matters (Gradient map). |
| `angle` | `number` | *optional* · Direction of a linear gradient, in degrees: 0 upwards, 90 to the right. `90` by default. |

**Example**

```json
{
  "type": "linear",
  "angle": 90,
  "stops": [
    {
      "color": "#140a2e",
      "at": 0
    },
    {
      "color": "#c264c2",
      "at": 55
    },
    {
      "color": "#ffffff",
      "at": 100
    }
  ]
}
```

<a name="type-gradientstop"></a>

### GradientStop

*Object*. Stop of a gradient.

| Member | Type | Description |
| --- | --- | --- |
| `color` | `Color` | CSS color of the stop; alpha (`#rrggbbaa`) is kept. |
| `at` | `number` | Position of the stop, from 0 (start) to 100 (end), in %. |

**Example**

```json
{
  "color": "#c264c2",
  "at": 55
}
```

## JSON Schema

The exact JSON Schema of the settings, the one the API uses to validate the params field:

`GET /v1/modules/qrcode/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "contentType": {
      "title": "Type",
      "default": "url",
      "type": "string",
      "enum": [
        "url",
        "text",
        "wifi",
        "email",
        "tel",
        "sms",
        "vcard",
        "geo"
      ]
    },
    "url": {
      "title": "Link",
      "default": "https://pixlub.com",
      "type": "string"
    },
    "wifiSsid": {
      "title": "Network name (SSID)",
      "default": "",
      "type": "string"
    },
    "wifiSecurity": {
      "title": "Security",
      "default": "WPA",
      "type": "string",
      "enum": [
        "WPA",
        "WEP",
        "none"
      ]
    },
    "wifiPassword": {
      "title": "Password",
      "default": "",
      "type": "string"
    },
    "wifiHidden": {
      "title": "Hidden network",
      "default": false,
      "type": "boolean"
    },
    "vcardFirstName": {
      "title": "First name",
      "default": "",
      "type": "string"
    },
    "vcardLastName": {
      "title": "Last name",
      "default": "",
      "type": "string"
    },
    "vcardOrg": {
      "title": "Organization",
      "default": "",
      "type": "string"
    },
    "vcardTitle": {
      "title": "Job title",
      "default": "",
      "type": "string"
    },
    "emailTo": {
      "title": "Email",
      "default": "",
      "type": "string"
    },
    "phone": {
      "title": "Phone",
      "default": "",
      "type": "string"
    },
    "emailSubject": {
      "title": "Subject",
      "default": "",
      "type": "string"
    },
    "vcardUrl": {
      "title": "Website",
      "default": "",
      "type": "string"
    },
    "vcardStreet": {
      "title": "Street",
      "default": "",
      "type": "string"
    },
    "vcardZip": {
      "title": "Postal code",
      "default": "",
      "type": "string"
    },
    "vcardCity": {
      "title": "City",
      "default": "",
      "type": "string"
    },
    "vcardCountry": {
      "title": "Country",
      "default": "",
      "type": "string"
    },
    "geoLat": {
      "title": "Latitude",
      "default": 48.8584,
      "type": "number",
      "minimum": -90,
      "maximum": 90
    },
    "geoLng": {
      "title": "Longitude",
      "default": 2.2945,
      "type": "number",
      "minimum": -180,
      "maximum": 180
    },
    "mode": {
      "title": "Mode",
      "default": "standard",
      "type": "string",
      "enum": [
        "standard",
        "shape",
        "image"
      ]
    },
    "outlineWidth": {
      "title": "Outline thickness",
      "default": 0.8,
      "type": "number",
      "minimum": 0,
      "maximum": 6,
      "multipleOf": 0.1
    },
    "outlineCustom": {
      "title": "Own outline color",
      "default": false,
      "type": "boolean"
    },
    "outlineColor": {
      "title": "Outline color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "patternDensity": {
      "title": "Pattern density",
      "default": 50,
      "type": "number",
      "minimum": 20,
      "maximum": 80,
      "multipleOf": 1
    },
    "qrSize": {
      "title": "QR code size",
      "default": 85,
      "type": "number",
      "minimum": 20,
      "maximum": 150,
      "multipleOf": 1
    },
    "cellSize": {
      "title": "Module size",
      "default": 12,
      "type": "number",
      "minimum": 3,
      "maximum": 64,
      "multipleOf": 1
    },
    "qrX": {
      "title": "Position X",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "qrY": {
      "title": "Position Y",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 0.1
    },
    "halo": {
      "title": "Halo",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 6,
      "multipleOf": 1
    },
    "seed": {
      "title": "Variant",
      "default": 1,
      "type": "number",
      "minimum": 0,
      "maximum": 9999
    },
    "finderGuard": {
      "title": "Clear the eyes",
      "default": true,
      "type": "boolean"
    },
    "convert": {
      "title": "Method",
      "default": "qr",
      "type": "string",
      "enum": [
        "qr",
        "threshold",
        "dither",
        "ordered"
      ]
    },
    "tone": {
      "title": "Tone depth",
      "default": 70,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "threshold": {
      "title": "Threshold",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "contrast": {
      "title": "Contrast",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "invertImage": {
      "title": "Invert",
      "default": false,
      "type": "boolean"
    },
    "silhouette": {
      "title": "Follow the silhouette",
      "default": true,
      "type": "boolean"
    },
    "outline": {
      "title": "Outline",
      "default": true,
      "type": "boolean"
    },
    "colorSource": {
      "title": "Module color",
      "default": "qr",
      "type": "string",
      "enum": [
        "qr",
        "image"
      ]
    },
    "halftone": {
      "title": "Image through the QR",
      "default": false,
      "type": "boolean"
    },
    "halftoneStrength": {
      "title": "QR strength",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "qrSolidBg": {
      "title": "Solid background under the QR",
      "default": true,
      "type": "boolean"
    },
    "backdropOpacity": {
      "title": "Original image",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "moduleScale": {
      "title": "Size",
      "default": 100,
      "type": "number",
      "minimum": 40,
      "maximum": 100,
      "multipleOf": 1
    },
    "roundness": {
      "title": "Roundness",
      "default": 50,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "eyeCustom": {
      "title": "Own colors",
      "default": false,
      "type": "boolean"
    },
    "eyeFrameColor": {
      "title": "Frame color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "eyeBallColor": {
      "title": "Center color",
      "default": "#1c2535",
      "type": "string",
      "minLength": 1
    },
    "color": {
      "title": "Modules",
      "default": "#000000",
      "anyOf": [
        {
          "type": "string",
          "minLength": 1
        },
        {
          "type": "object",
          "required": [
            "stops"
          ],
          "properties": {
            "stops": {
              "type": "array",
              "items": {
                "type": "object",
                "required": [
                  "color",
                  "at"
                ],
                "properties": {
                  "color": {
                    "type": "string",
                    "minLength": 1
                  },
                  "at": {
                    "type": "number",
                    "minimum": 0,
                    "maximum": 100
                  }
                }
              },
              "minItems": 2
            },
            "type": {
              "type": "string",
              "enum": [
                "linear",
                "radial"
              ]
            },
            "angle": {
              "type": "number"
            }
          }
        }
      ]
    },
    "fgOpacity": {
      "title": "Module opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "background": {
      "title": "Background",
      "default": "#ffffff",
      "type": "string",
      "minLength": 1
    },
    "bgOpacity": {
      "title": "Background opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "bgRadius": {
      "title": "Background corners",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 50,
      "multipleOf": 1
    },
    "size": {
      "title": "Size",
      "default": 1024,
      "type": "number",
      "minimum": 64,
      "maximum": 4096,
      "multipleOf": 1
    },
    "margin": {
      "title": "Margin (modules)",
      "default": 4,
      "type": "number",
      "minimum": 0,
      "maximum": 20,
      "multipleOf": 1
    },
    "logoSize": {
      "title": "Size",
      "default": 22,
      "type": "number",
      "minimum": 5,
      "maximum": 40,
      "multipleOf": 1
    },
    "logoSafe": {
      "title": "Safe size",
      "default": true,
      "type": "boolean"
    },
    "logoShape": {
      "title": "Plate",
      "default": "rounded",
      "type": "string",
      "enum": [
        "none",
        "square",
        "rounded",
        "circle"
      ]
    },
    "logoBg": {
      "title": "Plate color",
      "default": "#ffffff",
      "type": "string",
      "minLength": 1
    },
    "logoPadding": {
      "title": "Padding",
      "default": 1,
      "type": "number",
      "minimum": 0,
      "maximum": 4,
      "multipleOf": 0.5
    },
    "logoClear": {
      "title": "Clear the modules",
      "default": true,
      "type": "boolean"
    },
    "logoOpacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "ecl": {
      "title": "Error correction",
      "default": "auto",
      "type": "string",
      "enum": [
        "auto",
        "L",
        "M",
        "Q",
        "H"
      ]
    },
    "minVersion": {
      "title": "Minimum version",
      "default": 1,
      "type": "number",
      "minimum": 1,
      "maximum": 40,
      "multipleOf": 1
    },
    "mask": {
      "title": "Mask",
      "default": "auto",
      "type": "string",
      "enum": [
        "auto",
        "0",
        "1",
        "2",
        "3",
        "4",
        "5",
        "6",
        "7"
      ]
    },
    "text": {
      "type": "string",
      "default": ""
    },
    "emailBody": {
      "type": "string",
      "default": ""
    },
    "smsMessage": {
      "type": "string",
      "default": ""
    },
    "moduleShape": {
      "type": "string",
      "default": "square"
    },
    "eyeFrame": {
      "type": "string",
      "default": "square"
    },
    "eyeBall": {
      "type": "string",
      "default": "square"
    },
    "shape": {
      "type": "string",
      "default": "cloche"
    }
  }
}
```

## Errors

Out-of-range setting, missing file, not enough credits: every refusal has its HTTP status.
