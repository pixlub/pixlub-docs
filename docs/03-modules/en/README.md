# Modules

Every Pixlub module, by category. Each page has two views: usage on the site, and the API reference.

Each module has its own page, in two views:

- **App**: where to find the module on the site and how to use it, with a hand-written guide when there is one.
- **API**: the endpoint, expected files, every setting with its type, limits and default value, and request examples in cURL, JavaScript, Python and with the SDKs. This view is **generated** from the module registry: it follows every new release with no manual update.

Modules marked **API** can be called through the [API](../../02-api/en/01-getting-started.md); the others (video, documents, graph building blocks) are used on the site.

## Base modules

| Module | Description | API |
| --- | --- | --- |
| [Source image](./01-base/source/README.md) | Loads an image from a file and feeds it to the graph. | — |
| [Preview](./01-base/preview/README.md) | Displays the image and passes it through unchanged. The node grows when you zoom out for a better overview. | — |

## Output

| Module | Description | API |
| --- | --- | --- |
| [Export](./02-output/output/README.md) | Previews and exports the resulting image. | — |
| [Export a batch](./02-output/exportBatch/README.md) | Downloads every image of a batch: an archive, separate files or an animation. | — |

## Transformation

| Module | Description | API |
| --- | --- | --- |
| [Resize](./03-transform/resize/README.md) | Changes the image dimensions | [API](./03-transform/resize/api.md) |
| [Resize (Factor)](./03-transform/resizeFactor/README.md) | Scales the image by a multiplication factor | [API](./03-transform/resizeFactor/api.md) |
| [Extend](./03-transform/extend/README.md) | Enlarges the image area without distorting the content | [API](./03-transform/extend/api.md) |
| [Trim](./03-transform/crop/README.md) | Crops an area of the image | [API](./03-transform/crop/api.md) |
| [Auto crop](./03-transform/trim/README.md) | Automatically trims transparent edges | [API](./03-transform/trim/api.md) |
| [Rotation](./03-transform/rotate/README.md) | Rotates the image | [API](./03-transform/rotate/api.md) |
| [Mirror](./03-transform/flip/README.md) | Flips the image horizontally and/or vertically | [API](./03-transform/flip/api.md) |
| [Distortion](./03-transform/skew/README.md) | Skews the image (horizontal and vertical shear) | [API](./03-transform/skew/api.md) |
| [Corner pin](./03-transform/cornerPin/README.md) | Moves the four corners of the image freely to put it in perspective | [API](./03-transform/cornerPin/api.md) |
| [Sticker peel](./03-transform/sticker/README.md) | Peels the image off like a sticker, curling it in a chosen direction | [API](./03-transform/sticker/api.md) |
| [Translate](./03-transform/translate/README.md) | Moves the texture in X and Y, in % of the image | [API](./03-transform/translate/api.md) |
| [Transform](./03-transform/transform/README.md) | Moves, rotates, scales, mirrors and fades the image in one go | [API](./03-transform/transform/api.md) |
| [Puppet](./03-transform/puppet/README.md) | Warps the image by moving pins on a mesh (puppet warp) | [API](./03-transform/puppet/api.md) |
| [Polar](./03-transform/polar/README.md) | Converts between rectangular and polar coordinates (rings, rays, halos) | [API](./03-transform/polar/api.md) |
| [Ripple](./03-transform/ripple/README.md) | Distortion in concentric rings around a center | [API](./03-transform/ripple/api.md) |
| [Displacement](./03-transform/displace/README.md) | Warps the image using a displacement map (noise, gradient…) | [API](./03-transform/displace/api.md) |
| [Texture remap](./03-transform/remap/README.md) | Redraws the image by reading, for each pixel, the position given by a map (gradient, noise…) | [API](./03-transform/remap/api.md) |
| [Kaleidoscope](./03-transform/kaleidoscope/README.md) | Repeats a sector in radial symmetry | [API](./03-transform/kaleidoscope/api.md) |
| [Swirl](./03-transform/twirl/README.md) | Twists the image into a spiral around a center | [API](./03-transform/twirl/api.md) |
| [Wave](./03-transform/wave/README.md) | Sinusoidal horizontal / vertical displacement | [API](./03-transform/wave/api.md) |
| [Lens distortion](./03-transform/fisheye/README.md) | Bulges (fisheye) or pinches (pincushion) the image around a center | [API](./03-transform/fisheye/api.md) |
| [Seam offset](./03-transform/tile/README.md) | Offsets the image with wrapping : check and build tileable textures | [API](./03-transform/tile/api.md) |
| [Bend along path](./03-transform/warpPath/README.md) | Warps an image along a path (ribbon / curved trail) | [API](./03-transform/warpPath/api.md) |
| [Follow path](./03-transform/followPath/README.md) | Moves an image along a path, from 0% to 100% of its length; the path may leave the frame | [API](./03-transform/followPath/api.md) |
| [Trim](./03-transform/trimVideo/README.md) | Trims a portion of the video at a given time. | — |
| [Speed](./03-transform/speedVideo/README.md) | Speeds the video up or down. The output frame rate stays the same: what changes is which frames are pulled from the source. | — |
| [Frame rate](./03-transform/frameRateVideo/README.md) | Rewrites the video frame rate. Lowering it shrinks the file; raising it above the source duplicates frames. | — |

