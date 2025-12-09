# UniGO - Sistema de Carpooling Universitario

Sistema completo de carpooling para estudiantes universitarios con backend Node.js + Express + Sequelize y frontend React + Next.js.

## 📋 Requisitos Previos

- Node.js 18+ y npm
- PostgreSQL 14+
- Docker y Docker Compose (para infraestructura)
- Git

## 🚀 Quick Start (Para Nuevos Desarrolladores)

### 1. Clonar el Repositorio

```bash
git clone <repository-url>
cd UniGOsw
```

### 2. Levantar Infraestructura

```bash
make infra-up
```

Esto iniciará:
- PostgreSQL (puerto 5432)
- Redis (puerto 6379)
- MailHog (puerto 8025)
- Prometheus (puerto 9090)
- Grafana (puerto 3000)
- PgAdmin (puerto 5050)

### 3. Configurar Backend

```bash
# Instalar dependencias
cd src/backend
npm install

# Copiar variables de entorno
cp .env.example .env

# Editar .env con tus credenciales
```

### 4. Ejecutar Migraciones de Base de Datos

**⚠️ CRÍTICO: Este paso es OBLIGATORIO para nuevos desarrolladores**

```bash
# Desde la raíz del proyecto
make migrate
```

Esto creará todas las tablas necesarias:
- `users` - Usuarios y perfiles
- `email_codes` - Códigos de verificación
- `rides` - Viajes publicados
- `bookings` - Reservas de pasajeros
- `messages` - Mensajes directos
- `payments` - Pagos y transferencias
- `ratings` - Valoraciones
- `trip_group_messages` - Chats grupales de viajes

Ver documentación completa en: [src/backend/MIGRATIONS.md](src/backend/MIGRATIONS.md)

### 5. Iniciar Backend

```bash
# Opción 1: Desde raíz con Make
make backend

# Opción 2: Directamente
cd src/backend
npm run dev
```

Backend disponible en: http://127.0.0.1:8000

### 6. Iniciar Frontend

```bash
# Opción 1: Desde raíz con Make
make frontend

# Opción 2: Directamente
cd src/frontend
npm install
npm run dev
```

Frontend disponible en: http://127.0.0.1:3001

## 🔧 Comandos Make Disponibles

### Infraestructura
```bash
make infra-up        # Levantar servicios Docker
make infra-down      # Detener servicios (borra datos)
make infra-logs      # Ver logs de servicios
```

### Backend
```bash
make backend-setup   # Instalar dependencias
make backend         # Iniciar en desarrollo
make backend-test    # Verificar health check
make migrate         # Ejecutar migraciones pendientes
make migrate-undo    # Revertir última migración
make migrate-create  # Crear nueva migración
```

### Frontend
```bash
make frontend-setup  # Instalar dependencias
make frontend        # Iniciar en desarrollo
```

### Desarrollo Completo
```bash
make dev             # Infraestructura + Backend + Frontend
make urls            # Ver todas las URLs disponibles
```

## 🗄️ Sistema de Migraciones

Este proyecto usa **Sequelize CLI** para control de versiones de la base de datos.

### ¿Por qué usar migraciones?

- ✅ Control de versiones del esquema de base de datos
- ✅ Sincronización entre desarrolladores del equipo
- ✅ Rollback seguro en caso de errores
- ✅ Historial completo de cambios de esquema
- ✅ Deployment predecible a producción

### Comandos de Migraciones

```bash
# Ejecutar todas las migraciones pendientes
make migrate

# Revertir la última migración
make migrate-undo

# Crear una nueva migración
make migrate-create
# (Te pedirá el nombre, ej: "add-user-preferences")

# Ver estado de migraciones (desde backend/)
npx sequelize-cli db:migrate:status
```

### Primera Vez Configurando el Proyecto

Si clonas el repositorio por primera vez:

1. **Levantar infraestructura**: `make infra-up`
2. **Instalar dependencias**: `cd src/backend && npm install`
3. **Configurar .env**: Copiar y editar `.env.example`
4. **🔴 EJECUTAR MIGRACIONES**: `make migrate` (OBLIGATORIO)
5. **Iniciar backend**: `make backend`

### Troubleshooting Migraciones

