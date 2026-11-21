# Peinture

Transformer une image en aplats de peinture qui gardent les contours.

**Catégorie** : Filtres · **Identifiant** : `kuwahara` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/kuwahara)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image transformée en aplats picturaux. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Taille de touche.](../../../../assets/modules/kuwahara/demo.fr.webp)](../../../../assets/modules/kuwahara/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/kuwahara/demo.fr.mp4) : Taille de touche.

1. `0:00` Importer une image
2. `0:04` Taille de touche
3. `0:07` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Régler la touche**

   Plus elle est grande, plus les aplats s'élargissent.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Taille de touche** | 2 à 16 px. |

## Astuces

- Ajoutez [Netteté](../sharpen/README.md) après pour un effet peinture à l'huile plus marqué.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
