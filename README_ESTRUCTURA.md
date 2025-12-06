# UniGO - Estructura del Proyecto

## Estructura de Directorios

```
UniGOsw/
├── src/
│   ├── backend/       # Backend Node.js + Express
│   ├── frontend/      # Frontend Next.js + React
│   └── infra/         # Infraestructura Docker (PostgreSQL, etc.)
├── Makefile           # Comandos para gestionar el proyecto
└── README.md
```

## Componentes del Sistema

### Backend (`src/backend/`)
- **Framework**: Node.js con Express
- **Base de datos**: PostgreSQL
- **ORM**: Sequelize
- **Puerto**: 8000
- **Características**:
  - Autenticación JWT
  - API RESTful
  - WebSocket para chat en tiempo real
  - Integración con Stripe (pagos y Connect)
  - Sistema de reservas de viajes
  - Sistema de calificaciones

### Frontend (`src/frontend/`)
- **Framework**: Next.js 14 con TypeScript
- **UI**: React + Tailwind CSS
- **Puerto**: 3001
- **Características**:
  - Búsqueda de viajes
  - Sistema de reservas
  - Chat grupal por viaje
  - Gestión de perfil
  - Sistema de pagos integrado

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
DATABASE_URL=postgresql://unigo:unigo@localhost:5432/unigo
JWT_SECRET=your_jwt_secret
STRIPE_SECRET_KEY=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...
```

### Frontend (`src/frontend/.env.local`)
```env
NEXT_PUBLIC_API_URL=http://127.0.0.1:8000
NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=your_google_maps_key
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...
```

## Flujo de Desarrollo

1. **Iniciar infraestructura**: `make infra-up`
2. **Iniciar backend**: `make backend-start`
3. **Iniciar frontend**: `make frontend`

O todo junto: `make dev`

## Notas Importantes

- **Notificaciones**: Se ha eliminado completamente el sistema de notificaciones
- **Stripe Connect**: Los conductores reciben fondos automáticamente al aceptar reservas
- **Cancelaciones**: Sistema de reembolso con penalización (<24h: 30%, ≥24h: 0%)
- **Asientos**: Actualización en tiempo real al aceptar/cancelar reservas
