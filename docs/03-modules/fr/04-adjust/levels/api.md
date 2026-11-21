# Niveaux : référence API

Ajuste les points noir et blanc, le gamma et la plage de sortie, par canal

[Voir comment l'utiliser sur le site](./README.md)

| Point d’accès | Coût |
| --- | --- |
| `POST /v1/modules/levels` | 1 crédit par fichier |

## Fichiers

| Champ | Requis | Formats | Description |
| --- | --- | --- | --- |
| `in` (Une image ou plusieurs) | oui | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | **Image(s)**<br />Image dont les niveaux sont ajustés. |

## Réglages

### Général

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `space` | `string` | `"rgb"` | `rgb` RVB<br />`gray` Gris<br />`cmyk` CMJN<br />`lab` LAB | **Espace**<br />Espace colorimétrique dans lequel les canaux sont ajustés |

### Espace RVB

> Ces réglages ne comptent que quand `space` = `rgb` (RVB).

#### Maître

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackRgbMaster` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteRgbMaster` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaRgbMaster` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackRgbMaster` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteRgbMaster` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Rouge

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackRgbR` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteRgbR` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaRgbR` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackRgbR` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteRgbR` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Vert

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackRgbG` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteRgbG` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaRgbG` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackRgbG` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteRgbG` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Bleu

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackRgbB` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteRgbB` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaRgbB` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackRgbB` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteRgbB` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Alpha

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackRgbAlpha` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteRgbAlpha` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaRgbAlpha` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackRgbAlpha` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteRgbAlpha` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

### Espace Gris

> Ces réglages ne comptent que quand `space` = `gray` (Gris).

#### Maître

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackGrayMaster` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteGrayMaster` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaGrayMaster` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackGrayMaster` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteGrayMaster` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Intensité

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackGrayI` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteGrayI` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaGrayI` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackGrayI` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteGrayI` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Alpha

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackGrayAlpha` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteGrayAlpha` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaGrayAlpha` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackGrayAlpha` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteGrayAlpha` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

### Espace CMJN

> Ces réglages ne comptent que quand `space` = `cmyk` (CMJN).

#### Maître

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackCmykMaster` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteCmykMaster` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaCmykMaster` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackCmykMaster` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteCmykMaster` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Cyan

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackCmykC` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteCmykC` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaCmykC` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackCmykC` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteCmykC` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Magenta

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackCmykM` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteCmykM` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaCmykM` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackCmykM` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteCmykM` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Jaune

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackCmykY` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteCmykY` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaCmykY` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackCmykY` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteCmykY` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Noir

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackCmykK` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteCmykK` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaCmykK` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackCmykK` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteCmykK` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Alpha

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackCmykAlpha` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteCmykAlpha` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaCmykAlpha` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackCmykAlpha` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteCmykAlpha` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

### Espace LAB

> Ces réglages ne comptent que quand `space` = `lab` (LAB).

#### Maître

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackLabMaster` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteLabMaster` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaLabMaster` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackLabMaster` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteLabMaster` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Luminosité

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackLabL` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteLabL` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaLabL` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackLabL` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteLabL` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Chrominance A

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackLabA` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteLabA` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaLabA` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackLabA` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteLabA` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Chrominance B

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackLabB` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteLabB` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaLabB` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackLabB` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteLabB` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

#### Alpha

| Réglage | Type | Par défaut | Valeurs permises | Description |
| --- | --- | --- | --- | --- |
| `blackLabAlpha` | `number` | `0` | min 0 · max 254 · pas de 1 | **Niveau de noir**<br />Tout ce qui est plus sombre devient noir. Monter ce point approfondit les ombres et écrase le détail qui s'y trouve. |
| `whiteLabAlpha` | `number` | `255` | min 1 · max 255 · pas de 1 | **Niveau de blanc**<br />Tout ce qui est plus clair devient blanc. Descendre ce point éclaircit l'image et brûle les hautes lumières. |
| `gammaLabAlpha` | `number` | `1` | min 0.1 · max 4 · pas de 0.05 | **Gamma**<br />Courbe les tons moyens sans toucher aux deux bornes. Sous 1 le canal s'assombrit, au-dessus il s'éclaircit. |
| `outBlackLabAlpha` | `number` | `0` | min 0 · max 255 · pas de 1 | **Niveau de noir de sortie**<br />Valeur que prend le noir en sortie. La monter délave les ombres. |
| `outWhiteLabAlpha` | `number` | `255` | min 0 · max 255 · pas de 1 | **Niveau de blanc de sortie**<br />Valeur que prend le blanc en sortie. La descendre ternit les hautes lumières. |

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
curl -X POST https://api.pixlub.com/v1/modules/levels \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@in.png \
  -F 'params={"space":"rgb","blackRgbMaster":0,"whiteRgbMaster":255}'
```

### JavaScript

```js
import { openAsBlob } from 'node:fs'

const form = new FormData()
form.append('in', await openAsBlob('in.png'), 'in.png')
form.append('params', JSON.stringify({"space":"rgb","blackRgbMaster":0,"whiteRgbMaster":255}))

const res = await fetch('https://api.pixlub.com/v1/modules/levels', {
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
    "https://api.pixlub.com/v1/modules/levels",
    headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
    files=[("in", open("in.png", "rb"))],
    data={"params": json.dumps({"space": "rgb", "blackRgbMaster": 0, "whiteRgbMaster": 255})},
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
result = client.tools.run("levels", image="photo.png", params={"space": "rgb", "blackRgbMaster": 0, "whiteRgbMaster": 255})
result.save(f"levels{result.extension}")
print(result.cost, result.credits_balance)
```

### SDK Go

```go
client, err := pixlub.NewClient() // PIXLUB_API_KEY, PIXLUB_BASE_URL
if err != nil {
    log.Fatal(err)
}
result, err := client.Tools.Run(ctx, "levels", pixlub.RunRequest{
    Image: pixlub.FromPath("photo.png"),
    Params: map[string]any{"space": "rgb", "blackRgbMaster": 0, "whiteRgbMaster": 255},
})
if err != nil {
    log.Fatal(err)
}
err = result.Save("levels"+result.Extension(), false)
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
  "module": "levels",
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

`GET /v1/modules/levels/schema`

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
    "blackRgbMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbR": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbR": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbR": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbR": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbR": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbG": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbG": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbG": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbG": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbG": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbB": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbB": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbB": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbB": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbB": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackRgbAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteRgbAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaRgbAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackRgbAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteRgbAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackGrayMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteGrayMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaGrayMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackGrayMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteGrayMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackGrayI": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteGrayI": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaGrayI": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackGrayI": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteGrayI": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackGrayAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteGrayAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaGrayAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackGrayAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteGrayAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykC": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykC": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykC": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykC": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykC": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykM": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykM": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykM": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykM": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykM": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykY": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykY": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykY": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykY": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykY": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykK": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykK": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykK": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykK": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykK": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackCmykAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteCmykAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaCmykAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackCmykAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteCmykAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabMaster": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabMaster": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabMaster": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabMaster": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabMaster": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabL": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabL": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabL": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabL": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabL": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabA": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabA": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabA": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabA": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabA": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabB": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabB": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabB": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabB": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabB": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "blackLabAlpha": {
      "title": "Black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 254,
      "multipleOf": 1
    },
    "whiteLabAlpha": {
      "title": "White level",
      "default": 255,
      "type": "number",
      "minimum": 1,
      "maximum": 255,
      "multipleOf": 1
    },
    "gammaLabAlpha": {
      "title": "Gamma",
      "default": 1,
      "type": "number",
      "minimum": 0.1,
      "maximum": 4,
      "multipleOf": 0.05
    },
    "outBlackLabAlpha": {
      "title": "Output black level",
      "default": 0,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
      "multipleOf": 1
    },
    "outWhiteLabAlpha": {
      "title": "Output white level",
      "default": 255,
      "type": "number",
      "minimum": 0,
      "maximum": 255,
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
