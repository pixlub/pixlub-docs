# Modules

Tous les modules de Pixlub, par catégorie. Chaque fiche a deux vues : l'usage sur le site, et la référence API.

Chaque module a sa fiche, en deux vues :

- **Application** : où trouver le module sur le site et comment s'en servir, avec un guide écrit à la main quand il existe.
- **API** : le point d'accès, les fichiers attendus, chaque réglage avec son type, ses limites et sa valeur par défaut, et des exemples de requête en cURL, JavaScript, Python et avec les SDK. Cette vue est **générée** depuis le registre des modules : elle suit chaque nouvelle version sans mise à jour manuelle.

Les modules marqués **API** s'appellent par l'[API](../../02-api/fr/01-getting-started.md) ; les autres (vidéo, documents, blocs de graphe) s'utilisent sur le site.

## Modules de base

| Module | Description | API |
| --- | --- | --- |
| [Image source](./01-base/source/README.md) | Charge une image depuis un fichier et la fournit au graphe. | — |
| [Aperçu](./01-base/preview/README.md) | Affiche l'image et la transmet telle quelle. Le node s'agrandit quand on dézoome pour mieux visualiser globalement. | — |

## Sortie

| Module | Description | API |
| --- | --- | --- |
| [Export](./02-output/output/README.md) | Prévisualise et exporte l'image résultat. | — |
| [Exporter un batch](./02-output/exportBatch/README.md) | Télécharge toutes les images d'un batch : une archive, des fichiers séparés ou une animation. | — |

## Transformation

| Module | Description | API |
| --- | --- | --- |
| [Redimensionner](./03-transform/resize/README.md) | Modifie les dimensions de l'image | [API](./03-transform/resize/api.md) |
| [Redimensionner (Facteur)](./03-transform/resizeFactor/README.md) | Met l'image à l'échelle par un facteur multiplicatif | [API](./03-transform/resizeFactor/api.md) |
| [Étendre](./03-transform/extend/README.md) | Agrandit la zone de l'image sans déformer le contenu | [API](./03-transform/extend/api.md) |
| [Rogner](./03-transform/crop/README.md) | Découpe une zone de l'image | [API](./03-transform/crop/api.md) |
| [Recadrage auto](./03-transform/trim/README.md) | Rogne automatiquement les bords transparents | [API](./03-transform/trim/api.md) |
| [Rotation](./03-transform/rotate/README.md) | Fait pivoter l'image | [API](./03-transform/rotate/api.md) |
| [Miroir](./03-transform/flip/README.md) | Retourne l'image horizontalement et/ou verticalement | [API](./03-transform/flip/api.md) |
| [Distorsion](./03-transform/skew/README.md) | Incline l'image (cisaillement horizontal et vertical) | [API](./03-transform/skew/api.md) |
| [Perspective](./03-transform/cornerPin/README.md) | Déplace librement les quatre coins de l'image pour la mettre en perspective | [API](./03-transform/cornerPin/api.md) |
| [Sticker](./03-transform/sticker/README.md) | Décolle l'image comme un sticker, en l'enroulant dans une direction choisie | [API](./03-transform/sticker/api.md) |
| [Déplacement](./03-transform/translate/README.md) | Déplace la texture en X et Y, en % de l'image | [API](./03-transform/translate/api.md) |
| [Transformation](./03-transform/transform/README.md) | Déplace, tourne, met à l'échelle, retourne et estompe l'image en une fois | [API](./03-transform/transform/api.md) |
| [Marionnette](./03-transform/puppet/README.md) | Déforme l'image en déplaçant des épingles sur un maillage (puppet warp) | [API](./03-transform/puppet/api.md) |
| [Polaire](./03-transform/polar/README.md) | Convertit entre coordonnées rectangulaires et polaires (anneaux, rayons, halos) | [API](./03-transform/polar/api.md) |
| [Ondulation](./03-transform/ripple/README.md) | Distorsion en anneaux concentriques autour d'un centre | [API](./03-transform/ripple/api.md) |
| [Déplacement](./03-transform/displace/README.md) | Déforme l'image selon une carte de déplacement (bruit, dégradé…) | [API](./03-transform/displace/api.md) |
| [Remappage de texture](./03-transform/remap/README.md) | Redessine l'image en lisant, pour chaque pixel, la position donnée par une carte (dégradé, bruit…) | [API](./03-transform/remap/api.md) |
| [Kaléidoscope](./03-transform/kaleidoscope/README.md) | Répète un secteur en symétrie radiale | [API](./03-transform/kaleidoscope/api.md) |
| [Tourbillon](./03-transform/twirl/README.md) | Tord l'image en spirale autour d'un centre | [API](./03-transform/twirl/api.md) |
| [Onde](./03-transform/wave/README.md) | Déplacement sinusoïdal horizontal / vertical | [API](./03-transform/wave/api.md) |
| [Distorsion de lentille](./03-transform/fisheye/README.md) | Bombe (fisheye) ou creuse (coussinet) l'image autour d'un centre | [API](./03-transform/fisheye/api.md) |
| [Décalage raccord](./03-transform/tile/README.md) | Décale l'image : vérifier et fabriquer des textures tileables | [API](./03-transform/tile/api.md) |
| [Courber sur chemin](./03-transform/warpPath/README.md) | Déforme une image le long d'un chemin (ruban / trail courbé) | [API](./03-transform/warpPath/api.md) |
| [Suivre un chemin](./03-transform/followPath/README.md) | Fait voyager une image le long d'un chemin, de 0 % à 100 % de sa longueur ; le chemin peut sortir du cadre | [API](./03-transform/followPath/api.md) |
| [Découpe](./03-transform/trimVideo/README.md) | Découpe une partie de la vidéo à un moment donné. | — |
| [Vitesse](./03-transform/speedVideo/README.md) | Accélère ou ralentit la vidéo. La cadence de sortie reste la même : ce sont les images demandées à la source qui changent. | — |
| [Cadence](./03-transform/frameRateVideo/README.md) | Réécrit la cadence de la vidéo. Baisser la cadence allège le fichier ; l'augmenter au-delà de la source duplique des images. | — |

