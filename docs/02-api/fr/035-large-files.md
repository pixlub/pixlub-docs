# Gros fichiers et traitements longs

Envoyer un fichier de plus de 25 Mo, faire télécharger une URL, et suivre un traitement qui dure plusieurs minutes.

Un appel classique envoie le fichier dans la requête et attend le résultat. Deux cas sortent de ce cadre :

- un **gros fichier** (plus de **25 Mo**) ne passe pas dans la requête : déposez-le d'abord, ou donnez son adresse ;
- un **traitement long** répond tout de suite `202` avec un identifiant, à suivre jusqu'au résultat.

Les modules exécutés par nos serveurs (`handler` = `remote` dans `GET /v1/modules`) acceptent ces deux façons de faire. Les modules calculés par l'API restent limités à 25 Mo par fichier, dans la requête.

## Déposer un gros fichier

**1. Ouvrir un dépôt.** Annoncez le module, le nom et la taille exacte du fichier :

```bash
curl -X POST https://api.pixlub.com/v1/uploads \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"module":"removeBgApi","filename":"photo.png","bytes":48213977}'
```

```json
{
  "upload_id": "8a6f1f3e-6a1c-4c55-9a43-2f0e5b8f0c11",
  "upload_url": "https://files.pixlub.com/u/8a6f1f3e-…?exp=…&max=48213977&sig=…",
  "method": "PUT",
  "expires_at": "2026-10-26T14:15:00Z"
}
```

Une taille au-delà de votre offre est refusée tout de suite (`413`, `file_too_large`, plafond dans `max_bytes`), avant tout envoi.

**2. Envoyer le fichier** à `upload_url`, en un `PUT` dont le corps est le fichier brut. Pas besoin de clé d'API : l'URL signée suffit. Elle est valable **15 minutes** pour commencer l'envoi, et n'accepte pas plus d'octets que la taille annoncée.

```bash
curl -T photo.png "https://files.pixlub.com/u/8a6f1f3e-…?exp=…&max=48213977&sig=…"
```

Mettez l'URL entre guillemets et utilisez-la telle quelle, sans la réencoder : la signature porte sur chaque caractère.

**3. Lancer le module** avec le champ `upload_id` à la place du fichier :

```bash
curl -X POST https://api.pixlub.com/v1/modules/removeBgApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F upload_id=8a6f1f3e-6a1c-4c55-9a43-2f0e5b8f0c11 \
  -F 'params={}'
```

La réponse est la même qu'un appel direct. Un dépôt ne sert **qu'une fois** ; envoyé mais jamais utilisé, il est effacé au bout de 24 heures.

## Faire télécharger une URL

Si le fichier est déjà en ligne (votre propre stockage, un CDN), donnez son adresse dans `source_url` : nos serveurs le téléchargent eux-mêmes, sans envoi de votre côté.

```bash
curl -X POST https://api.pixlub.com/v1/modules/removeBgApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F source_url=https://cdn.example.com/photos/photo.png \
  -F 'params={}'
```

- L'adresse est en **`https`**, sur le port 443, sans identifiants dans l'URL. Une URL signée de votre stockage (S3, R2…) convient.
- Les adresses **non publiques** (réseau privé, boucle locale…) sont refusées, y compris derrière un nom ou une redirection (`400`, `forbidden_address`).
- La taille permise est celle de votre offre ; le téléchargement dure **15 minutes** au plus.
- Un téléchargement en échec rend `422` avec son code : `source_status` (réponse autre que `200`), `source_too_large`, `source_timeout`, `source_unreachable`.

## Suivre un traitement long

Un appel attend la fin du traitement **un peu moins d'une minute**. Au-delà, il répond `202` :

```json
{
  "job_id": "3c9e5a20-7f41-4b8e-9d2a-6a51f0b4c8e7",
  "module": "removeBgApi",
  "status": "running",
  "poll": "https://api.pixlub.com/v1/jobs/3c9e5a20-7f41-4b8e-9d2a-6a51f0b4c8e7"
}
```

Le traitement continue de notre côté, et ses crédits sont déjà débités. Suivez-le par `GET /v1/jobs/:id` ; l'en-tête `Prefer: wait=25` attend sa fin jusqu'à 25 secondes, ce qui évite de multiplier les appels :

```bash
curl https://api.pixlub.com/v1/jobs/3c9e5a20-7f41-4b8e-9d2a-6a51f0b4c8e7 \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -H "Prefer: wait=25"
```

| `status` | Contenu de la réponse |
| --- | --- |
| `queued`, `running` | Rien d'autre : relancez le suivi. |
| `succeeded` | La réponse du module (`outputs`, `expires_at`, `credits`…), comme un appel direct. |
| `failed` | `error`, `code` et `http_status` : l'erreur que l'appel direct aurait rendue. Un échec de notre côté est remboursé. |

```js
let job = await (await fetch(poll, { headers: { 'X-API-Key': key, Prefer: 'wait=25' } })).json()
while (job.status === 'queued' || job.status === 'running') {
  job = await (await fetch(poll, { headers: { 'X-API-Key': key, Prefer: 'wait=25' } })).json()
}
if (job.status === 'failed') throw new Error(`${job.http_status} ${job.code}`)
const url = job.outputs[0].url
```

Un traitement se consulte pendant **24 heures** ; ses liens de résultat restent valables une heure, comme ceux d'un appel direct. Les appels en lot (plusieurs images en une requête) attendent toujours leur résultat.

## Télécharger les résultats

Les fichiers produits par nos serveurs se téléchargent sur `https://files.pixlub.com`, sans clé d'API, par leur lien signé. Un téléchargement coupé reprend où il s'était arrêté :

```bash
curl -C - -o sortie.png "https://files.pixlub.com/r/…_result.png?exp=…&sig=…"
```
