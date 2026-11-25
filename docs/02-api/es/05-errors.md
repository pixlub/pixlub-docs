# Errores

Los códigos HTTP de la API, el formato de los errores y qué hacer con cada uno.

Un error responde con un código HTTP y un cuerpo JSON. `error` describe el problema en lenguaje claro; `code`, cuando está presente, es estable y está pensado para su programa.

```json
{
  "error": "not enough credits for this module",
  "code": "insufficient_credits"
}
```

## Los códigos

| Estado | Causa | Qué hacer |
| --- | --- | --- |
| `400` | Ajustes no válidos, archivo obligatorio ausente (`missing_file`) o de más de 25 MB, formato rechazado por la entrada (`unsupported_format`), demasiados archivos (`too_many_files`), solicitud multipart ilegible. | Corregir la solicitud. `details` enumera cada ajuste rechazado. |
| `401` | Clave ausente, desconocida o revocada. | Verificar el encabezado `X-API-Key`. |
| `402` | Créditos insuficientes (`insufficient_credits`); `required` da el costo de la llamada, todas las imágenes incluidas. | Recargar y volver a intentarlo. |
| `403` | Plan sin acceso a la API (`plan_required`), más imágenes de las que el plan procesa por llamada (`batch_limit`, con el límite en `limit`), o enlace de resultado caducado. | Pasar a un plan de pago; repartir las imágenes en varias llamadas; repetir la llamada para obtener un nuevo enlace. |
| `404` | Módulo o resultado desconocido; carga desconocida, ya usada o caducada (`upload_not_found`); proceso desconocido (`job_not_found`). | Verificar el identificador; abrir una nueva carga. |
| `409` | Archivo aún no enviado a `upload_url` (`upload_incomplete`). | Terminar el `PUT` y repetir la llamada. |
| `413` | Archivo más grande de lo que permite su plan (`file_too_large`, con el límite en `max_bytes`), o demasiado grande para la solicitud (`use_uploads`). | Reducir el archivo, o subirlo con [`POST /v1/uploads`](./035-large-files.md). |
| `422` | URL de origen ilegible: `source_status`, `source_too_large`, `source_timeout`, `source_unreachable`. | Verificar la dirección y el tamaño del archivo. |
| `429` | Demasiadas solicitudes. | Esperar unos segundos y volver a intentarlo. |
| `500` | Error por nuestra parte. El cargo se reembolsa. | Volver a intentarlo más tarde. |
| `501` | Módulo no ejecutable mediante la API (video, 3D…). | Usarlo en el sitio. |
| `503` | Servicio no disponible temporalmente. | Volver a intentarlo más tarde. |

## Ajustes rechazados

Un `400` sobre los ajustes detalla cada error, en formato JSON Schema:

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

`instancePath` designa el ajuste incorrecto. Los límites de cada ajuste figuran en la vista **API** de la [ficha del módulo](../../03-modules/es/README.md).

## Reintentar sin riesgo

- `400`, `401`, `402`, `403`, `404`: la solicitud no se ejecutó ni se cobró. Repetirla tal cual volverá a fallar.
- `429`: no se calculó ni se cobró nada; vuelva a intentarlo tras una breve pausa, espaciando los intentos.
- `500`, `503`, tiempo de espera agotado: la llamada puede haberse cobrado y luego reembolsado. Compruebe su saldo antes de repetir un módulo costoso.
