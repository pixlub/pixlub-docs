# Conversor de imágenes

Cambiar el formato de una o varias imágenes: formatos disponibles, ajustes, procesamiento local o en servidor.

El [conversor de imágenes](https://pixlub.com/es/image/convert) cambia el formato de sus archivos sin instalar nada. Cada formato de salida también tiene su propia página, por ejemplo [convertir a WebP](https://pixlub.com/es/image/convert/webp), que abre la herramienta con ese formato ya elegido.

## Convertir

1. **Soltar sus archivos**

   Arrastre una o varias imágenes a la zona de carga, o haga clic en **Elegir**. JPG, PNG, WebP, HEIC, GIF… e incluso videos, de los que se extrae la imagen.

2. **Elegir el formato**

   Los formatos van del más común al más especializado. Los ajustes se adaptan al formato: **calidad** para los formatos comprimidos, **escala**, y **fondo** para los formatos sin transparencia.

3. **Descargar**

   Descargue los archivos uno a uno, o todo el lote en un archivo ZIP.

## Local o en servidor

| Formato | Procesamiento |
| --- | --- |
| PNG, JPG, WebP | Codificados por su navegador: sus imágenes no salen de su dispositivo. |
| AVIF, JPEG XL, HEIC, TIFF, ICO, PDF… | Codificados por nuestra API: la insignia cambia a **Enviado al servidor** en cuanto se elige el formato. |

La página de cada formato indica dónde se codifica («En su navegador» o «Mediante nuestra API»), si conserva la transparencia y si su compresión es ajustable.

> [!TIP]
> **Transparencia**
>
> Un formato sin canal alfa (JPG, BMP…) aplana la imagen sobre el color de **fondo** elegido. Use PNG, WebP o AVIF para conservar la transparencia.

## Mediante la API

El mismo conversor es el módulo [`convert`](../../../03-modules/es/12-conversion/convert/api.md) de la API: un archivo en el campo `in` y el formato en `params`.
