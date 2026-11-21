# Pixeliser

Réduire une image en gros pixels, façon pixel art.

**Catégorie** : Filtres · **Identifiant** : `pixelate` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/pixelate)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image réduite en gros pixels. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Taille des pixels.](../../../../assets/modules/pixelate/demo.fr.webp)](../../../../assets/modules/pixelate/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/pixelate/demo.fr.mp4) : Taille des pixels.

1. `0:00` Importer une image
2. `0:02` Taille des pixels
3. `0:08` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Régler la taille**

   Tapez la taille des pixels, ou glissez sur la barre.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Taille des pixels** | 1 à 64 px. |

## Astuces

- Pour masquer une zone (plaque, visage), pixelisez puis limitez l'effet par un masque dans le [graphe d'image](../../../../01-app/fr/02-image/01-image-graph.md).

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
