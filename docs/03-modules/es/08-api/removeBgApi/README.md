# Quitar el fondo

Recortar el sujeto de una foto con IA, sea cual sea el fondo.

**Categoría** : Servicios de API · **Identificador** : `removeBgApi` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/removeBgApi)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen enviada al servidor, cuyo sujeto se detecta y cuyo fondo se vuelve transparente. | `PNG`, `JPEG`, `WebP`, `GIF` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Uso

1. **Iniciar sesión**

   El recorte pasa por nuestros servidores: se pide una cuenta.

2. **Importar**

   Persona, objeto, animal, producto: el sujeto se detecta sea cual sea el fondo.

3. **Ejecutar**

   El precio en créditos se muestra antes de iniciar; la imagen vuelve con un fondo transparente.

Sin ajustes: volver a enviar el mismo archivo da el mismo resultado, y vuelve a costar.

## Retocar con el borrador

- El botón **Borrador** de la vista previa lo activa: sus opciones flotan sobre la imagen.
- Pinte para quitar lo que quede; **Restaurar** (o **Alt**) recupera lo que el recorte se llevó.
- El retoque se hace en su navegador: no repite la llamada y no cuesta nada.
- **Zonas borradas en rojo** muestra todo lo que se ha quitado.

## Consejos

- Exporte en PNG, WebP o AVIF para conservar la transparencia.
- Para un fondo de un solo color, [Quitar un fondo liso](../../05-filter/removeBg/README.md) lo hace en su navegador, sin créditos.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
