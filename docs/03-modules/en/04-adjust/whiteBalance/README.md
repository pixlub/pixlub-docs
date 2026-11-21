# White balance

Warm up or cool down an image and fix its green or magenta cast.

**Category** : Adjustment · **Identifier** : `whiteBalance` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/whiteBalance)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose white balance is corrected. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Warm up, cool down, fix the cast, dose.](../../../../assets/modules/whiteBalance/demo.en.webp)](../../../../assets/modules/whiteBalance/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/whiteBalance/demo.en.mp4) : Warm up, cool down, fix the cast, dose.

1. `0:00` Import an image
2. `0:02` Warm up or cool down
3. `0:10` Fix the colour cast
4. `0:14` Dose it with the opacity
5. `0:22` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Set the temperature**

   To the right the picture warms up, to the left it cools down.

3. **Fix the tint**

   When the picture leans green or magenta.

## Settings

| Setting | Effect |
| --- | --- |
| **White balance** | −100 (blue) to 100 (orange yellow). |
| **Tint** | −100 (green) to 100 (magenta). |
| **Blending** | Blend mode and opacity: how the adjustment sits on the original picture. |

## Tips

- A photo shot under a light bulb leans yellow: cool it down a little.
- To set the light as well, [Basic adjustment](../baseAdjust/README.md) has it all.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
