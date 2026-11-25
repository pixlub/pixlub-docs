# Opacidad

Hacer una imagen más o menos transparente.

**Categoría** : Ajuste · **Identificador** : `opacity` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/opacity)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuya opacidad se modifica. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Bajar la opacidad.](../../../../assets/modules/opacity/demo.en.webp)](../../../../assets/modules/opacity/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/opacity/demo.en.mp4) : Bajar la opacidad.

1. `0:00` Import an image
2. `0:02` Lower the opacity
3. `0:07` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Ajustar la opacidad**

   Arrastre la barra o escriba el valor. La cuadrícula muestra la transparencia.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Opacidad** | 0 a 100 %. |

Exporte en PNG o WebP: el JPEG no conserva la transparencia.

## Consejos

- Para una marca de agua, baje la opacidad de un logotipo y luego superpóngalo en el [grafo de imagen](../../../../01-app/es/02-image/01-image-graph.md).

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
