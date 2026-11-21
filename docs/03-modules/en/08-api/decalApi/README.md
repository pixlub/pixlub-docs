# Decal

Drape an image over a photographed object, following its relief.

**Category** : API services · **Identifier** : `decalApi` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/decalApi)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Surface** (required)<br />Photo of the object whose 3D relief is rebuilt. It is the only image sent to the server. | `PNG`, `JPEG`, `WebP`, `GIF` | One file |
| **Artwork** (required)<br />Image placed and draped over the object. | `PNG`, `JPEG`, `WebP`, `GIF` | One file |

Through the API, the files and their formats are detailed in the [API view](./api.md).

## How to use

1. **Sign in**

   The relief is rebuilt by our servers: an account is required.

2. **Import**

   The **object photo**, then the **image to place** (a logo, a pattern).

3. **Run, then place**

   Only the photo is sent, once. Then place and adjust the image freely, without sending again.

## Settings

| Setting | Effect |
| --- | --- |
| **Placement** | Position, size, rotation and relief depth. |
| **Lighting** | Highlights and shadows, folds. |
| **Layer** | Opacity, blend mode, stay on the object. |

## Tips

- Moving or resizing the placed image costs nothing: only a new photo calls the server again.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
