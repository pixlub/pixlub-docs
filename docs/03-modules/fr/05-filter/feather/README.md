# Contour progressif

Adoucir les bords de la transparence d'une image.

**Catégorie** : Filtres · **Identifiant** : `feather` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/feather)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont les bords de la transparence sont adoucis. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Rayon, direction, puis fondu coloré.](../../../../assets/modules/feather/demo.fr.webp)](../../../../assets/modules/feather/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/feather/demo.fr.mp4) : Rayon, direction, puis fondu coloré.

1. `0:00` Importer une image détourée
2. `0:02` Rayon du fondu
3. `0:05` Direction
4. `0:07` Colorer le fondu
5. `0:08` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une image avec de la transparence.

2. **Régler le fondu**

   Le **rayon** fixe sa largeur, la **direction** son côté.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Rayon** | 1 à 100 px. |
| **Direction** | Les deux, intérieur ou extérieur. |
| **Colorer le fondu** | Teinte le bord adouci de la **couleur** choisie. |

## Astuces

- Un détourage trop net s'intègre mieux sur un nouveau fond avec 2 à 4 px de fondu.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
