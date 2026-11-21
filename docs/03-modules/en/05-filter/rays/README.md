# Light rays

Make rays of light burst from an image's bright areas.

**Category** : Filters · **Identifier** : `rays` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/rays)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose bright areas cast the rays. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Length, intensity, center, then rays only.](../../../../assets/modules/rays/demo.en.webp)](../../../../assets/modules/rays/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/rays/demo.en.mp4) : Length, intensity, center, then rays only.

1. `0:00` Import an image
2. `0:02` Length and intensity
3. `0:09` Place the center
4. `0:11` Rays only
5. `0:13` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Set the rays**

   Length, intensity and **threshold**: only brighter areas emit.

3. **Place the source**

   Click in the preview where the light comes from.

## Settings

| Setting | Effect |
| --- | --- |
| **Length** | 5 to 100%. |
| **Intensity** | 0 to 200%. |
| **Brightness threshold** | 0 to 100%: areas that emit. |
| **Rays only** | Shows the rays without the image. |
| **Center X** / **Y** | Position of the source, in %. |

## Tips

- Put the source on the sun or a window for a natural "god rays" effect.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
