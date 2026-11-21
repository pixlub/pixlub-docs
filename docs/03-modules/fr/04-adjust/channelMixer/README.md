# Mélangeur de canaux

Recomposer chaque canal d'une image à partir des autres.

**Catégorie** : Ajustement · **Identifiant** : `channelMixer` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/channelMixer)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont les canaux sont recomposés. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Recomposer le rouge, puis le bleu.](../../../../assets/modules/channelMixer/demo.fr.webp)](../../../../assets/modules/channelMixer/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/channelMixer/demo.fr.mp4) : Recomposer le rouge, puis le bleu.

1. `0:00` Importer une image
2. `0:02` Recomposer le rouge
3. `0:09` Puis le bleu
4. `0:17` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Choisir le canal**

   Le menu **Canal** choisit celui qu'on recompose.

3. **Doser ses sources**

   Chaque glissière dit quelle part d'un autre canal il reprend.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Espace** | RVB, Gris, CMJN ou LAB. |
| **Canal** | Canal recomposé ; tous s'appliquent ensemble. |
| **Sources** | Part de chaque canal d'origine, en %. |
| **Décalage** | Éclaircit ou assombrit le canal d'un bloc. |
| **Fusion** | Méthode de fusion et opacité : comment le réglage se pose sur l'image d'origine. |

## Astuces

- Rouge pris dans le bleu et bleu pris dans le rouge : les couleurs s'échangent, effet infrarouge.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
