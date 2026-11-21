# Brightness & Contrast

Lighten or darken an image and set its contrast.

**Category** : Adjustment · **Identifier** : `brightness` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/brightness)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose brightness and contrast are adjusted. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Brightness, contrast, blend mode and opacity.](../../../../assets/modules/brightness/demo.en.webp)](../../../../assets/modules/brightness/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/brightness/demo.en.mp4) : Brightness, contrast, blend mode and opacity.

1. `0:00` Import an image
2. `0:02` Brightness
3. `0:05` Contrast
4. `0:09` Blend mode
5. `0:12` Dose it with the opacity
6. `0:20` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Adjust**

   **Brightness** for the whole picture, **Contrast** for the gap between lights and darks.

## Settings

| Setting | Effect |
| --- | --- |
| **Brightness** | −100 to 100%, leaving contrast alone. |
| **Contrast** | −100% flattens the picture, +100% hardens it. |
| **Blending** | Blend mode and opacity: how the adjustment sits on the original picture. |

## Tips

- For finer tone control, see [Levels](../levels/README.md) or [Curves](../curves/README.md).

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
