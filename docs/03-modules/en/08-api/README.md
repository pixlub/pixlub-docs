# API services

| Module | Description | API |
| --- | --- | --- |
| [Remove background](./removeBgApi/README.md) | Detects the subject with AI (our services) and makes everything else transparent, whatever the background. | [API](./removeBgApi/api.md) |
| [Face blur](./faceBlurApi/README.md) | Blurs hand-drawn zones, or detects faces via AI (our services). Zones can be edited in the preview: create, move, resize, delete. | [API](./faceBlurApi/api.md) |
| [Decal](./decalApi/README.md) | Rebuilds the object's 3D relief via AI (our services), then drapes the image you place freely on top of it. Only the photo is sent, once; the placed image stays on your machine. | [API](./decalApi/api.md) |
| [Face blur (video)](./faceBlurVideoApi/README.md) | Blurs hand-drawn regions, or detects the faces on every frame through our API. Each region is tracked over time and can be adjusted in the preview, frame by frame. In automatic mode, detection is sent to the server once; the blur is always computed in the browser. | — |
| [Subtitles (video)](./transcribeVideoApi/README.md) | Transcribes the speech of a video through our API, word by word and timestamped, then burns the subtitles into the picture. Transcription is sent to the server once; styling stays computed in the browser. | — |
