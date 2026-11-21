# Onde

Onduler une image en vagues horizontales, verticales ou les deux.

**Catégorie** : Transformation · **Identifiant** : `wave` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/wave)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image déformée par la vague. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Axe, amplitude, longueur d'onde et phase.](../../../../assets/modules/wave/demo.fr.webp)](../../../../assets/modules/wave/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/wave/demo.fr.mp4) : Axe, amplitude, longueur d'onde et phase.

1. `0:00` Importer une image
2. `0:03` Axe de l’onde
3. `0:07` Amplitude et longueur d’onde
4. `0:11` Phase
5. `0:16` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Choisir l'axe**

   **Horizontal**, **Vertical** ou **Les deux** pour un effet de drapeau.

3. **Régler les vagues**

   **Amplitude** pour leur hauteur, **longueur d'onde** pour leur écart.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Axe** | Horizontal, vertical ou les deux. |
| **Amplitude** | 0 à 200 px. |
| **Longueur d'onde** | 4 à 1000 px entre deux crêtes. |
| **Phase** | 0° à 360°. Fait glisser les vagues. |

## Astuces

- Une grande longueur d'onde et une petite amplitude donnent un léger tremblé, comme un reflet.
- Animez la **phase** dans le [graphe d'image](../../../../01-app/fr/02-image/01-image-graph.md) pour un drapeau qui flotte.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
