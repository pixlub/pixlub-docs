# Reemplazar colores

Sustituir uno o varios colores de una imagen por otros.

**Categoría** : Ajuste · **Identificador** : `replaceColors` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/replaceColors)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuyos colores de origen se reemplazan. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Un par de colores y luego la tolerancia.](../../../../assets/modules/replaceColors/demo.en.webp)](../../../../assets/modules/replaceColors/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/replaceColors/demo.en.mp4) : Un par de colores y luego la tolerancia.

1. `0:00` Import an image
2. `0:02` Add a colour pair
3. `0:15` Widen with the tolerance
4. `0:19` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Añadir un par**

   **Añadir un color** y luego elija el color que reemplazar y el nuevo (código HEX o cuentagotas).

3. **Ajustar la tolerancia**

   Súbala para incluir los matices cercanos.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Colores** | Lista de pares: color que reemplazar → nuevo color. |
| **Tolerancia** | 0 %: solo el color exacto. 100 %: todos los colores. |

## Consejos

- Una tolerancia del 20 al 40 % basta para un color plano con sus ligeras variaciones.
- Para cambiar un color conservando sus matices, [HSL](../hsl/README.md) es más suave.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
