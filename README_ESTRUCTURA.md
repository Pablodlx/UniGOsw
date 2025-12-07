# UniGO - Plataforma de Carsharing Universitario

## Estructura de Directorios

```
UniGOsw/
├── src/
│   ├── backend/       # Backend Node.js + Express + Socket.IO
│   ├── frontend/      # Frontend Next.js + React
│   └── infra/         # Infraestructura Docker (PostgreSQL, etc.)
├── docs/              # Documentación del proyecto
├── Makefile           # Comandos para gestionar el proyecto
└── README_ESTRUCTURA.md
```

## Componentes del Sistema

### Backend (`src/backend/`)
- **Framework**: Node.js con Express
- **Base de datos**: PostgreSQL con Sequelize ORM
- **WebSocket**: Socket.IO para comunicación en tiempo real
- **Puerto**: 8000
- **Características Principales**:
  - ✅ Autenticación JWT con verificación de email
  - ✅ API RESTful completa
  - ✅ WebSocket para chat grupal en tiempo real
  - ✅ Integración con Stripe Payment + Connect
  - ✅ Sistema de reservas con estados (PENDING, ACCEPTED, REJECTED, CANCELLED)
  - ✅ Sistema de calificaciones entre usuarios
  - ✅ Gestión de perfiles con avatares
  - ✅ Sistema de cancelación con reembolsos automáticos
  - ✅ Transferencias automáticas a conductores vía Stripe Connect
  - ✅ Gestión de asientos en tiempo real
  - ✅ Historial de viajes completados

### Frontend (`src/frontend/`)
- **Framework**: Next.js 15 con TypeScript
- **UI**: React + Tailwind CSS
- **Mapas**: Google Maps API
- **Puerto**: 3001
- **Características Principales**:
  - ✅ Búsqueda de viajes con geolocalización
  - ✅ Sistema de reservas con pago integrado
  - ✅ Chat grupal en tiempo real por viaje
  - ✅ Gestión de perfil con avatar
  - ✅ Panel de conductor y pasajero
  - ✅ Sistema de calificaciones
  - ✅ Cancelación con cálculo automático de reembolso
  - ✅ Vista de pasajeros para conductores
  - ✅ Gestión de solicitudes pendientes
  - ✅ Registro de viajes completados

### Infraestructura (`src/infra/`)
- **PostgreSQL**: Base de datos principal (puerto 5432)
- **MailHog**: Servidor de email para desarrollo (puerto 8025)
- **Prometheus**: Monitoreo (puerto 9090)
- **Grafana**: Visualización de métricas (puerto 3000)
- **pgAdmin**: Administración de PostgreSQL (puerto 5050)

## Comandos Make

### Infraestructura
```bash
make infra-up      # Levantar servicios Docker
make infra-down    # Detener y eliminar servicios
make infra-logs    # Ver logs de contenedores
```

### Backend
```bash
make backend-setup    # Instalar dependencias
make backend          # Ejecutar en modo desarrollo
make backend-start    # Setup completo + migración + ejecución
make migrate          # Ejecutar migraciones
make backend-test     # Probar conexión del backend
```

### Frontend
```bash
make frontend-setup   # Instalar dependencias
make frontend         # Ejecutar en modo desarrollo
```

### Comandos combinados
```bash
make dev             # Levantar todo (infra + backend + frontend)
make start-all       # Alias de dev
make urls            # Mostrar URLs de todos los servicios
```

## URLs de Servicios

- **Backend API**: http://127.0.0.1:8000
  - Health: http://127.0.0.1:8000/health
  - Metrics: http://127.0.0.1:8000/metrics
- **Frontend**: http://127.0.0.1:3001
- **MailHog UI**: http://127.0.0.1:8025
- **Prometheus**: http://127.0.0.1:9090
- **Grafana**: http://127.0.0.1:3000

## Variables de Entorno

### Backend (`src/backend/.env`)
```env
# Base de datos
DATABASE_URL=postgresql://unigo:unigo@localhost:5432/unigo

# Autenticación
JWT_SECRET=your_jwt_secret
SECRET_KEY=your_secret_key

# Stripe (Pagos y Connect)
STRIPE_SECRET_KEY=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...

# Email (opcional para desarrollo)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_app_password

# Entorno
NODE_ENV=development
PORT=8000
```

