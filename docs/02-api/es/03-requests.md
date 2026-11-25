# Solicitudes y respuestas

Los endpoints, el formato de las solicitudes, las entradas múltiples, el esquema de los ajustes y la respuesta.

## Endpoints

| Método | Dirección | Clave | Función |
| --- | --- | --- | --- |
| `GET` | `/v1/modules` | no | Lista de los módulos y de sus entradas. |
| `GET` | `/v1/modules/:id/schema` | no | Esquema JSON de los ajustes de un módulo. |
| `POST` | `/v1/modules/:id` | sí | Ejecuta un módulo. |
| `POST` | `/v1/uploads` | sí | Abre una carga para un archivo grande ([Archivos grandes](./035-large-files.md)). |
| `GET` | `/v1/jobs/:id` | sí | Sigue un proceso largo ([Procesos largos](./035-large-files.md)). |
| `GET` | `/v1/results/:name` | no (enlace firmado) | Descarga un archivo generado. |
| `GET` | `/healthz` | no | Estado del servicio. |

Todas las direcciones parten de `https://api.pixlub.com`.

## Listar los módulos

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

`executable` indica si la API puede ejecutar el módulo; `handler` vale `local` (calculado por la API) o `remote` (servicio de IA). Cada entrada anuncia los formatos que acepta (`accept`) y cuántos archivos admite (`max_files`, con `per_file` cuando cada archivo se procesa por separado); cada salida, la clave con la que vuelve su archivo (`key`). Los módulos no ejecutables (video, 3D, bloques del grafo) siguen disponibles en el sitio.

## Enviar una solicitud

Una llamada es una solicitud `multipart/form-data`:

- **un campo por entrada**, con el nombre del `id` de la entrada, que contiene el archivo; una entrada de lista (`multiple`) **repite su campo**, una vez por archivo;
- **un campo `params`**, una cadena JSON con los ajustes.

```bash
curl -X POST https://api.pixlub.com/v1/modules/mask \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F image=@photo.png \
  -F mask=@mascara.png \
  -F 'params={}'
```

Los archivos pesan como máximo **25 MB** cada uno en la solicitud (por encima, o para un archivo ya en línea: [Archivos grandes](./035-large-files.md)); una solicitud lleva como máximo **8** archivos de lote, o hasta **64** imágenes procesadas una a una (ver más abajo). Lo que recibe una entrada depende de su tipo:

| Tipo de entrada | Archivos | Lo que lee el módulo |
| --- | --- | --- |
| `image` | Uno solo, o varios cuando `per_file` vale `true` | La imagen; cada imagen enviada se procesa por separado. |
| `channel` | Uno solo | Su valor en escala de grises, como las entradas `r`, `g`, `b`, `a` de `channelMerge`. |
| `batch` | Una lista: el campo se repite | Las imágenes en el orden de envío, como la entrada `overlay` de `merge` (`-F overlay=@a.png -F overlay=@b.png`). |

### Formatos admitidos

Cada entrada indica sus formatos, que figuran en la vista **API** de cada [ficha de módulo](../../03-modules/es/README.md) y en `accept` de `GET /v1/modules`:

- un módulo calculado por la API lee **PNG, JPEG, WebP, GIF, AVIF y BMP**;
- un módulo de IA (`handler` = `remote`) lee **PNG, JPEG, WebP y GIF**, a veces menos (solo fotos para la detección de rostros).

El formato se lee **en el contenido del archivo**, nunca en su nombre ni en su tipo declarado. Cualquier otro formato se rechaza (`400`, `unsupported_format`), igual que un campo simple que recibe varios archivos (`too_many_files`).

### Varias imágenes en una llamada

La mayoría de los módulos con una sola entrada de imagen (`resize`, `blur`, `convert`…) aceptan **varias imágenes**: repita el campo, una vez por imagen. Cada imagen se procesa **por separado**, con los mismos ajustes, como el lote de la página del módulo en el sitio. `GET /v1/modules` lo indica con `per_file: true` en la entrada.

```bash
curl -X POST https://api.pixlub.com/v1/modules/resize \
  -H "X-API-Key: $PIXLUB_API_KEY" \
  -F in=@photo-1.png \
  -F in=@photo-2.jpg \
  -F 'params={"size":{"width":800}}'
```

- **Costo**: el precio del módulo **por imagen**, descontado **de una sola vez** antes del primer renderizado. Si el saldo no cubre todo el lote, no se ejecuta nada (`402`; `required` da el costo total); un fallo por nuestra parte lo reembolsa todo.
- **Número**: su plan fija cuántas imágenes puede llevar una llamada (el mismo límite que los lotes del sitio), **64** como máximo. Por encima del plan: `403`, `batch_limit`, con el límite en `limit`.
- **Respuesta**: cada salida vuelve numerada en el orden de envío, `out#0`, `out#1`… (`r#0`, `g#0`, `b#0`, `r#1`… para `splitRgb`). Una sola imagen conserva su clave (`out`).

## Los ajustes

- Un ajuste **ausente** toma su valor por defecto. `params` se puede omitir o valer `{}`.
- Un ajuste **desconocido** se rechaza: la lista es cerrada.
- Los **tipos son estrictos**: `"12"` no es un número. Un valor fuera de los límites o de la lista permitida se rechaza.

El esquema exacto, con tipos, límites, pasos y valores por defecto, se consulta en `GET /v1/modules/:id/schema` y en la vista **API** de cada [ficha de módulo](../../03-modules/es/README.md). Una solicitud rechazada devuelve `400` con el detalle de cada error: consulte [Errores](./05-errors.md).

## La respuesta

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

| Campo | Contenido |
| --- | --- |
| `id` | Identificador del resultado (el del primer archivo). |
| `module` | El módulo ejecutado. |
| `outputs` | Los archivos generados: `key`, `name`, `url`, `content_type`, `bytes`. |
| `expires_at` | Fin de validez de los enlaces. |
| `credits` | Costo de la llamada y saldo restante. |
| `message` | Opcional: una observación del módulo. |

### Encontrar un archivo por su clave

Un módulo puede devolver varios archivos: `splitRgb` devuelve sus tres canales. Cada elemento de `outputs` lleva la **clave** de la salida que lo generó (`key`): `r`, `g`, `b` para `splitRgb`, `out` para la mayoría de los módulos, `data` para los datos de un módulo de IA. Una salida de lista, o una llamada que envía varias imágenes, devuelve un archivo por imagen, con las claves `out#0`, `out#1`… Las claves de cada módulo figuran en la sección **Salidas** de su ficha.

```js
const result = await res.json()
const red = result.outputs.find((o) => o.key === 'r')
```

El `name` de una salida indica lo que contiene:

| `name` | Contenido |
| --- | --- |
| `image` | La imagen generada. |
| `data` | Un archivo JSON: rostros detectados, relieve reconstruido… |
| `file` | Otro formato, como un PDF. |

## Los enlaces de resultado

- Un enlace está **firmado** y es válido durante **una hora**: se descarga sin clave de API, tantas veces como sea necesario, sin nuevo cargo.
- Los archivos generados por nuestros servidores se descargan desde `https://files.pixlub.com`, que admite reanudar una descarga interrumpida (`Range`): siga la `url` tal cual, sea cual sea su dominio.
- Los archivos se **eliminan al cabo de 24 horas**.
- Trate un enlace como un secreto hasta que caduque: cualquiera que lo tenga puede descargar el archivo.
