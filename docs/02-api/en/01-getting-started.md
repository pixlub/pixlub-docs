# Getting started

Your first call to the Pixlub API: a key, a request, a downloaded file.

The Pixlub API applies the editor's modules to your files, over HTTP. Each module is a `POST /v1/modules/:id` endpoint; the response lists the produced files, downloaded through signed links.

`POST https://api.pixlub.com/v1/modules/:id`

## Requirements

- A Pixlub account on a **Basic** or **Pro** plan: API keys are reserved for paid plans. The [custom API subscription](https://pixlub.com/en/credits) includes Basic from €8 a month and Pro from €25.
- An **API key**, created in [Settings → Workspace → Developer](https://pixlub.com/en/settings/workspace#developer). See [Authentication](./02-authentification.md).
- **Credits**: every call uses some. See [Credits](./04-credits.md).

## First call

1. **Store the key in an environment variable**

   Never write it in your source code.

   ```bash
   export PIXLUB_API_KEY="pix.xxxxxxxx.xxxxxxxxxxxxxxxx"
   ```

2. **Find the module**

   `GET /v1/modules` lists the modules, their inputs and whether the API can run them. The easiest way is to browse the [Modules](../../03-modules/en/README.md) section: each page has an **API** view with its settings and ready-to-copy examples.

   ```bash
   curl https://api.pixlub.com/v1/modules
   ```

3. **Send the file**

   A `multipart/form-data` request: the file in the input's field (often `in`), the settings as JSON in the `params` field. Here, a vertical mirror with the [`flip`](../../03-modules/en/03-transform/flip/api.md) module.

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

4. **Download the result**

   The response gives the address of each produced file. The link is signed: it downloads **without a key**, for one hour.

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

## Next steps

- **[Requests and responses](./03-requests.md)** : Several inputs, settings schema, data files.
- **[Errors](./05-errors.md)** : HTTP statuses and what to do about each.
- **[Python and Go SDKs](./06-sdk.md)** : Official clients that handle uploads, retries and downloads.
