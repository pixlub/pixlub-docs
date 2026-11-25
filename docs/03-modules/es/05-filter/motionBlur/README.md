# Desenfoque de movimiento

Dar una sensación de velocidad: barrido lineal, zoom o rotación.

**Categoría** : Filtros · **Identificador** : `motionBlur` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/motionBlur)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen a la que se aplica el desenfoque de movimiento. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Barrido lineal y luego zoom y rotación.](../../../../assets/modules/motionBlur/demo.en.webp)](../../../../assets/modules/motionBlur/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/motionBlur/demo.en.mp4) : Barrido lineal y luego zoom y rotación.

1. `0:00` Import an image
2. `0:02` Linear streak
3. `0:09` Zoom and spin
4. `0:13` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Elegir el modo**

   **Lineal**, **Zoom** o **Rotación**.

3. **Dosificar**

   La **intensidad**, y el **ángulo** en modo lineal.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Modo** | Lineal, zoom o rotación. |
| **Intensidad** | 0 a 100 %. |
| **Ángulo** | Modo lineal: dirección del barrido, −180° a 180°. |

## Consejos

- Alinee el ángulo con la dirección del sujeto para un efecto de velocidad creíble.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
