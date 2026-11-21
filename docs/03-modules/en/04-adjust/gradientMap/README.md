# Gradient map

Recolour an image by replacing its lightness with the colours of a gradient.

**Category** : Adjustment · **Identifier** : `gradientMap` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/gradientMap)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose luminance is colorized by the gradient. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Pick a gradient, blend it, invert it.](../../../../assets/modules/gradientMap/demo.en.webp)](../../../../assets/modules/gradientMap/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/gradientMap/demo.en.mp4) : Pick a gradient, blend it, invert it.

1. `0:00` Import an image
2. `0:03` Pick a gradient
3. `0:09` Blend and invert
4. `0:16` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Pick the gradient**

   Open the **Gradient** field: take one from the collection, or edit its stops.

3. **Dose**

   The **blend** keeps part of the original image.

## Settings

| Setting | Effect |
| --- | --- |
| **Gradient** | Blacks take the left colour, whites the right one. |
| **Blend** | 0 to 100% of the effect. |
| **Invert luminance** | Lights take the start of the gradient. |
| **Apply the gradient alpha** | A transparent gradient stop makes the matching tones transparent. |

## Tips

- A two-colour vivid gradient gives a duotone look.
- For a single colour, [Recolour](../recolor/README.md) is simpler.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
