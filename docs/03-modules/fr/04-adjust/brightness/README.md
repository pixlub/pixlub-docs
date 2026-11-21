# Luminosité & Contraste

Éclaircir ou assombrir une image et régler son contraste.

**Catégorie** : Ajustement · **Identifiant** : `brightness` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/brightness)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont la luminosité et le contraste sont ajustés. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Luminosité, contraste, méthode de fusion et opacité.](../../../../assets/modules/brightness/demo.fr.webp)](../../../../assets/modules/brightness/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/brightness/demo.fr.mp4) : Luminosité, contraste, méthode de fusion et opacité.

1. `0:00` Importer une image
2. `0:02` Luminosité
3. `0:05` Contraste
4. `0:09` Méthode de fusion
5. `0:12` Doser avec l’opacité
6. `0:20` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Régler**

   **Luminosité** pour toute l'image, **Contraste** pour l'écart entre clairs et foncés.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Luminosité** | −100 à 100 %, sans toucher au contraste. |
| **Contraste** | −100 % aplatit l'image, +100 % la durcit. |
| **Fusion** | Méthode de fusion et opacité : comment le réglage se pose sur l'image d'origine. |

## Astuces

- Pour un réglage plus fin des tons, voyez [Niveaux](../levels/README.md) ou [Courbes](../curves/README.md).

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
