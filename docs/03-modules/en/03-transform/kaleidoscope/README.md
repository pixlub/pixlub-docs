# Kaleidoscope

Repeat a slice of the image in symmetry around a center.

**Category** : Transformation · **Identifier** : `kaleidoscope` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/kaleidoscope)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose sector is repeated in radial symmetry. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Segments, rotation, mirror and center.](../../../../assets/modules/kaleidoscope/demo.en.webp)](../../../../assets/modules/kaleidoscope/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/kaleidoscope/demo.en.mp4) : Segments, rotation, mirror and center.

1. `0:00` Import an image
2. `0:03` Number of segments
3. `0:06` Rotation and mirror
4. `0:14` Place the center
5. `0:16` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Pick the segments**

   The more **segments**, the finer the pattern.

3. **Place the center**

   Click in the preview: the repeated slice starts from that point.

## Settings

| Setting | Effect |
| --- | --- |
| **Segments** | 1 to 64 slices around the center. |
| **Rotation** | −180° to 180°. Changes the slice of the image used. |
| **Mirror** | Checked: every other slice is flipped, the seams disappear. |
| **Center X** / **Y** | Position of the center, in %. |

## Tips

- 6 or 8 segments with the mirror give an even rosette pattern.
- A very colorful image gives the brightest patterns.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
