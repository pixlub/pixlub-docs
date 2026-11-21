# Scanlines CRT

Poser des lignes de balayage et un masque RVB façon écran cathodique.

**Catégorie** : Filtres · **Identifiant** : `scanlines` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/scanlines)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image sur laquelle les lignes de balayage sont posées. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Espacement, intensité, puis masque RVB.](../../../../assets/modules/scanlines/demo.fr.webp)](../../../../assets/modules/scanlines/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/scanlines/demo.fr.mp4) : Espacement, intensité, puis masque RVB.

1. `0:00` Importer une image
2. `0:04` Espacement et intensité
3. `0:09` Masque RVB
4. `0:12` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Régler les lignes**

   **Espacement** et **intensité**.

3. **Ajouter le masque RVB**

   Les triades rouge, vert, bleu d'un vieil écran.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Espacement** | 2 à 40 px entre les lignes. |
| **Intensité** | 0 à 100 %. |
| **Masque RVB (triades)** | Ajoute la grille de couleurs. |

## Astuces

- Combinez avec [Aberration chromatique](../chromatic/README.md) et [Vignette](../vignette/README.md) pour un rendu d'écran rétro complet.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
