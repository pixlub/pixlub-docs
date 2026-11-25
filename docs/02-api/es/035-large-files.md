# Archivos grandes y procesos largos

Enviar un archivo de más de 25 MB, hacer descargar una URL y seguir un proceso que dura varios minutos.

Una llamada clásica envía el archivo en la solicitud y espera el resultado. Hay dos casos que se salen de ese marco:

- un **archivo grande** (más de **25 MB**) no cabe en la solicitud: súbalo primero, o indique su dirección;
- un **proceso largo** responde de inmediato `202` con un identificador, que se sigue hasta obtener el resultado.

Los módulos ejecutados por nuestros servidores (`handler` = `remote` en `GET /v1/modules`) aceptan estas dos formas de trabajar. Los módulos calculados por la API siguen limitados a 25 MB por archivo, en la solicitud.

## Subir un archivo grande

**1. Abrir una carga.** Indique el módulo, el nombre y el tamaño exacto del archivo:

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

Un tamaño superior al de su plan se rechaza de inmediato (`413`, `file_too_large`, con el límite en `max_bytes`), antes de cualquier envío.

**2. Enviar el archivo** a `upload_url`, con un `PUT` cuyo cuerpo es el archivo sin procesar. No hace falta clave de API: basta con la URL firmada. Es válida durante **15 minutos** para empezar el envío y no acepta más bytes que el tamaño anunciado.

```bash
curl -T photo.png "https://files.pixlub.com/u/8a6f1f3e-…?exp=…&max=48213977&sig=…"
```

Ponga la URL entre comillas y úsela tal cual, sin volver a codificarla: la firma abarca cada carácter.

**3. Ejecutar el módulo** con el campo `upload_id` en lugar del archivo:

```bash
curl -X POST https://api.pixlub.com/v1/modules/removeBgApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F upload_id=8a6f1f3e-6a1c-4c55-9a43-2f0e5b8f0c11 \
  -F 'params={}'
```

La respuesta es la misma que la de una llamada directa. Una carga solo sirve **una vez**; si se envía pero nunca se usa, se elimina al cabo de 24 horas.

## Hacer descargar una URL

Si el archivo ya está en línea (su propio almacenamiento, una CDN), indique su dirección en `source_url`: nuestros servidores lo descargan por sí mismos, sin envío por su parte.

```bash
curl -X POST https://api.pixlub.com/v1/modules/removeBgApi \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F source_url=https://cdn.example.com/photos/photo.png \
  -F 'params={}'
```

- La dirección usa **`https`**, en el puerto 443, sin credenciales en la URL. Una URL firmada de su almacenamiento (S3, R2…) sirve.
- Las direcciones **no públicas** (red privada, bucle local…) se rechazan, incluso detrás de un nombre o de una redirección (`400`, `forbidden_address`).
- El tamaño permitido es el de su plan; la descarga dura **15 minutos** como máximo.
- Una descarga fallida devuelve `422` con su código: `source_status` (respuesta distinta de `200`), `source_too_large`, `source_timeout`, `source_unreachable`.

## Seguir un proceso largo

Una llamada espera el final del proceso **algo menos de un minuto**. Pasado ese tiempo, responde `202`:

```json
{
  "job_id": "3c9e5a20-7f41-4b8e-9d2a-6a51f0b4c8e7",
  "module": "removeBgApi",
  "status": "running",
  "poll": "https://api.pixlub.com/v1/jobs/3c9e5a20-7f41-4b8e-9d2a-6a51f0b4c8e7"
}
```

El proceso continúa por nuestra parte y sus créditos ya están descontados. Sígalo con `GET /v1/jobs/:id`; el encabezado `Prefer: wait=25` espera a que termine hasta 25 segundos, lo que evita multiplicar las llamadas:

```bash
curl https://api.pixlub.com/v1/jobs/3c9e5a20-7f41-4b8e-9d2a-6a51f0b4c8e7 \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -H "Prefer: wait=25"
```

| `status` | Contenido de la respuesta |
| --- | --- |
| `queued`, `running` | Nada más: vuelva a consultar. |
| `succeeded` | La respuesta del módulo (`outputs`, `expires_at`, `credits`…), como en una llamada directa. |
| `failed` | `error`, `code` y `http_status`: el error que habría devuelto la llamada directa. Un fallo por nuestra parte se reembolsa. |

```js
let job = await (await fetch(poll, { headers: { 'X-API-Key': key, Prefer: 'wait=25' } })).json()
while (job.status === 'queued' || job.status === 'running') {
  job = await (await fetch(poll, { headers: { 'X-API-Key': key, Prefer: 'wait=25' } })).json()
}
if (job.status === 'failed') throw new Error(`${job.http_status} ${job.code}`)
const url = job.outputs[0].url
```

Un proceso se puede consultar durante **24 horas**; sus enlaces de resultado siguen siendo válidos una hora, como los de una llamada directa. Las llamadas por lotes (varias imágenes en una solicitud) siempre esperan su resultado.

## Descargar los resultados

Los archivos generados por nuestros servidores se descargan desde `https://files.pixlub.com`, sin clave de API, mediante su enlace firmado. Una descarga interrumpida se reanuda donde se detuvo:

```bash
curl -C - -o salida.png "https://files.pixlub.com/r/…_result.png?exp=…&sig=…"
```
