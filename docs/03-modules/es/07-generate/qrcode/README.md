# Código QR

Generar un código QR legible por cualquier lector, con estilo, con un logotipo o fundido en una imagen.

**Categoría** : Generación · **Identificador** : `qrcode` · [Referencia de la API](./api.md)

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/qrcode)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Grafo de imagen](https://pixlub.com/es/image/graph)** : Conéctelo a otros módulos para componer un efecto más complejo.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Logotipo** (opcional)<br />Imagen opcional colocada en el centro del código QR; en automático, la corrección sube a H. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |
| **Imagen** (opcional)<br />Imagen opcional convertida en motivo de código QR, en la que se funde el código QR (modo «En una imagen»); su transparencia da la silueta. | `PNG`, `JPEG`, `WebP`, `GIF`, `AVIF`, `BMP` | Un archivo |

Mediante la API, los archivos y sus formatos se detallan en la [vista API](./api.md).

## Uso

1. **Elegir el contenido**

   Enlace, texto, Wi-Fi, correo electrónico, teléfono, SMS, contacto (vCard) o ubicación. Cada tipo sigue el formato que leen los lectores habituales.

2. **Dar estilo**

   Sección **Diseño**, botón **Diseño, colores y decoración**: una galería de miniaturas para la forma, los módulos, los ojos y los colores. Los ajustes finos (tamaño, opacidad, degradado…) siguen en el panel.

3. **Añadir un logotipo**

   Conecte una imagen a la entrada **Logotipo**: se coloca en el centro, sobre una placa, y la corrección sube a H.

4. **Poner dentro de una forma**

   Sección **Integración**, modo **En una forma**: campana, corazón, casa, nube, taza… o **Desde la imagen** para la silueta de una imagen conectada (su transparencia, o su contorno para un dibujo de línea). La silueta, blanca y perfilada, se rellena de módulos con el mismo dibujo que el código QR, que se coloca en ella solo; arrástrelo en la vista previa y tire de una esquina para cambiar su tamaño.

5. **Fundir en una imagen**

   Sección **Integración**, modo **En una imagen**, y luego conecte una imagen (un pez, un logotipo…) a la entrada **Imagen**. Se convierte en un motivo de módulos con el estilo del código QR; arrastre el código QR dentro en la vista previa y tire de una esquina para cambiar el tamaño de los módulos.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Tipo** | Enlace, texto, Wi-Fi, correo electrónico, teléfono, SMS, contacto, ubicación. |
| **Corrección de errores** | Auto (M, o H con logotipo o semitono), L, M, Q, H. |
| **Versión mínima** / **Máscara** | Cuadrícula más fina o fija; patrón de enmascaramiento. |
| **Módulos** | Cuadrados, fluido, puntos, cuadrados redondeados, rombos, estrellas, cruces, corazones, hojas, barras, confeti; tamaño y redondeado. |
| **Ojos** | Marco y centro de los ojos y de los patrones de alineación, colores propios. |
| **Colores** | Color o degradado de los módulos, fondo, opacidades, esquinas del fondo. |
| **Dimensiones** | Tamaño de la imagen y margen (4 módulos según la norma). |
| **Logotipo** | Tamaño, placa (cuadrada, redondeada, redonda), margen, despeje de los módulos, opacidad. **Tamaño seguro** reduce el logotipo al mayor tamaño que la corrección de errores puede reparar. |
| **Silueta** | Forma, grosor y color del contorno, densidad del motivo. |
| **Colocación** | Tamaño de los módulos, posición del código QR, halo claro alrededor, borde claro alrededor de los ojos. |
| **Conversión** | Motivo QR (por defecto), umbral, difusión o trama; relieve de los tonos, variante, umbral, contraste, inversión, silueta y contorno, color de los módulos. |
| **Fusión** | Imagen a través del QR (semitono) y su fuerza, fondo sólido bajo el QR, imagen original de fondo. |

## Consejos

- Pruebe siempre el escaneo con varios teléfonos antes de imprimir.
- Mantenga los módulos claramente más oscuros que el fondo; un código claro sobre fondo oscuro no lo leen todos los lectores.
- Para los ojos, mantenga una misma familia de formas entre el marco y el centro (cuadrado con cuadrado, redondo con redondo).
- En modo imagen, el **Motivo QR** convierte la imagen en una textura de código QR: con un halo a 0, el código se funde en ella sin borde. Con **Color de los módulos: De la imagen**, el motivo, el código QR y los ojos toman el color de la imagen que tienen debajo.
- Un logotipo demasiado grande tapa palabras del código: deje marcado **Tamaño seguro** y suba la corrección a H para un logotipo más grande.

## Exportación

El botón **Descargar** guarda el resultado en el formato del archivo importado: una foto JPEG sale en JPEG. El menú a su derecha abre los **Ajustes de exportación** para elegir otro formato y ajustar la calidad, el tamaño o el fondo, y ofrece **Copiar la imagen**.

- **[La ventana de exportación](../../../../01-app/es/02-image/04-exportation.md)** : Todos los formatos, sus ajustes, el procesamiento local o en el servidor, los lotes y la carpeta local.
