# Conciliador Financiero - n8n + PostgreSQL

Este proyecto despliega un ecosistema completo de automatización con:
- 🤖 **n8n**: Plataforma de automatización de flujos de trabajo
- 🗄️ **PostgreSQL**: Base de datos compartida

Siguiendo las [recomendaciones oficiales de n8n](https://docs.n8n.io/).

---

## 🚀 Inicio Rápido

¿Primera vez aquí? Lee la **[📘 Guía Rápida (QUICKSTART.md)](QUICKSTART.md)** para levantar n8n y PostgreSQL.

---

## 📋 Arquitectura del Sistema

```
┌─────────────────────────────────────────────────┐
│           conciliador-network (Docker)          │
│                                                 │
│  ┌──────────┐    ┌──────────┐               │
│  │   n8n    │◄───┤PostgreSQL│               │
│  │  :5678   │    │   :5432  │               │
│  └─────▲────┘    └──────────┘               │
│        │                                   │
└────────┼───────────────────────────────────┘
      │
    ┌────▼────┐
    │ Usuario │
    └─────────┘
```

## Versiones

- **n8n stable**: 2.6.3
- **PostgreSQL**: 16-alpine

- [Docker](https://docs.docker.com/get-docker/) (v20.10 o superior)
- [Docker Compose](https://docs.docker.com/compose/install/) (v2.0 o superior)

## 📋 Estructura del Proyecto

```
.
├── docker-compose.yml       # Configuración de servicios Docker
├── .env.example             # Template de variables de entorno
├── .env                     # Variables de entorno (crear manualmente)
├── n8n_data/               # Datos persistentes de n8n
├── postgres_data/          # Datos de PostgreSQL
```

## ⚙️ Configuración Inicial

### 1. Clonar el repositorio

```bash
git clone <url-del-repositorio>
cd solid-octo-happiness
```

### 2. Crear archivo de variables de entorno

Copia el archivo de ejemplo y personaliza las credenciales:

```bash
cp .env.example .env
```

Edita el archivo `.env` con tus credenciales:

```bash
# PostgreSQL
POSTGRES_USER=n8n_user
POSTGRES_PASSWORD=tu_password_segura_aqui
POSTGRES_DB=n8n_db
POSTGRES_SCHEMA=public

# Timezone
GENERIC_TIMEZONE=America/Caracas
TZ=America/Caracas

# n8n Encryption Key
N8N_ENCRYPTION_KEY=tu_clave_generada

```

**Generar credenciales seguras**:

```bash
# n8n encryption key
openssl rand -base64 32

```

### 3. Levantar los servicios

Ejecuta el siguiente comando para iniciar los contenedores en segundo plano:

```bash
docker-compose up -d
```

### 4. Verificar el estado de los servicios

```bash
docker-compose ps
```

## 🌐 Acceso a los Servicios

Una vez que los servicios estén corriendo:

| Servicio | URL | Descripción |
|----------|-----|-------------|
| **n8n** | http://localhost:5678 | Panel de automatización |
| **PostgreSQL** | localhost:5432 | Base de datos (interno) |

**Primera vez en n8n**: Se te pedirá crear una cuenta de administrador.

## 📊 Comandos Útiles

### Ver logs de los servicios
```bash
docker-compose logs -f
```

### Ver logs solo de n8n
```bash
docker-compose logs -f n8n
```

### Detener los servicios
```bash
docker-compose down
```

### Detener y eliminar volúmenes (⚠️ elimina todos los datos)
```bash
docker-compose down -v
```

### Reiniciar los servicios
```bash
docker-compose restart
```
### Actualizar n8n a la última versión
```bash
# Descargar la última imagen
docker-compose pull

# Detener y recrear los contenedores
docker-compose down
docker-compose up -d
```

### Usar una versión específica de n8n
Edita el `docker-compose.yml` y cambia la imagen:
```yaml
image: docker.n8n.io/n8nio/n8n:1.81.0  # versión específica
# o
image: docker.n8n.io/n8nio/n8n:next    # versión beta
```

## 🔒 Seguridad

- ✅ El archivo `.env` está excluido del control de versiones (`.gitignore`)
- ✅ Usa contraseñas seguras para PostgreSQL
- ✅ Genera una clave de encriptación única para N8N_ENCRYPTION_KEY
- ✅ En producción, considera usar secretos de Docker o servicios de gestión de secretos

## 🛠️ Solución de Problemas

### La base de datos no está lista
Si n8n no puede conectarse a PostgreSQL, espera unos segundos. El healthcheck asegura que PostgreSQL esté listo antes de iniciar n8n.

### Ver el estado del healthcheck
```bash
docker inspect --format='{{json .State.Health}}' <container_id>
```

### Reiniciar desde cero
```bash
docker-compose down
rm -rf n8n_data postgres_data
docker-compose up -d
```

## � Importante para Producción

⚠️ **No uses n8n con túnel (`--tunnel`) en producción**. El túnel es solo para desarrollo y pruebas locales.

Para producción, considera:
- Configurar un reverse proxy (Nginx, Traefik)
- Usar certificados SSL/TLS
- Configurar variables de entorno adicionales de seguridad
- Implementar respaldos automáticos de la base de datos

## 📚 Recursos Adicionales

- [Documentación oficial de n8n](https://docs.n8n.io/)
- [Guía de instalación con Docker](https://docs.n8n.io/hosting/installation/docker/)
- [n8n Community](https://community.n8n.io/)
- [Configuraciones de n8n-hosting](https://github.com/n8n-io/n8n-hosting)
- [PostgreSQL Docker Hub](https://hub.docker.com/_/postgres)
- [Timezones disponibles](https://momentjs.com/timezone/)

## 📝 Licencia

Este proyecto es de código abierto y está disponible bajo los términos especificados en el repositorio.