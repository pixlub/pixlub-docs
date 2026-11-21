# Module indépendant

Utiliser un module seul, sur sa propre page : déposer ses fichiers, régler, télécharger.

Chaque module qui peut se nourrir d'un simple fichier a sa propre page, à l'adresse `/module/<identifiant>` : par exemple [Redimensionner](https://pixlub.com/fr/module/resize) ou [Flou](https://pixlub.com/fr/module/blur). C'est la façon la plus rapide d'appliquer une opération, sans construire de graphe.

## Utiliser un module

1. **Ouvrir le module**

   Depuis l'accueil, le menu des outils ou la [liste des modules](./02-image/README.md). La fiche de chaque module, dans la section [Modules](../../03-modules/fr/README.md), mène aussi à sa page.

2. **Déposer vos fichiers**

   Cliquez sur la zone de dépôt ou glissez-y vos fichiers. Ils remplissent les entrées du module.

3. **Régler**

   Le panneau d'options, à droite, regroupe les réglages par section. L'aperçu se recalcule à chaque changement. **Reset** rend au module ses valeurs par défaut.

4. **Récupérer le résultat**

   **Télécharger** ouvre la [modale d'exportation](./02-image/04-exportation.md) : choisissez le format et ses réglages, l'aperçu montre déjà le résultat, puis **Exporter**. Son menu propose un **téléchargement rapide** en PNG et **Copier l'image**, qui la place dans le presse-papiers.

## Traiter plusieurs images

Déposez plusieurs images dans la même entrée : le module les traite toutes avec les mêmes réglages. Les flèches de l'aperçu passent d'une image à l'autre.

La colonne des entrées range les images en **espaces de travail**, une case par espace, chacun avec ses propres réglages. Une pastille indique combien d'images un espace réunit.

- Cliquez sur un espace pour l'ouvrir : le panneau montre ses réglages et ses images se déplient dans un menu, à l'horizontale.
- Dans ce menu, le **+** ajoute une image à l'espace : elle reçoit les mêmes réglages.
- **Nouvel espace**, sous la colonne, ajoute des images avec leurs propres réglages, un espace par image.
- Le bouton **Séparer** d'une image du menu la sort dans un nouvel espace.

L'export rend chaque image avec les réglages de son espace. La modale d'exportation les montre toutes, avec leur taille et leur poids, et sa section **Lot** choisit la livraison :

- **Archive ZIP** : toutes les images dans une archive ;
- **Fichiers séparés** : un fichier par image.

Le nombre de fichiers par lot dépend de votre offre : voir [Compte et crédits](./05-account-and-credits.md).

## Taille du rendu

Le panneau d'options a deux onglets : **Propriété** pour les réglages du module, **Paramètres** pour la taille de l'image rendue.

| Méthode | Taille du rendu |
| --- | --- |
| **Module** (par défaut) | Celle que produit le module. |
| **Source** | Celle de l'image reçue. |
| **Libre** | La largeur et la hauteur saisies. |

En **Source** et **Libre**, l'**ajustement** place le rendu : **Aucun** (recadré), **Contenir**, **Couvrir** ou **Étirer**, accroché selon l'**ancrage**.

## Variantes de la page

La page s'adapte au média du module :

| Média | Ce qui change |
| --- | --- |
| Image | Aperçu avec fond réglable (damier, couleur unie). |
| Vidéo | Lecteur ; décodage, rendu et encodage dans le navigateur. Rien ne part sur un serveur. |
| Document | Liste de fichiers réordonnable, aperçu des pages, bouton **Lancer**. Voir [Documents](./04-document.md). |
| Conversion | Choix du format de sortie et de ses options. Voir le [convertisseur](./02-image/02-image-converter.md). |

## Modules d'IA

Les modules d'IA (détourage, floutage automatique des visages, décalcomanie…) envoient l'image à nos serveurs. Leur page :

- demande un **compte** : sans session, elle redirige vers la connexion ;
- affiche le **prix en crédits** avant le lancement, et ne se relance jamais seule : chaque nouveau calcul passe par une confirmation ;
- passe la pastille de confidentialité sur **Envoyé au serveur** dès que le module est prêt à partir.
