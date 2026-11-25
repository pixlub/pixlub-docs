# Filtro de accesibilidad

Corregir los colores de una imagen para que sigan siendo legibles con una visión daltónica.

**Categoría** : Ajuste · **Identificador** : `colorAccessibility` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/colorAccessibility)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuyos colores se corrigen para una visión daltónica. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Elegir la visión, dosificar la corrección.](../../../../assets/modules/colorAccessibility/demo.en.webp)](../../../../assets/modules/colorAccessibility/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/colorAccessibility/demo.en.mp4) : Elegir la visión, dosificar la corrección.

1. `0:00` Import an image
2. `0:02` Pick the vision
3. `0:06` Dose the correction
4. `0:14` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Elegir la visión**

   Protanopía, deuteranopía, tritanopía o sus formas atenuadas.

3. **Dosificar**

   Contraste, separación de colores e intensidad de la corrección.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Simulación** | Visión para la que se corrige la imagen. **Normal** no cambia nada. |
| **Contraste** | Separa los colores alrededor del gris medio. |
| **Separación de colores** | Traslada los matices perdidos a los colores que aún se perciben. |
| **Intensidad** | Dosis de la corrección. |

## Consejos

- Útil para un gráfico o un mapa cuyos colores transmiten información.
- La deuteranomalía (verde mal percibido) es la forma más común.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
