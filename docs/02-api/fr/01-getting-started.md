# Prise en main

Votre premier appel à l'API Pixlub : une clé, une requête, un fichier téléchargé.

L'API Pixlub applique les modules de l'éditeur à vos fichiers, par HTTP. Chaque module est un point d'accès `POST /v1/modules/:id` ; la réponse liste les fichiers produits, à télécharger par des liens signés.

`POST https://api.pixlub.com/v1/modules/:id`

## Prérequis

- Un compte Pixlub avec une offre **Basique** ou **Pro** : les clés d'API sont réservées aux offres payantes. L'[abonnement API sur mesure](https://pixlub.com/fr/credits) offre Basique dès 8 € par mois et Pro dès 25 €.
- Une **clé d'API**, créée dans [Paramètres → Espace de travail → Développeur](https://pixlub.com/fr/settings/workspace#developer). Voir [Authentification](./02-authentification.md).
- Des **crédits** : chaque appel en consomme. Voir [Crédits](./04-credits.md).

## Premier appel

1. **Ranger la clé dans une variable d'environnement**

   Ne l'écrivez jamais dans votre code source.

   ```bash
   export PIXLUB_API_KEY="pix.xxxxxxxx.xxxxxxxxxxxxxxxx"
   ```

2. **Trouver le module**

   `GET /v1/modules` liste les modules, leurs entrées et s'ils sont exécutables par l'API. Le plus simple est de parcourir la section [Modules](../../03-modules/fr/README.md) : chaque fiche a une vue **API** avec ses réglages et des exemples prêts à copier.

   ```bash
   curl https://api.pixlub.com/v1/modules
   ```

3. **Envoyer le fichier**

   Une requête `multipart/form-data` : le fichier dans le champ de l'entrée (souvent `in`), les réglages en JSON dans le champ `params`. Ici, un miroir vertical avec le module [`flip`](../../03-modules/fr/03-transform/flip/api.md).

   **cURL**

   ```bash
   curl -X POST https://api.pixlub.com/v1/modules/flip \
     -H "X-API-Key: $PIXLUB_API_KEY" \
     -F in=@photo.png \
     -F 'params={"axis":"v"}'
   ```

   **JavaScript**

   ```js
   import { openAsBlob } from 'node:fs'

   const form = new FormData()
   form.append('in', await openAsBlob('photo.png'), 'photo.png')
   form.append('params', JSON.stringify({ axis: 'v' }))

   const res = await fetch('https://api.pixlub.com/v1/modules/flip', {
     method: 'POST',
     headers: { 'X-API-Key': process.env.PIXLUB_API_KEY },
     body: form,
   })
   const result = await res.json()
   ```

   **Python**

   ```python
   import json, os, requests

   res = requests.post(
       "https://api.pixlub.com/v1/modules/flip",
       headers={"X-API-Key": os.environ["PIXLUB_API_KEY"]},
       files={"in": open("photo.png", "rb")},
       data={"params": json.dumps({"axis": "v"})},
   )
   result = res.json()
   ```

4. **Télécharger le résultat**

   La réponse donne l'adresse de chaque fichier produit. Le lien est signé : il se télécharge **sans clé**, pendant une heure.

   ```json
   {
     "id": "e38dd247-5b1c-4c6e-9a0f-2f4d1a7c9b10",
     "module": "flip",
     "outputs": [
       {
         "key": "out",
         "name": "image",
         "url": "https://files.pixlub.com/r/e38dd247-…_result.png?exp=…&sig=…",
         "content_type": "image/png",
         "bytes": 184203
       }
     ],
     "expires_at": "2026-10-17T13:00:00Z",
     "credits": { "cost": 1, "balance": 189 }
   }
   ```

## Et ensuite

- **[Requêtes et réponses](./03-requests.md)** : Plusieurs entrées, schéma des réglages, fichiers de données.
- **[Erreurs](./05-errors.md)** : Les codes HTTP et ce qu'il faut faire pour chacun.
- **[SDK Python et Go](./06-sdk.md)** : Des clients officiels qui gèrent l'envoi, les relances et les téléchargements.
