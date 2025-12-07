# UniGO - Guía de Despliegue en la Nube
## Deployment Guide para Producción

---

## 📋 Tabla de Contenidos

1. [Opciones de Despliegue](#opciones-de-despliegue)
2. [Requisitos Previos](#requisitos-previos)
3. [Opción 1: Railway](#opcion-1-railway-recomendado)
4. [Opción 2: Render](#opcion-2-render)
5. [Opción 3: Heroku](#opcion-3-heroku)
6. [Configuración de Base de Datos](#configuracion-de-base-de-datos)
7. [Configuración de Variables de Entorno](#configuracion-de-variables-de-entorno)
8. [Configuración de Stripe](#configuracion-de-stripe)
9. [Configuración de Email](#configuracion-de-email)
10. [Post-Deployment](#post-deployment)

---

## Opciones de Despliegue

| Plataforma | Pros | Contras | Coste |
|------------|------|---------|-------|
| **Railway** | Fácil, PostgreSQL incluido, buen free tier | Límite de uso gratuito | $5/mes o gratis |
| **Render** | Deploy automático, SSL gratis | Backend se duerme en free tier | Gratis o $7/mes |
| **Heroku** | Maduro, documentación extensa | Eliminó free tier | Desde $7/mes |

---

## Requisitos Previos

✅ Cuenta en la plataforma elegida  
✅ Repositorio GitHub con el código  
✅ Cuenta Stripe (producción)  
✅ SMTP real configurado (Gmail, SendGrid, etc.)  
✅ Certificado SSL (automático en las plataformas)

---

## Opción 1: Railway (Recomendado)

### Paso 1: Crear Proyecto

1. Ve a [railway.app](https://railway.app)
2. Haz clic en **"Start a New Project"**
3. Selecciona **"Deploy from GitHub repo"**
4. Conecta tu repositorio **Pablodlx/UniGO**

### Paso 2: Configurar PostgreSQL

1. En tu proyecto, haz clic en **"+ New"**
2. Selecciona **"Database"** → **"PostgreSQL"**
3. Railway creará automáticamente la base de datos
4. Copia la **DATABASE_URL** de las variables de entorno

### Paso 3: Configurar Backend

1. Haz clic en el servicio del backend
2. Ve a **"Settings"**
3. Configura:
   - **Root Directory**: `src/backend`
   - **Start Command**: `npm start`
   - **Build Command**: `npm install`
4. Ve a **"Variables"** y añade:

```bash
NODE_ENV=production
PORT=8000
DATABASE_URL=${{Postgres.DATABASE_URL}}

# JWT
JWT_SECRET=tu-jwt-secret-seguro-aqui
SECRET_KEY=tu-secret-key-seguro-aqui

# Email (SMTP real para producción)
EMAIL_BACKEND=smtp
EMAIL_PROVIDER=Gmail
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=tu-email@gmail.com
SMTP_PASS=tu-app-password-de-gmail
EMAIL_FROM_NAME=UniGO
EMAIL_FROM=tu-email@gmail.com

# Stripe (claves de producción)
STRIPE_SECRET_KEY=sk_live_xxx
STRIPE_WEBHOOK_SECRET=whsec_xxx
APP_COMMISSION_PERCENT=15

# CORS (ajusta con tu dominio de frontend)
ALLOWED_ORIGINS=https://tu-dominio.com,https://www.tu-dominio.com

# Dominios de email permitidos
ALLOWED_EMAIL_DOMAINS=ugr.es,us.es,uma.es,ucm.es,upm.es,uva.es
```

5. Guarda y redeploy

### Paso 4: Configurar Frontend

1. Haz clic en **"+ New"** → **"Empty Service"**
2. Conecta el mismo repositorio
3. Configura:
   - **Root Directory**: `src/frontend`
   - **Build Command**: `npm run build`
   - **Start Command**: `npm start`
4. Variables de entorno:

```bash
# API Backend
NEXT_PUBLIC_API_BASE=https://tu-backend.railway.app/api
NEXT_PUBLIC_API_URL=https://tu-backend.railway.app

# WebSocket (mismo dominio que backend)
NEXT_PUBLIC_WS_URL=https://tu-backend.railway.app

# Google Maps
NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=tu-google-maps-api-key

# Stripe (clave pública de producción)
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_live_xxx
```

5. Guarda y deploy

### Paso 5: Migraciones

1. Abre el terminal de Railway (servicio backend)
2. Ejecuta:

```bash
npm run migrate
```

### Paso 6: Dominios Personalizados (Opcional)

1. En settings del frontend, haz clic en **"Generate Domain"**
2. O añade tu dominio personalizado en **"Custom Domain"**
3. Configura el DNS según las instrucciones

---

## Opción 2: Render

### Paso 1: Crear Base de Datos

1. Ve a [render.com](https://render.com)
2. Haz clic en **"New +"** → **"PostgreSQL"**
3. Configura:
   - **Name**: unigo-db
   - **Region**: Oregon (US West) o el más cercano
   - **PostgreSQL Version**: 14
   - **Plan**: Free o Starter
4. Crea la base de datos
5. Copia la **External Database URL**

### Paso 2: Crear Web Service (Backend)

1. Haz clic en **"New +"** → **"Web Service"**
2. Conecta tu repositorio GitHub
3. Configura:
   - **Name**: unigo-backend
   - **Region**: Mismo que la DB
   - **Branch**: main
   - **Root Directory**: `backend-node`
   - **Runtime**: Node
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Plan**: Free o Starter

4. Variables de entorno (añade en Environment):

```bash
NODE_ENV=production
PORT=8000
DATABASE_URL=postgresql://...
SECRET_KEY=tu-clave-secreta

# Resto de variables igual que Railway
```

5. Haz clic en **"Create Web Service"**

### Paso 3: Crear Web Service (Frontend)

1. Haz clic en **"New +"** → **"Static Site"**
2. Conecta tu repositorio
3. Configura:
   - **Name**: unigo-frontend
   - **Root Directory**: `frontend`
   - **Build Command**: `npm run build`
   - **Publish Directory**: `out` o `.next`

4. Variables de entorno:

```bash
VITE_API_BASE=https://unigo-backend.onrender.com
```

5. Crea el sitio

### Paso 4: Configurar WebSockets

⚠️ **Importante**: Render free tier tiene limitaciones con WebSockets.

En el backend, configura fallback HTTP para chat:

```javascript
// src/server.js
const io = new Server(server, {
  cors: { /* ... */ },
  transports: ['websocket', 'polling'], // Añadir polling como fallback
  allowEIO3: true
});
```

---

## Opción 3: Heroku

### Paso 1: Instalar Heroku CLI

```bash
npm install -g heroku
heroku login
```

### Paso 2: Crear Aplicaciones

```bash
# Backend
cd backend-node
heroku create unigo-backend

# Frontend
cd ../frontend
heroku create unigo-frontend
```

### Paso 3: Añadir PostgreSQL

```bash
cd ../backend-node
heroku addons:create heroku-postgresql:mini
```

### Paso 4: Configurar Variables

```bash
heroku config:set NODE_ENV=production
heroku config:set SECRET_KEY=tu-clave-secreta
heroku config:set STRIPE_SECRET_KEY=sk_live_xxx
# ... resto de variables
```

### Paso 5: Deploy

```bash
# Backend
git subtree push --prefix backend-node heroku main

# Frontend
cd ../frontend
git subtree push --prefix frontend heroku main
```

---

## Configuración de Base de Datos

### Migraciones en Producción

**Railway/Render**:
```bash
# Desde el dashboard, abre terminal y ejecuta:
npm run migrate
```

**Heroku**:
```bash
heroku run npm run migrate -a unigo-backend
```

### Backup de Base de Datos

**Railway**:
- Los backups automáticos están disponibles en planes pagados
- Backup manual: Usa `pg_dump`

**Render**:
```bash
pg_dump $DATABASE_URL > backup.sql
```

**Heroku**:
```bash
heroku pg:backups:capture -a unigo-backend
heroku pg:backups:download -a unigo-backend
```

---

## Configuración de Variables de Entorno

### Backend

```bash
# General
NODE_ENV=production
PORT=8000
HOST=0.0.0.0

# Database
DATABASE_URL=postgresql://user:pass@host:5432/db

# JWT
SECRET_KEY=genera-una-clave-segura-de-32-caracteres-minimo
ACCESS_TOKEN_EXPIRE_MINUTES=60

# Email (Producción con Gmail)
EMAIL_BACKEND=smtp
EMAIL_PROVIDER=Gmail
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USERNAME=tu-email@gmail.com
SMTP_PASSWORD=tu-app-password-de-google
SMTP_USE_TLS=true
SMTP_USE_SSL=false
EMAIL_FROM_NAME=UniGO
EMAIL_FROM=tu-email@gmail.com

# Stripe (PRODUCCIÓN)
STRIPE_SECRET_KEY=sk_live_xxxxxxxxxx
STRIPE_PUBLIC_KEY=pk_live_xxxxxxxxxx
STRIPE_WEBHOOK_SECRET=whsec_xxxxxxxxxx
APP_COMMISSION_PERCENT=15

# CORS
CORS_ORIGINS=https://tu-dominio.com,https://www.tu-dominio.com

# Dominios permitidos
ALLOWED_EMAIL_DOMAINS=ugr.es,us.es,uma.es,ucm.es,upm.es,uab.cat,ub.edu

# Google Maps (opcional)
GOOGLE_MAPS_API_KEY=tu-api-key
```

### Frontend

```bash
VITE_API_BASE=https://tu-backend.railway.app
NEXT_PUBLIC_STRIPE_PUBLIC_KEY=pk_live_xxxxxxxxxx
NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=tu-api-key
```

---

## Configuración de Stripe

### 1. Crear Cuenta de Producción

1. Ve a [stripe.com](https://stripe.com)
2. Completa el proceso de verificación de empresa
3. Activa tu cuenta de producción

### 2. Obtener Claves de API

1. Ve a Developers → API Keys
2. Copia:
   - **Publishable key** (pk_live_...)
   - **Secret key** (sk_live_...)

### 3. Configurar Webhooks

1. Ve a Developers → Webhooks
2. Haz clic en **"Add endpoint"**
3. URL: `https://tu-backend.railway.app/api/payments/webhook`
4. Selecciona eventos:
   - `payment_intent.succeeded`
   - `payment_intent.payment_failed`
   - `setup_intent.succeeded`
   - `charge.refunded`
5. Copia el **Signing secret** (whsec_...)

### 4. Configurar Stripe Connect (Conductores)

1. Ve a Connect → Settings
2. Configura:
   - **Onboarding**: Custom
   - **Redirect URIs**: Añade tu dominio
3. Habilita transferencias automáticas

---

## Configuración de Email

### Opción 1: Gmail

1. Activa verificación en 2 pasos en tu cuenta Google
2. Ve a Seguridad → Contraseñas de aplicaciones
3. Genera una contraseña de aplicación
4. Usa esa contraseña en `SMTP_PASSWORD`

### Opción 2: SendGrid

1. Regístrate en [sendgrid.com](https://sendgrid.com)
2. Verifica tu dominio
3. Crea una API Key
4. Configura:

```bash
EMAIL_BACKEND=smtp
EMAIL_PROVIDER=SendGrid
SMTP_HOST=smtp.sendgrid.net
SMTP_PORT=587
SMTP_USERNAME=apikey
SMTP_PASSWORD=tu-api-key-de-sendgrid
```

### Opción 3: Mailjet

Similar a SendGrid, sigue las instrucciones en [mailjet.com](https://mailjet.com)

---

## Post-Deployment

### 1. Probar la Aplicación

✅ **Registro**: Crear cuenta con email real  
✅ **Verificación**: Recibir y validar código  
✅ **Login**: Iniciar sesión con JWT  
✅ **Crear viaje**: Como conductor  
✅ **Reservar**: Como pasajero  
✅ **Chat**: Enviar mensajes en tiempo real  
✅ **Pago**: Guardar tarjeta y procesar pago  
✅ **Completar**: Finalizar viaje y capturar pago  

### 2. Monitorización

**Railway**:
- Métricas automáticas en el dashboard
- Logs en tiempo real

**Render**:
- Ve a Metrics para ver uso
- Logs accesibles desde el dashboard

**Heroku**:
```bash
heroku logs --tail -a unigo-backend
```

### 3. Configurar Alertas

**Render**:
- Configure health checks en Settings
- URL: `/health`
- Frecuencia: 60 segundos

**Railway/Heroku**:
- Usa servicios externos como UptimeRobot
- Monitor URLs de health check

### 4. SSL/HTTPS

✅ **Railway**: SSL automático
✅ **Render**: SSL automático  
✅ **Heroku**: SSL automático

### 5. Dominios Personalizados

**Railway**:
1. Settings → Domains
2. Añade tu dominio
3. Configura DNS: `CNAME` → `proxy.railway.app`

**Render**:
1. Settings → Custom Domain
2. Añade tu dominio
3. Configura DNS según instrucciones

---

## Troubleshooting

### Error: Cannot connect to database

**Solución**:
- Verifica que `DATABASE_URL` esté configurada
- Comprueba que el servidor de DB esté en la misma región
- Revisa los logs para errores de conexión

### Error: Emails no se envían

**Solución**:
- Verifica credenciales SMTP
- Comprueba que el puerto 587 esté abierto
- Usa contraseña de aplicación (no la del email)

### Error: WebSocket connection failed

**Solución**:
- Asegúrate de que el backend soporte WebSockets
- Configura fallback a HTTP polling
- Verifica CORS Origins

### Error: Stripe webhooks failing

**Solución**:
- Verifica que el webhook secret sea correcto
- Asegúrate de que el endpoint `/api/payments/webhook` sea público
- Revisa logs de Stripe dashboard

---

## Costes Estimados

### Railway (Recomendado)
- **Free Tier**: $5 crédito/mes
- **Starter**: $5/mes (Backend) + $5/mes (DB) = $10/mes
- **Uso estimado**: ~$10-15/mes

### Render
- **Free Tier**: Gratis (con limitaciones)
- **Starter**: $7/mes (Backend) + $7/mes (DB) = $14/mes
- **Pro**: $25/mes (Backend) + $25/mes (DB) = $50/mes

### Heroku
- **Basic**: $7/mes (Backend) + $5/mes (DB) = $12/mes
- **Standard**: $25/mes (Backend) + $50/mes (DB) = $75/mes

---

## Checklist Final

Antes de considerar el deployment completo:

- [ ] Base de datos creada y conectada
- [ ] Migraciones ejecutadas
- [ ] Variables de entorno configuradas
- [ ] Stripe en modo producción
- [ ] SMTP real configurado
- [ ] SSL activo (HTTPS)
- [ ] Dominios configurados
- [ ] Health checks funcionando
- [ ] Webhooks de Stripe configurados
- [ ] Pruebas end-to-end exitosas
- [ ] Monitorización activa
- [ ] Backups configurados
- [ ] Documentación actualizada

---

**¡Deployment completado!** 🚀

Para soporte adicional, consulta la documentación de cada plataforma:
- [Railway Docs](https://docs.railway.app)
- [Render Docs](https://render.com/docs)
- [Heroku Docs](https://devcenter.heroku.com)
