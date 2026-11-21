# Painting

Turn an image into painted flat areas that keep their edges.

**Category** : Filters · **Identifier** : `kuwahara` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/kuwahara)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image turned into painterly flat areas. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Brush size.](../../../../assets/modules/kuwahara/demo.en.webp)](../../../../assets/modules/kuwahara/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/kuwahara/demo.en.mp4) : Brush size.

1. `0:00` Import an image
2. `0:04` Brush size
3. `0:07` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Set the brush**

   The larger it is, the wider the flat areas.

## Settings

| Setting | Effect |
| --- | --- |
| **Brush size** | 2 to 16 px. |

## Tips

- Add [Sharpness](../sharpen/README.md) afterwards for a stronger oil-paint look.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
