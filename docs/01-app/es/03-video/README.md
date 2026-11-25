# Video

El editor de video y los módulos de video de Pixlub, por categoría.

El video se trabaja de dos formas: un módulo solo en su página, para una operación rápida (recortar, acelerar), o el [editor de video](./01-video-editor.md) para un montaje de verdad. En ambos casos, la decodificación, el renderizado y la codificación se hacen en su navegador.

- **[Editor de video](./01-video-editor.md)** : Montar clips, sonidos, textos y subtítulos.

## Las categorías

| Categoría | Qué contiene |
| --- | --- |
| Transformación | Recortar un video, cambiar su velocidad o su frecuencia de fotogramas. |
| Conversión | Extraer la pista de audio de un video. |
| Servicios de API | Desenfoque automático de rostros y subtítulos generados a partir del audio: estos dos módulos envían el video o su audio a nuestros servidores. |

En el editor de video, los módulos de imagen también se colocan como **efecto** sobre un clip: desenfoques, ajustes de color, deformaciones… se aplican fotograma a fotograma.

> [!NOTE]
> **Sin llamadas a la API**
>
> Los módulos de video se ejecutan en su navegador: no están expuestos en la API pública.

## Todos los módulos

[Lista de módulos](../../../03-modules/es/README.md)
