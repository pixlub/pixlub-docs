# Polaire

Enrouler une image en cercle, ou dérouler un cercle en bande : anneaux, rayons, halos.

**Catégorie** : Transformation · **Identifiant** : `polar` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/polar)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image convertie entre coordonnées rectangulaires et polaires. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Enroulement en cercle, rotation, puis conversion inverse.](../../../../assets/modules/polar/demo.fr.webp)](../../../../assets/modules/polar/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/polar/demo.fr.mp4) : Enroulement en cercle, rotation, puis conversion inverse.

1. `0:00` Importer une image
2. `0:03` Rotation
3. `0:07` Polaire vers rectangulaire
4. `0:12` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Choisir le sens**

   **Rectangulaire à Polaire** enroule l'image autour du centre ; **Polaire à Rectangulaire** fait l'inverse.

3. **Tourner**

   La **rotation** fait pivoter le résultat autour du centre.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Conversion** | **Rectangulaire à Polaire** ou **Polaire à Rectangulaire**. |
| **Rotation** | −180° à 180°. |

## Astuces

- Une image large (un panorama) donne un « petit monde » une fois enroulée.
- Polaire à Rectangulaire déroule une photo de cible ou de cadran en bande droite.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
