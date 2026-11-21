# Compte et crédits

Ce que change un compte, comment fonctionnent les crédits et les offres, et où se règle votre espace de travail.

Un compte n'est pas nécessaire pour utiliser les modules locaux. Il le devient pour les **modules d'IA**, qui consomment des **crédits**, et pour profiter des limites de votre offre.

## Les offres

| Offre | Pour qui |
| --- | --- |
| Gratuit | Tous les outils légers, et 30 crédits offerts chaque mois, sans carte bancaire. |
| Basique | Exports sans publicité ni attente, en 4K, les modules d'IA vidéo et les clés d'API. |
| Pro | Exports illimités, tous les modules d'IA et la file de traitement prioritaire. |
| Entreprise | Une offre sur mesure, avec accompagnement dédié. |

Les quotas exacts (exports par jour, définition, taille d'un fichier importé, fichiers par lot, calculs d'IA par jour) sont comparés sur la page [Tarifs](https://pixlub.com/fr/plans). Les abonnements sont sans engagement.

## Les crédits

- Un **module d'IA** coûte des crédits à chaque calcul : son prix s'affiche avant le lancement, et rien ne part sans votre confirmation.
- Certains modules se facturent **par fichier**, d'autres **par minute** (transcription) ou **par opération**.
- Un calcul qui échoue de notre côté est **remboursé** automatiquement.
- Chaque débit s'affiche à l'écran, et une notification vous prévient à mesure que vos crédits du mois s'épuisent.
- Des **packs de crédits** s'achètent en plus de l'abonnement, et n'expirent pas.

Les mêmes crédits servent pour l'[API](../../02-api/fr/04-credits.md).

## Les paramètres

La page [Paramètres](https://pixlub.com/fr/settings) regroupe trois rubriques :

| Rubrique | Contenu |
| --- | --- |
| Compte | Profil, préférences, sécurité. |
| Paiements | Moyens de paiement, gestion du plan, historique des paiements, crédits. |
| Espace de travail | Dossier local, et la section **Développeur** pour les clés d'API. |

## Dossier local

Dans **Espace de travail**, choisissez un dossier de votre ordinateur. Pixlub peut alors :

- y **sauvegarder automatiquement** vos projets de [graphe d'image](./02-image/01-image-graph.md) ;
- y **enregistrer vos exports** grâce au bouton dédié (le bouton **Exporter** télécharge toujours) ;
- lister ses projets à l'ouverture du graphe.

> [!NOTE]
> **Autorisation du navigateur**
>
> Le navigateur ne donne que le nom du dossier choisi, jamais son chemin complet, et peut redemander l'autorisation d'y accéder à une nouvelle visite. Cette fonction repose sur l'API File System Access, disponible dans Chrome, Edge et les navigateurs Chromium.
