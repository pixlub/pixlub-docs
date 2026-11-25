# Caleidoscopio

Repetir una parte de la imagen en simetría alrededor de un centro.

**Categoría** : Transformación · **Identificador** : `kaleidoscope` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/kaleidoscope)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen en la que un sector se repite en simetría radial. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Segmentos, rotación, espejo y centro.](../../../../assets/modules/kaleidoscope/demo.en.webp)](../../../../assets/modules/kaleidoscope/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/kaleidoscope/demo.en.mp4) : Segmentos, rotación, espejo y centro.

1. `0:00` Import an image
2. `0:03` Number of segments
3. `0:06` Rotation and mirror
4. `0:14` Place the center
5. `0:16` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Elegir los segmentos**

   Cuantos más **segmentos** haya, más fino es el motivo.

3. **Colocar el centro**

   Haga clic en la vista previa: la parte repetida parte de ese punto.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Segmentos** | 1 a 64 partes alrededor del centro. |
| **Rotación** | −180° a 180°. Cambia la parte de la imagen que se toma. |
| **Espejo** | Marcado: una de cada dos partes se invierte y las uniones desaparecen. |
| **Centro X** / **Y** | Posición del centro, en %. |

## Consejos

- 6 u 8 segmentos con el espejo dan un motivo de rosetón regular.
- Una imagen muy colorida da los motivos más vivos.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
