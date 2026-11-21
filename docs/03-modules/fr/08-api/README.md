# Services API

| Module | Description | API |
| --- | --- | --- |
| [Retirer un fond](./removeBgApi/README.md) | Détecte le sujet par IA (par nos services) et rend transparent tout le reste, quel que soit le fond. | [API](./removeBgApi/api.md) |
| [Floutage de visages](./faceBlurApi/README.md) | Floute des zones tracées à la main, ou détecte les visages via IA (nos services). Les zones sont éditables dans la préview : créer, déplacer, redimensionner, supprimer. | [API](./faceBlurApi/api.md) |
| [Décalcomanie](./decalApi/README.md) | Reconstruit via IA (nos services) le relief 3D de l'objet, puis y drape l'image que vous placez librement dessus. Seule la photo est envoyée, une seule fois ; l'image posée reste sur votre machine. | [API](./decalApi/api.md) |
| [Floutage de visages (vidéo)](./faceBlurVideoApi/README.md) | Floute des zones tracées à la main, ou détecte les visages de chaque image via notre API. Chaque zone se suit dans le temps et s'ajuste dans l'aperçu, image par image. En mode automatique, la détection part au serveur une seule fois ; le floutage reste toujours calculé dans le navigateur. | — |
| [Sous-titres (vidéo)](./transcribeVideoApi/README.md) | Transcrit la parole d'une vidéo via notre API, mot à mot et horodatée, puis grave les sous-titres dans l'image. La transcription part au serveur une seule fois ; la mise en forme reste calculée dans le navigateur. | — |
