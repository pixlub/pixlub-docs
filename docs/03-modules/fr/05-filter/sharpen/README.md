# Netteté

Renforcer les détails et les contours d'une image.

**Catégorie** : Filtres · **Identifiant** : `sharpen` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/sharpen)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont les détails et les contours sont renforcés. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Intensité, puis rayon, vus de près.](../../../../assets/modules/sharpen/demo.fr.webp)](../../../../assets/modules/sharpen/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/sharpen/demo.fr.mp4) : Intensité, puis rayon, vus de près.

1. `0:00` Importer une image
2. `0:04` Intensité
3. `0:08` Rayon
4. `0:12` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images. Zoomez dans l'aperçu pour juger.

2. **Doser**

   Montez l'**intensité**, ajustez le **rayon** à la finesse des détails.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Intensité** | 0 à 200 %. |
| **Rayon** | 1 à 10 px : fin pour les détails, large pour les contours. |

## Astuces

- Trop de netteté crée des halos clairs le long des bords : restez sous 100 % pour une photo.
- Appliquez la netteté en dernier, après un redimensionnement.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
