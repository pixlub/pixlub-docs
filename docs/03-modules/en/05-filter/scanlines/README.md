# CRT scanlines

Lay scan lines and an RGB mask in a CRT screen style.

**Category** : Filters · **Identifier** : `scanlines` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/scanlines)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image the scanlines are laid over. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Spacing, intensity, then RGB mask.](../../../../assets/modules/scanlines/demo.en.webp)](../../../../assets/modules/scanlines/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/scanlines/demo.en.mp4) : Spacing, intensity, then RGB mask.

1. `0:00` Import an image
2. `0:04` Spacing and intensity
3. `0:09` RGB mask
4. `0:12` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Set the lines**

   **Spacing** and **intensity**.

3. **Add the RGB mask**

   The red, green and blue triads of an old screen.

## Settings

| Setting | Effect |
| --- | --- |
| **Spacing** | 2 to 40 px between lines. |
| **Intensity** | 0 to 100%. |
| **RGB mask (triads)** | Adds the colour grid. |

## Tips

- Combine with [Chromatic aberration](../chromatic/README.md) and [Vignette](../vignette/README.md) for a full retro screen look.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
