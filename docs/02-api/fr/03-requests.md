# Requêtes et réponses

Les points d'accès, le format des requêtes, les entrées multiples, le schéma des réglages et la réponse.

## Points d'accès

| Méthode | Adresse | Clé | Rôle |
| --- | --- | --- | --- |
| `GET` | `/v1/modules` | non | Liste des modules et de leurs entrées. |
| `GET` | `/v1/modules/:id/schema` | non | Schéma JSON des réglages d'un module. |
| `POST` | `/v1/modules/:id` | oui | Exécute un module. |
| `POST` | `/v1/uploads` | oui | Ouvre un dépôt pour un gros fichier ([Gros fichiers](./035-large-files.md)). |
| `GET` | `/v1/jobs/:id` | oui | Suit un traitement long ([Traitements longs](./035-large-files.md)). |
| `GET` | `/v1/results/:name` | non (lien signé) | Télécharge un fichier produit. |
| `GET` | `/healthz` | non | État du service. |

Toutes les adresses partent de `https://api.pixlub.com`.

## Lister les modules

```json
[
  {
    "id": "mask",
    "name": "Mask",
    "description": "Applies a mask to an image.",
    "category": "compose",
    "executable": true,
    "handler": "local",
    "inputs": [
      { "id": "image", "label": "Image", "type": "image", "required": true, "multiple": false, "per_file": false, "max_files": 1, "accept": ["image/png", "image/jpeg", "image/webp", "image/gif", "image/avif", "image/bmp"] },
      { "id": "mask", "label": "Mask", "type": "image", "required": true, "multiple": false, "per_file": false, "max_files": 1, "accept": ["image/png", "image/jpeg", "image/webp", "image/gif", "image/avif", "image/bmp"] }
    ],
    "outputs": [
      { "key": "out", "label": "Image(s)", "kind": "image", "multiple": false, "content_types": ["image/png"] }
    ]
  }
]
```

