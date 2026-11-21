# Chromatic aberration

Shift the red and blue channels: lens effect, glitch or impact.

**Category** : Filters · **Identifier** : `chromatic` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/chromatic)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose red and blue channels are shifted. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Radial shift, center, then uniform as a trail.](../../../../assets/modules/chromatic/demo.en.webp)](../../../../assets/modules/chromatic/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/chromatic/demo.en.mp4) : Radial shift, center, then uniform as a trail.

1. `0:00` Import an image
2. `0:02` Radial shift
3. `0:08` Place the center
4. `0:10` Uniform, as a trail
5. `0:14` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Dose the shift**

   The **intensity** spreads the channels, the **preserved area** keeps the center sharp.

3. **Place the center**

   In radial mode, click in the preview.

## Settings

| Setting | Effect |
| --- | --- |
| **Mode** | **Radial** (from a center) or **Uniform** (in one direction). |
| **Intensity** | 0 to 100 px. |
| **Method** | Clean **Offset** or **Trail**. |
| **Preserved area** / **Softness** | Radial mode: untouched center and fade toward the edges. |
| **Angle** | Uniform mode: shift direction. |

## Tips

- A small radial shift mimics a real lens; a strong uniform shift gives a glitch look.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
