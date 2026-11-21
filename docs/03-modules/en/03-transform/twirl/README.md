# Swirl

Twist an image into a spiral around a center.

**Category** : Transformation · **Identifier** : `twirl` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/twirl)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image twisted into a spiral. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Angle, radius, concentration and center.](../../../../assets/modules/twirl/demo.en.webp)](../../../../assets/modules/twirl/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/twirl/demo.en.mp4) : Angle, radius, concentration and center.

1. `0:00` Import an image
2. `0:03` Twirl angle
3. `0:06` Radius and concentration
4. `0:13` Place the center
5. `0:15` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Twist**

   The **angle** sets how many turns, the **radius** the size of the swirl.

3. **Place the center**

   Click in the preview.

## Settings

| Setting | Effect |
| --- | --- |
| **Angle** | −720° to 720°. The sign picks the direction. |
| **Radius** | 1 to 150%: area affected around the center. |
| **Concentration** | 1 to 4. High: the twist tightens at the center. |
| **Center X** / **Y** | Position of the center, in %. |

## Tips

- A small angle (30° to 90°) is enough for swirling water.
- For a magnifier look instead of a spiral: [Lens distortion](../fisheye/README.md).

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
