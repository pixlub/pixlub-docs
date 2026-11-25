# Módulo independiente

Usar un módulo solo, en su propia página: soltar sus archivos, ajustar, descargar.

Cada módulo que puede alimentarse de un simple archivo tiene su propia página, en la dirección `/module/<identificador>`: por ejemplo [Redimensionar](https://pixlub.com/es/module/resize) o [Desenfoque](https://pixlub.com/es/module/blur). Es la forma más rápida de aplicar una operación, sin construir un grafo.

## Usar un módulo

1. **Abrir el módulo**

   Desde la página de inicio, el menú de herramientas o la [lista de módulos](./02-image/README.md). La ficha de cada módulo, en la sección [Módulos](../../03-modules/es/README.md), también lleva a su página.

2. **Soltar sus archivos**

   Haga clic en la zona de carga o arrastre allí sus archivos. Llenan las entradas del módulo.

3. **Ajustar**

   El panel de opciones, a la derecha, agrupa los ajustes por sección. La vista previa se recalcula con cada cambio. **Restablecer** devuelve al módulo sus valores por defecto.

4. **Obtener el resultado**

   **Descargar** abre la [ventana de exportación](./02-image/04-exportation.md): elija el formato y sus ajustes (la vista previa ya muestra el resultado) y luego **Exportar**. Su menú ofrece una **descarga rápida** en PNG y **Copiar la imagen**, que la coloca en el portapapeles.

## Procesar varias imágenes

Suelte varias imágenes en la misma entrada: el módulo las procesa todas con los mismos ajustes. Las flechas de la vista previa pasan de una imagen a otra.

La columna de entradas agrupa las imágenes en **espacios de trabajo**, una casilla por espacio, cada uno con sus propios ajustes. Una insignia indica cuántas imágenes reúne un espacio.

- Haga clic en un espacio para abrirlo: el panel muestra sus ajustes y sus imágenes se despliegan en un menú horizontal.
- En ese menú, el **+** añade una imagen al espacio: recibe los mismos ajustes.
- **Nuevo espacio**, debajo de la columna, añade imágenes con sus propios ajustes, un espacio por imagen.
- El botón **Separar** de una imagen del menú la pasa a un nuevo espacio.

La exportación genera cada imagen con los ajustes de su espacio. La ventana de exportación las muestra todas, con su tamaño y su peso, y su sección **Lote** elige cómo se entregan:

- **Archivo ZIP**: todas las imágenes en un archivo comprimido;
- **Archivos separados**: un archivo por imagen.

El número de archivos por lote depende de su plan: consulte [Cuenta y créditos](./05-account-and-credits.md).

## Tamaño del resultado

El panel de opciones tiene dos pestañas: **Propiedad** para los ajustes del módulo y **Ajustes** para el tamaño de la imagen generada.

| Método | Tamaño del resultado |
| --- | --- |
| **Módulo** (por defecto) | El que produce el módulo. |
| **Origen** | El de la imagen recibida. |
| **Libre** | El ancho y el alto introducidos. |

En **Origen** y **Libre**, el **ajuste** coloca el resultado: **Ninguno** (recortado), **Contener**, **Cubrir** o **Estirar**, alineado según el **anclaje**.

## Variantes de la página

La página se adapta al medio del módulo:

| Medio | Qué cambia |
| --- | --- |
| Imagen | Vista previa con fondo ajustable (cuadrícula, color sólido). |
| Video | Reproductor; decodificación, renderizado y codificación en el navegador. Nada se envía a un servidor. |
| Documento | Lista de archivos reordenable, vista previa de las páginas, botón **Iniciar**. Consulte [Documentos](./04-document.md). |
| Conversión | Elección del formato de salida y de sus opciones. Consulte el [conversor](./02-image/02-image-converter.md). |

## Módulos de IA

Los módulos de IA (quitar el fondo, desenfoque automático de rostros, calcomanía…) envían la imagen a nuestros servidores. Su página:

- pide una **cuenta**: sin sesión, redirige al inicio de sesión;
- muestra el **precio en créditos** antes de iniciar, y nunca se vuelve a ejecutar sola: cada nuevo cálculo pasa por una confirmación;
- cambia la insignia de privacidad a **Enviado al servidor** en cuanto el módulo está listo para enviarse.
