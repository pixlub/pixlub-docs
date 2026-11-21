# Rayons lumineux

Faire jaillir des rayons de lumière des zones claires d'une image.

**Catégorie** : Filtres · **Identifiant** : `rays` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/rays)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont les zones claires émettent les rayons. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Longueur, intensité, centre, puis rayons seuls.](../../../../assets/modules/rays/demo.fr.webp)](../../../../assets/modules/rays/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/rays/demo.fr.mp4) : Longueur, intensité, centre, puis rayons seuls.

1. `0:00` Importer une image
2. `0:02` Longueur et intensité
3. `0:08` Placer le centre
4. `0:10` Rayons seuls
5. `0:12` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Régler les rayons**

   Longueur, intensité et **seuil** : seules les zones plus claires émettent.

3. **Placer la source**

   Cliquez dans l'aperçu là d'où vient la lumière.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Longueur** | 5 à 100 %. |
| **Intensité** | 0 à 200 %. |
| **Seuil de luminosité** | 0 à 100 % : zones qui émettent. |
| **Rayons seuls** | Affiche les rayons sans l'image. |
| **Centre X** / **Y** | Position de la source, en %. |

## Astuces

- Placez la source sur le soleil ou une fenêtre pour un effet « god rays » naturel.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
