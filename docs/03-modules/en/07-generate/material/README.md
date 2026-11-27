# Material

Builds a 3D material: physical surface and one texture per map (color, normals, roughness…). To be linked to a material of the “3D model” module.

**Category** : Generation · **Identifier** : `material`

## Where to use it

- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

The files the module page accepts: drop them on the import area, or click it to browse. A file in another format is set aside, with a message listing the allowed formats.

| Input | Accepted formats | Files |
| --- | --- | --- |
| **Base color** (optional)<br />Surface color; its transparency cuts the material out. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |
| **Normals** (optional)<br />Normal map: fine relief without changing the shape. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |
| **Roughness** (optional)<br />Grayscale: light = matte, dark = glossy. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |
| **Metalness** (optional)<br />Grayscale: white = metal, black = non-metal. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |
| **Emission** (optional)<br />What glows by itself, tinted by the emission color. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |
| **Occlusion** (optional)<br />Contact shadows in the crevices. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |
| **Opacity** (optional)<br />Grayscale: white = opaque, black = transparent. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |
| **Bump** (optional)<br />Heights in grayscale: light parts stand out. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | One file |

> [!NOTE]
> **Guide coming soon**
>
> This module has no detailed guide yet. Its settings show their description in the app; the API view lists each of them with its limits.
