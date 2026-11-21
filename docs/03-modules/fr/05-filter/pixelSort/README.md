# Tri de pixels

Trier les pixels par clarté dans les zones claires ou sombres, effet glitch art.

**Catégorie** : Filtres · **Identifiant** : `pixelSort` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/pixelSort)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont les pixels sont triés par luminance. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Seuil, direction et zones triées.](../../../../assets/modules/pixelSort/demo.fr.webp)](../../../../assets/modules/pixelSort/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/pixelSort/demo.fr.mp4) : Seuil, direction et zones triées.

1. `0:00` Importer une image
2. `0:02` Seuil des zones triées
3. `0:05` Direction et zones
4. `0:09` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Régler le seuil**

   Il décide quelles zones sont triées.

3. **Choisir direction et zones**

   Horizontal ou vertical, zones claires ou sombres.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Direction** | Horizontal ou vertical. |
| **Zones triées** | Claires ou sombres. |
| **Seuil** | 0 à 100 % de luminance. |
| **Inverser le sens du tri** | Du clair au sombre, ou l'inverse. |

## Astuces

- Tri vertical des zones claires sur un ciel : des coulures de lumière.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
