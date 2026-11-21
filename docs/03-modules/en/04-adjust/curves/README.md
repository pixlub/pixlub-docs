# Curves

Adjust an image's tones with a curve, on every channel or just one.

**Category** : Adjustment · **Identifier** : `curves` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/curves)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose tones are adjusted by the curves. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![S curve, ready-made curves, a single channel.](../../../../assets/modules/curves/demo.en.webp)](../../../../assets/modules/curves/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/curves/demo.en.mp4) : S curve, ready-made curves, a single channel.

1. `0:00` Import an image
2. `0:02` S curve: more contrast
3. `0:09` Ready-made curves
4. `0:13` One channel at a time
5. `0:21` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Pull the curve**

   Drag a point of the curve: up lightens the tones, down darkens them.

3. **Or start from a preset**

   The menu below the curve offers ready-made curves.

## Settings

| Setting | Effect |
| --- | --- |
| **Space** | RGB, Gray, CMYK or LAB. |
| **Channel** | Master (every channel) or a single one. All curves apply together. |
| **Curve** | Horizontal axis: original value. Vertical axis: the value it takes. |
| **Blending** | Blend mode and opacity: how the adjustment sits on the original picture. |

## Tips

- An **S** curve (shadows down, highlights up) adds contrast without clipping.
- Raising the start of the curve gives faded blacks, a film look.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
