# UniGO - Presentación del Proyecto
## Sistemas Web I - 2025
### Carpooling Universitario

---

## DIAPOSITIVA 1: Portada

```
┌──────────────────────────────────────────────────────┐
│                                                       │
│               🎓 🚗 UniGO                            │
│                                                       │
│        Carpooling Universitario                      │
│        Conectando Estudiantes                        │
│                                                       │
│                                                       │
│              Sistemas Web I - 2025                   │
│              Equipo UniGO                            │
│                                                       │
└──────────────────────────────────────────────────────┘
```

---

## DIAPOSITIVA 2: ¿Qué es UniGO?

### Problema
- Transporte universitario caro
- Viajes en coche vacíos entre ciudades
- Falta de conexión entre estudiantes

### Solución
**UniGO**: Plataforma web que conecta estudiantes universitarios para compartir viajes

### Beneficios
- 💰 **Ahorro**: Divide costes de combustible
- 🌱 **Sostenibilidad**: Menos coches en carretera
- 👥 **Comunidad**: Conoce otros estudiantes

---

## DIAPOSITIVA 3: Funcionalidades Principales

### Para Pasajeros
- 🔍 Buscar viajes disponibles
- 💳 Reservar con pago seguro (Stripe)
- 💬 Chat en tiempo real
- ⭐ Valorar conductores

### Para Conductores
- 🚗 Publicar viajes
- ✅ Gestionar solicitudes
- 💰 Recibir pagos (menos 15% comisión)
- 👥 Ver lista de pasajeros

### Para Todos
- 📧 Email institucional obligatorio
- 🔐 Autenticación segura (JWT)
- 🔔 Notificaciones en tiempo real
- 📱 Diseño responsive

---

## DIAPOSITIVA 4: Tecnologías Utilizadas

### Frontend
- ⚛️ **React 19** + Next.js 15
- 🎨 **Tailwind CSS 4**
- 📘 **TypeScript**
- 📡 **Socket.io-client** (WebSockets)
- 💳 **Stripe React**

### Backend ✨ (Migrado a Node.js)
- 🟢 **Node.js** + Express.js
- 🗄️ **PostgreSQL** + Sequelize
- 🔐 **JWT** para autenticación
- ✅ **Joi** para validación
- 📧 **Nodemailer** para emails
- 💳 **Stripe** para pagos
- 🔌 **Socket.io** para tiempo real

### Infraestructura
- 🐳 **Docker** + Docker Compose
- 📊 **Prometheus** + Grafana
- 📨 **MailHog** (desarrollo)

---

## DIAPOSITIVA 5: Arquitectura del Sistema

```
┌─────────────────────────────────────────┐
│         Frontend (React/Next.js)        │
│              Puerto 3001                │
└───────────────┬─────────────────────────┘
                │ HTTP/HTTPS + WebSocket
┌───────────────▼─────────────────────────┐
│       Backend (Node.js/Express)         │
│              Puerto 8000                │
│   • API REST                            │
│   • WebSocket Server (Socket.io)       │
│   • Autenticación JWT                   │
│   • Validaciones (Joi)                  │
└───────────────┬─────────────────────────┘
                │ SQL (Sequelize)
┌───────────────▼─────────────────────────┐
│         PostgreSQL Database             │
│              Puerto 5432                │
│   • 8 tablas principales                │
│   • Relaciones definidas                │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│         Servicios Externos              │
│  Stripe | Google Maps | SMTP            │
└─────────────────────────────────────────┘
```

---

## DIAPOSITIVA 6: Flujo de Usuario - Registro

```
1. Usuario → Registra con email institucional
   └─> Solo dominios permitidos (ugr.es, us.es, etc.)

2. Backend → Genera código de 6 dígitos
   └─> Expira en 15 minutos

3. Backend → Envía email con código
   └─> Nodemailer + SMTP

4. Usuario → Introduce código en app
   └─> Validación en servidor

5. Backend → Marca usuario como verificado
   └─> is_verified = true

6. Usuario → Puede iniciar sesión
   └─> Genera JWT válido 60 minutos
```

---

## DIAPOSITIVA 7: Flujo de Usuario - Reservar Viaje

```
1. Pasajero busca viaje
   └─> Filtros: origen, destino, fecha

2. Selecciona viaje → Ve detalles
   └─> Info conductor, precio, plazas

3. Hace clic en "Reservar"
   └─> Guarda tarjeta (primera vez)

4. Stripe → SetupIntent
   └─> Valida y guarda tarjeta

5. Backend → Crea reserva (status: pending)
   └─> Notifica conductor por email

6. Conductor → Acepta reserva
   └─> Stripe retiene el pago (NO captura)

7. Reserva confirmada
   └─> Chat habilitado

8. Al completar viaje
   └─> Stripe captura pago (con comisión 15%)
```

---

## DIAPOSITIVA 8: Chat en Tiempo Real

