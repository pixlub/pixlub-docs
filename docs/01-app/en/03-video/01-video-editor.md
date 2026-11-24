# Video editor

Edit videos, sounds, images and texts in the browser: timeline, effects, transitions, subtitles and export.

The [video editor](https://pixlub.com/en/video/editor) is a complete editing tool that runs in your browser. Decoding, preview and encoding happen on your device; only **automatic subtitles** send the edit's audio to our servers.

## The interface

| Area | Role |
| --- | --- |
| Media | Your imported files (videos, sounds, images), texts, solids, transitions, compositions and recordings. |
| Preview | Playback of the edit, in **Project** or **Clip** view (the selected clip alone). |
| Panel | Settings of the selected clip, or of the project (size, frame rate, background). |
| Timeline | Video and audio tracks, clips, playhead and animation curves. |

## Editing

1. **Import**

   Drop videos, sounds or images into **Media**, or straight onto the timeline.

2. **Place on the timeline**

   Drag a media onto a track. Dropping it above the existing tracks creates a new line in front.

3. **Cut and arrange**

   Move clips, drag their edges to shorten them. **Snap guides** align clips with one another; holding <kbd>Ctrl</kbd> while dragging suspends them.

4. **Export**

   **Export** opens the export window: format (MP4, WebM, MOV…), size, quality. Encoding happens in the browser.

## Shortcuts

| Action | Shortcut |
| --- | --- |
| Play / Pause | <kbd>Space</kbd> |
| Previous / next frame | <kbd>←</kbd> / <kbd>→</kbd> |
| Back / forward 10 frames | <kbd>Shift</kbd> + <kbd>←</kbd> / <kbd>Shift</kbd> + <kbd>→</kbd> |
| Previous / next edit point | <kbd>Ctrl</kbd> + <kbd>←</kbd> / <kbd>Ctrl</kbd> + <kbd>→</kbd> |
| Start / end of the edit | <kbd>Home</kbd> / <kbd>End</kbd> |
| Loop playback | <kbd>L</kbd> |
| Mute | <kbd>M</kbd> |
| Split at the playhead | <kbd>S</kbd> |
| Trim start / end to the playhead | <kbd>Q</kbd> / <kbd>W</kbd> |
| Cut / Copy / Paste | <kbd>Ctrl</kbd> + <kbd>X</kbd> / <kbd>Ctrl</kbd> + <kbd>C</kbd> / <kbd>Ctrl</kbd> + <kbd>V</kbd> |
| Duplicate the clip | <kbd>Ctrl</kbd> + <kbd>D</kbd> |
| Select all | <kbd>Ctrl</kbd> + <kbd>A</kbd> |
| Delete the clip | <kbd>Del</kbd> |
| Detach audio | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>D</kbd> |
| Precompose | <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>C</kbd> |
| Undo / Redo | <kbd>Ctrl</kbd> + <kbd>Z</kbd> / <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Z</kbd> |
| Timeline zoom | <kbd>Ctrl</kbd> + <kbd>+</kbd> / <kbd>Ctrl</kbd> + <kbd>-</kbd> |
| Fit the timeline | <kbd>Shift</kbd> + <kbd>1</kbd> |
| Clip-only view | <kbd>Alt</kbd> + <kbd>V</kbd> |
| Snap guides | <kbd>Alt</kbd> + <kbd>G</kbd> |
| Monitor full frame | <kbd>F</kbd> |
| New project | <kbd>Alt</kbd> + <kbd>N</kbd> |
| Open a file / from storage | <kbd>Ctrl</kbd> + <kbd>O</kbd> / <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>O</kbd> |
| Save | <kbd>Ctrl</kbd> + <kbd>S</kbd> |
| Export | <kbd>Ctrl</kbd> + <kbd>E</kbd> |

Every command is also listed, with its shortcut, in the **File**, **Edit**, **Clip**, **Playback** and **View** menus of the top bar. The **MCP** menu shows the state of the link with a connected AI and opens its options.

A clip's context menu also offers **Copy**, **Cut**, **Paste**, **Split** and **Detach audio**.

## Tracks

Each track can be **hidden**, **muted**, **locked** or reordered by drag and drop. A video track has a **blend mode** with what lies behind it.

## Effects and animation

Video and image modules are placed as **effects** on a clip. Their settings are **animatable**: expand the effect in the timeline to set keyframes, then refine them in the **Curves** view or the **Dope sheet**.

## Texts, solids and transitions

- **Texts**: drop a text on a track, then set its font, styles and animations in the clip panel. A placed text composition is edited with a double-click.
- **Solids**: flat colors and shapes placed like a clip.
- **Effects**: ready-made visual effects to place above a clip — click ripples, swipes, lights, bursts, pointers, ambiences. Each one is a composition of shapes, particles and keyframes: a double-click opens it to change its colours, shapes or pacing.
- **Sounds**: nearly two hundred sound effects sorted by theme — clicks, interface, alerts, whooshes, impacts, risers, magic, retro game, sci-fi, cartoon, ambiences. A click plays the sound, a drag places it on a track. Every sound effect is synthesized in your browser: no file is downloaded, and no music is provided.
- **Transitions**: drop them on a cut between two touching clips, or at the start and end of a track. Two clips overlapping on the same track become a crossfade.

## Compositions

A **composition** is an edit inside the edit. Select clips and **Precompose** them to group them; open the composition to change it, then go back up through the trail of open compositions.

## Motion tracking

**Motion tracking** pins a text, an image or a shape to something that moves in a video or an animated image. The analysis runs in the browser: nothing is sent.

1. **Open the tool**

   Right-click the video, in the timeline or the preview, then **Tools → Motion tracking**. The same entry is in the **Edit** menu, and as an icon at the top of the preview when the selected clip allows it. The right panel then shows the tool; **Clip settings**, at the top, leaves it.

2. **Choose what to track**

   **Point** for an element that only moves, **Object** for an element that turns, comes closer or moves away, **Surface** for a flat surface seen at an angle (screen, poster, wall) whose four corners you place.

3. **Place the blue frame**

   A frame is already on the preview. Drag it onto the element and pull its corners around it: a contrasted zone tracks better than a flat area.

4. **Start tracking**

   **Start tracking** analyses the whole clip from the displayed frame. The bar shows what is tracked; click it to go to a frame.

5. **Attach an element**

   The clips placed above the video are listed: a switch attaches each one to the frame. The element keeps the place it has on the displayed frame, then follows; you can still move, scale or rotate it. **Orient along the path** turns it with the direction of travel, like an arrow on its path.

The frame is drawn and grabbed around the picture too: to frame an element that leaves the shot, zoom the preview out and pull its corners past the edge. In **Object** mode, the frame rotates when grabbed just outside a corner. On the timeline, a target icon marks the tracked clip, and a filled target the attached clip.

**If the frame loses the element** (it goes behind an obstacle, leaves the picture), tracking stops and the frame turns red. Move forward to the frame where the element comes back and put the frame on it: tracking resumes by itself, and the hidden stretch is filled in. To correct tracking that drifted, put the frame back on an image, then pick **Correct what follows** or **Correct before**.

### Adjusting a passage by hand

Tracking draws a **line**: the path followed by the centre of the frame. When it drifts, **Adjust by hand** lets you edit that line without running the analysis again. A tool palette then slides in at the top of the preview; the frame itself is no longer moved by hand — it stays reserved for automatic tracking.

The fastest way is to make **a whole passage** editable in one gesture: drag across the tracking bar in the panel (from 1 s to 3 s, for instance), or along the line with the **Section** tool. The passage becomes a single orange curve, held by a few points set where the trajectory changes; its shape does not move until you touch it.

- **Select**: drag a point to move it — the preview jumps to its frame, so you place it while seeing what it must follow. A selected point shows its two **handles**: drag them to set the curvature. <kbd>Shift</kbd> + click or a box drawn in empty space picks several points, which move together.
- **Point**: click the line to add a point. Inside a passage, the curve is split in two without changing shape.
- **Curve point** keeps both handles aligned; **Corner point** makes them independent (<kbd>Alt</kbd> while dragging a handle does the same).
- **Smooth** gives the selected points the handles of an even curve; **Delete** removes them, and where nothing covers it any more, the line goes back to the analysis.

If the first or last point of a passage moves away from the tracking, the neighbouring frames join it smoothly: no jump at the junction. The edited passage shows in orange on the line and in the bar. **Resume automatic tracking from here** restarts the analysis from the frame on screen, keeping your points; while scrubbing the timeline, the playhead sticks to nearby points.

### Attach to a clip

For an element animated with keys (a text, a shape, an image moving on the timeline), nothing needs analysing: **Tools → Attach to a clip** makes a clip take on another clip's motion. Pick the carrying clip, then what is taken on — **position** only, or **all the motion** (position, scale, rotation). The attached clip keeps the place it has on the first frame where both are visible; it can still be moved and animated, and can orient along the path.

### Linking two clips on the timeline

Each clip shows its tool icons at the bottom of its block. Drag a clip's **link** icon onto another clip to attach it there; drag a tracked clip's **target** icon onto another clip to attach that one to the tracked element (when the clip tracks several, a small menu asks which). During the gesture, only the clips overlapping the starting one stay in colour; releasing elsewhere changes nothing. A plain click on the icon opens the tool. In the panels, clicking a clip's name finds it in the timeline, where it glows for a moment.

## Subtitles

The **Subtitles** panel offers three starts:

- **Automatic subtitles**: the edit's audio is transcribed by our service. Pick the original language (or automatic detection); subtitles are written in the spoken language. The estimated cost, charged per started minute, shows before sending.
- **Import an SRT / VTT file**.
- **Write subtitles** by hand.

Lines are then edited one by one: split at the cursor, merge, assign a speaker, adjust each word's timing. **Export as .srt** saves the subtitle file.

> [!WARNING]
> **Sent to the server**
>
> As soon as the automatic subtitles panel is open, the privacy badge switches to **Sent to the server**: it is the only case where the video editor transmits content. See [Local and server processing](../06-privacy.md).

## Recording

The **Recording** tab captures the screen, the camera and the microphone, together or separately, with the camera inset in a corner. Everything is captured in the browser; takes join the media, ready to drag onto the edit.
