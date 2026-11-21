# Mélangeur de canaux : référence API

Recompose chaque canal à partir des autres, dans l'espace choisi

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/channelMixer` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Une image ou plusieurs) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image dont les canaux sont recomposés. |

## Réglages

### Général

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `space` | `string` | `"rgb"` | `rgb` RVB<br />`gray` Gris<br />`cmyk` CMJN<br />`lab` LAB | **Espace**<br />Espace colorimétrique dans lequel les canaux sont ajustés |

### Espace RVB

> Ces réglages ne comptent que quand `space` = `rgb` (RVB).

#### Sortie Rouge

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `rgbRFromRgbR` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Rouge**<br />Part du canal Rouge reportée dans le canal de sortie Rouge. 100 % le recopie, une valeur négative le soustrait. |
| `rgbRFromRgbG` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Vert**<br />Part du canal Vert reportée dans le canal de sortie Rouge. 100 % le recopie, une valeur négative le soustrait. |
| `rgbRFromRgbB` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Bleu**<br />Part du canal Bleu reportée dans le canal de sortie Rouge. 100 % le recopie, une valeur négative le soustrait. |
| `rgbRFromRgbAlpha` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Rouge. 100 % le recopie, une valeur négative le soustrait. |
| `offsetRgbR` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Rouge, quelle que soit l'image. |

#### Sortie Vert

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `rgbGFromRgbR` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Rouge**<br />Part du canal Rouge reportée dans le canal de sortie Vert. 100 % le recopie, une valeur négative le soustrait. |
| `rgbGFromRgbG` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Vert**<br />Part du canal Vert reportée dans le canal de sortie Vert. 100 % le recopie, une valeur négative le soustrait. |
| `rgbGFromRgbB` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Bleu**<br />Part du canal Bleu reportée dans le canal de sortie Vert. 100 % le recopie, une valeur négative le soustrait. |
| `rgbGFromRgbAlpha` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Vert. 100 % le recopie, une valeur négative le soustrait. |
| `offsetRgbG` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Vert, quelle que soit l'image. |

#### Sortie Bleu

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `rgbBFromRgbR` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Rouge**<br />Part du canal Rouge reportée dans le canal de sortie Bleu. 100 % le recopie, une valeur négative le soustrait. |
| `rgbBFromRgbG` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Vert**<br />Part du canal Vert reportée dans le canal de sortie Bleu. 100 % le recopie, une valeur négative le soustrait. |
| `rgbBFromRgbB` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Bleu**<br />Part du canal Bleu reportée dans le canal de sortie Bleu. 100 % le recopie, une valeur négative le soustrait. |
| `rgbBFromRgbAlpha` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Bleu. 100 % le recopie, une valeur négative le soustrait. |
| `offsetRgbB` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Bleu, quelle que soit l'image. |

#### Sortie Alpha

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `rgbAlphaFromRgbR` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Rouge**<br />Part du canal Rouge reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `rgbAlphaFromRgbG` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Vert**<br />Part du canal Vert reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `rgbAlphaFromRgbB` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Bleu**<br />Part du canal Bleu reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `rgbAlphaFromRgbAlpha` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `offsetRgbAlpha` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Alpha, quelle que soit l'image. |

### Espace Gris

> Ces réglages ne comptent que quand `space` = `gray` (Gris).

#### Sortie Intensité

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `grayIFromGrayI` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Intensité**<br />Part du canal Intensité reportée dans le canal de sortie Intensité. 100 % le recopie, une valeur négative le soustrait. |
| `grayIFromGrayAlpha` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Intensité. 100 % le recopie, une valeur négative le soustrait. |
| `offsetGrayI` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Intensité, quelle que soit l'image. |

#### Sortie Alpha

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `grayAlphaFromGrayI` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Intensité**<br />Part du canal Intensité reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `grayAlphaFromGrayAlpha` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `offsetGrayAlpha` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Alpha, quelle que soit l'image. |

### Espace CMJN

> Ces réglages ne comptent que quand `space` = `cmyk` (CMJN).

#### Sortie Cyan

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `cmykCFromCmykC` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Cyan**<br />Part du canal Cyan reportée dans le canal de sortie Cyan. 100 % le recopie, une valeur négative le soustrait. |
| `cmykCFromCmykM` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Magenta**<br />Part du canal Magenta reportée dans le canal de sortie Cyan. 100 % le recopie, une valeur négative le soustrait. |
| `cmykCFromCmykY` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Jaune**<br />Part du canal Jaune reportée dans le canal de sortie Cyan. 100 % le recopie, une valeur négative le soustrait. |
| `cmykCFromCmykK` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Noir**<br />Part du canal Noir reportée dans le canal de sortie Cyan. 100 % le recopie, une valeur négative le soustrait. |
| `cmykCFromCmykAlpha` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Cyan. 100 % le recopie, une valeur négative le soustrait. |
| `offsetCmykC` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Cyan, quelle que soit l'image. |

#### Sortie Magenta

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `cmykMFromCmykC` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Cyan**<br />Part du canal Cyan reportée dans le canal de sortie Magenta. 100 % le recopie, une valeur négative le soustrait. |
| `cmykMFromCmykM` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Magenta**<br />Part du canal Magenta reportée dans le canal de sortie Magenta. 100 % le recopie, une valeur négative le soustrait. |
| `cmykMFromCmykY` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Jaune**<br />Part du canal Jaune reportée dans le canal de sortie Magenta. 100 % le recopie, une valeur négative le soustrait. |
| `cmykMFromCmykK` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Noir**<br />Part du canal Noir reportée dans le canal de sortie Magenta. 100 % le recopie, une valeur négative le soustrait. |
| `cmykMFromCmykAlpha` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Magenta. 100 % le recopie, une valeur négative le soustrait. |
| `offsetCmykM` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Magenta, quelle que soit l'image. |

#### Sortie Jaune

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `cmykYFromCmykC` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Cyan**<br />Part du canal Cyan reportée dans le canal de sortie Jaune. 100 % le recopie, une valeur négative le soustrait. |
| `cmykYFromCmykM` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Magenta**<br />Part du canal Magenta reportée dans le canal de sortie Jaune. 100 % le recopie, une valeur négative le soustrait. |
| `cmykYFromCmykY` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Jaune**<br />Part du canal Jaune reportée dans le canal de sortie Jaune. 100 % le recopie, une valeur négative le soustrait. |
| `cmykYFromCmykK` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Noir**<br />Part du canal Noir reportée dans le canal de sortie Jaune. 100 % le recopie, une valeur négative le soustrait. |
| `cmykYFromCmykAlpha` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Jaune. 100 % le recopie, une valeur négative le soustrait. |
| `offsetCmykY` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Jaune, quelle que soit l'image. |

#### Sortie Noir

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `cmykKFromCmykC` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Cyan**<br />Part du canal Cyan reportée dans le canal de sortie Noir. 100 % le recopie, une valeur négative le soustrait. |
| `cmykKFromCmykM` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Magenta**<br />Part du canal Magenta reportée dans le canal de sortie Noir. 100 % le recopie, une valeur négative le soustrait. |
| `cmykKFromCmykY` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Jaune**<br />Part du canal Jaune reportée dans le canal de sortie Noir. 100 % le recopie, une valeur négative le soustrait. |
| `cmykKFromCmykK` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Noir**<br />Part du canal Noir reportée dans le canal de sortie Noir. 100 % le recopie, une valeur négative le soustrait. |
| `cmykKFromCmykAlpha` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Noir. 100 % le recopie, une valeur négative le soustrait. |
| `offsetCmykK` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Noir, quelle que soit l'image. |

#### Sortie Alpha

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `cmykAlphaFromCmykC` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Cyan**<br />Part du canal Cyan reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `cmykAlphaFromCmykM` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Magenta**<br />Part du canal Magenta reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `cmykAlphaFromCmykY` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Jaune**<br />Part du canal Jaune reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `cmykAlphaFromCmykK` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Noir**<br />Part du canal Noir reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `cmykAlphaFromCmykAlpha` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `offsetCmykAlpha` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Alpha, quelle que soit l'image. |

### Espace LAB

> Ces réglages ne comptent que quand `space` = `lab` (LAB).

#### Sortie Luminosité

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `labLFromLabL` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Luminosité**<br />Part du canal Luminosité reportée dans le canal de sortie Luminosité. 100 % le recopie, une valeur négative le soustrait. |
| `labLFromLabA` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Chrominance A**<br />Part du canal Chrominance A reportée dans le canal de sortie Luminosité. 100 % le recopie, une valeur négative le soustrait. |
| `labLFromLabB` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Chrominance B**<br />Part du canal Chrominance B reportée dans le canal de sortie Luminosité. 100 % le recopie, une valeur négative le soustrait. |
| `labLFromLabAlpha` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Luminosité. 100 % le recopie, une valeur négative le soustrait. |
| `offsetLabL` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Luminosité, quelle que soit l'image. |

#### Sortie Chrominance A

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `labAFromLabL` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Luminosité**<br />Part du canal Luminosité reportée dans le canal de sortie Chrominance A. 100 % le recopie, une valeur négative le soustrait. |
| `labAFromLabA` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Chrominance A**<br />Part du canal Chrominance A reportée dans le canal de sortie Chrominance A. 100 % le recopie, une valeur négative le soustrait. |
| `labAFromLabB` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Chrominance B**<br />Part du canal Chrominance B reportée dans le canal de sortie Chrominance A. 100 % le recopie, une valeur négative le soustrait. |
| `labAFromLabAlpha` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Chrominance A. 100 % le recopie, une valeur négative le soustrait. |
| `offsetLabA` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Chrominance A, quelle que soit l'image. |

#### Sortie Chrominance B

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `labBFromLabL` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Luminosité**<br />Part du canal Luminosité reportée dans le canal de sortie Chrominance B. 100 % le recopie, une valeur négative le soustrait. |
| `labBFromLabA` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Chrominance A**<br />Part du canal Chrominance A reportée dans le canal de sortie Chrominance B. 100 % le recopie, une valeur négative le soustrait. |
| `labBFromLabB` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Chrominance B**<br />Part du canal Chrominance B reportée dans le canal de sortie Chrominance B. 100 % le recopie, une valeur négative le soustrait. |
| `labBFromLabAlpha` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Chrominance B. 100 % le recopie, une valeur négative le soustrait. |
| `offsetLabB` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Chrominance B, quelle que soit l'image. |

#### Sortie Alpha

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `labAlphaFromLabL` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Luminosité**<br />Part du canal Luminosité reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `labAlphaFromLabA` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Chrominance A**<br />Part du canal Chrominance A reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `labAlphaFromLabB` | `number` | `0` | min -200 % · max 200 % · pas de 1 | **Chrominance B**<br />Part du canal Chrominance B reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `labAlphaFromLabAlpha` | `number` | `100` | min -200 % · max 200 % · pas de 1 | **Alpha**<br />Part du canal Alpha reportée dans le canal de sortie Alpha. 100 % le recopie, une valeur négative le soustrait. |
| `offsetLabAlpha` | `number` | `0` | min -100 % · max 100 % · pas de 1 | **Décalage**<br />Valeur ajoutée au canal de sortie Alpha, quelle que soit l'image. |

### Fusion

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blendMode` | `string`<br />*Mode de fusion* | `"normal"` | `normal` Normal : Le calque recouvre ce qui est dessous.<br />`multiply` Produit : Fonce : le blanc disparaît.<br />`screen` Écran : Éclaircit : le noir disparaît.<br />`overlay` Incrustation : Renforce le contraste du dessous.<br />`darken` Obscurcir : Garde le plus sombre des deux.<br />`color-burn` Densité + : Fonce en saturant les couleurs.<br />`lighten` Éclaircir : Garde le plus clair des deux.<br />`color-dodge` Densité - : Éclaircit jusqu'à l'éclat.<br />`soft-light` Lumière douce : Contraste doux, comme une lumière diffuse.<br />`hard-light` Lumière crue : Contraste franc, comme un projecteur.<br />`difference` Différence : Inverse là où le calque est clair.<br />`exclusion` Exclusion : Comme Différence, en plus doux.<br />`hue` Teinte : Prend seulement la teinte du calque.<br />`saturation` Saturation : Prend seulement la saturation du calque.<br />`color` Couleur : Prend teinte et saturation, garde la clarté.<br />`luminosity` Luminosité : Prend seulement la clarté du calque. | **Méthode de fusion**<br />Façon dont le réglage se pose sur l'image d'origine. |
| `blendOpacity` | `number` | `100` | min 0 % · max 100 % · pas de 1 | **Opacité**<br />Dosage du réglage. |

