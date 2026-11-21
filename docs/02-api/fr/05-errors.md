# Erreurs

Les codes HTTP de l'API, le format des erreurs et la conduite à tenir pour chacune.

Une erreur répond avec un code HTTP et un corps JSON. `error` décrit le problème en clair ; `code`, quand il est présent, est stable et fait pour votre programme.

```json
{
  "error": "not enough credits for this module",
  "code": "insufficient_credits"
}
```

## Les codes

| Statut | Cause | Que faire |
| --- | --- | --- |
| `400` | Réglages invalides, fichier requis manquant (`missing_file`) ou de plus de 25 Mo, format refusé par l'entrée (`unsupported_format`), trop de fichiers (`too_many_files`), requête multipart illisible. | Corriger la requête. `details` liste chaque réglage refusé. |
| `401` | Clé absente, inconnue ou révoquée. | Vérifier l'en-tête `X-API-Key`. |
| `402` | Crédits insuffisants (`insufficient_credits`) ; `required` donne le coût de l'appel, toutes images comprises. | Recharger, puis relancer. |
| `403` | Offre sans accès à l'API (`plan_required`), plus d'images que l'offre n'en traite par appel (`batch_limit`, plafond dans `limit`), ou lien de résultat expiré. | Passer à une offre payante ; répartir les images sur plusieurs appels ; relancer l'appel pour un nouveau lien. |
| `404` | Module ou résultat inconnu ; dépôt inconnu, déjà utilisé ou expiré (`upload_not_found`) ; traitement inconnu (`job_not_found`). | Vérifier l'identifiant ; rouvrir un dépôt. |
| `409` | Fichier pas encore envoyé à `upload_url` (`upload_incomplete`). | Terminer le `PUT`, puis relancer l'appel. |
| `413` | Fichier plus gros que votre offre (`file_too_large`, plafond dans `max_bytes`), ou trop gros pour la requête (`use_uploads`). | Réduire le fichier, ou le déposer par [`POST /v1/uploads`](./035-large-files.md). |
| `422` | URL source illisible : `source_status`, `source_too_large`, `source_timeout`, `source_unreachable`. | Vérifier l'adresse et la taille du fichier. |
| `429` | Trop de requêtes. | Patienter quelques secondes, puis relancer. |
| `500` | Erreur de notre côté. Le débit est remboursé. | Relancer plus tard. |
| `501` | Module non exécutable par l'API (vidéo, 3D…). | L'utiliser sur le site. |
| `503` | Service momentanément indisponible. | Relancer plus tard. |

## Réglages refusés

Un `400` sur les réglages détaille chaque erreur, au format JSON Schema :

```json
{
  "error": "Paramètres invalides",
  "details": [
    {
      "instancePath": "/radius",
      "keyword": "maximum",
      "params": { "comparison": "<=", "limit": 40 },
      "message": "must be <= 40"
    }
  ]
}
```

`instancePath` désigne le réglage fautif. Les limites de chaque réglage sont sur la vue **API** de la [fiche du module](../../03-modules/fr/README.md).

## Relancer sans risque

- `400`, `401`, `402`, `403`, `404` : la requête n'a pas été exécutée ni débitée. La relancer telle quelle échouera de nouveau.
- `429` : rien n'a été calculé ni débité ; relancez après une courte pause, en espaçant les tentatives.
- `500`, `503`, délai dépassé : l'appel a pu être débité puis remboursé. Vérifiez votre solde avant de relancer un module coûteux.
