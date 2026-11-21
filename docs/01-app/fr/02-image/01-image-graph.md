# Graphe d'image

Composer une image en reliant des modules : sources, effets, sorties, animation et projets .epxl.

Le [graphe d'image](https://pixlub.com/fr/image/graph) est l'éditeur le plus complet de Pixlub. Chaque **module** y devient un nœud ; on relie la sortie d'un nœud à l'entrée d'un autre pour enchaîner les opérations. Rien n'est figé : changer un réglage en amont recalcule toute la chaîne.

## Démarrer un projet

À l'ouverture, une fenêtre propose trois départs :

- **Nouveau projet** : une toile vierge ;
- **Importer** : un projet `.epxl` enregistré plus tôt, ou un projet de votre [dossier local](../05-account-and-credits.md#dossier-local) ;
- **Guides découverte** : des mini-projets annotés qui montrent comment combiner les modules.

## Construire le graphe

1. **Ajouter une image**

   Glissez une ou plusieurs images sur la toile : chacune devient un module **Image source**. Plusieurs images déposées ensemble forment un **batch**, traité d'un coup.

2. **Ajouter des modules**

   Le rayon de gauche liste tous les modules, avec une recherche et des préréglages. Glissez-en un sur la toile, ou faites un clic droit sur la toile.

3. **Relier les ports**

   Tirez depuis la sortie d'un module jusqu'à l'entrée d'un autre. Un port ne se branche que sur un type compatible ; la légende des connexions rappelle les couleurs.

4. **Régler**

   Cliquez sur un module pour ouvrir son panneau. L'onglet **Paramètres** contient ses réglages ; l'onglet **Propriété** son titre, sa couleur et l'affichage de son aperçu.

5. **Exporter**

   Reliez le résultat à un module **Sortie**, puis exportez dans le format voulu.

## Les types de port

| Port | Ce qui circule |
| --- | --- |
| Image | Une image en couleur, avec transparence. |
| Canal | Une image en niveaux de gris : un canal R, G, B ou A, un masque. |
| Nombre | Une valeur, issue des modules **Valeurs** (taille d'image, addition…). |
| Couleur | Une couleur unie. |
| Palette | Une liste de couleurs. |
| Batch | Un lot d'images traitées ensemble. |
| Tracé | Un chemin vectoriel. |
| Modèle 3D | Un modèle, pour les modules 3D. |

Une entrée **obligatoire** non branchée est signalée sur le nœud. Un port **Batch** branché sur une entrée simple n'utilise qu'une image du lot ; l'aperçu permet de choisir laquelle.

## Organiser la toile

- **Outils** de la barre : déplacement, sélection au lasso, regroupement de la sélection dans une **frame**, recadrage de la vue et zoom.
- **Notes** : ajoutez une note depuis le rayon pour annoter le graphe (gras, italique).
- **Désactiver** un module le met hors circuit sans le supprimer : utile pour comparer.
- **Annuler / Rétablir** : <kbd>Ctrl</kbd> + <kbd>Z</kbd> et <kbd>Ctrl</kbd> + <kbd>Y</kbd>.
- **Pause** : la barre du haut suspend le calcul des images pendant que vous construisez un graphe lourd.

## Aperçus et outils

L'aperçu d'un nœud s'affiche dans la toile et en grand dans le panneau. On peut y zoomer, changer le fond, isoler le canal alpha ou un canal de couleur. Plusieurs modules s'y manipulent directement : recadrage, rotation, perspective, déformation à épingles, tracés, zones de flou…

> [!NOTE]
> **Aperçu réduit**
>
> Pour rester fluide, l'aperçu peut être calculé à une résolution réduite ; la mention **Aperçu réduit** l'indique. L'export, lui, se fait toujours en pleine résolution.

## Animation

Le mode **Animation** de la barre du haut ouvre le bandeau de temps. Les modules animés (particules, lueurs, ondulations…) et les réglages animés y sont joués en boucle, et l'export propose alors les formats animés : GIF, APNG ou vidéo.

## Enregistrer et reprendre

- **Enregistrer le projet** produit un fichier `.epxl` : modules, connexions, réglages, et les images sources si vous le souhaitez.
- **Importer un projet** remplace le graphe courant par celui d'un fichier `.epxl`.
- Avec un [dossier local](../05-account-and-credits.md#dossier-local) choisi dans les paramètres, le graphe s'y **sauvegarde automatiquement**.

Un projet ouvert dans une version plus récente de Pixlub met à jour ses modules ; un module qui n'existe plus est signalé sur son nœud.

## Performances

Le bouton **Paramètres** de la barre règle la fréquence de recalcul et la taille des aperçus (Rapide, Normal, Optimisé). L'**accélération GPU** exécute les modules compatibles sur la carte graphique via WebGPU, avec repli automatique sur le processeur.

## Modules d'IA dans le graphe

Un module d'IA posé dans le graphe ne part pas seul : il affiche **Lancer la requête** avec son prix. Si un module en amont change, son résultat devient **périmé** et attend que vous le relanciez. Voir [Traitement local et serveur](../06-privacy.md).
