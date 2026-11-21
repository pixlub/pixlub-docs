# Pixel sorting

Sort pixels by brightness in light or dark areas, a glitch-art effect.

**Category** : Filters · **Identifier** : `pixelSort` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/pixelSort)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose pixels are sorted by luminance. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Threshold, direction and sorted areas.](../../../../assets/modules/pixelSort/demo.en.webp)](../../../../assets/modules/pixelSort/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/pixelSort/demo.en.mp4) : Threshold, direction and sorted areas.

1. `0:00` Import an image
2. `0:02` Threshold of sorted areas
3. `0:05` Direction and areas
4. `0:09` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Set the threshold**

   It decides which areas get sorted.

3. **Pick direction and areas**

   Horizontal or vertical, highlights or shadows.

## Settings

| Setting | Effect |
| --- | --- |
| **Direction** | Horizontal or vertical. |
| **Sorted areas** | Highlights or shadows. |
| **Threshold** | 0 to 100% luminance. |
| **Reverse sort order** | Light to dark, or the other way round. |

## Tips

- Vertical sorting of highlights on a sky: light drips.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
