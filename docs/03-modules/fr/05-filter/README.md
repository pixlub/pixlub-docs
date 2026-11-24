# Filtres

| Module | Description | API |
| --- | --- | --- |
| [Flou](./blur/README.md) | Flou gaussien, de mouvement, de rotation ou de zoom (centre interactif) | [API](./blur/api.md) |
| [Flou de mouvement](./motionBlur/README.md) | Flou directionnel, zoom ou rotation (vitesse, traînées, impacts) | [API](./motionBlur/api.md) |
| [Netteté](./sharpen/README.md) | Renforce les détails et les contours (masque flou) | [API](./sharpen/api.md) |
| [Débruitage](./denoise/README.md) | Réduit le bruit en préservant les contours (filtre médian) | [API](./denoise/api.md) |
| [Détection de contours](./edgeDetect/README.md) | Extrait les contours (Sobel) avec double seuil, couleurs et pré-flou | [API](./edgeDetect/api.md) |
| [Aberration chromatique](./chromatic/README.md) | Décale les canaux rouge et bleu (effet lentille, glitch, impact) | [API](./chromatic/api.md) |
| [Dilater / Éroder](./morphology/README.md) | Épaissit ou contracte les zones opaques (masques, contours, silhouettes) | [API](./morphology/api.md) |
| [Carte de normales](./normalMap/README.md) | Génère une normal map depuis une heightmap (relief pour moteurs 3D / VFX) | [API](./normalMap/api.md) |
| [Pixeliser](./pixelate/README.md) | Réduit l'image en gros pixels (effet pixel art) | [API](./pixelate/api.md) |
| [Demi-teinte](./halftone/README.md) | Trame de points, tramage ordonné (Bayer) ou diffusion d'erreur (rétro / print) | [API](./halftone/api.md) |
| [Peinture](./kuwahara/README.md) | Aplats picturaux qui préservent les contours (filtre de Kuwahara, effet huile) | [API](./kuwahara/api.md) |
| [Tri de pixels](./pixelSort/README.md) | Trie les pixels par luminance dans les zones claires ou sombres (glitch art) | [API](./pixelSort/api.md) |
| [Scanlines CRT](./scanlines/README.md) | Lignes de balayage et masque RVB façon écran cathodique | [API](./scanlines/api.md) |
| [Rayons lumineux](./rays/README.md) | Rayons volumétriques émis par les zones claires depuis un centre (god rays) | [API](./rays/api.md) |
| [Contour progressif](./feather/README.md) | Adoucit les bords de la transparence (fondu du masque alpha) | [API](./feather/api.md) |
| [Vignette](./vignette/README.md) | Assombrit progressivement les bords de l'image | [API](./vignette/api.md) |
| [Bloom](./bloom/README.md) | Diffuse les zones lumineuses en halo additif (glow) | [API](./bloom/api.md) |
| [Retirer un fond uni](./removeBg/README.md) | Rend transparent un fond d'une seule couleur (fond vert, studio…), détectée ou choisie. | [API](./removeBg/api.md) |
| [Séparer RVB](./splitRgb/README.md) | Sépare l'image en ses canaux Rouge, Vert et Bleu | [API](./splitRgb/api.md) |
| [Séparer transparence](./splitAlpha/README.md) | Sépare l'image en son canal couleur (RVB opaque) et son canal alpha (niveaux de gris) | [API](./splitAlpha/api.md) |
| [Paillettes](./glitter/README.md) | Couvre l'image de paillettes qui scintillent : facettes irisées, étoiles et reflet, en boucle. | [API](./glitter/api.md) |
