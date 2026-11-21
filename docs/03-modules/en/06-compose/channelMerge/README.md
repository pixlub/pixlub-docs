# Merge channels

Rebuilds an image from R, G, B and/or Alpha channels

**Category** : Composition · **Identifier** : `channelMerge` · [API reference](./api.md)

## Where to use it

- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **R** (optional)<br />Grayscale channel that becomes the image's red; when missing, red is 0. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |
| **G** (optional)<br />Grayscale channel that becomes the image's green; when missing, green is 0. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |
| **B** (optional)<br />Grayscale channel that becomes the image's blue; when missing, blue is 0. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |
| **A** (optional)<br />Grayscale channel that becomes the image's alpha; when missing, the image is opaque. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |

Through the API, the files and their formats are detailed in the [API view](./api.md).

> [!NOTE]
> **Guide coming soon**
>
> This module has no detailed guide yet. Its settings show their description in the app; the API view lists each of them with its limits.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
