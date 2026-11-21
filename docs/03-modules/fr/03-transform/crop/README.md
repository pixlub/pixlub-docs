# Rogner

Garder une zone rectangulaire de l'image, à la souris ou au pixel près.

**Catégorie** : Transformation · **Identifiant** : `crop` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/crop)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dans laquelle la zone est découpée. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Tirer les poignées, déplacer la zone, saisir une taille exacte.](../../../../assets/modules/crop/demo.fr.webp)](../../../../assets/modules/crop/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/crop/demo.fr.mp4) : Tirer les poignées, déplacer la zone, saisir une taille exacte.

1. `0:00` Importer une image
2. `0:02` Tirer les poignées
3. `0:09` Déplacer la zone
4. `0:12` Saisir une taille exacte
5. `0:19` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Cadrer**

   Tirez les poignées du cadre pour le redimensionner, glissez son intérieur pour le déplacer.

3. **Ajuster au pixel près**

   Saisissez **X**, **Y**, **Largeur** et **Hauteur** dans le panneau.

## Réglages

| Réglage | Effet |
| --- | --- |
| **X** / **Y** | Coin haut gauche de la zone, en pixels. |
| **Largeur** / **Hauteur** | Taille de la zone, en pixels ou en %. |

## Astuces

- Dans un lot, la même zone s'applique à chaque image : préférez des tailles en **%** si les images n'ont pas la même taille.
- Pour retirer seulement des bords transparents, [Recadrage auto](../trim/README.md) le fait seul.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
