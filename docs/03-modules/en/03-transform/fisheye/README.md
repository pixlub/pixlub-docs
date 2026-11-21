# Lens distortion

Bulge an image like a fisheye, or pinch it into a pincushion.

**Category** : Transformation · **Identifier** : `fisheye` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/fisheye)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image bulged or pinched around the center. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Bulge, pinch, place the center.](../../../../assets/modules/fisheye/demo.en.webp)](../../../../assets/modules/fisheye/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/fisheye/demo.en.mp4) : Bulge, pinch, place the center.

1. `0:00` Import an image
2. `0:02` Bulge the image
3. `0:07` Pinch it
4. `0:11` Place the center
5. `0:13` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Set the intensity**

   Positive bulges the image; negative pinches it.

3. **Place the center**

   Click in the preview.

## Settings

| Setting | Effect |
| --- | --- |
| **Intensity** | −100 to 100%. Positive: bulge (fisheye). Negative: pinch (pincushion). |
| **Center X** / **Y** | Position of the center, in %. |

## Tips

- A small negative value corrects the bulge of a wide-angle lens.
- A strong positive value centered on a face gives a fun magnifier effect.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