### Taille

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `frameMethod` | `string` | `"module"` | `module` Module : Le module agrandit ou réduit l'image selon ce qu'il produit.<br />`source` Source : Le rendu garde la taille de l'image reçue.<br />`custom` Libre : Le rendu prend la largeur et la hauteur choisies. | **Méthode**<br />D'où vient la taille du rendu. |
| `frameWidth` | `number` |  | min 1 px · max 16384 px | **Largeur**<br />Largeur du rendu, en pixels.<br />*Pris en compte quand `frameMethod` = `custom` (Libre).* |
| `frameHeight` | `number` |  | min 1 px · max 16384 px | **Hauteur**<br />Hauteur du rendu, en pixels.<br />*Pris en compte quand `frameMethod` = `custom` (Libre).* |
| `frameFit` | `string` | `"none"` | `none` Aucun (recadre) : Le rendu garde son échelle et se recadre.<br />`contain` Contenir : Le rendu entier tient dans la taille.<br />`cover` Couvrir : Le rendu remplit la taille, quitte à déborder.<br />`stretch` Étirer : Le rendu s'étire à la taille, sans garder ses proportions. | **Ajustement**<br />Comment le rendu se place dans la taille imposée.<br />*Pris en compte quand `frameMethod` = `source` (Source) ou `custom` (Libre).* |
| `frameAnchor` | `string`<br />*Ancrage* | `"center"` | [grille ci-dessous](#anchor-frameanchor) | **Ancrage**<br />Côté où le rendu s'accroche.<br />*Pris en compte quand `frameMethod` = `source` (Source) ou `custom` (Libre) et `frameFit` = `none` (Aucun (recadre)) ou `contain` (Contenir) ou `cover` (Couvrir).*<br />*Ancrage* : Point d'une grille 3 × 3, du coin haut gauche au coin bas droit. |

<a name="anchor-frameanchor"></a>

**Positions de `frameAnchor`**

| | Gauche | Centre | Droite |
| --- | --- | --- | --- |
| **Haut** | `top-left`<br />En haut à gauche | `top`<br />En haut | `top-right`<br />En haut à droite |
| **Milieu** | `left`<br />À gauche | **`center`**<br />**Au centre** | `right`<br />À droite |
| **Bas** | `bottom-left`<br />En bas à gauche | `bottom`<br />En bas | `bottom-right`<br />En bas à droite |

## Exemples

### cURL

```bash
curl -X POST https://api.pixlub.com/v1/modules/channelMixer \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"space":"rgb","rgbRFromRgbR":100,"rgbRFromRgbG":0}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"space":"rgb","rgbRFromRgbR":100,"rgbRFromRgbG":0}))

const res = await fetch('https://api.pixlub.com/v1/modules/channelMixer', {
  method: 'POST',
  headers: { 'X-API-Key': process.env.PIXLUB_API_KEY },
  body: form,
})
const result = await res.json()
const output = result.outputs.find((o) => o.key === 'out')
const image = await fetch(output.url) // lien signé, sans clé
```

### Python

```python
import json, os, requests

res = requests.post(
    "https://api.pixlub.com/v1/modules/channelMixer",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"space": "rgb", "rgbRFromRgbR": 100, "rgbRFromRgbG": 0})},
)
res.raise_for_status()
result = res.json()
output = next(o for o in result["outputs"] if o["key"] == "out")
print(output["url"])
```

### SDK Python

```python
import pixlub

client = pixlub.Client()  # PIXLUB_API_KEY, PIXLUB_BASE_URL
result = client.tools.run("channelMixer", image="photo.png", params={"space": "rgb", "rgbRFromRgbR": 100, "rgbRFromRgbG": 0})
result.save(f"channelMixer{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "channelMixer", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"space": "rgb", "rgbRFromRgbR": 100, "rgbRFromRgbG": 0},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("channelMixer"+result.Extension(), false)
```

## Sorties

Chaque fichier rendu porte dans `outputs` la clé de sa sortie (`key`) : cherchez-la pour retrouver le fichier voulu plutôt que de compter sur sa position.

### 1 fichier

> **1 fichier** : Une seule image dans `in`.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out` | `image` | `PNG` | **Image(s)**<br />Image produite par le module.<br />Une seule image envoyée : le fichier garde la clé `out`. |

### Plusieurs fichiers

> **Plusieurs fichiers** : Plusieurs images dans `in`, jusqu'à 64 : leur nombre se déduit des fichiers envoyés, vous ne l'envoyez pas.

| key | Type | Formats | Description |
| --- | --- | --- | --- |
| `out#n` | `image` | `PNG` | **Image(s)**<br />Image produite par le module.<br />Plusieurs images envoyées dans `in` : un fichier par image, sous les clés `out#0`, `out#1`…, dans l'ordre d'envoi. |

## Réponse

La réponse liste les fichiers produits dans outputs. Chaque lien est signé et valable une heure, sans clé d'API ; les fichiers sont effacés au bout de 24 heures.

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "channelMixer",
  "outputs": [
    {
      "key": "out",
      "name": "image",
      "url": "https://files.pixlub.com/r/e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10_result.png?exp=1767268800&sig=…",
      "content_type": "image/png",
      "bytes": 184203
    }
  ],
  "expires_at": "2026-01-01T12:00:00Z",
  "credits": {
    "cost": 1,
    "balance": 190
  }
}
```

## Schéma JSON

Le schéma JSON exact des réglages, celui que l'API applique pour valider le champ params :

`GET /v1/modules/channelMixer/schema`

```json
{
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "space": {
      "title": "Space",
      "default": "rgb",
      "type": "string",
      "enum": [
        "rgb",
        "gray",
        "cmyk",
        "lab"
      ]
    },
    "rgbRFromRgbR": {
      "title": "Red",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbRFromRgbG": {
      "title": "Green",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbRFromRgbB": {
      "title": "Blue",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbRFromRgbAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbR": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "rgbGFromRgbR": {
      "title": "Red",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbGFromRgbG": {
      "title": "Green",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbGFromRgbB": {
      "title": "Blue",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbGFromRgbAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbG": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "rgbBFromRgbR": {
      "title": "Red",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbBFromRgbG": {
      "title": "Green",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbBFromRgbB": {
      "title": "Blue",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbBFromRgbAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbB": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbR": {
      "title": "Red",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbG": {
      "title": "Green",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbB": {
      "title": "Blue",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "rgbAlphaFromRgbAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetRgbAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "grayIFromGrayI": {
      "title": "Intensity",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "grayIFromGrayAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetGrayI": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "grayAlphaFromGrayI": {
      "title": "Intensity",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "grayAlphaFromGrayAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetGrayAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykCFromCmykC": {
      "title": "Cyan",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykCFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykC": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykMFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykM": {
      "title": "Magenta",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykMFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykM": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykYFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykY": {
      "title": "Yellow",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykYFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykY": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykKFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykK": {
      "title": "Black",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykKFromCmykAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykK": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykC": {
      "title": "Cyan",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykM": {
      "title": "Magenta",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykY": {
      "title": "Yellow",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykK": {
      "title": "Black",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "cmykAlphaFromCmykAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetCmykAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labLFromLabL": {
      "title": "Lightness",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labLFromLabA": {
      "title": "Chroma A",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labLFromLabB": {
      "title": "Chroma B",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labLFromLabAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabL": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labAFromLabL": {
      "title": "Lightness",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAFromLabA": {
      "title": "Chroma A",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAFromLabB": {
      "title": "Chroma B",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAFromLabAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabA": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labBFromLabL": {
      "title": "Lightness",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labBFromLabA": {
      "title": "Chroma A",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labBFromLabB": {
      "title": "Chroma B",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labBFromLabAlpha": {
      "title": "Alpha",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabB": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "labAlphaFromLabL": {
      "title": "Lightness",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAlphaFromLabA": {
      "title": "Chroma A",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAlphaFromLabB": {
      "title": "Chroma B",
      "default": 0,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "labAlphaFromLabAlpha": {
      "title": "Alpha",
      "default": 100,
      "type": "number",
      "minimum": -200,
      "maximum": 200,
      "multipleOf": 1
    },
    "offsetLabAlpha": {
      "title": "Offset",
      "default": 0,
      "type": "number",
      "minimum": -100,
      "maximum": 100,
      "multipleOf": 1
    },
    "blendMode": {
      "title": "Blend mode",
      "default": "normal",
      "type": "string",
      "enum": [
        "normal",
        "multiply",
        "screen",
        "overlay",
        "darken",
        "color-burn",
        "lighten",
        "color-dodge",
        "soft-light",
        "hard-light",
        "difference",
        "exclusion",
        "hue",
        "saturation",
        "color",
        "luminosity"
      ]
    },
    "blendOpacity": {
      "title": "Opacity",
      "default": 100,
      "type": "number",
      "minimum": 0,
      "maximum": 100,
      "multipleOf": 1
    },
    "frameMethod": {
      "title": "Method",
      "default": "module",
      "type": "string",
      "enum": [
        "module",
        "source",
        "custom"
      ]
    },
    "frameWidth": {
      "title": "Width",
      "type": "number",
      "minimum": 1,
      "maximum": 16384
    },
    "frameHeight": {
      "title": "Height",
      "type": "number",
      "minimum": 1,
      "maximum": 16384
    },
    "frameFit": {
      "title": "Fit",
      "default": "none",
      "type": "string",
      "enum": [
        "none",
        "contain",
        "cover",
        "stretch"
      ]
    },
    "frameAnchor": {
      "title": "Anchor",
      "default": "center",
      "type": "string",
      "enum": [
        "top-left",
        "top",
        "top-right",
        "left",
        "center",
        "right",
        "bottom-left",
        "bottom",
        "bottom-right"
      ]
    }
  }
}
```

## Erreurs

Réglage hors limites, fichier manquant, crédits insuffisants : chaque refus a son code HTTP.
