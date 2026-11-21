# Distorsion de lentille

Bomber une image comme un fisheye, ou la creuser en coussinet.

**Catégorie** : Transformation · **Identifiant** : `fisheye` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/fisheye)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image bombée ou creusée autour du centre. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Bomber, creuser, placer le centre.](../../../../assets/modules/fisheye/demo.fr.webp)](../../../../assets/modules/fisheye/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/fisheye/demo.fr.mp4) : Bomber, creuser, placer le centre.

1. `0:00` Importer une image
2. `0:02` Bomber l’image
3. `0:07` La creuser
4. `0:11` Placer le centre
5. `0:13` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Doser l'intensité**

   Positive, l'image se bombe ; négative, elle se creuse.

3. **Placer le centre**

   Cliquez dans l'aperçu.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Intensité** | −100 à 100 %. Positif : bombé (fisheye). Négatif : creusé (coussinet). |
| **Centre X** / **Y** | Position du centre, en %. |

## Astuces

- Une faible valeur négative corrige le bombé d'un objectif grand-angle.
- Une forte valeur positive, centrée sur un visage, donne un effet de loupe amusant.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
