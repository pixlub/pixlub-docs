# Palette from image

Extract the dominant colours of an image.

**Category** : Generation · **Identifier** : `paletteFromImage` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/paletteFromImage)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose dominant colors are extracted. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Number of colours, then sorting.](../../../../assets/modules/paletteFromImage/demo.en.webp)](../../../../assets/modules/paletteFromImage/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/paletteFromImage/demo.en.mp4) : Number of colours, then sorting.

1. `0:00` Import an image
2. `0:02` Number of colours
3. `0:05` Sort the colours
4. `0:09` Export the result

## How to use

1. **Import**

   Drop one or more images: their dominant colours show as bands.

2. **Adjust**

   The **number** of colours and their **sorting**.

## Settings

| Setting | Effect |
| --- | --- |
| **Number of colors** | 2 to 32. |
| **Sort by** | Brightness, hue or frequency. |

## Tips

- Sort by **frequency** to see first the colours that dominate the image.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
