# Autenticación

Crear, usar, proteger y revocar una clave de API.

Cada llamada a un módulo se autentica con una **clave de API**, enviada en el encabezado `X-API-Key`. Los endpoints de lectura (`GET /v1/modules`, el esquema de un módulo) y los enlaces de resultado firmados no la necesitan.

```http
POST /v1/modules/blur HTTP/1.1
Host: api.pixlub.com
X-API-Key: pix.AbCdEf12.xxxxxxxxxxxxxxxxxxxxxxxx
Content-Type: multipart/form-data; boundary=…
```

## Crear una clave

1. **Abrir la sección Desarrollador**

   [Configuración → Espacio de trabajo → Desarrollador](https://pixlub.com/es/settings/workspace#developer). La sección está reservada a los planes **Básico** y **Pro**.

2. **Crear la clave**

   **Crear una clave** y luego póngale un nombre que indique dónde se usa («servidor de producción», «script nocturno»).

3. **Copiarla de inmediato**

   La clave completa solo se muestra una vez. Pixlub solo guarda una huella: no se podrá volver a leer.

Una clave tiene la forma `pix.<prefijo>.<secreto>`. El prefijo, visible en la lista de claves, sirve para reconocerla; solo el secreto debe permanecer oculto. La lista también indica la fecha de creación y el último uso de cada clave. Una cuenta puede tener hasta 20 claves activas.

## Revocar una clave

**Revocar** desactiva la clave de inmediato: las llamadas siguientes reciben `401`. Revoque sin esperar una clave que se haya filtrado y luego cree una nueva.

## Buenas prácticas

- **Una clave por uso** (un servidor, un script, un entorno): se revoca una sin cortar las demás.
- **Nunca en el código fuente** ni en un repositorio: variable de entorno o gestor de secretos.
- **Nunca en un navegador ni en una aplicación móvil**: cualquiera podría leer la clave. Llame a la API desde su servidor.
- **Solo HTTPS**, y nunca en la dirección: la clave viaja en el encabezado `X-API-Key`.

> [!WARNING]
> **Plan y claves**
>
> Si su cuenta vuelve al plan gratuito, sus claves siguen registradas pero las llamadas se rechazan con `403` y el código `plan_required`.
