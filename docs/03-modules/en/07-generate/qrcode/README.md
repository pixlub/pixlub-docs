# QR code

Generate a QR code any reader can scan, styled, with a logo, or blended into an image.

**Category** : Generation · **Identifier** : `qrcode` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/qrcode)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Logo** (optional)<br />Optional image placed in the middle of the QR code; automatic correction rises to H. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |
| **Image** (optional)<br />Optional image turned into a QR code pattern the QR code blends into ("In an image" mode); its transparency gives the silhouette. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |

Through the API, the files and their formats are detailed in the [API view](./api.md).

## How to use

1. **Pick the content**

   Link, text, Wi-Fi, email, phone, SMS, contact (vCard) or location. Each type follows the format common readers understand.

2. **Style it**

   **Design** section, **Design, colors and decoration** button: a thumbnail gallery for the shape, body, eyes and colours. Fine settings (size, opacity, gradient…) stay in the panel.

3. **Add a logo**

   Connect an image to the **Logo** input: it sits in the middle, on a plate, and correction rises to H.

4. **Put it in a shape**

   **Blending** section, **In a shape** mode: cloche, heart, house, cloud, cup… or **From the image** for the silhouette of a connected image (its transparency, or its outline for a line drawing). The white, outlined silhouette fills with modules drawn like the QR code, which places itself; drag it in the preview, pull a corner for its size.

5. **Blend it into an image**

   **Blending** section, **In an image** mode, then connect an image (a fish, a logo…) to the **Image** input. It turns into a module pattern in the QR code style; drag the QR code inside it in the preview, pull a corner to change the module size.

## Settings

| Setting | Effect |
| --- | --- |
| **Type** | Link, text, Wi-Fi, email, phone, SMS, contact, location. |
| **Error correction** | Auto (M, or H with a logo or halftone), L, M, Q, H. |
| **Minimum version** / **Mask** | Finer or fixed grid; scrambling pattern. |
| **Modules** | Squares, fluid, dots, rounded squares, diamonds, stars, crosses, hearts, leaves, bars, confetti; size and roundness. |
| **Eyes** | Frame and center of the eyes and alignment patterns, own colours. |
| **Colors** | Module colour or gradient, background, opacities, background corners. |
| **Dimensions** | Image size and margin (4 modules per the standard). |
| **Logo** | Size, plate (square, rounded, round), padding, module clearing, opacity. **Safe size** brings the logo back to the largest size error correction can repair. |
| **Silhouette** | Shape, outline thickness and colour, pattern density. |
| **Placement** | Module size, QR code position, light halo around it, light rim around the eyes. |
| **Conversion** | QR pattern (default), threshold, diffusion or ordered; tone depth, variant, threshold, contrast, invert, silhouette and outline, module colour. |
| **Merge** | Image through the QR (halftone) and its strength, solid background under the QR, original image underneath. |

## Tips

- Always test the scan with several phones before printing.
- Keep the modules clearly darker than the background; a light code on a dark background is not read by every reader.
- For the eyes, keep one shape family between frame and center (square with square, round with round).
- In image mode, **QR pattern** turns the image into a QR code texture: with a 0 halo, the code melts into it with no edge. With **Module color: from the image**, pattern, QR code and eyes take the image colour under them.
- An oversized logo hides codewords: keep **Safe size** checked, and raise correction to H for a bigger logo.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
