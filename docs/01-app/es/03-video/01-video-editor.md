# Editor de video

Montar videos, sonidos, imágenes y textos en el navegador: línea de tiempo, efectos, transiciones, subtítulos y exportación.

El [editor de video](https://pixlub.com/es/video/editor) es un programa de edición completo que se ejecuta en su navegador. La decodificación, la vista previa y la codificación se hacen en su dispositivo; solo los **subtítulos automáticos** envían el audio del montaje a nuestros servidores.

## La interfaz

| Zona | Función |
| --- | --- |
| Medios | Sus archivos importados (videos, sonidos, imágenes), los textos, los sólidos, las transiciones, las composiciones y las grabaciones. |
| Vista previa | La reproducción del montaje, en vista **Proyecto** o **Clip** (solo el clip seleccionado). |
| Panel | Los ajustes del clip seleccionado, o los del proyecto (dimensiones, frecuencia de fotogramas, fondo). |
| Línea de tiempo | Las pistas de video y de audio, los clips, el cabezal de reproducción y las curvas de animación. |

## Montar

1. **Importar**

   Suelte videos, sonidos o imágenes en **Medios**, o directamente en la línea de tiempo.

2. **Colocar en la línea de tiempo**

   Arrastre un medio a una pista. Si lo suelta por encima de las pistas existentes, se crea una nueva línea en primer plano.

3. **Recortar y organizar**

   Mueva los clips y tire de sus bordes para acortarlos. Las **guías magnéticas** alinean los clips entre sí; <kbd>Ctrl</kbd> durante el desplazamiento las desactiva.

4. **Exportar**

   **Exportar** abre la ventana de exportación: formato (MP4, WebM, MOV…), dimensiones, calidad. La codificación se hace en el navegador.

## Atajos

| Acción | Atajo |
| --- | --- |
| Reproducir / Pausa | <kbd>Espacio</kbd> |
| Fotograma anterior / siguiente | <kbd>←</kbd> / <kbd>→</kbd> |
| Retroceder / avanzar 10 fotogramas | <kbd>Mayús</kbd> + <kbd>←</kbd> / <kbd>Mayús</kbd> + <kbd>→</kbd> |
| Punto de edición anterior / siguiente | <kbd>Ctrl</kbd> + <kbd>←</kbd> / <kbd>Ctrl</kbd> + <kbd>→</kbd> |
| Inicio / final del montaje | <kbd>Inicio</kbd> / <kbd>Fin</kbd> |
| Reproducción en bucle | <kbd>L</kbd> |
| Silenciar | <kbd>M</kbd> |
| Dividir en el cabezal de reproducción | <kbd>S</kbd> |
| Recortar el inicio / el final hasta el cabezal de reproducción | <kbd>Q</kbd> / <kbd>W</kbd> |
| Cortar / Copiar / Pegar | <kbd>Ctrl</kbd> + <kbd>X</kbd> / <kbd>Ctrl</kbd> + <kbd>C</kbd> / <kbd>Ctrl</kbd> + <kbd>V</kbd> |
| Duplicar el clip | <kbd>Ctrl</kbd> + <kbd>D</kbd> |
| Seleccionar todo | <kbd>Ctrl</kbd> + <kbd>A</kbd> |
| Eliminar el clip | <kbd>Supr</kbd> |
| Separar el audio | <kbd>Ctrl</kbd> + <kbd>Mayús</kbd> + <kbd>D</kbd> |
| Precomponer | <kbd>Ctrl</kbd> + <kbd>Mayús</kbd> + <kbd>C</kbd> |
| Deshacer / Rehacer | <kbd>Ctrl</kbd> + <kbd>Z</kbd> / <kbd>Ctrl</kbd> + <kbd>Mayús</kbd> + <kbd>Z</kbd> |
| Zoom de la línea de tiempo | <kbd>Ctrl</kbd> + <kbd>+</kbd> / <kbd>Ctrl</kbd> + <kbd>-</kbd> |
| Ajustar la línea de tiempo | <kbd>Mayús</kbd> + <kbd>1</kbd> |
| Vista solo del clip | <kbd>Alt</kbd> + <kbd>V</kbd> |
| Guías magnéticas | <kbd>Alt</kbd> + <kbd>G</kbd> |
| Monitor a cuadro completo | <kbd>F</kbd> |
| Nuevo proyecto | <kbd>Alt</kbd> + <kbd>N</kbd> |
| Abrir un archivo / desde el almacenamiento | <kbd>Ctrl</kbd> + <kbd>O</kbd> / <kbd>Ctrl</kbd> + <kbd>Mayús</kbd> + <kbd>O</kbd> |
| Guardar | <kbd>Ctrl</kbd> + <kbd>S</kbd> |
| Exportar | <kbd>Ctrl</kbd> + <kbd>E</kbd> |

Todos estos comandos están, con su atajo, en los menús **Archivo**, **Edición**, **Clip**, **Reproducción** y **Ver** de la barra superior. El menú **MCP** muestra el estado de la conexión con una IA vinculada y abre sus opciones.

El menú contextual de un clip también ofrece **Copiar**, **Cortar**, **Pegar**, **Dividir** y **Separar el audio**.

## Pistas

Cada pista se puede **ocultar**, **silenciar** (audio), **bloquear** o reordenar arrastrándola. Una pista de video tiene su propio **modo de fusión** con lo que hay detrás de ella.

## Efectos y animación

Los módulos de video y de imagen se colocan como **efecto** sobre un clip. Sus ajustes son **animables**: despliegue el efecto en la línea de tiempo para colocar fotogramas clave y luego afínelos en la vista **Curvas** o en la **Hoja**.

## Textos, sólidos y transiciones

- **Textos**: suelte un texto en una pista y luego ajuste la fuente, los estilos y las animaciones en el panel del clip. Una composición de texto colocada se modifica con un doble clic.
- **Sólidos**: colores sólidos y formas que se colocan como un clip.
- **Efectos**: efectos visuales listos para colocar sobre un clip: ondas de clic, deslizamientos, luces, destellos, marcas, ambientes. Cada uno es una composición de formas, partículas y fotogramas clave: un doble clic la abre para cambiar sus colores, sus formas o su ritmo.
- **Sonidos**: cerca de doscientos efectos de sonido agrupados por tema: clics, interfaz, alertas, soplos, impactos, subidas, magia, juego retro, ciencia ficción, dibujos animados, ambientes. Un clic reproduce el sonido y, al arrastrarlo, se coloca en una pista. Cada efecto de sonido se sintetiza en su navegador: no se descarga ningún archivo ni se incluye música.
- **Transiciones**: se sueltan sobre un punto de edición entre dos clips que se tocan, o al principio y al final de una pista. Dos clips que se superponen en la misma pista se convierten en un fundido.

## Composiciones

Una **composición** es un montaje dentro del montaje. Seleccione clips y **precompóngalos** para agruparlos; abra la composición para modificarla y luego vuelva al nivel superior mediante la ruta de las composiciones abiertas.

## Seguimiento de movimiento

El **seguimiento de movimiento** fija un texto, una imagen o una forma a algo que se mueve en un video o en una imagen animada. El análisis se ejecuta en el navegador: no se envía nada.

1. **Abrir la herramienta**

   Haga clic derecho en el video, en la línea de tiempo o en la vista previa, y luego **Herramientas → Seguimiento de movimiento**. La misma entrada está en el menú **Edición** y como icono en la parte superior de la vista previa cuando el clip seleccionado lo permite. El panel derecho muestra entonces la herramienta; **Ajustes del clip**, arriba, permite salir de ella.

2. **Elegir qué seguir**

   **Punto** para un elemento que solo se desplaza, **Objeto** para un elemento que gira, se acerca o se aleja, **Superficie** para una superficie plana vista en ángulo (pantalla, cartel, pared) cuyas cuatro esquinas usted coloca.

3. **Colocar el marco azul**

   Ya hay un marco sobre la vista previa. Arrástrelo sobre el elemento y estire sus esquinas a su alrededor: una zona contrastada se sigue mejor que una zona uniforme.

4. **Iniciar el seguimiento**

   **Iniciar el seguimiento** analiza todo el clip a partir del fotograma mostrado. La barra indica lo que está seguido; haga clic en ella para ir a un fotograma.

5. **Enlazar un elemento**

   Los clips colocados por encima del video aparecen en una lista: un interruptor enlaza cada uno al marco. El elemento conserva el lugar que ocupa en el fotograma mostrado y luego lo sigue; todavía puede moverlo, escalarlo o girarlo. **Orientar según la trayectoria** lo hace girar con la dirección del desplazamiento, como una flecha en su camino.

El marco también se dibuja y se agarra alrededor de la imagen: para encuadrar un elemento que sale del plano, aleje la vista previa y estire sus esquinas más allá del borde. En el modo **Objeto**, el marco gira cuando se agarra justo fuera de una esquina. En la línea de tiempo, un icono de diana marca el clip seguido, y una diana rellena el clip enlazado.

**Si el marco pierde el elemento** (pasa detrás de un obstáculo, sale de la imagen), el seguimiento se detiene y el marco se vuelve rojo. Avance hasta el fotograma en el que el elemento reaparece y coloque el marco sobre él: el seguimiento se reanuda solo y el tramo oculto se completa. Para corregir un seguimiento que se ha desviado, vuelva a colocar el marco en un fotograma y elija **Corregir lo que sigue** o **Corregir lo anterior**.

### Ajustar un tramo a mano

El seguimiento dibuja una **línea**: el recorrido del centro del marco. Cuando se desvía, **Ajustar a mano** permite editar esa línea sin volver a ejecutar el análisis. Una paleta de herramientas aparece entonces en la parte superior de la vista previa; el marco ya no se mueve a mano: queda reservado al seguimiento automático.

Lo más rápido es volver editable **todo un tramo** en un solo gesto: arrastre a lo largo de la barra de seguimiento del panel (de 1 s a 3 s, por ejemplo) o a lo largo de la línea con la herramienta **Tramo**. El tramo se convierte en una sola curva naranja, sostenida por unos pocos puntos situados donde cambia la trayectoria; su forma no se mueve mientras no la toque.

- **Seleccionar**: arrastre un punto para moverlo; la vista previa salta a su fotograma, de modo que lo coloca viendo lo que debe seguir. Un punto seleccionado muestra sus dos **tiradores**: arrástrelos para ajustar la curvatura. <kbd>Mayús</kbd> + clic o un recuadro trazado en una zona vacía eligen varios puntos, que se mueven juntos.
- **Punto**: haga clic en la línea para añadir un punto. Dentro de un tramo, la curva se divide en dos sin cambiar de forma.
- **Punto de curva** mantiene los dos tiradores alineados; **Punto de esquina** los vuelve independientes (<kbd>Alt</kbd> al arrastrar un tirador hace lo mismo).
- **Suavizar** da a los puntos seleccionados los tiradores de una curva regular; **Eliminar** los quita y, donde ya nada la cubre, la línea vuelve al análisis.

Si el primer o el último punto de un tramo se aleja del seguimiento, los fotogramas vecinos se unen a él suavemente: no hay salto en la unión. El tramo editado aparece en naranja en la línea y en la barra. **Reanudar el seguimiento automático desde aquí** vuelve a lanzar el análisis desde el fotograma en pantalla, conservando sus puntos; al recorrer la línea de tiempo, el cabezal de reproducción se pega a los puntos cercanos.

### Enlazar a un clip

Para un elemento animado con fotogramas clave (un texto, una forma, una imagen que se mueve en la línea de tiempo), no hay nada que analizar: **Herramientas → Enlazar a un clip** hace que un clip tome el movimiento de otro clip. Elija el clip que lo lleva y luego lo que toma de él: solo la **posición** o **todo el movimiento** (posición, escala, rotación). El clip enlazado conserva el lugar que ocupa en el primer fotograma en el que ambos son visibles; todavía se puede mover y animar, y puede orientarse según la trayectoria.

### Enlazar dos clips en la línea de tiempo

Cada clip muestra los iconos de sus herramientas en la parte inferior de su bloque. Arrastre el icono de **enlace** de un clip sobre otro clip para enlazarlo a él; arrastre el icono de **diana** de un clip seguido sobre otro clip para enlazar este último al elemento seguido (si el clip sigue varios, un pequeño menú pregunta cuál). Durante el gesto, solo los clips que se superponen al de partida conservan su color; soltar en otro lugar no cambia nada. Un simple clic en el icono abre la herramienta. En los paneles, un clic en el nombre de un clip lo localiza en la línea de tiempo, donde brilla un instante.

## Subtítulos

El panel **Subtítulos** ofrece tres puntos de partida:

- **Subtítulos automáticos**: nuestro servicio transcribe el audio del montaje. Elija el idioma original (o la detección automática); los subtítulos se escriben en el idioma hablado. El costo estimado, facturado por minuto iniciado, se muestra antes del envío.
- **Importar un archivo SRT / VTT**.
- **Escribir los subtítulos** a mano.

Después, las líneas se modifican una a una: cortar en el cursor, combinar, asignar un hablante, ajustar el tiempo de cada palabra. **Exportar en .srt** guarda el archivo de subtítulos.

> [!WARNING]
> **Enviado al servidor**
>
> En cuanto se abre el panel de subtítulos automáticos, la insignia de privacidad cambia a **Enviado al servidor**: es el único caso en el que el editor de video transmite contenido. Consulte [Procesamiento local y en servidor](../06-privacy.md).

## Grabar

La pestaña **Grabación** captura la pantalla, la cámara y el micrófono, juntos o por separado, con la cámara incrustada en una esquina. Todo se captura en el navegador; las tomas se suman a los medios, listas para arrastrarlas al montaje.
