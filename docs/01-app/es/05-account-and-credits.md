# Cuenta y créditos

Qué cambia con una cuenta, cómo funcionan los créditos y los planes, y dónde se configura su espacio de trabajo.

No necesita una cuenta para usar los módulos locales. Sí la necesita para los **módulos de IA**, que consumen **créditos**, y para aprovechar los límites de su plan.

## Los planes

| Plan | Para quién |
| --- | --- |
| Gratis | Todas las herramientas ligeras y 30 créditos gratuitos cada mes, sin tarjeta bancaria. |
| Básico | Exportaciones sin publicidad ni espera, en 4K, los módulos de IA de video y las claves de API. |
| Pro | Exportaciones ilimitadas, todos los módulos de IA y la cola de procesamiento prioritaria. |
| Empresa | Un plan a medida, con acompañamiento dedicado. |

Las cuotas exactas (exportaciones por día, resolución, tamaño de un archivo importado, archivos por lote, cálculos de IA por día) se comparan en la página [Precios](https://pixlub.com/es/plans). Las suscripciones son sin permanencia.

## Los créditos

- Un **módulo de IA** cuesta créditos en cada cálculo: su precio se muestra antes de iniciar, y nada se envía sin su confirmación.
- Algunos módulos se facturan **por archivo**, otros **por minuto** (transcripción) o **por operación**.
- Un cálculo que falla por nuestra parte se **reembolsa** automáticamente.
- Cada cargo se muestra en pantalla, y una notificación le avisa a medida que se agotan sus créditos del mes.
- Los **paquetes de créditos** se compran además de la suscripción y no caducan.

Los mismos créditos sirven para la [API](../../02-api/es/04-credits.md).

## La configuración

La página [Configuración](https://pixlub.com/es/settings) reúne tres apartados:

| Apartado | Contenido |
| --- | --- |
| Cuenta | Perfil, preferencias, seguridad. |
| Pagos | Medios de pago, gestión del plan, historial de pagos, créditos. |
| Espacio de trabajo | Carpeta local y la sección **Desarrollador** para las claves de API. |

## Carpeta local

En **Espacio de trabajo**, elija una carpeta de su equipo. Pixlub puede entonces:

- **guardar automáticamente** allí sus proyectos del [grafo de imagen](./02-image/01-image-graph.md);
- **guardar allí sus exportaciones** con el botón dedicado (el botón **Exportar** siempre descarga);
- enumerar sus proyectos al abrir el grafo.

> [!NOTE]
> **Permiso del navegador**
>
> El navegador solo indica el nombre de la carpeta elegida, nunca su ruta completa, y puede volver a pedir permiso para acceder a ella en una nueva visita. Esta función se basa en la API File System Access, disponible en Chrome, Edge y los navegadores Chromium.