## Ajustement

| Module | Description | API |
| --- | --- | --- |
| [Ajustement Base](./04-adjust/baseAdjust/README.md) | Les réglages essentiels d'une photo réunis : lumière, tons, balance des blancs et couleurs | [API](./04-adjust/baseAdjust/api.md) |
| [Niveaux](./04-adjust/levels/README.md) | Ajuste les points noir et blanc, le gamma et la plage de sortie, par canal | [API](./04-adjust/levels/api.md) |
| [Balance des blancs](./04-adjust/whiteBalance/README.md) | Réchauffe ou refroidit l'image et corrige sa dominante verte ou magenta | [API](./04-adjust/whiteBalance/api.md) |
| [Recolorer](./04-adjust/recolor/README.md) | Teinte toute l'image d'une seule couleur, en gardant ses ombres et ses lumières | [API](./04-adjust/recolor/api.md) |
| [HSL](./04-adjust/hsl/README.md) | Décale la teinte, la saturation et la luminosité d'une plage de couleurs | [API](./04-adjust/hsl/api.md) |
| [Noir et blanc](./04-adjust/blackWhite/README.md) | Passe l'image en gris en dosant la clarté de chaque couleur | [API](./04-adjust/blackWhite/api.md) |
| [Luminosité & Contraste](./04-adjust/brightness/README.md) | Ajuste la luminosité et le contraste | [API](./04-adjust/brightness/api.md) |
| [Postériser](./04-adjust/posterize/README.md) | Réduit le nombre de niveaux par canal (aplats stylisés, cel shading) | [API](./04-adjust/posterize/api.md) |
| [Exposition](./04-adjust/exposure/README.md) | Rehausse ou baisse la lumière de l'image, cran par cran comme un appareil photo | [API](./04-adjust/exposure/api.md) |
| [Courbes](./04-adjust/curves/README.md) | Ajuste la tonalité par une courbe éditable, par canal ou globale | [API](./04-adjust/curves/api.md) |
| [Courbes de saturation / teinte](./04-adjust/hueSatCurves/README.md) | Règle la saturation ou la teinte selon la luminance, la saturation ou la teinte de chaque couleur | [API](./04-adjust/hueSatCurves/api.md) |
| [Mélangeur de canaux](./04-adjust/channelMixer/README.md) | Recompose chaque canal à partir des autres, dans l'espace choisi | [API](./04-adjust/channelMixer/api.md) |
| [Inverser](./04-adjust/invert/README.md) | Passe l'image en négatif | [API](./04-adjust/invert/api.md) |
| [Balance des couleurs](./04-adjust/colorBalance/README.md) | Ajuste les teintes par plage de tons (clairs, moyens, foncés), masquable | [API](./04-adjust/colorBalance/api.md) |
| [Filtre d'accessibilité](./04-adjust/colorAccessibility/README.md) | Corrige les couleurs pour qu'elles restent lisibles par une vision daltonienne | [API](./04-adjust/colorAccessibility/api.md) |
| [Palette : recolorer](./04-adjust/paletteRemap/README.md) | Génère une variante recolorée de l'image par couleur de la palette (batch) | [API](./04-adjust/paletteRemap/api.md) |
| [Seuil](./04-adjust/threshold/README.md) | Binarise la luminance selon un seuil (avec transition douce) | [API](./04-adjust/threshold/api.md) |
| [Remplacer couleurs](./04-adjust/replaceColors/README.md) | Remplace une liste de couleurs sources par des couleurs cibles | [API](./04-adjust/replaceColors/api.md) |
| [Opacité](./04-adjust/opacity/README.md) | Modifie l'opacité de l'image | [API](./04-adjust/opacity/api.md) |
| [Contour](./04-adjust/outline/README.md) | Ajoute un contour à l'image | [API](./04-adjust/outline/api.md) |
| [Ombre](./04-adjust/shadow/README.md) | Projette une ombre (extérieure ou intérieure) à partir de l'alpha de l'image | [API](./04-adjust/shadow/api.md) |
| [Mappe dégradé](./04-adjust/gradientMap/README.md) | Colorise l'image en mappant sa luminance sur un dégradé | [API](./04-adjust/gradientMap/api.md) |

## Filtres

| Module | Description | API |
| --- | --- | --- |
| [Flou](./05-filter/blur/README.md) | Flou gaussien, de mouvement, de rotation ou de zoom (centre interactif) | [API](./05-filter/blur/api.md) |
| [Flou de mouvement](./05-filter/motionBlur/README.md) | Flou directionnel, zoom ou rotation (vitesse, traînées, impacts) | [API](./05-filter/motionBlur/api.md) |
| [Netteté](./05-filter/sharpen/README.md) | Renforce les détails et les contours (masque flou) | [API](./05-filter/sharpen/api.md) |
| [Débruitage](./05-filter/denoise/README.md) | Réduit le bruit en préservant les contours (filtre médian) | [API](./05-filter/denoise/api.md) |
| [Détection de contours](./05-filter/edgeDetect/README.md) | Extrait les contours (Sobel) avec double seuil, couleurs et pré-flou | [API](./05-filter/edgeDetect/api.md) |
| [Aberration chromatique](./05-filter/chromatic/README.md) | Décale les canaux rouge et bleu (effet lentille, glitch, impact) | [API](./05-filter/chromatic/api.md) |
| [Dilater / Éroder](./05-filter/morphology/README.md) | Épaissit ou contracte les zones opaques (masques, contours, silhouettes) | [API](./05-filter/morphology/api.md) |
| [Carte de normales](./05-filter/normalMap/README.md) | Génère une normal map depuis une heightmap (relief pour moteurs 3D / VFX) | [API](./05-filter/normalMap/api.md) |
| [Pixeliser](./05-filter/pixelate/README.md) | Réduit l'image en gros pixels (effet pixel art) | [API](./05-filter/pixelate/api.md) |
| [Demi-teinte](./05-filter/halftone/README.md) | Trame de points, tramage ordonné (Bayer) ou diffusion d'erreur (rétro / print) | [API](./05-filter/halftone/api.md) |
| [Peinture](./05-filter/kuwahara/README.md) | Aplats picturaux qui préservent les contours (filtre de Kuwahara, effet huile) | [API](./05-filter/kuwahara/api.md) |
| [Tri de pixels](./05-filter/pixelSort/README.md) | Trie les pixels par luminance dans les zones claires ou sombres (glitch art) | [API](./05-filter/pixelSort/api.md) |
| [Scanlines CRT](./05-filter/scanlines/README.md) | Lignes de balayage et masque RVB façon écran cathodique | [API](./05-filter/scanlines/api.md) |
| [Rayons lumineux](./05-filter/rays/README.md) | Rayons volumétriques émis par les zones claires depuis un centre (god rays) | [API](./05-filter/rays/api.md) |
| [Contour progressif](./05-filter/feather/README.md) | Adoucit les bords de la transparence (fondu du masque alpha) | [API](./05-filter/feather/api.md) |
| [Vignette](./05-filter/vignette/README.md) | Assombrit progressivement les bords de l'image | [API](./05-filter/vignette/api.md) |
| [Bloom](./05-filter/bloom/README.md) | Diffuse les zones lumineuses en halo additif (glow) | [API](./05-filter/bloom/api.md) |
| [Retirer un fond uni](./05-filter/removeBg/README.md) | Rend transparent un fond d'une seule couleur (fond vert, studio…), détectée ou choisie. | [API](./05-filter/removeBg/api.md) |
| [Séparer RVB](./05-filter/splitRgb/README.md) | Sépare l'image en ses canaux Rouge, Vert et Bleu | [API](./05-filter/splitRgb/api.md) |
| [Séparer transparence](./05-filter/splitAlpha/README.md) | Sépare l'image en son canal couleur (RVB opaque) et son canal alpha (niveaux de gris) | [API](./05-filter/splitAlpha/api.md) |
| [Paillettes](./05-filter/glitter/README.md) | Couvre l'image de paillettes qui scintillent : facettes irisées, étoiles et reflet, en boucle. | [API](./05-filter/glitter/api.md) |

## Composition

| Module | Description | API |
| --- | --- | --- |
| [Séparer les canaux](./06-compose/channelSplit/README.md) | Extrait les canaux R, V, B et Alpha sous forme de canaux (niveaux de gris) | [API](./06-compose/channelSplit/api.md) |
| [Fusionner les canaux](./06-compose/channelMerge/README.md) | Recompose une image depuis des canaux R, V, B et/ou Alpha | [API](./06-compose/channelMerge/api.md) |
| [Image vers masque](./06-compose/imageToMask/README.md) | Convertit une image en canal de masque (alpha, canal ou luminance) | [API](./06-compose/imageToMask/api.md) |
| [Fusion](./06-compose/merge/README.md) | Superpose une ou plusieurs images (calques) sur une autre | [API](./06-compose/merge/api.md) |
| [Fusionner transparence](./06-compose/mergeAlpha/README.md) | Recombine un canal couleur (RVB) et un canal alpha en une image transparente | [API](./06-compose/mergeAlpha/api.md) |
| [Planche de sprites](./06-compose/spriteSheet/README.md) | Assemble plusieurs images en grille (flipbook, atlas de VFX) | [API](./06-compose/spriteSheet/api.md) |
| [Disposition](./06-compose/arrange/README.md) | Aligne plusieurs images côte à côte ou empilées (bandeaux, comparatifs) | [API](./06-compose/arrange/api.md) |
| [Assembler un batch](./06-compose/arrayBatch/README.md) | Regroupe des images et des batchs en un seul batch | — |
| [Séparer un batch](./06-compose/arraySplitBatch/README.md) | Éclate un batch en images individuelles | — |
| [Masque](./06-compose/mask/README.md) | Module l'opacité d'une image par la luminance (ou l'alpha) d'un masque | [API](./06-compose/mask/api.md) |
| [Gomme](./06-compose/eraser/README.md) | Efface à la main des parties de l'image, avec une palette de pointes réglables | [API](./06-compose/eraser/api.md) |
| [Fusion Modèle 3D](./06-compose/model3dMerge/README.md) | Rend un modèle 3D et le superpose sur une image : position, rotation, échelle. | — |

## Génération

| Module | Description | API |
| --- | --- | --- |
| [Bruit](./07-generate/noise/README.md) | Génère un bruit procédural (Perlin, simplex, aléatoire, Voronoï, pastilles, cubiste, éclats) avec post-traitement et fusion | [API](./07-generate/noise/api.md) |
| [Dessiner un masque](./07-generate/drawShape/README.md) | Dessine des formes précises (courbes) combinées en ajout/soustraction — sortie masque | — |
| [Solide](./07-generate/solid/README.md) | Génère une forme remplie d'une couleur unie ou d'un dégradé | [API](./07-generate/solid/api.md) |
| [Palette](./07-generate/palette/README.md) | Définit une palette de couleurs à réutiliser dans le graphe | — |
| [Palette depuis dégradé](./07-generate/paletteFromGradient/README.md) | Échantillonne un dégradé en un nombre fixe de couleurs | — |
| [Palette depuis image](./07-generate/paletteFromImage/README.md) | Extrait les couleurs dominantes d'une image (median cut) | [API](./07-generate/paletteFromImage/api.md) |
| [Modèle 3D](./07-generate/model3d/README.md) | Importe un modèle 3D (GLB, GLTF, OBJ, FBX, STL) : caméra, matériaux et animation. À fusionner sur une image via « Fusion Modèle 3D ». | — |
| [Matériau](./07-generate/material/README.md) | Compose un matériau 3D : type de rendu (Standard, sans éclairage, dessin animé, matcap, tessellation), surface, une texture par carte et des effets. Le même matériau que dans l’éditeur 3D ; à relier à un matériau du module « Modèle 3D ». | — |
| [Motif](./07-generate/checker/README.md) | Génère un motif répété : damier, grille, points, rayures, briques, nid d'abeille | — |
| [Dégradé](./07-generate/gradient/README.md) | Génère un dégradé linéaire, circulaire, radial ou en losange | — |
| [QR code](./07-generate/qrcode/README.md) | Génère un QR code lisible par tout lecteur (lien, Wi-Fi, contact…), stylé, avec logo, ou fondu dans une image | [API](./07-generate/qrcode/api.md) |
| [Lens flare](./07-generate/flare/README.md) | Éclat optique : cœur, branches en étoile, halo chromatique et reflets fantômes | — |
| [Lueur radiale](./07-generate/glow/README.md) | Génère une lueur radiale (core, glow, aura) avec contrôle du falloff | — |
| [Éclair](./07-generate/lightning/README.md) | Génère un éclair procédural ramifié entre deux points | — |
| [Tracé](./07-generate/pathStroke/README.md) | Dessine des tracés vectoriels : plume, crayon, formes, traits fuselés et remplissages | — |
| [Particules](./07-generate/particles/README.md) | Disperse une image source (ou un mélange d'images d'un batch) en particules (forme d'émission, traînées, atténuation), pilotées par une graine | [API](./07-generate/particles/api.md) |

## Services API

| Module | Description | API |
| --- | --- | --- |
| [Retirer un fond](./08-api/removeBgApi/README.md) | Détecte le sujet par IA (par nos services) et rend transparent tout le reste, quel que soit le fond. | [API](./08-api/removeBgApi/api.md) |
| [Floutage de visages](./08-api/faceBlurApi/README.md) | Floute des zones tracées à la main, ou détecte les visages via IA (nos services). Les zones sont éditables dans la préview : créer, déplacer, redimensionner, supprimer. | [API](./08-api/faceBlurApi/api.md) |
| [Décalcomanie](./08-api/decalApi/README.md) | Reconstruit via IA (nos services) le relief 3D de l'objet, puis y drape l'image que vous placez librement dessus. Seule la photo est envoyée, une seule fois ; l'image posée reste sur votre machine. | [API](./08-api/decalApi/api.md) |
| [Floutage de visages (vidéo)](./08-api/faceBlurVideoApi/README.md) | Floute des zones tracées à la main, ou détecte les visages de chaque image via notre API. Chaque zone se suit dans le temps et s'ajuste dans l'aperçu, image par image. En mode automatique, la détection part au serveur une seule fois ; le floutage reste toujours calculé dans le navigateur. | — |
| [Sous-titres (vidéo)](./08-api/transcribeVideoApi/README.md) | Transcrit la parole d'une vidéo via notre API, mot à mot et horodatée, puis grave les sous-titres dans l'image. La transcription part au serveur une seule fois ; la mise en forme reste calculée dans le navigateur. | — |

## Valeurs

| Module | Description | API |
| --- | --- | --- |
| [Valeur](./09-operation/value/README.md) | Émet une valeur numérique constante. | — |
| [Addition](./09-operation/add/README.md) | Somme de deux entrées (A + B). | — |
| [Soustraction](./09-operation/subtract/README.md) | Différence de deux entrées (A - B). | — |
| [Multiplication](./09-operation/multiply/README.md) | Produit de deux entrées (A × B). | — |
| [Division](./09-operation/divide/README.md) | Quotient de deux entrées (A ÷ B), 0 si B = 0. | — |
| [Taille image](./09-operation/size/README.md) | Largeur et hauteur de l'image en entrée. | — |

## Texte

| Module | Description | API |
| --- | --- | --- |
| [Texte](./10-text/text/README.md) | Compose un texte : typographie, couleur ou dégradé, pile de styles et animation. | — |
| [Texte vers Image](./10-text/textRender/README.md) | Rend un texte dans un cadre choisi : taille, ancrage, fond. | — |

## Couleurs

| Module | Description | API |
| --- | --- | --- |
| [Couleur](./11-color/color/README.md) | Émet une couleur (unie ou dégradé). | — |

## Conversion

| Module | Description | API |
| --- | --- | --- |
| [Extraction audio](./12-conversion/extractAudioVideo/README.md) | Sort la piste sonore d'une vidéo dans un fichier audio : MP3, AAC, Opus, FLAC, WAV… ou la piste d'origine telle quelle, sans perte. | — |
| [Conversion audio](./12-conversion/convertAudio/README.md) | Convertit un fichier son dans un autre format — MP3, AAC, Opus, Vorbis, FLAC, WAV ou AIFF — avec son débit, sa fréquence et ses canaux, et en garde la partie voulue. | — |
| [Conversion](./12-conversion/convert/README.md) | Convertit images, animations, vidéos et sons vers n’importe quel format de l’export : PNG, JPG, WebP, GIF, MP4, WebM, MP3, FLAC, WAV, PDF… | [API](./12-conversion/convert/api.md) |

## Documents

| Module | Description | API |
| --- | --- | --- |
| [Fusionner des PDF](./13-document/docMerge/README.md) | Assemble plusieurs PDF en un seul fichier, dans l’ordre choisi. | — |
| [Découper un PDF](./13-document/docSplit/README.md) | Sépare un PDF en plusieurs fichiers : page par page, par paquets, aux repères posés sur l’aperçu ou selon vos plages. À l’export, en PDF ou en images. | — |
| [Organiser les pages](./13-document/docPages/README.md) | Garde, supprime, réordonne, duplique ou tourne les pages d’un PDF. | — |
| [Rogner un PDF](./13-document/docCrop/README.md) | Retire une marge autour des pages, sans toucher à leur contenu : la même partout, ou propre à certaines pages. | — |
| [Numéroter les pages](./13-document/docPageNumbers/README.md) | Ajoute un numéro sur chaque page, à la place et au format de votre choix. | — |
| [Filigrane](./13-document/docWatermark/README.md) | Pose un texte ou une image translucide sur les pages, une fois ou en mosaïque. | — |
| [Métadonnées](./13-document/docMetadata/README.md) | Lit et modifie le titre, l’auteur, le sujet et les mots-clés d’un PDF, ou les efface. | — |
| [Signer un PDF](./13-document/docSign/README.md) | Pose votre signature, dessinée ou importée, sur les pages choisies. | — |
| [Images vers PDF](./13-document/docImagesToPdf/README.md) | Assemble des images en un PDF : composez vos pages, une ou plusieurs images chacune, placées où vous voulez. | — |
| [PDF vers images](./13-document/docPdfToImages/README.md) | Exporte chaque page en PNG, JPEG ou WebP, à la résolution choisie. | — |
| [PDF vers Word](./13-document/docPdfToWord/README.md) | Reprend les titres, paragraphes et tableaux d’un PDF dans un document Word modifiable. | — |
| [PDF vers Excel](./13-document/docPdfToExcel/README.md) | Range le contenu d’un PDF dans un classeur : les colonnes alignées deviennent des colonnes, les nombres des nombres. | — |
| [Office vers PDF](./13-document/docOfficeToPdf/README.md) | Convertit un document Word, Excel, PowerPoint ou OpenDocument en PDF. | — |
| [HTML vers PDF](./13-document/docHtmlToPdf/README.md) | Met en page un fichier HTML et le rend en PDF, texte sélectionnable compris. | — |
| [Compresser un PDF](./13-document/docCompress/README.md) | Réduit le poids d’un PDF en réencodant ses images ; le texte reste net et sélectionnable. | — |
| [Réparer un PDF](./13-document/docRepair/README.md) | Reconstruit un PDF endommagé ou qui s’ouvre mal : table des objets, catalogue et arbre des pages. | — |
| [Protéger un PDF](./13-document/docProtect/README.md) | Chiffre un PDF en AES-256 avec un mot de passe, et limite ce qu’on peut en faire. | — |
| [Déverrouiller un PDF](./13-document/docUnlock/README.md) | Retire le mot de passe et les restrictions d’un PDF protégé, si vous connaissez son mot de passe. | — |
| [Caviarder un PDF](./13-document/docRedact/README.md) | Noircit les mots ou motifs choisis : le texte disparaît vraiment de la page. | — |
| [Extraire le texte (OCR)](./13-document/docOcrText/README.md) | Lit le texte d’un PDF, d’un scan ou d’une photo de document, puis l’exporte en texte brut ou en PDF consultable. | — |
| [Comparer deux PDF](./13-document/docCompare/README.md) | Liste les lignes ajoutées et retirées page par page, et signale les pages dont l’aspect a changé. | — |
