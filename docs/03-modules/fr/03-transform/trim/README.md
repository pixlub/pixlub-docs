# Recadrage auto

Rogner automatiquement les bords transparents d'une image.

**Catégorie** : Transformation · **Identifiant** : `trim` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/trim)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont les bords transparents sont rognés. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Bords vides retirés, marge gardée, seuil de transparence.](../../../../assets/modules/trim/demo.fr.webp)](../../../../assets/modules/trim/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/trim/demo.fr.mp4) : Bords vides retirés, marge gardée, seuil de transparence.

1. `0:00` Importer une image transparente
2. `0:04` Les bords vides sont rognés
3. `0:08` Garder une marge
4. `0:12` Seuil de transparence
5. `0:17` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une image avec de la transparence (PNG, WebP…).

2. **C'est tout**

   Les bords vides disparaissent : l'image se resserre sur son contenu.

3. **Ajuster si besoin**

   Gardez une **marge** autour du contenu, ou montez le **seuil** pour ignorer les pixels presque transparents.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Seuil de transparence** | 0 à 100 %. Un pixel moins opaque que ce seuil compte comme vide. |
| **Marge conservée** | 0 à 500 px gardés autour du contenu. |

## Astuces

- Idéal après un détourage : l'objet se retrouve cadré au plus près.
- Une image sans transparence ne change pas : utilisez [Rogner](../crop/README.md).

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
