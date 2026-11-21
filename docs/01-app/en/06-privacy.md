# Local and server processing

What stays on your device, what goes to our servers, and how the privacy badge tells you.

Pixlub processes your files **in your browser**. It is a promise: as long as no remote operation is involved, your images, videos and documents never leave your device.

## The badge

Editing pages (module page, image graph, video editor, adjustment editor) show a badge at the bottom of the screen:

| Badge | Meaning |
| --- | --- |
| **Local processing** | Nothing leaves: everything is computed on your device. |
| **Sent to the server** | An operation on the page sends a file to our servers. Open the badge to see which one. |

The badge announces what the page **is about to** send, not only what has already gone: it switches as soon as you place an AI module, pick a server-encoded format or open automatic subtitles. It also keeps a history of what was already sent during the session. You can drag it; it docks to the nearest side.

## What goes to our servers

| Operation | What is sent |
| --- | --- |
| AI module (background removal, auto face blur, decal…) | The module's input image, and only the settings the service needs. |
| Export format encoded by the API (AVIF, HEIC, TIFF, PDF…) | The image to convert. |
| Automatic subtitles | The edit's audio. |
| Office or HTML to PDF conversion | The file to convert. |

An AI module's other settings stay on your device: changing them does not send anything again and does not make the result stale.

## What happens to sent files

The result is available through a signed link, valid for one hour; files are deleted from our servers after 24 hours. Usage statistics only keep the names of the modules used, and the size and kind of imported files, never their name or content.

For the details of our security measures, see the [Security](https://pixlub.com/en/security) page.
