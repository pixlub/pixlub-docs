# Inverser

Passer une image en négatif.

**Catégorie** : Ajustement · **Identifiant** : `invert` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/invert)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image passée en négatif. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Le négatif en un geste.](../../../../assets/modules/invert/demo.fr.webp)](../../../../assets/modules/invert/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/invert/demo.fr.mp4) : Le négatif en un geste.

1. `0:00` Importer une image
2. `0:02` Le négatif, sans réglage
3. `0:05` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images : elles passent en négatif, sans réglage.

## Astuces

- Inverser deux fois redonne l'image d'origine.
- Pour inverser un masque noir et blanc dans le [graphe d'image](../../../../01-app/fr/02-image/01-image-graph.md), c'est le même module.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