## Adjustment

| Module | Description | API |
| --- | --- | --- |
| [Basic adjustment](./04-adjust/baseAdjust/README.md) | The essential photo settings in one place: light, tones, white balance and colours | [API](./04-adjust/baseAdjust/api.md) |
| [Levels](./04-adjust/levels/README.md) | Adjusts the black and white points, gamma and output range, per channel | [API](./04-adjust/levels/api.md) |
| [White balance](./04-adjust/whiteBalance/README.md) | Warms or cools the picture and corrects its green or magenta cast | [API](./04-adjust/whiteBalance/api.md) |
| [Recolour](./04-adjust/recolor/README.md) | Tints the whole picture with a single colour, keeping its shadows and highlights | [API](./04-adjust/recolor/api.md) |
| [HSL](./04-adjust/hsl/README.md) | Shifts the hue, saturation and lightness of a colour range | [API](./04-adjust/hsl/api.md) |
| [Black and white](./04-adjust/blackWhite/README.md) | Turns the picture grey, setting how light each colour becomes | [API](./04-adjust/blackWhite/api.md) |
| [Brightness & Contrast](./04-adjust/brightness/README.md) | Adjusts brightness and contrast | [API](./04-adjust/brightness/api.md) |
| [Posterize](./04-adjust/posterize/README.md) | Reduces the number of levels per channel (stylized flats, cel shading) | [API](./04-adjust/posterize/api.md) |
| [Exposure](./04-adjust/exposure/README.md) | Raises or lowers the light of the picture, stop by stop like a camera | [API](./04-adjust/exposure/api.md) |
| [Curves](./04-adjust/curves/README.md) | Adjusts tone with an editable curve, per channel or global | [API](./04-adjust/curves/api.md) |
| [Saturation / hue curves](./04-adjust/hueSatCurves/README.md) | Sets saturation or hue according to the luminance, saturation or hue of each colour | [API](./04-adjust/hueSatCurves/api.md) |
| [Channel mixer](./04-adjust/channelMixer/README.md) | Rebuilds each channel from the others, in the chosen space | [API](./04-adjust/channelMixer/api.md) |
| [Invert](./04-adjust/invert/README.md) | Turns the picture into its negative | [API](./04-adjust/invert/api.md) |
| [Color balance](./04-adjust/colorBalance/README.md) | Adjusts hues per tonal range (highlights, midtones, shadows), maskable | [API](./04-adjust/colorBalance/api.md) |
| [Accessibility filter](./04-adjust/colorAccessibility/README.md) | Corrects colours so they stay readable for colour-blind vision | [API](./04-adjust/colorAccessibility/api.md) |
| [Palette: recolor](./04-adjust/paletteRemap/README.md) | Generates a recolored variant of the image for each palette color (batch) | [API](./04-adjust/paletteRemap/api.md) |
| [Threshold](./04-adjust/threshold/README.md) | Binarizes luminance against a threshold (with a soft transition) | [API](./04-adjust/threshold/api.md) |
| [Replace colors](./04-adjust/replaceColors/README.md) | Replaces a list of source colors with target colors | [API](./04-adjust/replaceColors/api.md) |
| [Opacity](./04-adjust/opacity/README.md) | Changes the image opacity | [API](./04-adjust/opacity/api.md) |
| [Outline](./04-adjust/outline/README.md) | Adds an outline to the image | [API](./04-adjust/outline/api.md) |
| [Shadow](./04-adjust/shadow/README.md) | Casts a shadow (outer or inner) from the image alpha | [API](./04-adjust/shadow/api.md) |
| [Gradient map](./04-adjust/gradientMap/README.md) | Colorizes the image by mapping its luminance onto a gradient | [API](./04-adjust/gradientMap/api.md) |

## Filters

