# n8n Local Projects

Este repositorio contiene la configuración completa para desplegar un entorno de **n8n** localmente utilizando Docker, así como las distintas automatizaciones y flujos (workflows) creados para funcionar en este entorno.

## Estructura del Proyecto

* **`n8n-local-docker/`**: Contiene la configuración de infraestructura (Docker Compose) para levantar la instancia de n8n conectada a una base de datos PostgreSQL local.
* **`autoInvoice/`**: Contiene el flujo de trabajo para el procesamiento automático de facturas con Inteligencia Artificial.

## ¿Cómo correr el proyecto localmente?

Para ejecutar tu propia instancia de n8n con esta configuración, sigue estos pasos:

### 1. Configurar Variables de Entorno
Dirígete a la carpeta de la infraestructura y crea tu archivo de entorno:

```bash
cd n8n-local-docker
cp .env.example .env
```

Abre el archivo `.env` recién creado y completa todas las variables de configuración. Esto incluye los puertos, credenciales de la base de datos y cualquier clave de API de terceros que utilicen tus flujos (ej. Google Gemini API, IDs de Google Drive y Sheets).

### 2. Levantar los Contenedores
Asegúrate de tener Docker instalado en tu máquina. Luego, dentro de la misma carpeta `n8n-local-docker`, ejecuta:

```bash
docker compose up -d
```

Este comando descargará las imágenes necesarias e iniciará la base de datos de Postgres junto con tu servidor de n8n en segundo plano.

### 3. Acceder a n8n
Una vez que los contenedores estén corriendo, abre tu navegador y dirígete a:
**[http://localhost:5678](http://localhost:5678)**

Si es tu primera vez ejecutándolo, n8n te pedirá crear una cuenta de administrador local. A partir de allí, podrás comenzar a importar los flujos de trabajo (como `autoInvoice`).

---
> **Nota:** Para detener los contenedores, puedes usar el comando `docker compose down` dentro de la carpeta `n8n-local-docker`.