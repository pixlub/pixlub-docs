# Courbes

Régler les tons d'une image par une courbe, sur tous les canaux ou un seul.

**Catégorie** : Ajustement · **Identifiant** : `curves` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/curves)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont la tonalité est ajustée par les courbes. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Courbe en S, courbes toutes prêtes, un canal seul.](../../../../assets/modules/curves/demo.fr.webp)](../../../../assets/modules/curves/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/curves/demo.fr.mp4) : Courbe en S, courbes toutes prêtes, un canal seul.

1. `0:00` Importer une image
2. `0:02` Courbe en S : plus de contraste
3. `0:09` Courbes toutes prêtes
4. `0:14` Un canal à la fois
5. `0:21` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Tirer la courbe**

   Glissez un point de la courbe : vers le haut les tons s'éclaircissent, vers le bas ils s'assombrissent.

3. **Ou partir d'un modèle**

   Le menu sous la courbe propose des courbes toutes prêtes.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Espace** | RVB, Gris, CMJN ou LAB. |
| **Canal** | Maître (tous les canaux) ou un seul. Toutes les courbes s'appliquent ensemble. |
| **Courbe** | Axe horizontal : valeur d'origine. Axe vertical : valeur qu'elle prend. |
| **Fusion** | Méthode de fusion et opacité : comment le réglage se pose sur l'image d'origine. |

## Astuces

- Une courbe en **S** (ombres baissées, lumières montées) ajoute du contraste sans brûler.
- Monter le début de la courbe donne des noirs délavés, effet film.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
