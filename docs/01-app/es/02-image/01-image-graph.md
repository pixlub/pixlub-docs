# Grafo de imagen

Componer una imagen conectando módulos: orígenes, efectos, salidas, animación y proyectos .epxl.

El [grafo de imagen](https://pixlub.com/es/image/graph) es el editor más completo de Pixlub. Cada **módulo** se convierte en un nodo; se conecta la salida de un nodo a la entrada de otro para encadenar las operaciones. Nada queda fijo: cambiar un ajuste aguas arriba recalcula toda la cadena.

## Empezar un proyecto

Al abrirlo, una ventana propone tres puntos de partida:

- **Nuevo proyecto**: un lienzo en blanco;
- **Importar**: un proyecto `.epxl` guardado antes, o un proyecto de su [carpeta local](../05-account-and-credits.md#carpeta-local);
- **Guías de descubrimiento**: miniproyectos comentados que muestran cómo combinar los módulos.

## Construir el grafo

1. **Añadir una imagen**

   Arrastre una o varias imágenes al lienzo: cada una se convierte en un módulo **Imagen de origen**. Varias imágenes soltadas juntas forman un **lote**, procesado de una sola vez.

2. **Añadir módulos**

   La barra lateral izquierda enumera todos los módulos, con un buscador y preajustes. Arrastre uno al lienzo, o haga clic derecho en el lienzo.

3. **Conectar los puertos**

   Arrastre desde la salida de un módulo hasta la entrada de otro. Un puerto solo se conecta a un tipo compatible; la leyenda de las conexiones recuerda los colores.

4. **Ajustar**

   Haga clic en un módulo para abrir su panel. La pestaña **Ajustes** contiene sus parámetros; la pestaña **Propiedad**, su título, su color y la visualización de su vista previa.

5. **Exportar**

   Conecte el resultado a un módulo **Salida** y luego exporte en el formato deseado.

## Los tipos de puerto

| Puerto | Qué circula |
| --- | --- |
| Imagen | Una imagen en color, con transparencia. |
| Canal | Una imagen en escala de grises: un canal R, G, B o A, una máscara. |
| Número | Un valor, procedente de los módulos **Valores** (tamaño de imagen, suma…). |
| Color | Un color sólido. |
| Paleta | Una lista de colores. |
| Lote | Un conjunto de imágenes procesadas juntas. |
| Trazado | Un trazado vectorial. |
| Modelo 3D | Un modelo, para los módulos 3D. |

Una entrada **obligatoria** sin conectar se señala en el nodo. Un puerto **Lote** conectado a una entrada simple solo usa una imagen del lote; la vista previa permite elegir cuál.

## Organizar el lienzo

- **Herramientas** de la barra: desplazamiento, selección con lazo, agrupación de la selección en un **marco**, encuadre de la vista y zoom.
- **Notas**: añada una nota desde la barra lateral para comentar el grafo (negrita, cursiva).
- **Desactivar** un módulo lo deja fuera del circuito sin eliminarlo: útil para comparar.
- **Deshacer / Rehacer**: <kbd>Ctrl</kbd> + <kbd>Z</kbd> y <kbd>Ctrl</kbd> + <kbd>Y</kbd>.
- **Pausa**: la barra superior suspende el cálculo de las imágenes mientras construye un grafo pesado.

## Vistas previas y herramientas

La vista previa de un nodo se muestra en el lienzo y en grande en el panel. En ella se puede hacer zoom, cambiar el fondo, aislar el canal alfa o un canal de color. Varios módulos se manipulan directamente allí: recorte, rotación, perspectiva, deformación con alfileres, trazados, zonas de desenfoque…

> [!NOTE]
> **Vista previa reducida**
>
> Para mantener la fluidez, la vista previa puede calcularse a una resolución reducida; la mención **Vista previa reducida** lo indica. La exportación, en cambio, siempre se hace a resolución completa.

## Animación

El modo **Animación** de la barra superior abre la franja de tiempo. Los módulos animados (partículas, brillos, ondulaciones…) y los ajustes animados se reproducen allí en bucle, y la exportación ofrece entonces los formatos animados: GIF, APNG o video.

## Guardar y retomar

- **Guardar el proyecto** genera un archivo `.epxl`: módulos, conexiones, ajustes y, si lo desea, las imágenes de origen.
- **Importar un proyecto** reemplaza el grafo actual por el de un archivo `.epxl`.
- Con una [carpeta local](../05-account-and-credits.md#carpeta-local) elegida en la configuración, el grafo se **guarda automáticamente** allí.

Un proyecto abierto en una versión más reciente de Pixlub actualiza sus módulos; un módulo que ya no existe se señala en su nodo.

## Rendimiento

El botón **Configuración** de la barra ajusta la frecuencia de recálculo y el tamaño de las vistas previas (Rápido, Normal, Optimizado). La **aceleración por GPU** ejecuta los módulos compatibles en la tarjeta gráfica mediante WebGPU, con respaldo automático en el procesador.

## Módulos de IA en el grafo

Un módulo de IA colocado en el grafo no se ejecuta solo: muestra **Ejecutar la solicitud** con su precio. Si un módulo aguas arriba cambia, su resultado queda **obsoleto** y espera a que lo vuelva a ejecutar. Consulte [Procesamiento local y en servidor](../06-privacy.md).
