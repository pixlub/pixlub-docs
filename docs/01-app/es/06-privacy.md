# Procesamiento local y en servidor

Lo que se queda en su dispositivo, lo que se envía a nuestros servidores y cómo se lo indica la insignia de privacidad.

Pixlub procesa sus archivos **en su navegador**. Es un compromiso: mientras no intervenga ninguna operación remota, sus imágenes, videos y documentos no salen de su dispositivo.

## La insignia

Las páginas de edición (página de módulo, grafo de imagen, editor de video, editor de ajustes) muestran una insignia en la parte inferior de la pantalla:

| Insignia | Significado |
| --- | --- |
| **Procesamiento local** | No se envía nada: todo se calcula en su dispositivo. |
| **Enviado al servidor** | Una operación de la página envía un archivo a nuestros servidores. Abra la insignia para ver cuál. |

La insignia anuncia lo que la página **está a punto** de enviar, no solo lo que ya se ha enviado: cambia en cuanto coloca un módulo de IA, elige un formato codificado por el servidor o abre los subtítulos automáticos. También conserva el historial de lo que ya se ha enviado durante la sesión. Puede moverla; se coloca en el lado más cercano.

## Lo que se envía a nuestros servidores

| Operación | Lo que se envía |
| --- | --- |
| Módulo de IA (quitar el fondo, desenfoque automático, calcomanía…) | La imagen de entrada del módulo, y solo los ajustes que necesita el servicio. |
| Formato de exportación codificado por la API (AVIF, HEIC, TIFF, PDF…) | La imagen que convertir. |
| Subtítulos automáticos | El audio del montaje. |
| Conversión de Office o HTML a PDF | El archivo que convertir. |

Los demás ajustes de un módulo de IA se quedan en su dispositivo: modificarlos no provoca un nuevo envío ni deja el resultado obsoleto.

## Qué pasa con los archivos enviados

El resultado está disponible mediante un enlace firmado, válido durante una hora; los archivos se eliminan de nuestros servidores al cabo de 24 horas. Las estadísticas de uso solo guardan el nombre de los módulos usados, y el tamaño y el tipo de los archivos importados, nunca su nombre ni su contenido.

Para conocer en detalle las medidas de seguridad, consulte la página [Seguridad](https://pixlub.com/es/security).
