# Aberration chromatique

Décaler les canaux rouge et bleu : effet d'objectif, glitch ou impact.

**Catégorie** : Filtres · **Identifiant** : `chromatic` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/chromatic)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont les canaux rouge et bleu sont décalés. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Décalage radial, centre, puis uniforme en traînée.](../../../../assets/modules/chromatic/demo.fr.webp)](../../../../assets/modules/chromatic/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/chromatic/demo.fr.mp4) : Décalage radial, centre, puis uniforme en traînée.

1. `0:00` Importer une image
2. `0:02` Décalage radial
3. `0:08` Placer le centre
4. `0:10` Uniforme, en traînée
5. `0:14` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Doser le décalage**

   L'**intensité** écarte les canaux, la **zone préservée** garde le centre net.

3. **Placer le centre**

   En mode radial, cliquez dans l'aperçu.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Mode** | **Radial** (depuis un centre) ou **Uniforme** (dans une direction). |
| **Intensité** | 0 à 100 px. |
| **Méthode** | **Décalage** net ou **Traînée**. |
| **Zone préservée** / **Douceur** | Mode radial : centre intact et fondu vers les bords. |
| **Angle** | Mode uniforme : direction du décalage. |

## Astuces

- Un faible décalage radial imite un vrai objectif ; un fort décalage uniforme donne un effet glitch.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