**Error: "relation X does not exist"**
```bash
# La base de datos está vacía, ejecutar migraciones
make migrate
```

**Error: "relation X already exists"**
```bash
# Tablas creadas manualmente, eliminar esquema y migrar
# CUIDADO: Esto borra todos los datos
cd src/backend
PGPASSWORD=unigo psql -h localhost -U unigo -d unigo -c "DROP SCHEMA public CASCADE; CREATE SCHEMA public;"
make migrate
```

**Error: "SequelizeMeta doesn't exist"**
```bash
# Primera ejecución, completamente normal
make migrate
```

## 🌐 URLs del Proyecto

| Servicio | URL | Descripción |
|----------|-----|-------------|
| Backend | http://127.0.0.1:8000 | API REST + WebSockets |
| Health Check | http://127.0.0.1:8000/health | Estado del backend |
| Metrics | http://127.0.0.1:8000/metrics | Prometheus metrics |
| Frontend | http://127.0.0.1:3001 | Interfaz web React |
| MailHog | http://127.0.0.1:8025 | Email testing |
| Prometheus | http://127.0.0.1:9090 | Métricas |
| Grafana | http://127.0.0.1:3000 | Dashboards |
| PgAdmin | http://127.0.0.1:5050 | Admin PostgreSQL |

## 📁 Estructura del Proyecto

```
UniGOsw/
├── src/
│   ├── backend/          # API Node.js + Express + Sequelize
│   │   ├── app/          # Código de aplicación
│   │   ├── config/       # Configuraciones (DB, etc)
│   │   ├── src/database/ # Migraciones y seeders
│   │   ├── .sequelizerc  # Config de Sequelize CLI
│   │   ├── MIGRATIONS.md # Documentación de migraciones
│   │   └── package.json
│   │
│   ├── frontend/         # React + Next.js 15
│   │   ├── src/          # Código fuente
│   │   └── package.json
│   │
│   └── infra/            # Docker compose
│       └── docker-compose.yml
│
├── Makefile              # Comandos de desarrollo
└── README.md             # Este archivo
```

## 🔐 Variables de Entorno

Archivo `.env` en `src/backend/`:

```env
# Base de datos
DATABASE_URL=postgresql://unigo:unigo@localhost:5432/unigo

# JWT
JWT_SECRET=tu-secreto-aqui

# Stripe
STRIPE_SECRET_KEY=sk_test_...
STRIPE_PUBLISHABLE_KEY=pk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...

# Email (MailHog en desarrollo)
SMTP_HOST=localhost
SMTP_PORT=1025
SMTP_USER=
SMTP_PASS=
```

## 🧪 Testing

```bash
# Backend tests
make test

# Health check
make backend-test
curl http://127.0.0.1:8000/health
```

## 📚 Documentación Adicional

- [MIGRATIONS.md](src/backend/MIGRATIONS.md) - Sistema de migraciones completo
- [README_ESTRUCTURA.md](README_ESTRUCTURA.md) - Estructura detallada
- [GUIA_IMPLEMENTACION_STRIPE.md](GUIA_IMPLEMENTACION_STRIPE.md) - Integración de pagos
- [frontend/SETUP_INSTRUCTIONS.md](src/frontend/SETUP_INSTRUCTIONS.md) - Setup de frontend

## 🐛 Problemas Comunes

### Backend no inicia
```bash
# Verificar que PostgreSQL esté corriendo
make infra-up

# Verificar migraciones ejecutadas
cd src/backend
npx sequelize-cli db:migrate:status
```

### Frontend no compila
```bash
# Limpiar y reinstalar
cd src/frontend
rm -rf .next node_modules
npm install
```

### Errores de base de datos
```bash
# Recrear base de datos desde cero (CUIDADO: borra datos)
make infra-down
make infra-up
make migrate
```

## 👥 Equipo de Desarrollo

Para colaborar en el proyecto:

1. Clonar el repositorio
2. Crear rama feature: `git checkout -b feature/mi-feature`
3. **Ejecutar migraciones**: `make migrate`
4. Desarrollar y commitear
5. Crear Pull Request

## 📝 Licencia

[Especificar licencia]

---

**¿Problemas con las migraciones?** Ver [MIGRATIONS.md](src/backend/MIGRATIONS.md) para guía completa.
