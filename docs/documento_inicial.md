# UniGO - Documento Inicial del Proyecto
## Sistemas Web I - 2025

---

## HISTÓRICO DE CAMBIOS

| Versión | Fecha | Autor | Descripción |
|---------|-------|-------|-------------|
| 1.0 | 27 Oct 2024 | Equipo UniGO | Implementación inicial |
| 2.0 | 04 Dic 2024 | Equipo UniGO | Backend Node.js + Express |
| 3.0 | 07 Dic 2024 | Equipo UniGO | WebSocket chat grupal + Stripe Connect + Sistema de reembolsos |

---

## 1. DESCRIPCIÓN DEL PROYECTO

### 1.1 Resumen Ejecutivo

**UniGO** es una aplicación web fullstack de carpooling universitario que conecta a estudiantes de universidades españolas para compartir viajes entre ciudades. El proyecto facilita el transporte sostenible y económico entre comunidades universitarias.

### 1.2 Objetivos

- Proporcionar una plataforma segura para compartir viajes entre estudiantes universitarios
- Reducir costes de transporte mediante el uso compartido de vehículos
- Fomentar la sostenibilidad y reducción de emisiones de CO2
- Crear una comunidad universitaria conectada

### 1.3 Alcance

La aplicación permite:
- Registro y autenticación con email institucional (.ugr.es, .us.es, etc.)
- Creación y búsqueda de viajes con Google Maps
- Sistema de reservas con aceptación/rechazo
- Chat grupal en tiempo real (WebSocket) por viaje
- Pagos seguros con Stripe Payment Intents + Connect
- Transferencias automáticas a conductores (85% del pago)
- Sistema de cancelaciones con reembolsos
- Sistema de valoraciones mutuas

### 1.4 Tecnologías Utilizadas

#### Backend
- **Framework**: Express.js 4.x (Node.js 18+)
- **Base de datos**: PostgreSQL 15
- **ORM**: Sequelize 6.x
- **Autenticación**: JWT (jsonwebtoken)
- **Validación**: Joi
- **Email**: Nodemailer (SMTP)
- **Pagos**: Stripe Payment Intents + Connect
- **WebSockets**: Socket.io (chat grupal)
- **Observabilidad**: Prometheus + Winston

#### Frontend
- **Framework**: Next.js 15 (React 19)
- **Lenguaje**: TypeScript 5
- **Estilos**: Tailwind CSS
- **Gestión de estado**: React Hooks + Context API
- **HTTP Client**: Fetch API nativo
- **Mapas**: Google Maps React (@react-google-maps/api)
- **Pagos**: @stripe/react-stripe-js + Elements
- **WebSocket**: Socket.io-client

#### Infraestructura
- **Contenedores**: Docker + Docker Compose
- **Base de datos**: PostgreSQL 15 (contenedor)
- **Email (dev)**: MailHog
- **Monitorización**: Prometheus + Grafana
- **Admin DB**: pgAdmin 4

---

## 2. DIAGRAMA DE CASOS DE USO

### 2.1 Actores

1. **Usuario No Registrado (Visitante)**
2. **Usuario Registrado (Estudiante)**
3. **Conductor (Estudiante con viaje creado)**
4. **Pasajero (Estudiante con reserva)**
5. **Sistema de Pagos (Stripe)**
6. **Sistema de Notificaciones**

### 2.2 Casos de Uso Principales

