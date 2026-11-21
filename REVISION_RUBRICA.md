# Proyecto personal PWA — Miguel Angel Chipana Choque

## Actualización según la rúbrica de Diseño Web II

Se conservaron los archivos y recursos originales. Se añadieron mejoras sin eliminar las secciones existentes.

### Cambios realizados
- **PWA y despliegue:** se mantiene `manifest.json` y `sw.js`; se incrementó la versión de caché y se agregó `perfil.json` a los recursos precargados.
- **Carga asíncrona:** `app.js` obtiene los datos del encabezado desde `perfil.json` mediante `fetch()`. Si el JSON no está disponible, conserva el contenido de respaldo del HTML.
- **Rendimiento:** las imágenes de contenido usan `loading="lazy"` y `decoding="async"`; el avatar visible al inicio conserva prioridad alta.
- **Eventos:** se conserva la delegación de eventos con jQuery y la limpieza previa mediante `.off(".app")` para evitar listeners duplicados.
- **Seguridad DOM:** los datos del perfil se insertan con `.text()` y no como HTML; las vistas dinámicas existentes escapan el contenido antes de construir HTML; el formulario valida los campos y limita la longitud de entradas.
- **Responsividad:** se añadieron reglas para móviles compactos (hasta 390 px), tablets y orientación horizontal; se incluyeron tamaños táctiles y alternativas `vh` para navegadores que no soportan `dvh`.

## Archivos importantes
- `index.html`: página personal.
- `styles.css`: diseño adaptable.
- `app.js`: lógica, eventos, carga dinámica y validaciones.
- `manifest.json`: configuración instalable PWA.
- `sw.js`: caché y funcionamiento offline.
- `perfil.json`: datos públicos que carga `fetch()`.
- `diagnostico.html` y `diagnostico.css`: módulo de diagnóstico DOM.
- `Horario_Miguel_Angel.xlsx`: plantilla editable de horario.

## Publicación en GitHub Pages
1. Crea o abre el repositorio destinado a la página personal.
2. Sube **el contenido de esta carpeta** directamente a la raíz del repositorio, de modo que `index.html` quede en la raíz publicada.
3. En GitHub entra a **Settings → Pages** y selecciona la rama y la carpeta raíz (`/root`).
4. Espera la publicación y abre la URL HTTPS generada.
5. Comprueba que `index.html`, `perfil.json`, `manifest.json`, `sw.js`, `styles.css`, `app.js` e imágenes respondan sin error 404.
6. Abre una vez con conexión para instalar la caché; luego prueba la navegación sin conexión.

## Comprobaciones recomendadas para la evaluación
- Probar anchos de 360 px, 390 px y 768 px, además de un teléfono en horizontal.
- En DevTools → Application comprobar que el manifiesto y el Service Worker estén registrados.
- En DevTools → Network activar Offline después de la primera carga.
- En Console comprobar que no haya errores JavaScript.
- Enviar el formulario con campos vacíos y con datos válidos para comprobar sus validaciones.

## Alcance de este ZIP
Este archivo contiene el **proyecto personal** y su página de diagnóstico. La rúbrica también menciona un módulo separado de Reservas/Karaoke. Ese segundo proyecto no venía dentro del ZIP recibido, por lo que no se creó ni se simuló: debe entregarse y publicarse como repositorio/carpeta independiente para completar el criterio colectivo de ambos módulos.

**Importante:** el formulario no puede enviar mensajes a un servidor mientras `formEndpoint` siga vacío en `app.js`. En ese estado prepara el correo mediante `mailto:` cuando hay conexión y guarda localmente los mensajes si no hay conexión. Para sincronización real se debe configurar un endpoint HTTPS propio.


## Actualización "Avance Unificado" (Core Web Vitals, Service Worker, BEM y DOMPurify)
- **DOMPurify 3.1.6** (jsDelivr, versión fija) en `index.html` y `diagnostico.html`. Todo HTML dinámico pasa por `limpiarHTML()` / `$.fn.htmlSeguro()`; `renderizarDetalleSeguro()` sanitiza y usa `.html()` sobre `#detalleProyecto`. Si DOMPurify no está disponible, se escapa como texto.
- **BEM:** bloque `tarjeta-ods` con `tarjeta-ods__imagen`, `tarjeta-ods__detalle`, `tarjeta-ods__boton` y `tarjeta-ods__boton--destacado` (modal "Detalle del proyecto"). Se eliminó el `!important` de `.check` (ahora `.campo label.check`). Quedan solo el reset `[hidden]` y `prefers-reduced-motion` (accesibilidad).
- **CLS:** `width`/`height` en imágenes, `aspect-ratio` en `.tarjeta-ods__imagen`, `.img-modal` y `.juego img`.
- **Service Worker:** caché `v8`; DOMPurify se precarga y se sirve desde Cache Storage (caché primero). HTML: red primero con respaldo.
- **Diagnóstico:** nuevas secciones con LCP/CLS en vivo, estado de SW y red, checklist del sábado 21 de noviembre (se guarda en el dispositivo) y auditoría de la página. El analizador detecta imágenes sin dimensiones, `!important` y HTML dinámico sin DOMPurify.
- **Otros:** icono corregido ("MA"), motivo de contacto "Fútbol / Deporte".

## Pendiente fuera de este ZIP
La **Empresa ODS / proyecto grupal** (`proyecto-grupal/`) no venía en el ZIP y no se creó. Debe aplicar el mismo bloque BEM + DOMPurify + `sw.js` y presentarse junto al personal.
