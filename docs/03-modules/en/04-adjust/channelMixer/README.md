# Channel mixer

Rebuild each channel of an image from the others.

**Category** : Adjustment · **Identifier** : `channelMixer` · [API reference](./api.md)

## Where to use it

- **[Module page](https://pixlub.com/en/module/channelMixer)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Image(s)** (required)<br />Image whose channels are remixed. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One or more: each image is processed on its own, with the same settings |

How many images are processed at once depends on your plan.

Through the API, the files and their formats are detailed in the [API view](./api.md).

## Video walkthrough

[![Rebuild the red, then the blue.](../../../../assets/modules/channelMixer/demo.en.webp)](../../../../assets/modules/channelMixer/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/channelMixer/demo.en.mp4) : Rebuild the red, then the blue.

1. `0:00` Import an image
2. `0:02` Rebuild the red
3. `0:11` Then the blue
4. `0:20` Export the result

## How to use

1. **Import**

   Drop one or more images.

2. **Pick the channel**

   The **Channel** menu picks the one being rebuilt.

3. **Dose its sources**

   Each slider sets how much of another channel it takes.

## Settings

| Setting | Effect |
| --- | --- |
| **Space** | RGB, Gray, CMYK or LAB. |
| **Channel** | Rebuilt channel; all apply together. |
| **Sources** | Share of each original channel, in %. |
| **Offset** | Lightens or darkens the channel as a whole. |
| **Blending** | Blend mode and opacity: how the adjustment sits on the original picture. |

## Tips

- Red taken from blue and blue taken from red: the colours swap, an infrared look.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

With several images, the button becomes **ZIP download**; the menu also offers separate files, or only the image on display.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
