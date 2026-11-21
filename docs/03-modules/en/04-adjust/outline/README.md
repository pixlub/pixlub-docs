# Outline

Surround the silhouette of a cut-out image with a coloured line.

**Category** : Adjustment · **Identifier** : `outline` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/outline)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose silhouette (alpha) gets the outline. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Thickness, then outline colour.](../../../../assets/modules/outline/demo.en.webp)](../../../../assets/modules/outline/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/outline/demo.en.mp4) : Thickness, then outline colour.

1. `0:00` Import a cut-out image
2. `0:03` Thickness
3. `0:07` Colour
4. `0:12` Export the result

## How to use

1. **Import**

   Drop an image with transparency: the outline follows its silhouette.

2. **Adjust**

   Pick the **thickness**, then the **colour**.

## Settings

| Setting | Effect |
| --- | --- |
| **Thickness** | 0 to 100 px. |
| **Color** | Colour of the line. |

## Tips

- A thick white outline gives a sticker look; add [Shadow](../shadow/README.md) for depth.
- On an image without transparency, the outline only follows the frame edge.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
