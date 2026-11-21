# Black and white

Turn an image grey while choosing how light each colour becomes.

**Category** : Adjustment · **Identifier** : `blackWhite` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/blackWhite)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image turned to black and white. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![The sky through blue, the facades through red and yellow.](../../../../assets/modules/blackWhite/demo.en.webp)](../../../../assets/modules/blackWhite/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/blackWhite/demo.en.mp4) : The sky through blue, the facades through red and yellow.

1. `0:00` Import an image
2. `0:03` Lighten the blue: the sky
3. `0:10` Red and yellow: the facades
4. `0:17` Export the result

## How to use

1. **Import**

   Drop one or more images: they turn grey.

2. **Dose each colour**

   A raised colour gets lighter in the grey, a lowered one darker.

## Settings

| Setting | Effect |
| --- | --- |
| **Red**, **Yellow**, **Green**, **Cyan**, **Blue**, **Magenta** | 0 to 100%: how light each colour becomes. |
| **Blending** | Blend mode and opacity: how the adjustment sits on the original picture. |

## Tips

- Lowering **blue** gives a dark, dramatic sky, like a red filter.
- Raising **red** and **yellow** lightens skin tones.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
