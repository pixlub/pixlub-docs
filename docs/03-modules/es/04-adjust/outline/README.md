# Contorno

Rodear la silueta de una imagen recortada con un trazo de color.

**Categoría** : Ajuste · **Identificador** : `outline` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/outline)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuya silueta (alfa) recibe el contorno. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Grosor y luego color del contorno.](../../../../assets/modules/outline/demo.en.webp)](../../../../assets/modules/outline/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/outline/demo.en.mp4) : Grosor y luego color del contorno.

1. `0:00` Import a cut-out image
2. `0:03` Thickness
3. `0:07` Colour
4. `0:12` Export the result

## Uso

1. **Importar**

   Suelte una imagen con transparencia: el contorno sigue su silueta.

2. **Ajustar**

   Elija el **grosor** y luego el **color**.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Grosor** | 0 a 100 px. |
| **Color** | Color del trazo. |

## Consejos

- Un contorno blanco grueso da un efecto de pegatina; añada [Sombra](../shadow/README.md) para dar relieve.
- En una imagen sin transparencia, el contorno solo sigue el borde del marco.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
