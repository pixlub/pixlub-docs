# Noir et blanc

Passer une image en gris en choisissant la clarté de chaque couleur.

**Catégorie** : Ajustement · **Identifiant** : `blackWhite` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/blackWhite)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image passée en noir et blanc. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Le ciel par le bleu, les façades par le rouge et le jaune.](../../../../assets/modules/blackWhite/demo.fr.webp)](../../../../assets/modules/blackWhite/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/blackWhite/demo.fr.mp4) : Le ciel par le bleu, les façades par le rouge et le jaune.

1. `0:00` Importer une image
2. `0:03` Éclaircir le bleu : le ciel
3. `0:09` Rouge et jaune : les façades
4. `0:17` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images : elles passent en gris.

2. **Doser chaque couleur**

   Une couleur montée s'éclaircit dans le gris, baissée elle s'assombrit.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Rouge**, **Jaune**, **Vert**, **Cyan**, **Bleu**, **Magenta** | 0 à 100 % : clarté que prend chaque couleur. |
| **Fusion** | Méthode de fusion et opacité : comment le réglage se pose sur l'image d'origine. |

## Astuces

- Baisser le **bleu** donne un ciel sombre et dramatique, comme avec un filtre rouge.
- Monter le **rouge** et le **jaune** éclaircit les peaux.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