```
┌─────────────────────────────────────────────────────────────┐
│                     Sistema UniGO                            │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ Gestión de Usuarios                                   │  │
│  │  • Registrarse (con email institucional)             │  │
│  │  • Verificar email (código 6 dígitos)                │  │
│  │  • Iniciar sesión (JWT)                              │  │
│  │  • Actualizar perfil                                  │  │
│  │  • Subir avatar                                       │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ Gestión de Viajes (Conductor)                        │  │
│  │  • Crear viaje                                        │  │
│  │  • Ver solicitudes pendientes                         │  │
│  │  • Aceptar/rechazar reservas                          │  │
│  │  • Ver lista de pasajeros                             │  │
│  │  • Completar viaje (captura pagos)                    │  │
│  │  • Cancelar viaje (con penalizaciones)                │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ Gestión de Reservas (Pasajero)                       │  │
│  │  • Buscar viajes                                      │  │
│  │  • Solicitar reserva                                  │  │
│  │  • Guardar método de pago (Stripe)                    │  │
│  │  • Ver estado de reserva                              │  │
│  │  • Cancelar reserva (con penalizaciones)              │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ Chat en Tiempo Real                                   │  │
│  │  • Conectar a WebSocket                               │  │
│  │  • Enviar mensajes                                    │  │
│  │  • Recibir mensajes en tiempo real                    │  │
│  │  • Ver indicador de escritura                         │  │
│  │  • Marcar mensajes como leídos                        │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ Sistema de Pagos (Stripe)                            │  │
│  │  • Guardar tarjeta (SetupIntent)                      │  │
│  │  • Autorizar pago (al aceptar reserva)                │  │
│  │  • Capturar pago (al completar viaje)                 │  │
│  │  • Aplicar comisión de app (15%)                      │  │
│  │  • Reembolsar (al cancelar)                           │  │
│  │  • Procesar webhooks                                  │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ Sistema de Notificaciones                            │  │
│  │  • Enviar email de verificación                       │  │
│  │  • Notificar nueva reserva (email)                    │  │
│  │  • Notificar confirmación (email)                     │  │
│  │  • Alertas in-app de mensajes                         │  │
│  │  • Notificaciones en tiempo real                      │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐  │
│  │ Sistema de Valoraciones                              │  │
│  │  • Valorar conductor (1-5 estrellas)                  │  │
│  │  • Valorar pasajero (1-5 estrellas)                   │  │
│  │  • Ver valoración promedio                            │  │
│  │  • Añadir comentario                                  │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

### 2.3 Diagrama de Casos de Uso UML

```
                    ┌─────────────────┐
                    │    Visitante    │
                    └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │   Registrarse   │
                    └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │ Verificar Email │
                    └────────┬────────┘
                             │
    ┌────────────────────────▼──────────────────────────┐
    │                    Usuario                        │
    └────┬──────────────────┬──────────────────┬────────┘
         │                  │                  │
    ┌────▼─────┐      ┌─────▼─────┐     ┌─────▼──────┐
    │ Conductor│      │  Pasajero │     │   Chat     │
    └────┬─────┘      └─────┬─────┘     └─────┬──────┘
         │                  │                  │
    ┌────▼─────┐      ┌─────▼─────┐     ┌─────▼──────┐
    │ Crear    │      │ Buscar    │     │ Enviar     │
    │ Viaje    │      │ Viajes    │     │ Mensaje    │
    └──────────┘      └───────────┘     └────────────┘
         │                  │
    ┌────▼─────┐      ┌─────▼─────┐
    │ Aceptar  │      │ Solicitar │
    │ Reserva  │      │ Reserva   │
    └────┬─────┘      └─────┬─────┘
         │                  │
         └────────┬─────────┘
                  │
         ┌────────▼─────────┐
         │  Sistema Stripe  │
         │  (Pagos)         │
         └──────────────────┘
