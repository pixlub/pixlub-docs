# Extracción de audio

Sacar la pista de audio de un video a un archivo de audio.

**Categoría** : Conversión · **Identificador** : `extractAudioVideo`

## Dónde usarlo

- **[Página del módulo](https://pixlub.com/es/module/extractAudioVideo)** : Suelte sus archivos, ajuste y descargue: el módulo por sí solo, sin nada más.
- **[Editor de video](https://pixlub.com/es/video/editor)** : Añádalo como efecto en un clip del montaje.

## Entradas

Los archivos que acepta la página del módulo: suéltelos en la zona de importación o haga clic en ella para buscarlos. Un archivo de otro formato se descarta, con un mensaje que recuerda los formatos permitidos.

| Entrada | Formatos aceptados | Archivos |
| --- | --- | --- |
| **Video** (obligatoria)<br />Video cuya pista de sonido se extrae. | `MP4`, `WebM`, `MOV`, `MKV` | Un archivo |

## Presentación en video

[![Importar un video, elegir el formato de audio.](../../../../assets/modules/extractAudioVideo/demo.en.webp)](../../../../assets/modules/extractAudioVideo/demo.en.mp4)

▶ [Ver el video](../../../../assets/modules/extractAudioVideo/demo.en.mp4) : Importar un video, elegir el formato de audio.

1. `0:00` Import a video
2. `0:05` Pick the audio format
3. `0:09` Export the result

## Uso

1. **Importar**

   Suelte uno o varios videos con sonido: cada uno tiene su espacio de trabajo.

2. **Conservar una parte**

   Tire de los controladores de la línea de tiempo, donde la forma de onda sigue a las imágenes.

3. **Elegir el formato**

   En la ventana de exportación: pista original, MP3, AAC, Opus, Vorbis, FLAC, WAV o AIFF.

## Ajustes

| Ajuste | Efecto |
| --- | --- |
| **Inicio / Final** | Parte del sonido que se conserva, en segundos (0 al final = hasta el final). |
| **Formato** (exportación) | Pista original (sin pérdida), MP3, AAC, Opus, Vorbis, FLAC, WAV o AIFF. |
| **Tasa de bits, frecuencia, canales, profundidad** (exportación) | Según el formato elegido. |

## Consejos

- La **pista original** es instantánea y sin pérdida: prefiérala si su formato le conviene.
- FLAC conserva todo el sonido, con la mitad de peso que el WAV.

## Exportación

El resultado se exporta desde la página del módulo o desde el editor de video, en MP4, WebM u otro contenedor de video, sin salir de su navegador.

- **[El editor de video](../../../../01-app/es/03-video/01-video-editor.md)** : Editar, ajustar los efectos y exportar un video.