`executable` dit si l'API peut lancer le module ; `handler` vaut `local` (calculé par l'API) ou `remote` (service d'IA). Chaque entrée annonce les formats qu'elle accepte (`accept`) et combien de fichiers elle prend (`max_files`, avec `per_file` quand chaque fichier est traité seul) ; chaque sortie, la clé sous laquelle son fichier revient (`key`). Les modules non exécutables (vidéo, 3D, blocs de graphe) restent utilisables sur le site.

## Envoyer une requête

Un appel est une requête `multipart/form-data` :

- **un champ par entrée**, nommé d'après l'`id` de l'entrée, qui contient le fichier ; une entrée en liste (`multiple`) **répète son champ**, une fois par fichier ;
- **un champ `params`**, une chaîne JSON avec les réglages.

```bash
curl -X POST https://api.pixlub.com/v1/modules/mask \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F image=@photo.png \
  -F mask=@masque.png \
  -F 'params={}'
```

Les fichiers font au plus **25 Mo** chacun dans la requête (au-delà, ou pour un fichier déjà en ligne : [Gros fichiers](./035-large-files.md)) ; une requête porte **8** fichiers de lot au plus, ou jusqu'à **64** images traitées une par une (voir plus bas). Ce qu'une entrée reçoit dépend de son type :

| Type d'entrée | Fichiers | Ce que le module lit |
| --- | --- | --- |
| `image` | Un seul, ou plusieurs quand `per_file` vaut `true` | L'image ; chaque image envoyée est traitée seule. |
| `channel` | Un seul | Sa valeur en niveaux de gris, comme les entrées `r`, `g`, `b`, `a` de `channelMerge`. |
| `batch` | Une liste : le champ se répète | Les images dans l'ordre d'envoi, comme l'entrée `overlay` de `merge` (`-F overlay=@a.png -F overlay=@b.png`). |

### Formats acceptés

Chaque entrée nomme ses formats, listés dans la vue **API** de chaque [fiche module](../../03-modules/fr/README.md) et dans `accept` de `GET /v1/modules` :

- un module calculé par l'API lit **PNG, JPEG, WebP, GIF, AVIF et BMP** ;
- un module d'IA (`handler` = `remote`) lit **PNG, JPEG, WebP et GIF**, parfois moins (photos seules pour la détection de visages).

Le format est lu **dans le contenu du fichier**, jamais dans son nom ni dans son type déclaré. Un autre format est refusé (`400`, `unsupported_format`), comme un champ simple qui reçoit plusieurs fichiers (`too_many_files`).

### Plusieurs images en un appel

La plupart des modules à une seule entrée image (`resize`, `blur`, `convert`…) acceptent **plusieurs images** : répétez le champ, une fois par image. Chaque image est traitée **seule**, avec les mêmes réglages, comme le lot de la page du module sur le site. `GET /v1/modules` le signale par `per_file: true` sur l'entrée.

```bash
curl -X POST https://api.pixlub.com/v1/modules/resize \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@photo-1.png \
  -F in=@photo-2.jpg \
  -F 'params={"size":{"width":800}}'
```

- **Coût** : le prix du module **par image**, débité **en une fois** avant le premier rendu. Si le solde ne couvre pas tout le lot, rien n'est exécuté (`402`, `required` donne le coût total) ; un échec de notre côté rembourse le tout.
- **Nombre** : votre offre fixe combien d'images un appel peut porter (le même plafond que les lots du site), **64** au plus. Au-delà de l'offre : `403`, `batch_limit`, avec le plafond dans `limit`.
- **Réponse** : chaque sortie revient numérotée dans l'ordre d'envoi, `out#0`, `out#1`… (`r#0`, `g#0`, `b#0`, `r#1`… pour `splitRgb`). Une image seule garde sa clé (`out`).

## Les réglages

- Un réglage **absent** prend sa valeur par défaut. `params` peut être omis ou valoir `{}`.
- Un réglage **inconnu** est refusé : la liste est fermée.
- Les **types sont stricts** : `"12"` n'est pas un nombre. Une valeur hors limites ou hors de la liste permise est refusée.

Le schéma exact, avec types, limites, pas et valeurs par défaut, se lit sur `GET /v1/modules/:id/schema`, et dans la vue **API** de chaque [fiche module](../../03-modules/fr/README.md). Une requête refusée renvoie `400` avec le détail de chaque erreur : voir [Erreurs](./05-errors.md).

## La réponse

```json
{
  "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
  "module": "faceBlurApi",
  "outputs": [
    { "key": "out", "name": "image", "url": "https://files.pixlub.com/r/…_result.png?exp=…&sig=…", "content_type": "image/png", "bytes": 172891 },
    { "key": "data", "name": "data", "url": "https://files.pixlub.com/r/…_result.json?exp=…&sig=…", "content_type": "application/json", "bytes": 82 }
  ],
  "expires_at": "2026-10-17T13:00:00Z",
  "credits": { "cost": 10, "balance": 190 }
}
```

| Champ | Contenu |
| --- | --- |
| `id` | Identifiant du résultat (celui du premier fichier). |
| `module` | Le module exécuté. |
| `outputs` | Les fichiers produits : `key`, `name`, `url`, `content_type`, `bytes`. |
| `expires_at` | Fin de validité des liens. |
| `credits` | Coût de l'appel et solde restant. |
| `message` | Facultatif : une remarque du module. |

### Retrouver un fichier par sa clé

Un module peut rendre plusieurs fichiers : `splitRgb` rend ses trois canaux. Chaque élément de `outputs` porte la **clé** de la sortie qui l'a produit (`key`) : `r`, `g`, `b` pour `splitRgb`, `out` pour la plupart des modules, `data` pour les données d'un module d'IA. Une sortie en liste, ou un appel qui envoie plusieurs images, rend un fichier par image, sous `out#0`, `out#1`… Les clés de chaque module sont listées dans la section **Sorties** de sa fiche.

```js
const result = await res.json()
const red = result.outputs.find((o) => o.key === 'r')
```

Le `name` d'une sortie dit ce qu'elle contient :

| `name` | Contenu |
| --- | --- |
| `image` | L'image produite. |
| `data` | Un fichier JSON : visages détectés, relief reconstruit… |
| `file` | Un autre format, comme un PDF. |

## Les liens de résultat

- Un lien est **signé** et valable **une heure** : il se télécharge sans clé d'API, autant de fois que nécessaire, sans nouveau débit.
- Les fichiers produits par nos serveurs se téléchargent sur `https://files.pixlub.com`, qui accepte la reprise d'un téléchargement coupé (`Range`) : suivez l'`url` telle quelle, quel que soit son domaine.
- Les fichiers sont **effacés au bout de 24 heures**.
- Traitez un lien comme un secret jusqu'à son expiration : quiconque le possède peut télécharger le fichier.
