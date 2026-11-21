# Crédits

Ce que coûte un appel, quand il est débité, et quand il est remboursé.

Chaque appel à un module est payé en **crédits**, les mêmes que sur le site. Le coût d'un module figure en tête de la vue **API** de sa [fiche](../../03-modules/fr/README.md).

## Combien coûte un appel

| Module | Coût |
| --- | --- |
| Module calculé par l'API (flou, redimensionnement, conversion…) | 1 crédit |
| Module d'IA (détourage, floutage auto, décalcomanie…) | Son prix propre, 10 crédits pour la plupart |

L'unité est précisée sur chaque fiche : **par fichier**, **par minute** ou **par opération**. Un module dont l'IA est facultative (Floutage de visages en mode `manual`, par exemple) coûte le prix d'un module standard tant qu'il n'appelle pas le service distant.

## Quand le débit a lieu

1. La requête est vérifiée : clé, réglages, fichiers. Une requête invalide est refusée **sans débit**.
2. Le coût est **prélevé avant** le calcul. Sans crédits suffisants, l'API répond `402` et rien n'est calculé.
3. Si le calcul échoue **de notre côté** (erreur serveur, service indisponible), le débit est **remboursé** automatiquement.

La réponse indique le coût et le solde restant :

```json
"credits": { "cost": 10, "balance": 190 }
```

Télécharger un résultat ne coûte rien, même plusieurs fois tant que le lien est valable.

## Recharger

Les crédits viennent de votre abonnement (crédits mensuels) et des packs achetés à part, qui n'expirent pas. Le solde et l'historique se consultent dans [Paramètres → Paiements → Crédits](https://pixlub.com/fr/settings/payments#credits).

> [!TIP]
> **Après une coupure**
>
> Après un délai dépassé ou une erreur `5xx` sur un appel, vérifiez votre solde avant de relancer : l'appel a pu être débité puis remboursé, ou aboutir sans que la réponse vous parvienne.
