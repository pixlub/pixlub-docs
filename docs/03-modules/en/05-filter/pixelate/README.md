# Pixelate

Reduce an image to large pixels, pixel-art style.

**Category** : Filters · **Identifier** : `pixelate` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/pixelate)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image reduced to large pixels. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Pixel size.](../../../../assets/modules/pixelate/demo.en.webp)](../../../../assets/modules/pixelate/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/pixelate/demo.en.mp4) : Pixel size.

1. `0:00` Import an image
2. `0:02` Pixel size
3. `0:08` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Set the size**

   Type the pixel size, or drag along the bar.

## Settings

| Setting | Effect |
| --- | --- |
| **Pixel size** | 1 to 64 px. |

## Tips

- To hide an area (plate, face), pixelate and limit the effect with a mask in the [image graph](../../../../01-app/en/02-image/01-image-graph.md).

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
