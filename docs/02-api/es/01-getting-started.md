# Primeros pasos

Su primera llamada a la API de Pixlub: una clave, una solicitud, un archivo descargado.

La API de Pixlub aplica los módulos del editor a sus archivos, por HTTP. Cada módulo es un endpoint `POST /v1/modules/:id`; la respuesta enumera los archivos generados, que se descargan mediante enlaces firmados.

`POST https://api.pixlub.com/v1/modules/:id`

## Requisitos previos

- Una cuenta de Pixlub con un plan **Básico** o **Pro**: las claves de API están reservadas a los planes de pago. La [suscripción API a medida](https://pixlub.com/es/credits) ofrece Básico desde 8 € al mes y Pro desde 25 €.
- Una **clave de API**, creada en [Configuración → Espacio de trabajo → Desarrollador](https://pixlub.com/es/settings/workspace#developer). Consulte [Autenticación](./02-authentification.md).
- **Créditos**: cada llamada consume créditos. Consulte [Créditos](./04-credits.md).

## Primera llamada

1. **Guardar la clave en una variable de entorno**

   No la escriba nunca en su código fuente.

   ```bash
   export PIXLUB_API_KEY="pix.xxxxxxxx.xxxxxxxxxxxxxxxx"
   ```

2. **Encontrar el módulo**

   `GET /v1/modules` enumera los módulos, sus entradas y si se pueden ejecutar mediante la API. Lo más sencillo es recorrer la sección [Módulos](../../03-modules/es/README.md): cada ficha tiene una vista **API** con sus ajustes y ejemplos listos para copiar.

   ```bash
   curl https://api.pixlub.com/v1/modules
   ```

3. **Enviar el archivo**

   Una solicitud `multipart/form-data`: el archivo en el campo de la entrada (a menudo `in`) y los ajustes en JSON en el campo `params`. Aquí, un volteo vertical con el módulo [`flip`](../../03-modules/es/03-transform/flip/api.md).

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

4. **Descargar el resultado**

   La respuesta da la dirección de cada archivo generado. El enlace está firmado: se descarga **sin clave**, durante una hora.

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

## Y después

- **[Solicitudes y respuestas](./03-requests.md)** : Varias entradas, esquema de los ajustes, archivos de datos.
- **[Errores](./05-errors.md)** : Los códigos HTTP y qué hacer con cada uno.
- **[SDK de Python y Go](./06-sdk.md)** : Clientes oficiales que gestionan el envío, los reintentos y las descargas.