| Module | Description | API |
| --- | --- | --- |
| [Blur](./05-filter/blur/README.md) | Gaussian, motion, spin or zoom blur (interactive center) | [API](./05-filter/blur/api.md) |
| [Motion blur](./05-filter/motionBlur/README.md) | Directional, zoom or spin blur (speed, trails, impacts) | [API](./05-filter/motionBlur/api.md) |
| [Sharpness](./05-filter/sharpen/README.md) | Enhances details and edges (unsharp mask) | [API](./05-filter/sharpen/api.md) |
| [Denoise](./05-filter/denoise/README.md) | Reduces noise while preserving edges (median filter) | [API](./05-filter/denoise/api.md) |
| [Edge detection](./05-filter/edgeDetect/README.md) | Extracts edges (Sobel) with dual threshold, colors and pre-blur | [API](./05-filter/edgeDetect/api.md) |
| [Chromatic aberration](./05-filter/chromatic/README.md) | Shifts the red and blue channels (lens effect, glitch, impact) | [API](./05-filter/chromatic/api.md) |
| [Dilate / Erode](./05-filter/morphology/README.md) | Thickens or shrinks opaque areas (masks, outlines, silhouettes) | [API](./05-filter/morphology/api.md) |
| [Normal map](./05-filter/normalMap/README.md) | Generates a normal map from a heightmap (relief for 3D engines / VFX) | [API](./05-filter/normalMap/api.md) |
| [Pixelate](./05-filter/pixelate/README.md) | Reduces the image to large pixels (pixel art effect) | [API](./05-filter/pixelate/api.md) |
| [Halftone](./05-filter/halftone/README.md) | Dot screen, ordered dithering (Bayer) or error diffusion (retro / print) | [API](./05-filter/halftone/api.md) |
| [Painting](./05-filter/kuwahara/README.md) | Painterly flat areas that preserve edges (Kuwahara filter, oil effect) | [API](./05-filter/kuwahara/api.md) |
| [Pixel sorting](./05-filter/pixelSort/README.md) | Sorts pixels by luminance in bright or dark areas (glitch art) | [API](./05-filter/pixelSort/api.md) |
| [CRT scanlines](./05-filter/scanlines/README.md) | Scan lines and RGB mask in CRT screen style | [API](./05-filter/scanlines/api.md) |
| [Light rays](./05-filter/rays/README.md) | Volumetric rays emitted by bright areas from a center (god rays) | [API](./05-filter/rays/api.md) |
| [Feather](./05-filter/feather/README.md) | Softens transparency edges (alpha mask fade) | [API](./05-filter/feather/api.md) |
| [Vignette](./05-filter/vignette/README.md) | Progressively darkens the image edges | [API](./05-filter/vignette/api.md) |
| [Bloom](./05-filter/bloom/README.md) | Diffuses bright areas into an additive halo (glow) | [API](./05-filter/bloom/api.md) |
| [Remove solid background](./05-filter/removeBg/README.md) | Makes a single-color background (green screen, studio…) transparent, detected or picked. | [API](./05-filter/removeBg/api.md) |
| [Split RGB](./05-filter/splitRgb/README.md) | Splits the image into its Red, Green and Blue channels | [API](./05-filter/splitRgb/api.md) |
| [Split transparency](./05-filter/splitAlpha/README.md) | Splits the image into its color channel (opaque RGB) and its alpha channel (grayscale) | [API](./05-filter/splitAlpha/api.md) |

## Composition

| Module | Description | API |
| --- | --- | --- |
| [Split channels](./06-compose/channelSplit/README.md) | Extracts the R, G, B and Alpha channels as channels (grayscale) | [API](./06-compose/channelSplit/api.md) |
| [Merge channels](./06-compose/channelMerge/README.md) | Rebuilds an image from R, G, B and/or Alpha channels | [API](./06-compose/channelMerge/api.md) |
| [Image to mask](./06-compose/imageToMask/README.md) | Converts an image into a mask channel (alpha, channel or luminance) | [API](./06-compose/imageToMask/api.md) |
| [Merge](./06-compose/merge/README.md) | Overlays one or more images (layers) on another | [API](./06-compose/merge/api.md) |
| [Merge transparency](./06-compose/mergeAlpha/README.md) | Recombines a color channel (RGB) and an alpha channel into a transparent image | [API](./06-compose/mergeAlpha/api.md) |
| [Sprite sheet](./06-compose/spriteSheet/README.md) | Assembles several images into a grid (flipbook, VFX atlas) | [API](./06-compose/spriteSheet/api.md) |
| [Layout](./06-compose/arrange/README.md) | Aligns several images side by side or stacked (banners, comparisons) | [API](./06-compose/arrange/api.md) |
| [Assemble a batch](./06-compose/arrayBatch/README.md) | Groups images and batches into a single batch | — |
| [Split a batch](./06-compose/arraySplitBatch/README.md) | Splits a batch into individual images | — |
| [Mask](./06-compose/mask/README.md) | Modulates an image's opacity by the luminance (or alpha) of a mask | [API](./06-compose/mask/api.md) |
| [Eraser](./06-compose/eraser/README.md) | Erases parts of the image by hand, with a palette of adjustable tips | [API](./06-compose/eraser/api.md) |
| [3D model merge](./06-compose/model3dMerge/README.md) | Renders a 3D model and overlays it on an image: position, rotation, scale. | — |