### Antes (Versión 1.0 - Python)
- ❌ Polling cada 20 segundos
- ❌ Alta carga en servidor
- ❌ Latencia alta

### Ahora (Versión 2.0 - Node.js)
- ✅ **WebSockets** con Socket.io
- ✅ Mensajes instantáneos
- ✅ Indicador de escritura
- ✅ Confirmación de lectura
- ✅ Notificaciones push

### Eventos Implementados
- `authenticate` - Validar usuario
- `join_trip` - Unirse a chat de viaje
- `send_message` - Enviar mensaje
- `new_message` - Recibir mensaje
- `typing` / `stop_typing` - Indicadores
- `mark_read` - Marcar como leído

---

## DIAPOSITIVA 9: Sistema de Pagos con Stripe

### Funcionalidades
- 💳 **Setup Intent**: Guardar tarjeta
- 🔒 **Payment Intent**: Autorización manual
- 💰 **Captura diferida**: Al completar viaje
- 🔄 **Reembolsos automáticos**: Al cancelar
- 📊 **Comisión app**: 15%
- 🔔 **Webhooks**: Procesamiento asíncrono

### Penalizaciones por Cancelación
| Tiempo antes | Pasajero | Conductor |
|--------------|----------|-----------|
| >24 horas    | 0%       | 0%        |
| 12-24 horas  | 30%      | N/A       |
| 6-12 horas   | 50%      | N/A       |
| <6 horas     | 100%     | N/A       |
| <24 horas    | N/A      | 50%       |

---

## DIAPOSITIVA 10: Base de Datos

### Modelo Entidad-Relación

```
users (8 tablas)
├── email_codes (verificación)
├── rides (viajes publicados)
│   └── bookings (reservas)
│       └── payments (transacciones Stripe)
├── messages (chat)
├── notifications (alertas in-app)
└── ratings (valoraciones)
```

### Tecnologías
- **PostgreSQL 14**: Base de datos relacional
- **Sequelize**: ORM para Node.js
- **Migraciones**: Control de versiones de BD
- **Índices**: Optimización de consultas

---

## DIAPOSITIVA 11: Seguridad

### Autenticación
- 🔐 JWT con expiración (60 min)
- 🔑 Contraseñas hasheadas (bcrypt)
- ✉️ Verificación obligatoria por email
- 🎓 Solo emails institucionales

### Autorización
- 👮 Middleware de autenticación
- ✅ Verificación de ownership
- 🚫 CORS configurado
- 🛡️ Helmet headers

### Validación
- ✅ Cliente: React Hook Form + Zod
- ✅ Servidor: Joi schemas
- ✅ Doble validación

### Pagos
- 💳 PCI-DSS compliance (Stripe)
- 🔒 Datos de tarjeta nunca en servidor
- 🔐 3D Secure support

---

## DIAPOSITIVA 12: Observabilidad

### Métricas (Prometheus)
- 📊 Peticiones HTTP (total, duración)
- 👥 Conexiones WebSocket activas
- 📦 Reservas creadas por estado
- 💰 Pagos procesados
- 💬 Mensajes enviados

### Logging (Winston)
- 📝 Logs estructurados
- 🔍 Niveles: error, warn, info, debug
- 📁 Archivos rotativos
- 🖥️ Consola en desarrollo

### Visualización (Grafana)
- 📈 Dashboards personalizables
- ⚠️ Alertas configurables
- 📊 Gráficas en tiempo real

---

## DIAPOSITIVA 13: Cumplimiento de Requisitos

### Obligatorios ✅ (100%)
- ✅ **Backend Node.js**: Migrado de Python
- ✅ **Métodos HTTP**: GET, POST, PUT, DELETE
- ✅ **Login/Registro**: JWT + email verificación
- ✅ **Base de Datos**: PostgreSQL + Sequelize
- ✅ **Validación formularios**: Cliente + Servidor
- ✅ **Tiempo real**: WebSockets (Socket.io)
- ✅ **Manejo excepciones**: Error handler global
- ✅ **Notificación errores**: Mensajes claros

### Extras ⭐
- ⭐ **Dockerizado**: docker-compose.yml
- ⭐ **Observabilidad**: Prometheus + Grafana
- ⭐ **Pagos**: Stripe completo
- ⭐ **Responsive**: Tailwind CSS
- ⭐ **Accesibilidad**: ARIA labels

---

## DIAPOSITIVA 14: Demo en Vivo

### Demostración
1. **Registro** con email institucional
2. **Verificación** con código
3. **Buscar** viajes disponibles
4. **Crear** nuevo viaje (conductor)
5. **Reservar** plaza (pasajero)
6. **Chat en tiempo real** entre usuarios
7. **Completar** viaje y capturar pago
8. **Valorar** experiencia

