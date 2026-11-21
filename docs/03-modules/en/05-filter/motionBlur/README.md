# Motion blur

Add a sense of speed: linear streak, zoom or spin.

**Category** : Filters · **Identifier** : `motionBlur` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/motionBlur)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image the motion blur is applied to. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Linear streak, then zoom and spin.](../../../../assets/modules/motionBlur/demo.en.webp)](../../../../assets/modules/motionBlur/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/motionBlur/demo.en.mp4) : Linear streak, then zoom and spin.

1. `0:00` Import an image
2. `0:02` Linear streak
3. `0:09` Zoom and spin
4. `0:13` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Pick the mode**

   **Linear**, **Zoom** or **Spin**.

3. **Dose**

   The **intensity**, and the **angle** in linear mode.

## Settings

| Setting | Effect |
| --- | --- |
| **Mode** | Linear, zoom or spin. |
| **Intensity** | 0 to 100%. |
| **Angle** | Linear mode: streak direction, −180° to 180°. |

## Tips

- Align the angle with the subject's direction for a believable sense of speed.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
