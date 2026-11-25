# Combinar los canales

Recompone una imagen a partir de canales R, G, B y/o alfa

**Categoría** : Composición · **Identificador** : `channelMerge` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **R** (opcional)<br />Canal en escala de grises que se convierte en el rojo de la imagen; si falta, el rojo vale 0. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |
| **G** (opcional)<br />Canal en escala de grises que se convierte en el verde de la imagen; si falta, el verde vale 0. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |
| **B** (opcional)<br />Canal en escala de grises que se convierte en el azul de la imagen; si falta, el azul vale 0. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |
| **A** (opcional)<br />Canal en escala de grises que se convierte en el alfa de la imagen; si falta, la imagen es opaca. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

> [!NOTE]
> **Guía en preparación**
>
> Este módulo todavía no tiene una guía detallada. Sus ajustes muestran su descripción en la aplicación; la vista API enumera cada uno de ellos con sus límites.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
