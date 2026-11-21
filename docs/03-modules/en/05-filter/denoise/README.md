# Denoise

Reduce an image's noise while preserving its edges.

**Category** : Filters · **Identifier** : `denoise` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/denoise)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose noise is reduced. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Filter radius, then mix with the original.](../../../../assets/modules/denoise/demo.en.webp)](../../../../assets/modules/denoise/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/denoise/demo.en.mp4) : Filter radius, then mix with the original.

1. `0:00` Import an image
2. `0:04` Filter radius
3. `0:08` Mix with the original
4. `0:12` Export the result

## How to use

1. **Import**

   Drop one or more images. Zoom in to see the grain.

2. **Adjust**

   The **radius** sets the smoothing strength, the **intensity** the mix with the original.

## Settings

| Setting | Effect |
| --- | --- |
| **Radius** | 1 to 3 px. |
| **Intensity** | 0 to 100%: share of the denoised image. |

## Tips

- A high radius also wipes fine details: lower the intensity to keep a natural look.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
