# Posterizar

Reducir el número de matices por canal para obtener colores planos estilizados.

**Categoría** : Ajuste · **Identificador** : `posterize` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/posterize)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuyos niveles de cada canal se reducen. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![3 niveles, luego 8, y la opacidad.](../../../../assets/modules/posterize/demo.en.webp)](../../../../assets/modules/posterize/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/posterize/demo.en.mp4) : 3 niveles, luego 8, y la opacidad.

1. `0:00` Import an image
2. `0:03` Number of levels
3. `0:09` Dose it with the opacity
4. `0:17` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Elegir el número de niveles**

   Pocos niveles: colores planos marcados. Muchos: la imagen se acerca a la original.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Niveles** | 2 a 256 escalones por canal. |
| **Aplicar a la transparencia** | También posteriza el canal alfa. |
| **Fusión** | Modo de fusión y opacidad: cómo se aplica el ajuste sobre la imagen original. |

## Consejos

- De 4 a 6 niveles dan un efecto de cartel o de dibujo animado.
- Combínelo con [Contorno](../outline/README.md) para un acabado de cómic.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
