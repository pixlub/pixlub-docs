# Image graph

Build an image by connecting modules: sources, effects, outputs, animation and .epxl projects.

The [image graph](https://pixlub.com/en/image/graph) is the most complete Pixlub editor. Each **module** becomes a node; you connect a node output to another node input to chain operations. Nothing is baked: changing an upstream setting recomputes the whole chain.

## Starting a project

On opening, a window offers three starts:

- **New project**: a blank canvas;
- **Import**: a `.epxl` project saved earlier, or a project from your [local folder](../05-account-and-credits.md#local-folder);
- **Discovery guides**: annotated mini-projects that show how to combine modules.

## Building the graph

1. **Add an image**

   Drag one or more images onto the canvas: each becomes a **Source image** module. Several images dropped together form a **batch**, processed at once.

2. **Add modules**

   The left shelf lists every module, with search and presets. Drag one onto the canvas, or right-click the canvas.

3. **Connect ports**

   Drag from a module output to another module input. A port only connects to a compatible type; the connection legend recalls the colors.

4. **Adjust**

   Click a module to open its panel. The **Settings** tab holds its settings; the **Properties** tab its title, color and preview display.

5. **Export**

   Connect the result to an **Output** module, then export in the format you want.

## Port types

| Port | What flows through it |
| --- | --- |
| Image | A color image, with transparency. |
| Channel | A grayscale image: an R, G, B or A channel, a mask. |
| Number | A value, from the **Values** modules (image size, addition…). |
| Color | A plain color. |
| Palette | A list of colors. |
| Batch | A set of images processed together. |
| Path | A vector path. |
| 3D model | A model, for the 3D modules. |

An unconnected **required** input is flagged on the node. A **Batch** port connected to a single input only uses one image of the batch; the preview lets you pick which.

## Organizing the canvas

- **Toolbar tools**: pan, lasso selection, grouping the selection into a **frame**, fit view and zoom.
- **Notes**: add a note from the shelf to annotate the graph (bold, italic).
- **Disabling** a module takes it out of the chain without deleting it: handy for comparisons.
- **Undo / Redo**: <kbd>Ctrl</kbd> + <kbd>Z</kbd> and <kbd>Ctrl</kbd> + <kbd>Y</kbd>.
- **Pause**: the top bar suspends image computation while you build a heavy graph.

## Previews and tools

A node preview shows in the canvas and, larger, in the panel. You can zoom, change the backdrop, isolate the alpha channel or a color channel. Several modules are handled directly in it: crop, rotation, perspective, pin warp, paths, blur zones…

> [!NOTE]
> **Reduced preview**
>
> To stay smooth, the preview may be computed at a lower resolution; the **Reduced preview** label says so. The export is always full resolution.

## Animation

The **Animation** mode in the top bar opens the time strip. Animated modules (particles, glows, ripples…) and animated settings play in a loop, and the export then offers animated formats: GIF, APNG or video.

## Saving and resuming

- **Save project** produces a `.epxl` file: modules, connections, settings, and the source images if you wish.
- **Import project** replaces the current graph with the one from a `.epxl` file.
- With a [local folder](../05-account-and-credits.md#local-folder) chosen in the settings, the graph is **saved automatically** there.

A project opened in a newer Pixlub version updates its modules; a module that no longer exists is flagged on its node.

## Performance

The **Settings** button in the top bar sets the recompute rate and the preview size (Fast, Normal, Optimized). **GPU acceleration** runs compatible modules on the graphics card through WebGPU, with an automatic fallback to the processor.

## AI modules in the graph

An AI module placed in the graph does not run on its own: it shows **Run request** with its price. If an upstream module changes, its result becomes **stale** and waits for you to run it again. See [Local and server processing](../06-privacy.md).
