# Génération

| Module | Description | API |
| --- | --- | --- |
| [Bruit](./noise/README.md) | Génère un bruit procédural (Perlin, simplex, aléatoire, Voronoï, pastilles, cubiste, éclats) avec post-traitement et fusion | [API](./noise/api.md) |
| [Dessiner un masque](./drawShape/README.md) | Dessine des formes précises (courbes) combinées en ajout/soustraction — sortie masque | — |
| [Solide](./solid/README.md) | Génère une forme remplie d'une couleur unie ou d'un dégradé | [API](./solid/api.md) |
| [Palette](./palette/README.md) | Définit une palette de couleurs à réutiliser dans le graphe | — |
| [Palette depuis dégradé](./paletteFromGradient/README.md) | Échantillonne un dégradé en un nombre fixe de couleurs | — |
| [Palette depuis image](./paletteFromImage/README.md) | Extrait les couleurs dominantes d'une image (median cut) | [API](./paletteFromImage/api.md) |
| [Modèle 3D](./model3d/README.md) | Importe un modèle 3D (GLB, GLTF, OBJ, FBX, STL) : caméra, matériaux et animation. À fusionner sur une image via « Fusion Modèle 3D ». | — |
| [Matériau](./material/README.md) | Compose un matériau 3D : surface physique et une texture par carte (couleur, normales, rugosité…). À relier à un matériau du module « Modèle 3D ». | — |
| [Motif](./checker/README.md) | Génère un motif répété : damier, grille, points, rayures, briques, nid d'abeille | — |
| [Dégradé](./gradient/README.md) | Génère un dégradé linéaire, circulaire, radial ou en losange | — |
| [QR code](./qrcode/README.md) | Génère un QR code lisible par tout lecteur (lien, Wi-Fi, contact…), stylé, avec logo, ou fondu dans une image | [API](./qrcode/api.md) |
| [Lens flare](./flare/README.md) | Éclat optique : cœur, branches en étoile, halo chromatique et reflets fantômes | — |
| [Lueur radiale](./glow/README.md) | Génère une lueur radiale (core, glow, aura) avec contrôle du falloff | — |
| [Éclair](./lightning/README.md) | Génère un éclair procédural ramifié entre deux points | — |
| [Tracé](./pathStroke/README.md) | Dessine des tracés vectoriels : plume, crayon, formes, traits fuselés et remplissages | — |
| [Particules](./particles/README.md) | Disperse une image source (ou un mélange d'images d'un batch) en particules (forme d'émission, traînées, atténuation), pilotées par une graine | [API](./particles/api.md) |
