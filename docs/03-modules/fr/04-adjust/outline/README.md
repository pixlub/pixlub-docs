# Contour

Entourer la silhouette d'une image détourée d'un trait de couleur.

**Catégorie** : Ajustement · **Identifiant** : `outline` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/outline)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont la silhouette (alpha) reçoit le contour. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Épaisseur, puis couleur du contour.](../../../../assets/modules/outline/demo.fr.webp)](../../../../assets/modules/outline/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/outline/demo.fr.mp4) : Épaisseur, puis couleur du contour.

1. `0:00` Importer une image détourée
2. `0:03` Épaisseur
3. `0:07` Couleur
4. `0:12` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une image avec de la transparence : le contour suit sa silhouette.

2. **Régler**

   Choisissez l'**épaisseur** puis la **couleur**.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Épaisseur** | 0 à 100 px. |
| **Couleur** | Couleur du trait. |

## Astuces

- Un contour blanc épais donne un effet autocollant ; ajoutez [Ombre](../shadow/README.md) pour le relief.
- Sur une image sans transparence, le contour suit seulement le bord du cadre.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
