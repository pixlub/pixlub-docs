# Standalone module

Use a module on its own page: drop your files, adjust, download.

Every module that can be fed with a plain file has its own page, at `/module/<id>`: for example [Resize](https://pixlub.com/en/module/resize) or [Blur](https://pixlub.com/en/module/blur). It is the fastest way to apply one operation, without building a graph.

## Using a module

1. **Open the module**

   From the home page, the tools menu or the [module list](./02-image/README.md). Each module page in the [Modules](../../03-modules/en/README.md) section also links to it.

2. **Drop your files**

   Click the drop zone or drag your files onto it. They fill the module inputs.

3. **Adjust**

   The options panel, on the right, groups settings by section. The preview recomputes on every change. **Reset** brings the module back to its defaults.

4. **Get the result**

   **Download** opens the [export dialog](./02-image/04-exportation.md): pick the format and its settings, the preview already shows the result, then **Export**. Its menu offers a **quick download** as PNG and **Copy image**, which puts it on the clipboard.

## Processing several images

Drop several images into the same input: the module processes all of them with the same settings. The preview arrows move from one image to the next.

The inputs column sorts the images into **workspaces**, one box per workspace, each with its own settings. A badge tells how many images a workspace holds.

- Click a workspace to open it: the panel shows its settings and its images unfold horizontally in a menu.
- In that menu, the **+** adds an image to the workspace: it gets the same settings.
- **New workspace**, below the column, adds images with their own settings, one workspace per image.
- The **Split** button of an image in the menu moves it into a new workspace.

The export renders each image with its workspace's settings. The export dialog shows them all, with their dimensions and file size, and its **Batch** section picks the delivery:

- **ZIP archive**: every image in one archive;
- **Separate files**: one file per image.

The number of files per batch depends on your plan: see [Account and credits](./05-account-and-credits.md).

## Output size

The options panel has two tabs: **Property** for the module settings, **Settings** for the size of the rendered image.

| Method | Output size |
| --- | --- |
| **Module** (default) | The one the module produces. |
| **Source** | The one of the incoming image. |
| **Custom** | The width and height you type. |

In **Source** and **Custom**, the **fit** places the output: **None** (cropped), **Contain**, **Cover** or **Stretch**, attached by the **anchor**.

## Page variants

The page adapts to the module media:

| Media | What changes |
| --- | --- |
| Image | Preview with an adjustable backdrop (checkerboard, plain color). |
| Video | Player; decoding, rendering and encoding in the browser. Nothing goes to a server. |
| Document | Reorderable file list, page preview, **Run** button. See [Documents](./04-document.md). |
| Conversion | Output format and its options. See the [converter](./02-image/02-image-converter.md). |

## AI modules

AI modules (background removal, automatic face blur, decal…) send the image to our servers. Their page:

- needs an **account**: without a session, it redirects to sign-in;
- shows the **price in credits** before running, and never reruns on its own: every new computation goes through a confirmation;
- switches the privacy badge to **Sent to the server** as soon as the module is ready to go.
