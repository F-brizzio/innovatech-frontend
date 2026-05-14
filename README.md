# 🚀 Innovatech Frontend — React + Vite

Aplicación web de gestión de despachos para **Innovatech Chile**, desarrollada con React y Vite, contenedorizada con Docker y desplegada en AWS EC2.

## 🛠️ Tecnologías
- React 18 + Vite
- Tailwind CSS
- Nginx Alpine (producción)
- Docker multi-stage build

## 📋 Requisitos
- Docker Desktop instalado
- Node.js 20+ (solo desarrollo local)

## 🐳 Ejecutar con Docker

### Build de la imagen
```bash
docker build -t innovatech-frontend .
```

### Correr el contenedor
```bash
docker run -d -p 80:80 --name innovatech-frontend innovatech-frontend
```

### Acceder
http://localhost
## 🔧 Ejecutar con Docker Compose
Desde la carpeta raíz del proyecto completo:
```bash
docker-compose up -d
```

## 📦 Estructura del Dockerfile
El Dockerfile usa **multi-stage build**:
- **Stage 1 (builder):** Node.js 20 Alpine — instala dependencias y genera el build de producción
- **Stage 2 (production):** Nginx Alpine — sirve los archivos estáticos generados

Buenas prácticas aplicadas:
- ✅ Multi-stage build (imagen final liviana)
- ✅ Usuario no root
- ✅ Cache de dependencias optimizado

## 🔄 Pipeline CI/CD
El pipeline se activa automáticamente con cada push a la rama `deploy`:
1. Construye la imagen Docker
2. Publica en Docker Hub (`lucianodelgado/innovatech-frontend`)
3. Despliega en EC2 vía SSH

### Secrets requeridos en GitHub
| Secret | Descripción |
|--------|-------------|
| `DOCKER_USERNAME` | Usuario Docker Hub |
| `DOCKER_TOKEN` | Token Docker Hub |
| `EC2_FRONTEND_HOST` | IP pública EC2 Frontend |
| `EC2_SSH_KEY` | Clave privada SSH (.pem) |

## ☁️ Despliegue en AWS
- **Instancia:** EC2 Ubuntu 24.04 LTS (t2.micro)
- **IP:** 3.227.60.83
- **Puerto:** 80 (HTTP)
- **Acceso:** http://3.227.60.83