# Bloom

Faire diffuser les zones lumineuses d'une image en halo.

**Catégorie** : Filtres · **Identifiant** : `bloom` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/bloom)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont les zones lumineuses diffusent un halo. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Seuil, diffusion et intensité.](../../../../assets/modules/bloom/demo.fr.webp)](../../../../assets/modules/bloom/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/bloom/demo.fr.mp4) : Seuil, diffusion et intensité.

1. `0:00` Importer une image
2. `0:02` Seuil des zones lumineuses
3. `0:05` Diffusion et intensité
4. `0:11` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Choisir le seuil**

   Seules les zones plus claires rayonnent.

3. **Doser le halo**

   **Diffusion** pour sa taille, **intensité** pour sa force.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Seuil** | 0 à 100 % de luminosité. |
| **Diffusion** | 0 à 300 px. |
| **Intensité** | 0 à 400 %. |

## Astuces

- Idéal sur des néons ou des lumières de nuit ; sur un ciel clair, montez le seuil.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