### Frontend (`src/frontend/.env.local`)
```env
# API Backend
NEXT_PUBLIC_API_BASE=http://localhost:8000/api
NEXT_PUBLIC_API_URL=http://localhost:8000

# WebSocket
NEXT_PUBLIC_WS_URL=http://localhost:8000

# Google Maps
NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=your_google_maps_key

# Stripe
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...
```

## Comandos Disponibles (Makefile)

**Todos los comandos se ejecutan desde la raíz del proyecto (`/home/pablodlx/UniGOsw/`)**

### Infraestructura
- `make infra-up` - Iniciar contenedores Docker (PostgreSQL, MailHog, Prometheus, Grafana, pgAdmin)
- `make infra-down` - Detener contenedores Docker
- `make infra-restart` - Reiniciar contenedores Docker

### Backend
- `make backend-install` - Instalar dependencias npm del backend
- `make backend-dev` - Iniciar backend en modo desarrollo (puerto 8000)
- `make backend-logs` - Ver logs del backend

### Frontend
- `make frontend-install` - Instalar dependencias npm del frontend
- `make frontend-dev` - Iniciar frontend Next.js en desarrollo (puerto 3001)
- `make frontend-build` - Construir aplicación para producción
- `make frontend-start` - Iniciar aplicación en modo producción

### Base de Datos
- `make db-migrate` - Ejecutar migraciones Sequelize
- `make db-seed` - Ejecutar seeders (datos de prueba)
- `make db-reset` - Resetear base de datos completa

### Utilidades
- `make clean` - Limpiar node_modules, builds y archivos temporales
- `make dev` - Iniciar todo junto (infra + backend + frontend)
- `make logs` - Ver logs de todos los servicios

## Flujo de Desarrollo Rápido

```bash
# Primera vez
make infra-up
make backend-install
make frontend-install
make db-migrate

# Día a día
make dev  # Inicia todo junto

# O por separado
make infra-up
make backend-dev  # Terminal 1
make frontend-dev # Terminal 2
```

## Notas Técnicas Importantes

### 🚫 Eliminado del Proyecto
- **Sistema de Notificaciones**: Completamente removido (frontend + backend)
- **Alertas de Búsqueda**: Funcionalidad "Mis Alertas" eliminada
- **Backend Python**: Migrado completamente a Node.js + Express
- **Carpetas obsoletas**: `backend-node/` y `frontend/` raíz (pueden eliminarse)

### ✅ Características Implementadas
- **Stripe Connect**: Pagos automáticos a conductores mediante `transfer_data`
- **Chat en Tiempo Real**: WebSocket (Socket.IO) + HTTP fallback para grupos de viaje
- **Sistema de Reembolsos**: 
  - Cancelación ≥24h antes: Reembolso 100%
  - Cancelación <24h antes: Reembolso 70% (30% penalización)
  - Tarifas de Stripe deducidas automáticamente
- **Gestión de Asientos**: Actualización en tiempo real (total_seats/booked_seats)
- **Google Maps**: Visualización de rutas y cálculo de distancias
- **Autenticación JWT**: Con verificación de email
- **Roles**: Conductor, Pasajero, Ambos (dual role)

### 🔧 Stack Técnico
- **Backend**: Node.js 18+ / Express 4.x / Sequelize ORM / Socket.IO
- **Frontend**: Next.js 15 / React 19 / TypeScript 5 / Tailwind CSS
- **Database**: PostgreSQL 15
- **Payments**: Stripe Payment Intents + Connect
- **Real-time**: WebSocket (Socket.IO) con fallback HTTP
- **Infrastructure**: Docker Compose
- **Auth**: JWT tokens + bcrypt

### 📡 Puertos de Servicio
- Backend API: `http://localhost:8000`
- Frontend: `http://localhost:3001`
- PostgreSQL: `localhost:5432`
- MailHog UI: `http://localhost:8025`
- Prometheus: `http://localhost:9090`
- Grafana: `http://localhost:3000`
- pgAdmin: `http://localhost:5050`
