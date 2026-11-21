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
| Split at the playhead | <kbd>S</kbd> |
| Duplicate the clip | <kbd>Ctrl</kbd> + <kbd>D</kbd> |
| Delete the clip | <kbd>Del</kbd> |
| Undo / Redo | <kbd>Ctrl</kbd> + <kbd>Z</kbd> / <kbd>Ctrl</kbd> + <kbd>Y</kbd> |

A clip's context menu also offers **Copy**, **Cut**, **Paste**, **Split** and **Detach audio**.

## Tracks

Each track can be **hidden**, **muted**, **locked** or reordered by drag and drop. A video track has a **blend mode** with what lies behind it.

## Effects and animation

Video and image modules are placed as **effects** on a clip. Their settings are **animatable**: expand the effect in the timeline to set keyframes, then refine them in the **Curves** view or the **Dope sheet**.

## Texts, solids and transitions

- **Texts**: drop a text on a track, then set its font, styles and animations in the clip panel. A placed text composition is edited with a double-click.
- **Solids**: flat colors and shapes placed like a clip.
- **Transitions**: drop them on a cut between two touching clips, or at the start and end of a track. Two clips overlapping on the same track become a crossfade.

## Compositions

A **composition** is an edit inside the edit. Select clips and **Precompose** them to group them; open the composition to change it, then go back up through the trail of open compositions.

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
