# Exposition

Rehausser ou baisser la lumière d'une image, cran par cran comme un appareil photo.

**Catégorie** : Ajustement · **Identifiant** : `exposure` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/exposure)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont l'exposition est corrigée. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Surexposer, puis sous-exposer.](../../../../assets/modules/exposure/demo.fr.webp)](../../../../assets/modules/exposure/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/exposure/demo.fr.mp4) : Surexposer, puis sous-exposer.

1. `0:00` Importer une image
2. `0:02` Surexposer
3. `0:06` Sous-exposer
4. `0:10` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Régler l'exposition**

   Vers la droite l'image s'éclaire, vers la gauche elle s'assombrit.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Exposition** | −10 à 10 IL. +1 double la lumière, −1 la divise par deux. |
| **Fusion** | Méthode de fusion et opacité : comment le réglage se pose sur l'image d'origine. |

## Astuces

- Au-delà de +2 IL, les zones claires brûlent : baissez ensuite les hautes lumières dans [Ajustement Base](../baseAdjust/README.md).

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
