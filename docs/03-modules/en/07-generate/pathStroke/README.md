# Path

Draw a freehand curve, smoothed and tapered.

**Category** : Generation · **Identifier** : `pathStroke`

## Where to use it

- **[Module page](https://pixlub.com/en/module/pathStroke)** : Drop your files, adjust, download: the module on its own, nothing else.
- **[Image graph](https://pixlub.com/en/image/graph)** : Connect it to other modules to build a richer effect.

## Inputs

This module has no input: it creates the image from its settings alone.

## Video walkthrough

[![Draw the path, thickness and taper, colour.](../../../../assets/modules/pathStroke/demo.en.webp)](../../../../assets/modules/pathStroke/demo.en.mp4)

▶ [Watch the video](../../../../assets/modules/pathStroke/demo.en.mp4) : Draw the path, thickness and taper, colour.

1. `0:00` The render shows right away
2. `0:01` Draw the path
3. `0:07` Thickness and taper
4. `0:13` Colour
5. `0:18` Export the result

## How to use

1. **Draw**

   Pick **Bézier** (rounded) or **linear** (sharp) points on the left of the preview, then click to place them; click on the line to insert one, on the first point to close the shape.

2. **Shape it**

   Drag the points: they snap to the other points and the center, **Shift** guides them in 15° steps. Orange handles set the curvature, green squares the local thickness.

3. **Set the stroke**

   **Thickness**, **taper** and **colour**.

## Settings

| Setting | Effect |
| --- | --- |
| **Color** / **Thickness** | Stroke look, 1 to 200 px. |
| **Taper** | Thinning at the ends, 0 to 100%. |
| **Corner radius** | Strength of the curves at Bézier points; 50% = exact circular arcs. |
| **Closed loop** | Links the last point to the first. |
| **Points** | Position, local thickness and type (**Bézier** or **linear**) of each point; in the graph, each point's X, Y and thickness can be animated. |
| **Dimensions** | Area size. |

## Tips

- Place a few points in a ring, then **Perfect circle**; **Even out points** regularises a shape already drawn.
- A double-click on a point removes it; **Alt** breaks the curvature, **Ctrl** keeps it symmetric, **Ctrl+Z** undoes.

## Export

The **Download** button saves the result in the format of the imported file: a JPEG photo comes out as JPEG. The menu on its right opens the **Export settings** to pick another format, set the quality, size or background, and offers **Copy image**.

- **[The export dialog](../../../../01-app/en/02-image/04-exportation.md)** : Every format, its settings, local or server processing, batches and the local folder.
