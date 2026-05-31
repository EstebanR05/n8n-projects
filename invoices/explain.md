# AutoInvoice: Digitalización Inteligente de Facturas

**AutoInvoice** es un producto de software diseñado para transformar, automatizar y simplificar el procesamiento de documentos financieros utilizando orquestación de flujos e Inteligencia Artificial.

---

## 1. El Producto y su Objetivo

* **El Problema:** La transcripción manual de facturas es una de las tareas más repetitivas, lentas y propensas a errores humanos dentro de los departamentos administrativos y contables. Extraer datos de imágenes (fotos o escaneos) y pasarlos a una hoja de cálculo consume un tiempo valioso.
* **La Solución:** AutoInvoice recibe una imagen en formato crudo (PNG, JPG) de cualquier factura, la analiza mediante IA y devuelve un documento de Excel estructurado, recreando el diseño original de la factura para su lectura inmediata.
* **Objetivo Principal:** Eliminar el trabajo manual de "data entry", reduciendo los tiempos de procesamiento de minutos a segundos por factura, garantizando alta fidelidad en los datos extraídos.

---

## 2. Público Objetivo

Este producto está diseñado para cualquier entidad o individuo que procese volúmenes de comprobantes de pago:
* **Departamentos de Contabilidad y Finanzas:** Para agilizar el cuadre de gastos mensuales e impuestos.
* **Pequeñas y Medianas Empresas (PyMEs):** Que no cuentan con costosos softwares ERP y manejan su administración mediante hojas de cálculo.
* **Trabajadores Autónomos / Freelancers:** Que necesitan digitalizar sus recibos físicos rápidamente para la declaración de renta.

---

## 3. Arquitectura y Tecnologías Utilizadas

El producto fue construido integrando los siguientes componentes tecnológicos, formando una arquitectura moderna y modular:

* **n8n (Motor de Orquestación):** Es el "cerebro" del producto. Se encarga de enlazar los distintos servicios, recibir la imagen, controlar la lógica de procesamiento (el "dibujado" del Excel mediante JavaScript) y manejar el flujo de los datos desde el origen hasta el destino final.
* **Google Gemini 2.5 Flash (IA & OCR Avanzado):** A diferencia de un OCR tradicional que solo extrae texto plano, Gemini actúa como el "ojo inteligente". Analiza la factura, comprende su contexto semántico (qué es un total, qué es un IVA, cuáles son los productos) sin importar el diseño o proveedor de la factura.
* **Ecosistema Google Workspace (Drive & Sheets API):** 
  * *Drive:* Actúa como repositorio documental, guardando la imagen original como respaldo (Storage).
  * *Sheets:* Actúa como base de datos y capa de visualización, donde se construyen los reportes financieros en tiempo real.

---

## 4. ¿Cómo Funciona? (Paso a Paso)

El flujo de procesamiento desde la perspectiva del sistema se divide en 4 pasos concretos:

1. **Recepción del Documento:** El usuario envía la imagen de la factura al sistema (vía Webhook/Integración). El sistema valida el formato de la imagen y la prepara para su procesamiento.
2. **Respaldo Automático:** El archivo físico se envía a Google Drive, generando un respaldo seguro en la nube.
3. **Análisis Dinámico (IA):** La imagen se envía a la API de Gemini. Aquí ocurre la magia: la IA no busca campos en posiciones fijas; identifica de forma **dinámica** todo el encabezado (emisor, cliente, fechas), las columnas de los productos y la sección de totales, devolviendo un objeto de datos estructurado (JSON).
4. **Formateo y Renderizado (Google Sheets):** 
   * n8n toma los datos dinámicos y ejecuta un script para transformarlos en una matriz visual.
   * Se invoca a la API de Google Sheets para crear **una pestaña (hoja) nueva** bautizada con el nombre del archivo.
   * Se inyectan los datos dibujando literalmente la factura en la hoja de cálculo (encabezados, tabla de productos, y totales alineados).

---

## 5. Valor Agregado e Innovación

* **100% Agnosticidad de Formato:** A diferencia de sistemas legados que requieren mapear una plantilla (template) por cada proveedor distinto, AutoInvoice se adapta a *cualquier* factura nueva que se le presente gracias a la capacidad deductiva de Gemini.
* **Recreación Visual:** No entrega una base de datos plana e incomprensible, sino un documento perfectamente formateado y legible para un humano, listo para ser auditado o enviado a un cliente.
