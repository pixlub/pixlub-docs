# Ripple

Warp an image into concentric rings, like a drop in water.

**Category** : Transformation · **Identifier** : `ripple` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/ripple)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image distorted by the ripple. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Amplitude, wavelength, phase and center.](../../../../assets/modules/ripple/demo.en.webp)](../../../../assets/modules/ripple/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/ripple/demo.en.mp4) : Amplitude, wavelength, phase and center.

1. `0:00` Import an image
2. `0:02` Amplitude and wavelength
3. `0:07` Phase
4. `0:12` Place the center
5. `0:14` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Set the waves**

   The **amplitude** sets their height, the **wavelength** the gap between two rings.

3. **Place the center**

   Click in the preview where the drop falls.

## Settings

| Setting | Effect |
| --- | --- |
| **Amplitude** | 0 to 200 px. |
| **Wavelength** | 2 to 500 px between two crests. |
| **Phase** | 0° to 360°. Moves the rings forward. |
| **Center X** / **Y** | Position of the center, in %. |

## Tips

- Animate the **phase** from 0° to 360° in the [image graph](../../../../01-app/en/02-image/01-image-graph.md) for waves that keep spreading in a loop.
- For straight waves instead of rings: [Wave](../wave/README.md).

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
