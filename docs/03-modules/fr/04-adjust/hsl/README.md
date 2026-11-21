# HSL

Changer la teinte, la saturation et la luminosité d'une plage de couleurs seulement.

**Catégorie** : Ajustement · **Identifiant** : `hsl` · [Référence API](./api.md)

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/hsl)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Les fichiers que la page du module accepte : déposez-les sur la zone d’import, ou cliquez dessus pour parcourir. Un fichier d’un autre format est écarté, avec un message qui rappelle les formats permis.

| Entrée | Formats acceptés | Fichiers |
| --- | --- | --- |
| **Image(s)** (obligatoire)<br />Image dont une plage de couleurs est décalée en teinte, saturation et luminosité. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un ou plusieurs : chaque image est traitée à part, avec les mêmes réglages |

Le nombre d’images traitées d’un coup dépend de votre offre.

Par l’API, les fichiers et leurs formats sont détaillés dans la [vue API](./api.md).

## Présentation vidéo

[![Viser le bleu du ciel, décaler sa teinte, sa saturation et sa luminosité.](../../../../assets/modules/hsl/demo.fr.webp)](../../../../assets/modules/hsl/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/hsl/demo.fr.mp4) : Viser le bleu du ciel, décaler sa teinte, sa saturation et sa luminosité.

1. `0:00` Importer une image
2. `0:02` Viser une couleur : le bleu du ciel
3. `0:11` Décaler sa teinte
4. `0:14` Saturation et luminosité
5. `0:22` Exporter le résultat

## Utilisation

1. **Importer**

   Déposez une ou plusieurs images.

2. **Viser une couleur**

   Réglez la **couleur ciblée**, puis réduisez l'**étendue** pour ne toucher qu'elle.

3. **La modifier**

   Décalez sa **teinte**, sa **saturation** ou sa **luminosité**.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Couleur ciblée** | Teinte, saturation et luminosité des couleurs à modifier. |
| **Étendue** | 0 à 100 %. À 100 %, toute l'image change. |
| **Décalage teinte** | −180° à 180°. |
| **Décalage saturation** / **luminosité** | −100 à 100 % : vers le gris ou plus vif, vers le noir ou le blanc. |
| **Fusion** | Méthode de fusion et opacité : comment le réglage se pose sur l'image d'origine. |

## Astuces

- Pour un ciel plus profond : visez le bleu et baissez sa luminosité.
- Une étendue faible évite de toucher les peaux en modifiant un orange.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

Avec plusieurs images, le bouton devient **Téléchargement ZIP** ; le menu propose aussi les fichiers séparés, ou la seule image affichée.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