### URLs
- Frontend: http://127.0.0.1:3001
- Backend API: http://127.0.0.1:8000
- Swagger Docs: http://127.0.0.1:8000/docs
- Prometheus: http://127.0.0.1:9090
- Grafana: http://127.0.0.1:3000

---

## DIAPOSITIVA 15: Estadísticas del Proyecto

### Código
- **Líneas de código**: ~15,000
- **Archivos**: ~150
- **Lenguajes**: JavaScript, TypeScript, SQL
- **Commits**: 50+

### Backend
- **Endpoints API**: 40+
- **Modelos**: 8
- **Middlewares**: 5
- **Servicios**: 4

### Frontend
- **Componentes React**: 30+
- **Páginas**: 15
- **Hooks personalizados**: 8

### Documentación
- **READMEs**: 3
- **Docs técnicos**: 4 (inicial, diseño, manual, presentación)
- **Páginas totales**: 100+

---

## DIAPOSITIVA 16: Desafíos y Soluciones

### Desafío 1: Migración Python → Node.js
**Problema**: Backend original en FastAPI  
**Solución**: Migración completa a Express.js manteniendo funcionalidades

### Desafío 2: Tiempo Real
**Problema**: Polling ineficiente  
**Solución**: WebSockets con Socket.io

### Desafío 3: Pagos Complejos
**Problema**: Retener y capturar pagos de forma segura  
**Solución**: Stripe Payment Intents con captura manual

### Desafío 4: Validaciones Dobles
**Problema**: Seguridad y UX  
**Solución**: Validación en cliente (rápida) y servidor (segura)

---

## DIAPOSITIVA 17: Trabajo Futuro

### Versión 2.1 (Próximas Mejoras)
- 🔄 **Refresh tokens**: Para sesiones más largas
- 🔍 **Búsqueda avanzada**: Filtros adicionales
- 📍 **Geolocalización**: Rutas en mapa
- 🚀 **Optimización**: Caching con Redis
- 📱 **App móvil**: React Native
- 🌍 **i18n**: Soporte multiidioma
- 🤖 **Moderación**: IA para detección de contenido

### Despliegue en Producción
- ☁️ **Cloud**: Railway, Render o Heroku
- 🔐 **HTTPS**: Certificados SSL
- 📧 **Email real**: SendGrid o Mailjet
- 💳 **Stripe producción**: Keys reales
- 🗄️ **DB managed**: Postgres as a Service

---

## DIAPOSITIVA 18: Lecciones Aprendidas

### Técnicas
- 🎓 **Node.js**: Ecosistema amplio y potente
- 🔌 **WebSockets**: Tiempo real es el futuro
- 💳 **Stripe**: Pagos complejos simplificados
- 📊 **Observabilidad**: Crítica para producción
- 🐳 **Docker**: Consistencia entre entornos

### Metodológicas
- 📝 **Documentación**: Clave para mantenibilidad
- ✅ **Validación**: Nunca confiar en el cliente
- 🔒 **Seguridad**: Diseño desde el principio
- 🧪 **Testing**: Previene regresiones
- 👥 **Trabajo en equipo**: Comunicación constante

---

## DIAPOSITIVA 19: Repositorio y Documentación

### GitHub
```
https://github.com/Pablodlx/UniGO
```

### Estructura del Repositorio
```
UniGO/
├── docs/
│   ├── documento_inicial.md
│   ├── documento_diseno.md
│   ├── manual_uso.md
│   └── presentacion.md
├── backend-node/ (Node.js/Express)
├── frontend/ (Next.js/React)
├── infra/ (Docker Compose)
└── README.md
```

### Documentos Entregados
- ✅ Documento Inicial (historia, requisitos, casos uso)
- ✅ Documento de Diseño (sitemap, wireframes, arquitectura)
- ✅ Manual de Uso (instrucciones paso a paso)
- ✅ Presentación (esta presentación)
- ✅ README actualizado

---

## DIAPOSITIVA 20: Conclusiones

### Logros
✅ Aplicación fullstack completa y funcional  
✅ 100% de requisitos obligatorios cumplidos  
✅ Extras: Docker, observabilidad, pagos  
✅ Migración exitosa a Node.js  
✅ WebSockets para tiempo real  
✅ Documentación completa  

### Impacto
- 💰 **Ahorro** para estudiantes
- 🌱 **Sostenibilidad** ambiental
- 👥 **Comunidad** universitaria conectada
- 📚 **Aprendizaje** de tecnologías modernas

### Agradecimientos
Gracias por su atención y por la oportunidad de desarrollar este proyecto.

**¡Preguntas?** 🙋

---

## DIAPOSITIVA 21: Contacto

### Equipo UniGO
📧 **Email**: equipo@unigo.app  
🐙 **GitHub**: https://github.com/Pablodlx/UniGO  
🌐 **Demo**: http://unigo-demo.app  

### Código QR
```
[QR al repositorio de GitHub]
```

---

**¡Gracias!** 🎓🚗

**Sistemas Web I - 2025**
