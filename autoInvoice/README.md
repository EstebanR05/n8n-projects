# AutoInvoice Workflow

**AutoInvoice** es un flujo de automatización diseñado para n8n que se encarga de procesar imágenes de facturas, extraer la información clave de manera dinámica utilizando Inteligencia Artificial (Google Gemini) y sincronizar los datos estructurados directamente en **Google Sheets**, guardando también una copia de la imagen original en **Google Drive**.

## Requisitos Previos: Variables de Entorno

Este flujo ha sido diseñado para ser **100% dinámico y portátil**. Esto significa que no tiene identificadores ni claves "quemadas" (hardcoded) en el código. Para que funcione correctamente, la instancia de n8n donde lo importes **debe** tener configuradas las siguientes variables de entorno:

* `G_API_KEY`: Tu clave de API para Google Gemini (Generative Language).
* `GFOLTER_DRIVE_URL`: La URL pública o ID de la carpeta de Google Drive donde se guardarán los archivos.
* `GSHEETS_DOCUMENT_ID`: El ID del documento de Google Sheets.
* `GSHEETS_DOCUMENT_NAME`: El nombre visual del documento de Sheets (para mantener la caché de la interfaz).

*(Si estás corriendo n8n usando la carpeta `n8n-local-docker` de este repositorio, estas variables se inyectan automáticamente desde tu archivo `.env`).*

Además, requerirás tener dadas de alta las credenciales OAuth2 de Google Drive y Google Sheets dentro de las opciones de conexión (Credentials) de n8n.

## ¿Cómo publicar / importar el flujo en n8n?

Sigue estos pasos para cargar y activar este flujo de trabajo en tu entorno de n8n:

1. Ingresa a la interfaz web de tu instancia de n8n (generalmente `http://localhost:5678`).
2. En el panel izquierdo, haz clic en **Workflows** y luego en **Add Workflow**.
3. En la esquina superior derecha, abre el menú de opciones (los tres puntos `...`) y selecciona **Import from File**.
4. Busca y selecciona el archivo `.json` de este directorio (ej. `invoices.json` o `autoInvoice.json`).
5. El flujo se cargará visualmente en el lienzo. 
6. **Revisar credenciales:** Es posible que n8n te advierta que los nodos de Google Drive o Google Sheets no tienen credenciales seleccionadas. Haz doble clic en ellos y, en el apartado "Credential for...", selecciona las tuyas.
7. Una vez que no haya errores visuales, enciende el botón superior derecho a **Active** para habilitar el webhook de recepción.

¡Y listo! Ya puedes enviar peticiones `POST` (multipart/form-data con la imagen) a la ruta del Webhook para que el flujo procese tus facturas automáticamente.
