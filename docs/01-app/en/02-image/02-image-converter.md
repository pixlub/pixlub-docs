# Image converter

Change the format of one or more images: available formats, settings, local or server processing.

The [image converter](https://pixlub.com/en/image/convert) changes the format of your files with nothing to install. Each output format also has its own page, for example [convert to WebP](https://pixlub.com/en/image/convert/webp), which opens the tool with that format already chosen.

## Converting

1. **Drop your files**

   Drag one or more images into the drop zone, or click **Browse**. JPG, PNG, WebP, HEIC, GIF… and even videos, whose frame is extracted.

2. **Choose the format**

   Formats go from the most common to the most specialized. Settings adapt to the format: **quality** for compressed formats, **scale**, and **background** for formats without transparency.

3. **Download**

   Get the files one by one, or the whole batch in a ZIP archive.

## Local or server

| Format | Processing |
| --- | --- |
| PNG, JPG, WebP | Encoded by your browser: your images never leave your device. |
| AVIF, JPEG XL, HEIC, TIFF, ICO, PDF… | Encoded by our API: the badge switches to **Sent to the server** as soon as the format is chosen. |

Each format page says where it is encoded ("In your browser" or "By our API"), whether it keeps transparency and whether its compression is adjustable.

> [!TIP]
> **Transparency**
>
> A format without an alpha channel (JPG, BMP…) flattens the image onto the chosen **background** color. Keep PNG, WebP or AVIF to preserve transparency.

## Through the API

The same converter is the [`convert`](../../../03-modules/en/12-conversion/convert/api.md) module of the API: one file in the `in` field, the format in `params`.