## Generation

| Module | Description | API |
| --- | --- | --- |
| [Noise](./07-generate/noise/README.md) | Generates procedural noise (Perlin, simplex, random, Voronoi, spots, cubist, shards) with post-processing and blending | [API](./07-generate/noise/api.md) |
| [Draw a mask](./07-generate/drawShape/README.md) | Draws precise shapes (curves) combined by add/subtract — mask output | — |
| [Solid](./07-generate/solid/README.md) | Generates a shape filled with a solid color or a gradient | [API](./07-generate/solid/api.md) |
| [Palette](./07-generate/palette/README.md) | Defines a color palette to reuse in the graph | — |
| [Palette from gradient](./07-generate/paletteFromGradient/README.md) | Samples a gradient into a fixed number of colors | — |
| [Palette from image](./07-generate/paletteFromImage/README.md) | Extracts the dominant colors of an image (median cut) | [API](./07-generate/paletteFromImage/api.md) |
| [3D model](./07-generate/model3d/README.md) | Imports a 3D model (GLB, GLTF, OBJ, FBX, STL): camera, materials and animation. To be merged onto an image with “3D model merge”. | — |
| [Pattern](./07-generate/checker/README.md) | Generates a repeating pattern: checkerboard, grid, dots, stripes, bricks, honeycomb | — |
| [Gradient](./07-generate/gradient/README.md) | Generates a linear, circular, radial or diamond gradient | — |
| [QR code](./07-generate/qrcode/README.md) | Generates a QR code any reader can scan (link, Wi-Fi, contact…), styled, with a logo, or blended into an image | [API](./07-generate/qrcode/api.md) |
| [Lens flare](./07-generate/flare/README.md) | Optical flare: core, star branches, chromatic halo and ghost reflections | — |
| [Radial glow](./07-generate/glow/README.md) | Generates a radial glow (core, glow, aura) with falloff control | — |
| [Lightning](./07-generate/lightning/README.md) | Generates a branching procedural lightning bolt between two points | — |
| [Path](./07-generate/pathStroke/README.md) | Draws a hand-drawn curve, smoothed and tapered | — |
| [Particles](./07-generate/particles/README.md) | Scatters a source image (or a mix of images from a batch) into particles (emission shape, trails, falloff), driven by a seed | [API](./07-generate/particles/api.md) |

## API services

| Module | Description | API |
| --- | --- | --- |
| [Remove background](./08-api/removeBgApi/README.md) | Detects the subject with AI (our services) and makes everything else transparent, whatever the background. | [API](./08-api/removeBgApi/api.md) |
| [Face blur](./08-api/faceBlurApi/README.md) | Blurs hand-drawn zones, or detects faces via AI (our services). Zones can be edited in the preview: create, move, resize, delete. | [API](./08-api/faceBlurApi/api.md) |
| [Decal](./08-api/decalApi/README.md) | Rebuilds the object's 3D relief via AI (our services), then drapes the image you place freely on top of it. Only the photo is sent, once; the placed image stays on your machine. | [API](./08-api/decalApi/api.md) |
| [Face blur (video)](./08-api/faceBlurVideoApi/README.md) | Blurs hand-drawn regions, or detects the faces on every frame through our API. Each region is tracked over time and can be adjusted in the preview, frame by frame. In automatic mode, detection is sent to the server once; the blur is always computed in the browser. | — |
| [Subtitles (video)](./08-api/transcribeVideoApi/README.md) | Transcribes the speech of a video through our API, word by word and timestamped, then burns the subtitles into the picture. Transcription is sent to the server once; styling stays computed in the browser. | — |

## Values

| Module | Description | API |
| --- | --- | --- |
| [Value](./09-operation/value/README.md) | Emits a constant numeric value. | — |
| [Addition](./09-operation/add/README.md) | Sum of two inputs (A + B). | — |
| [Subtraction](./09-operation/subtract/README.md) | Difference of two inputs (A - B). | — |
| [Multiply](./09-operation/multiply/README.md) | Product of two inputs (A × B). | — |
| [Division](./09-operation/divide/README.md) | Quotient of two inputs (A ÷ B), 0 if B = 0. | — |
| [Image size](./09-operation/size/README.md) | Width and height of the input image. | — |

