# Carte de normales

Fabriquer une carte de normales (normal map) à partir d'une carte de hauteur, pour la 3D.

**Catégorie** : Filtres · **Identifiant** : `normalMap` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/normalMap)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Carte de hauteur (heightmap) en niveaux de gris : le clair est haut, le sombre est bas. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Relief, puis convention OpenGL ou DirectX.](../../../../assets/modules/normalMap/demo.fr.webp)](../../../../assets/modules/normalMap/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/normalMap/demo.fr.mp4) : Relief, puis convention OpenGL ou DirectX.

1. `0:00` Importer une carte de hauteur
2. `0:03` Relief
3. `0:06` Convention OpenGL ou DirectX
4. `0:08` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une carte de hauteur : le clair est haut, le sombre est bas.

2. **Doser le relief**

   Plus fort, les pentes s'accentuent.

3. **Choisir la convention**

   Celle de votre moteur 3D.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Relief** | 1 à 400 %. |
| **Convention** | **OpenGL (Y+)** : Blender, Unity, Godot. **DirectX (Y−)** : Unreal, 3ds Max. |

## Astuces

- Exportez en PNG : la compression JPEG abîme les normales.
- Une photo passée en [Noir et blanc](../../04-adjust/blackWhite/README.md) fait une carte de hauteur rapide.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