```

---

## 3. REQUISITOS FUNCIONALES

### RF01 - Registro y Autenticación
**Estado**: ✅ **CUMPLIDO**

**Descripción**: El sistema debe permitir el registro de usuarios con email institucional y autenticación mediante JWT.

**Criterios de aceptación**:
- Solo se permiten emails de dominios universitarios españoles (ugr.es, us.es, uma.es, etc.)
- Se envía un código de verificación de 6 dígitos por email
- El código expira en 15 minutos
- Login genera un token JWT válido por 60 minutos
- Las contraseñas se almacenan hasheadas con bcrypt

**Implementación**:
- Backend Node.js: `/api/auth/register`, `/api/auth/verify`, `/api/auth/login`
- Validación con Joi
- Email con Nodemailer (MailHog en desarrollo)
- JWT con jsonwebtoken

### RF02 - Gestión de Perfil
**Estado**: ✅ **CUMPLIDO**

**Descripción**: Los usuarios pueden actualizar su información personal y subir avatar.

**Criterios de aceptación**:
- Campos editables: nombre completo, teléfono, biografía, preferencias
- Subida de imagen de avatar (máx 5MB)
- Las imágenes se almacenan en servidor
- URL pública accesible para avatares

**Implementación**:
- Backend: `/api/users/me` (GET/PUT)
- Multer para subida de archivos
- Almacenamiento en `data/avatars/`
- Endpoint estático: `/static/avatars/:filename`

### RF03 - Creación de Viajes
**Estado**: ✅ **CUMPLIDO**

**Descripción**: Los conductores pueden crear ofertas de viaje con todos los detalles necesarios.

**Criterios de aceptación**:
- Campos obligatorios: origen, destino, fecha, hora, plazas, precio
- Campos opcionales: descripción, coordenadas GPS
- Validación de datos en servidor
- Integración opcional con Google Maps API

**Implementación**:
- Backend: `POST /api/rides`
- Modelo Ride con Sequelize
- Validación de campos
- Cálculo opcional de duración de viaje

### RF04 - Búsqueda de Viajes
**Estado**: ✅ **CUMPLIDO**

**Descripción**: Los usuarios pueden buscar viajes disponibles con filtros.

**Criterios de aceptación**:
- Búsqueda por origen, destino, fecha
- Filtros adicionales: precio, plazas disponibles
- Resultados paginados
- Información del conductor visible

**Implementación**:
- Backend: `GET /api/rides` con query parameters
- Filtros con Sequelize
- Include de información del conductor

### RF05 - Sistema de Reservas
**Estado**: ✅ **CUMPLIDO**

**Descripción**: Los pasajeros pueden solicitar reservas y los conductores gestionarlas.

**Criterios de aceptación**:
- Pasajero solicita reserva (status: pending)
- Conductor recibe notificación
- Conductor puede aceptar (status: confirmed) o rechazar (status: rejected)
- Al aceptar, se crea PaymentIntent en Stripe
- Se verifica disponibilidad de plazas

**Implementación**:
- Backend: `/api/bookings` (POST)
- `/api/bookings/:id/accept` (POST) - crea PaymentIntent
- `/api/bookings/:id/reject` (POST)
- `/api/bookings/pending-for-driver` (GET)
- Notificaciones por email

### RF06 - Sistema de Pagos con Stripe
**Estado**: ✅ **CUMPLIDO**

**Descripción**: Integración completa de pagos seguros con Stripe.

**Criterios de aceptación**:
- Guardar tarjeta con SetupIntent
- Crear PaymentIntent al aceptar reserva (captura manual)
- Retener pago hasta completar viaje
- Capturar pago al completar viaje (con comisión 15%)
- Reembolsos automáticos al cancelar
- Penalizaciones según tiempo:
  - >24h antes: 0% penalización
  - 12-24h: 30% penalización
  - 6-12h: 50% penalización
  - <6h: 100% penalización (pasajero)
  - <24h: 50% penalización (conductor)

**Implementación**:
- Backend: `/api/payments/create-setup-intent`
- `/api/payments/confirm-setup-intent`
- `/api/payments/webhook` (procesa eventos de Stripe)
- `/api/rides/:id/complete` (captura pagos)
- `/api/bookings/:id/cancel` (aplica penalizaciones)
- Frontend: @stripe/react-stripe-js

### RF07 - Chat en Tiempo Real
**Estado**: ✅ **CUMPLIDO** (Mejorado con WebSockets)

**Descripción**: Comunicación en tiempo real entre conductor y pasajeros.

**Criterios de aceptación**:
- Chat 1-a-1 por viaje
- Mensajes en tiempo real con WebSockets
- Indicador de escritura
- Marcado de mensajes como leídos
- Historial de mensajes persistente
- Notificaciones de mensajes no leídos

**Implementación**:
- Backend: Socket.io en `/websocket/index.js`
- Eventos: `authenticate`, `join_trip`, `send_message`, `typing`, `mark_read`
- HTTP fallback: `GET/POST /api/chat/trips/:tripId/messages`
- Frontend: socket.io-client

### RF08 - Sistema de Emails
**Estado**: ✅ **CUMPLIDO**

**Descripción**: Emails transaccionales para eventos importantes.

**Criterios de aceptación**:
- Email de verificación al registrarse (código 6 dígitos)
- Email al conductor cuando recibe nueva solicitud de reserva
- Email al pasajero cuando aceptan su reserva

**Implementación**:
- Backend: Nodemailer con SMTP (Gmail en desarrollo)
- Plantillas HTML para emails
- Configuración en variables de entorno

### RF09 - Sistema de Valoraciones
**Estado**: ✅ **CUMPLIDO**

**Descripción**: Conductores y pasajeros pueden valorarse mutuamente.

**Criterios de aceptación**:
- Valoración de 1 a 5 estrellas
- Comentario opcional
- Solo después de completar el viaje
- Valoración promedio visible en perfil

**Implementación**:
- Backend: `/api/ratings` (POST)
- Modelo Rating con Sequelize
- Cálculo de promedio en consultas

### RF10 - Completar y Cancelar Viajes
**Estado**: ✅ **CUMPLIDO**

**Descripción**: Gestión del ciclo de vida completo de viajes y reservas.

**Criterios de aceptación**:
- Conductor puede completar viaje (captura todos los pagos)
- Conductor puede cancelar viaje (<24h: penalización 50%)
- Pasajero puede cancelar reserva (penalización según tiempo)
- Reembolsos automáticos
- Actualización de estados en BD

**Implementación**:
- Backend: `POST /api/rides/:id/complete`
- `POST /api/bookings/:id/cancel`
- Lógica de penalizaciones en service layer
- Integración con Stripe para refunds

---

## 4. REQUISITOS NO FUNCIONALES

### RNF01 - Rendimiento
- Tiempo de respuesta < 2 segundos para operaciones estándar
- Mensajes de chat entregados en < 500ms
- Soporte para 100+ usuarios concurrentes

### RNF02 - Seguridad
- Contraseñas hasheadas con bcrypt (salt rounds: 10)
- Tokens JWT con expiración
- HTTPS en producción
- Validación de entrada en cliente y servidor
- Headers de seguridad con Helmet
- Protección CORS configurada

### RNF03 - Disponibilidad
- Disponibilidad objetivo: 99% (excluyendo mantenimiento)
- Manejo gracioso de errores
- Logs de auditoría
- Monitorización con Prometheus

### RNF04 - Escalabilidad
- Arquitectura desacoplada (frontend/backend)
- Base de datos PostgreSQL escalable
- Posibilidad de despliegue en múltiples contenedores
- WebSockets con múltiples instancias (sticky sessions)

### RNF05 - Usabilidad
- Interfaz responsiva (mobile-first)
- Tiempos de carga optimizados
- Feedback visual inmediato
- Mensajes de error claros
- Accesibilidad WCAG 2.1 AA

### RNF06 - Mantenibilidad
- Código modular y bien documentado
- Tests unitarios e integración
- Logging estructurado con Winston
- Métricas de negocio en Prometheus
- README con instrucciones claras

---

## 5. JUSTIFICACIÓN DE REQUISITOS

### 5.1 Requisitos CUMPLIDOS ✅

#### ✅ Backend en Node.js
**Cumplido al 100%** - El sistema ha sido completamente migrado de FastAPI/Python a Node.js/Express en la versión 2.0 (diciembre 2025).

#### ✅ Métodos HTTP
**Cumplido** - Se utilizan correctamente:
- GET para consultas (listar viajes, obtener mensajes)
- POST para creaciones (registro, login, crear viaje, reservar)
- PUT para actualizaciones (actualizar perfil)
- DELETE para eliminaciones (cancelar reserva)

#### ✅ Login y Registro
**Cumplido** - Sistema completo con:
- Registro con email institucional
- Verificación por código de 6 dígitos
- Login con JWT
- Gestión de sesiones

#### ✅ Base de Datos
**Cumplido** - PostgreSQL con Sequelize:
- 8 tablas principales (users, rides, bookings, payments, messages, etc.)
- Relaciones definidas
- Índices optimizados
- Migraciones

#### ✅ Procesamiento de Formularios
**Cumplido** - Validación en cliente y servidor:
- Cliente: React Hook Form + Zod
- Servidor: Joi validation middleware
- Mensajes de error claros

#### ✅ Funcionalidad en Tiempo Real
**Cumplido** - Chat con WebSockets (Socket.io):
- Mensajes en tiempo real
- Indicador de escritura
- Notificaciones instantáneas
- Eventos bidireccionales

#### ✅ Manejo de Excepciones
**Cumplido** - Sistema robusto:
- Middleware errorHandler global
- Try-catch en todas las rutas
- Logging con Winston
- Códigos de estado HTTP apropiados

#### ✅ Notificación de Errores al Usuario
**Cumplido** - Feedback claro:
- Mensajes de error descriptivos
- Validaciones con mensajes específicos
- Alertas visuales en frontend
- Toast notifications

### 5.2 Extras Implementados ⭐

#### ⭐ Dockerización
**Implementado** - Docker Compose completo:
- Servicio PostgreSQL
- Servicio MailHog (desarrollo)
- Servicio Prometheus
- Servicio Grafana
- Backend y frontend dockerizables

#### ⭐ Observabilidad
**Implementado** - Stack completo:
- Prometheus para métricas
- Grafana para visualización
- Métricas personalizadas (bookings, payments, messages)
- Dashboards configurables

#### ⭐ Sistema de Pagos
**Implementado** - Integración completa de Stripe:
- Setup Intent para guardar tarjetas
- Payment Intent con captura manual
- Webhooks
- Comisiones (15%)
- Penalizaciones automáticas
- Reembolsos

#### ⭐ Diseño Responsive
**Implementado** - Tailwind CSS:
- Mobile-first design
- Media queries
- Componentes adaptativos

#### ⭐ Accesibilidad
**Implementado parcialmente**:
- Labels semánticos
- ARIA labels en componentes clave
- Contraste de colores adecuado
- **Pendiente**: Más ARIA roles, navegación por teclado completa

### 5.3 Requisitos NO Cumplidos o Parciales ⚠️

#### ⚠️ Despliegue en la Nube
**Estado**: Configuración lista, NO desplegado actualmente

**Justificación**:
- El proyecto está completamente dockerizado y listo para despliegue
- Se incluyen instrucciones para Railway, Render, Heroku
- No se ha desplegado en producción por:
  - Proyecto académico sin necesidad de hosting público
  - Costes asociados a servicios cloud
  - Base de datos y Stripe requieren configuración de producción
  
**Para cumplir**: Seguir guía de despliegue en `docs/deployment-guide.md`

---

## 6. CONCLUSIONES

UniGO es un proyecto fullstack completo que cumple **al 100% con los requisitos obligatorios** de la asignatura Sistemas Web I:

✅ Backend en **Node.js/Express** (migrado de Python)  
✅ Frontend con **HTML/JSX + CSS (Tailwind) + JavaScript (React)**  
✅ Sistema de **autenticación y registro** completo  
✅ Base de datos **PostgreSQL** con ORM  
✅ Validación de formularios en **cliente y servidor**  
✅ Funcionalidad en **tiempo real** con WebSockets  
✅ **Manejo de excepciones** y notificación de errores  
✅ **Dockerizado** y con observabilidad  

Además, incluye funcionalidades avanzadas como:
- ⭐ Sistema de pagos con Stripe
- ⭐ Observabilidad con Prometheus/Grafana  
- ⭐ Diseño responsive
- ⭐ Chat en tiempo real con WebSockets

El único aspecto pendiente es el **despliegue en la nube**, que está completamente preparado pero no ejecutado por ser un proyecto académico.

---

## EQUIPO DE DESARROLLO

**Equipo UniGO - 2025**
- Desarrollo Backend
- Desarrollo Frontend  
- Infraestructura y DevOps
- Documentación

---

**Fecha de elaboración**: 04 de Diciembre de 2025  
**Versión del documento**: 2.0  
**Asignatura**: Sistemas Web I  
**Curso**: 2024-2025