## Text

| Module | Description | API |
| --- | --- | --- |
| [Text](./10-text/text/README.md) | Composes text: typography, solid or gradient color, a stack of styles and an animation. | — |
| [Text to image](./10-text/textRender/README.md) | Renders text into a chosen frame: size, anchor, background. | — |

## Colors

| Module | Description | API |
| --- | --- | --- |
| [Color](./11-color/color/README.md) | Emits a color (solid or gradient). | — |

## Conversion

| Module | Description | API |
| --- | --- | --- |
| [Audio extraction](./12-conversion/extractAudioVideo/README.md) | Pulls the soundtrack out of a video into an audio file: MP3, AAC, Opus, FLAC, WAV… or the original track as is, losslessly. | — |
| [Audio conversion](./12-conversion/convertAudio/README.md) | Converts a sound file to another format — MP3, AAC, Opus, Vorbis, FLAC, WAV or AIFF — with its bitrate, sample rate and channels, keeping the part you want. | — |
| [Conversion](./12-conversion/convert/README.md) | Converts images, animations, videos and sounds to any export format: PNG, JPG, WebP, GIF, MP4, WebM, MP3, FLAC, WAV, PDF… | [API](./12-conversion/convert/api.md) |

## Documents

| Module | Description | API |
| --- | --- | --- |
| [Merge PDFs](./13-document/docMerge/README.md) | Combines several PDFs into a single file, in the order you choose. | — |
| [Split a PDF](./13-document/docSplit/README.md) | Splits a PDF into several files: page by page, in batches, at the marks placed on the preview or by your own ranges. Exported as PDF or images. | — |
| [Organize pages](./13-document/docPages/README.md) | Keeps, deletes, reorders, duplicates or rotates the pages of a PDF. | — |
| [Crop a PDF](./13-document/docCrop/README.md) | Trims a margin around the pages, without touching their content: the same everywhere, or specific to some pages. | — |
| [Number pages](./13-document/docPageNumbers/README.md) | Adds a number to each page, where and how you want it. | — |
| [Watermark](./13-document/docWatermark/README.md) | Lays translucent text or an image over the pages, once or as a tiled pattern. | — |
| [Metadata](./13-document/docMetadata/README.md) | Reads and edits the title, author, subject and keywords of a PDF, or wipes them. | — |
| [Sign a PDF](./13-document/docSign/README.md) | Places your signature, drawn or imported, on the pages you choose. | — |
| [Images to PDF](./13-document/docImagesToPdf/README.md) | Combines images into a PDF: lay out your pages, one or more images each, placed wherever you want. | — |
| [PDF to images](./13-document/docPdfToImages/README.md) | Exports each page as PNG, JPEG or WebP, at the chosen resolution. | — |
| [PDF to Word](./13-document/docPdfToWord/README.md) | Carries the headings, paragraphs and tables of a PDF into an editable Word document. | — |
| [PDF to Excel](./13-document/docPdfToExcel/README.md) | Lays out the content of a PDF in a workbook: aligned columns become columns, numbers become numbers. | — |
| [Office to PDF](./13-document/docOfficeToPdf/README.md) | Converts a Word, Excel, PowerPoint or OpenDocument file to PDF. | — |
| [HTML to PDF](./13-document/docHtmlToPdf/README.md) | Lays out an HTML file and renders it as a PDF, with selectable text. | — |
| [Compress a PDF](./13-document/docCompress/README.md) | Shrinks a PDF by re-encoding its images; the text stays sharp and selectable. | — |
| [Repair a PDF](./13-document/docRepair/README.md) | Rebuilds a damaged PDF or one that opens badly: object table, catalog and page tree. | — |
| [Protect a PDF](./13-document/docProtect/README.md) | Encrypts a PDF with AES-256 and a password, and limits what can be done with it. | — |
| [Unlock a PDF](./13-document/docUnlock/README.md) | Removes the password and restrictions of a protected PDF, if you know its password. | — |
| [Redact a PDF](./13-document/docRedact/README.md) | Blacks out the chosen words or patterns: the text truly disappears from the page. | — |
| [Extract text (OCR)](./13-document/docOcrText/README.md) | Reads the text of a PDF, a scan or a document photo, then exports it as plain text or a searchable PDF. | — |
| [Compare two PDFs](./13-document/docCompare/README.md) | Lists the lines added and removed page by page, and flags the pages whose look has changed. | — |
