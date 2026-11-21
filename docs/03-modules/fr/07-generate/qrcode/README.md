# QR code

Générer un QR code lisible par tout lecteur, stylé, avec un logo, ou fondu dans une image.

**Catégorie** : Génération · **Identifiant** : `qrcode` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/qrcode)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Logo** (facultative)<br />Image facultative posée au centre du QR code ; la correction monte à H en automatique. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un fichier |
| **Image** (facultative)<br />Image facultative convertie en motif de QR code, dans laquelle le QR code se fond (mode « Dans une image ») ; sa transparence donne la silhouette. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un fichier |

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Utilisation

1. **Choisir le contenu**

   Lien, texte, Wi-Fi, e-mail, téléphone, SMS, contact (vCard) ou position. Chaque type suit le format que lisent les lecteurs courants.

2. **Styler**

   Section **Design**, bouton **Design, couleurs et décor** : une galerie en vignettes pour la forme, les modules, les yeux et les couleurs. Les réglages fins (taille, opacité, dégradé…) restent dans le panneau.

3. **Ajouter un logo**

   Reliez une image à l'entrée **Logo** : elle se pose au centre, sur une plaque, et la correction monte à H.

4. **Mettre dans une forme**

   Section **Intégration**, mode **Dans une forme** : cloche, cœur, maison, nuage, tasse… ou **Depuis l'image** pour la silhouette d'une image reliée (sa transparence, ou son contour pour un dessin au trait). La silhouette, blanche et cernée, se remplit de modules du même dessin que le QR code, qui s'y place tout seul ; glissez-le dans l'aperçu, tirez un coin pour sa taille.

5. **Fondre dans une image**

   Section **Intégration**, mode **Dans une image**, puis reliez une image (un poisson, un logo…) à l'entrée **Image**. Elle devient un motif de modules dans le style du QR code ; glissez le QR code dedans dans l'aperçu, tirez un coin pour changer la taille des modules.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Type** | Lien, texte, Wi-Fi, e-mail, téléphone, SMS, contact, position. |
| **Correction d'erreur** | Auto (M, ou H avec logo ou demi-teinte), L, M, Q, H. |
| **Version minimale** / **Masque** | Grille plus fine ou fixe ; motif de brouillage. |
| **Modules** | Carrés, fluide, points, carrés arrondis, losanges, étoiles, croix, cœurs, feuilles, barres, confettis ; taille et arrondi. |
| **Yeux** | Cadre et centre des yeux et des motifs d'alignement, couleurs propres. |
| **Couleurs** | Couleur ou dégradé des modules, fond, opacités, coins du fond. |
| **Dimensions** | Taille de l'image et marge (4 modules selon la norme). |
| **Logo** | Taille, plaque (carrée, arrondie, ronde), marge, dégagement des modules, opacité. **Taille sûre** ramène le logo à la plus grande taille que la correction d'erreur sait réparer. |
| **Silhouette** | Forme, épaisseur et couleur du contour, densité du motif. |
| **Placement** | Taille des modules, position du QR code, halo clair autour, liseré clair autour des yeux. |
| **Conversion** | Motif QR (par défaut), seuil, diffusion ou trame ; relief des tons, variante, seuil, contraste, inversion, silhouette et contour, couleur des modules. |
| **Fusion** | Image à travers le QR (demi-teinte) et sa force, fond plein sous le QR, image d'origine en fond. |

## Astuces

- Testez toujours le scan avec plusieurs téléphones avant d'imprimer.
- Gardez des modules nettement plus sombres que le fond ; un code clair sur fond sombre n'est pas lu par tous les lecteurs.
- Pour les yeux, gardez une même famille de formes entre cadre et centre (carré avec carré, rond avec rond).
- En mode image, le **Motif QR** transforme l'image en texture de QR code : avec un halo à 0, le code s'y fond sans bord. Avec **Couleur des modules : de l'image**, motif, QR code et yeux prennent la couleur de l'image sous eux.
- Un logo trop grand cache des mots de code : laissez **Taille sûre** cochée, et montez la correction à H pour un logo plus grand.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
