# Vue d'ensemble de l'application

Les outils du site Pixlub, ce qu'ils font et quand choisir l'un plutôt que l'autre.

Le site Pixlub est un éditeur qui s'ouvre dans le navigateur, sans installation. Chaque outil part du même catalogue de **modules** : un module est une opération (flouter, redimensionner, détourer, fusionner deux PDF…) avec ses réglages.

## Les outils

- **[Module indépendant](./01-module-independant.md)** : Un module seul sur sa page : déposer, régler, télécharger.
- **[Graphe d'image](./02-image/01-image-graph.md)** : Relier des modules entre eux pour composer un effet, l'animer et l'exporter.
- **[Convertisseur d'image](./02-image/02-image-converter.md)** : Changer le format de vos images, une à une ou par lot.
- **[Éditeur de réglages](./02-image/03-image-adjust.md)** : Empiler luminosité, courbes, teinte… sur une même image.
- **[Éditeur vidéo](./03-video/01-video-editor.md)** : Monter des plans, des sons, des textes et des sous-titres.
- **[Documents](./04-document.md)** : Fusionner, signer, compresser, convertir vos PDF.

## Quel outil choisir

- **Une seule opération sur un ou plusieurs fichiers** : la page du module. C'est le plus direct.
- **Plusieurs opérations enchaînées, ou une image composée de plusieurs sources** : le graphe d'image.
- **Seulement changer de format** : le convertisseur.
- **Corriger les couleurs et la lumière** : l'éditeur de réglages.
- **Une vidéo à monter** : l'éditeur vidéo. Pour une seule opération sur une vidéo (couper, accélérer), sa page module suffit.

## Ce qui est commun à tous les outils

- **Traitement local.** Les modules s'exécutent dans votre navigateur. Seuls les modules d'IA et certains formats d'export passent par nos serveurs, et une pastille en bas de l'écran le signale toujours. Voir [Traitement local et serveur](./06-privacy.md).
- **Aperçu en direct.** Chaque réglage modifié recalcule l'aperçu ; l'export se fait en pleine résolution.
- **Export commun.** Tous les outils partagent le même catalogue de formats (PNG, JPG, WebP, AVIF, GIF, MP4, WebM…) et la même fenêtre d'export.
- **Compte facultatif.** Sans compte, tous les modules locaux restent utilisables. Le compte sert aux modules d'IA, aux crédits et aux limites de votre offre : voir [Compte et crédits](./05-account-and-credits.md).
