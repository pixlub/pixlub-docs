# Aberración cromática

Desplazar los canales rojo y azul: efecto de objetivo, glitch o impacto.

**Categoría** : Filtros · **Identificador** : `chromatic` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/chromatic)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Imagen(es)** (obligatoria)<br />Imagen cuyos canales rojo y azul se desplazan. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Uno o varios: cada imagen se procesa por separado, con los mismos ajustes |

El número de imágenes que se procesan a la vez depende de su plan.

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Presentación en video

[![Desplazamiento radial, centro y luego uniforme con estela.](../../../../assets/modules/chromatic/demo.en.webp)](../../../../assets/modules/chromatic/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/chromatic/demo.en.mp4) : Desplazamiento radial, centro y luego uniforme con estela.

1. `0:00` Import an image
2. `0:02` Radial shift
3. `0:08` Place the center
4. `0:10` Uniform, as a trail
5. `0:14` Export the result

## Uso

1. **Importar**

   Suelte una o varias imágenes.

2. **Dosificar el desplazamiento**

   La **intensidad** separa los canales y la **zona preservada** mantiene nítido el centro.

3. **Colocar el centro**

   En modo radial, haga clic en la vista previa.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Modo** | **Radial** (desde un centro) o **Uniforme** (en una dirección). |
| **Intensidad** | 0 a 100 px. |
| **Método** | **Desplazamiento** nítido o **Estela**. |
| **Zona preservada** / **Suavidad** | Modo radial: centro intacto y fundido hacia los bordes. |
| **Ángulo** | Modo uniforme: dirección del desplazamiento. |

## Consejos

- Un desplazamiento radial pequeño imita un objetivo real; un desplazamiento uniforme fuerte da un efecto glitch.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

Con varias imágenes, el botón pasa a ser **Descargar en ZIP**; el menú también ofrece los archivos por separado o solo la imagen mostrada.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
