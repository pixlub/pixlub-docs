# Remove background

Cut out the subject of a photo with AI, whatever the background.

**Category** : API services · **Identifier** : `removeBgApi` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/removeBgApi)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image sent to the server, whose subject is detected and background made transparent. | `PNG`, `JPEG`, `WebP`, `GIF` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## How to use

1. **Sign in**

   The cut-out runs on our servers: an account is required.

2. **Import**

   Person, object, animal, product: the subject is found whatever the background.

3. **Run**

   The price in credits shows before running; the image comes back with a transparent background.

No settings: running the same file again gives the same result, and costs again.

## Touch up with the eraser

- The **Eraser** button of the preview turns it on: its options float over the image.
- Paint to remove what is left; **Restore** (or **Alt**) brings back what the cutout took away.
- The touch-up runs in your browser: it does not run the call again and costs nothing.
- **Erased areas in red** shows everything that was removed.

## Tips

- Export to PNG, WebP or AVIF to keep the transparency.
- For a single-colour background, [Remove solid background](../../05-filter/removeBg/README.md) does it in your browser, with no credits.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
