# Tracé

Dessiner une courbe à main levée, lissée et fuselée.

**Catégorie** : Génération · **Identifiant** : `pathStroke`

## Où l'utiliser

- **[Page du module](https://pixlub.com/fr/module/pathStroke)** : Déposez vos fichiers, réglez, téléchargez : le module seul, sans rien d'autre.
- **[Graphe d'image](https://pixlub.com/fr/image/graph)** : Reliez-le à d'autres modules pour composer un effet plus complexe.

## Entrées

Ce module n’a pas d’entrée : il crée l’image à partir de ses seuls réglages.

## Présentation vidéo

[![Dessiner le tracé, épaisseur et fuselage, couleur.](../../../../assets/modules/pathStroke/demo.fr.webp)](../../../../assets/modules/pathStroke/demo.fr.mp4)

▶ [Voir la vidéo](../../../../assets/modules/pathStroke/demo.fr.mp4) : Dessiner le tracé, épaisseur et fuselage, couleur.

1. `0:00` Le rendu s’affiche d’emblée
2. `0:01` Dessiner le tracé
3. `0:07` Épaisseur et fuselage
4. `0:13` Couleur
5. `0:18` Exporter le résultat

## Utilisation

1. **Dessiner**

   Choisissez à gauche de l'aperçu des points **Bézier** (arrondis) ou **linéaires** (vifs), puis cliquez pour les poser ; cliquez sur le trait pour en insérer un, sur le premier point pour fermer la forme.

2. **Façonner**

   Glissez les points : ils s'aimantent aux autres points et au centre, **Maj** les guide par pas de 15°. Les poignées orange règlent la courbure, les carrés verts l'épaisseur locale.

3. **Régler le trait**

   **Épaisseur**, **fuselage** et **couleur**.

## Réglages

| Réglage | Effet |
| --- | --- |
| **Couleur** / **Épaisseur** | Aspect du trait, 1 à 200 px. |
| **Fuselage** | Affinement aux extrémités, 0 à 100 %. |
| **Arrondi des angles** | Force des courbes aux points Bézier ; 50 % = arcs de cercle exacts. |
| **Boucle fermée** | Relie le dernier point au premier. |
| **Points** | Position, épaisseur locale et type (**Bézier** ou **linéaire**) de chaque point ; dans le graphe, X, Y et l'épaisseur de chaque point s'animent. |
| **Dimensions** | Taille de la zone. |

## Astuces

- Posez quelques points en rond puis **Cercle parfait** ; **Répartir les points** régularise une forme déjà dessinée.
- Un double-clic sur un point le retire ; **Alt** brise la courbure, **Ctrl** la garde symétrique, **Ctrl+Z** annule.

## Exportation

Le bouton **Télécharger** enregistre le résultat dans le format du fichier importé : une photo JPEG ressort en JPEG. Le menu à sa droite ouvre les **Paramètres d’export** pour choisir un autre format, régler la qualité, la taille ou le fond, et propose **Copier l’image**.

- **[La modale d’exportation](../../../../01-app/fr/02-image/04-exportation.md)** : Tous les formats, leurs réglages, le traitement local ou serveur, les lots et le dossier local.
