# UniGO - Manual de Uso
## Guía del Usuario - Sistemas Web I 2025

---

## 1. INTRODUCCIÓN

Bienvenido a UniGO, la plataforma de carpooling universitario que conecta a estudiantes para compartir viajes de forma segura y económica.

Este manual te guiará paso a paso en el uso de todas las funcionalidades de la aplicación.

---

## 2. PRIMEROS PASOS

### 2.1 Requisitos del Sistema

- **Navegador web**: Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
- **Conexión a Internet**: Recomendada 2 Mbps o superior
- **Email institucional**: De una universidad española (ugr.es, us.es, uma.es, etc.)

### 2.2 Acceder a la Aplicación

1. Abre tu navegador web
2. Navega a: `http://unigo.app` (o la URL proporcionada)
3. Verás la página principal de UniGO

[CAPTURA: Página principal con logo UniGO y botones de registro/login]

---

## 3. REGISTRO DE USUARIO

### 3.1 Crear una Cuenta

**Paso 1**: En la página principal, haz clic en **"Registrarse"**

[CAPTURA: Botón de registrarse resaltado]

**Paso 2**: Completa el formulario de registro
- **Email institucional**: tu-email@ugr.es
- **Contraseña**: Mínimo 8 caracteres
- **Nombre completo** (opcional)

[CAPTURA: Formulario de registro completado]

**Paso 3**: Haz clic en **"Registrarse"**

✅ **Importante**: Solo se aceptan emails de universidades españolas.

### 3.2 Verificar tu Email

**Paso 1**: Revisa tu bandeja de entrada

Recibirás un email con un código de 6 dígitos:

```
Tu código de verificación es: 123456
Este código expirará en 15 minutos.
```

[CAPTURA: Email de verificación]

**Paso 2**: Introduce el código en la pantalla de verificación

[CAPTURA: Pantalla de verificación con código ingresado]

**Paso 3**: Haz clic en **"Verificar"**

✅ **¡Listo!** Tu cuenta ha sido verificada y puedes iniciar sesión.

### 3.3 ¿No recibiste el código?

- Revisa tu carpeta de **Spam** o **Correo no deseado**
- Haz clic en **"Reenviar código"** para recibir uno nuevo
- Verifica que tu email esté escrito correctamente

---

## 4. INICIAR SESIÓN

**Paso 1**: En la página principal, haz clic en **"Iniciar Sesión"**

**Paso 2**: Introduce tus credenciales
- **Email**: tu-email@ugr.es
- **Contraseña**: Tu contraseña

[CAPTURA: Formulario de login]

**Paso 3**: Haz clic en **"Iniciar Sesión"**

✅ Serás redirigido al **Dashboard Principal**

---

## 5. DASHBOARD PRINCIPAL

El dashboard es tu página de inicio después de iniciar sesión.

[CAPTURA: Dashboard completo]

### 5.1 Elementos del Dashboard

1. **Barra de navegación**
   - Logo UniGO (volver al inicio)
   - Enlaces: Inicio, Buscar, Mis Viajes
   - Notificaciones (🔔)
   - Perfil de usuario

2. **Buscador rápido**
   - Origen
   - Destino
   - Fecha
   - Botón "Buscar"

3. **Viajes disponibles**
   - Lista de viajes recientes
   - Información del conductor
   - Precio y plazas disponibles

4. **Mis próximos viajes**
   - Viajes donde eres conductor o pasajero
   - Estado de cada viaje

5. **Botón "Crear Viaje"**
   - Para publicar un nuevo viaje

---

## 6. BUSCAR VIAJES

### 6.1 Búsqueda Rápida

**Desde el Dashboard:**

**Paso 1**: Completa el formulario de búsqueda
- **Origen**: Granada
- **Destino**: Madrid
- **Fecha**: 15/12/2025

[CAPTURA: Formulario de búsqueda completado]

**Paso 2**: Haz clic en **"Buscar"**

**Paso 3**: Verás la lista de viajes disponibles

[CAPTURA: Resultados de búsqueda]

### 6.2 Información de cada Viaje

Cada viaje muestra:
- 📍 **Origen → Destino**
- 📅 **Fecha y hora**
- 💰 **Precio por plaza**
- 👤 **Conductor**: Nombre y valoración (⭐)
- 💺 **Plazas disponibles**
- **Botón "Ver detalles"**

---

## 7. DETALLE DE VIAJE Y RESERVAR

### 7.1 Ver Información Completa

**Paso 1**: Haz clic en **"Ver detalles"** de un viaje

[CAPTURA: Página de detalle de viaje]

Verás:
- Información completa del viaje
- Direcciones exactas de salida y llegada
- Duración estimada
- Descripción del conductor
- Perfil del conductor con valoración
- Condiciones del viaje

### 7.2 Solicitar Reserva

**Paso 1**: Revisa toda la información

**Paso 2**: Si el viaje te conviene, haz clic en **"Reservar Plaza"**

[CAPTURA: Botón de reservar resaltado]

**Paso 3**: Confirma el número de plazas (generalmente 1)

**Paso 4**: **Guardar método de pago** (si es tu primera reserva)

[CAPTURA: Formulario de Stripe para guardar tarjeta]

- Introduce tu número de tarjeta
- Fecha de vencimiento
- CVC
- Código postal

✅ **Seguridad**: Los pagos están procesados por Stripe, líder mundial en pagos seguros. UniGO nunca ve ni almacena los datos completos de tu tarjeta.

**Paso 5**: Haz clic en **"Guardar y Reservar"**

✅ **¡Reserva enviada!** El conductor recibirá una notificación y podrá aceptar o rechazar tu solicitud.

### 7.3 Estados de una Reserva

- 🟡 **Pendiente**: Esperando respuesta del conductor
- 🟢 **Confirmada**: El conductor aceptó tu reserva
- 🔴 **Rechazada**: El conductor rechazó tu solicitud
- ⚫ **Cancelada**: La reserva fue cancelada
- ✅ **Completada**: El viaje finalizó con éxito

---

## 8. CREAR UN VIAJE (Como Conductor)

### 8.1 Publicar Nuevo Viaje

**Paso 1**: Haz clic en **"+ Crear Viaje"** (botón superior derecha)

[CAPTURA: Botón crear viaje]

**Paso 2**: Completa el formulario

[CAPTURA: Formulario de creación de viaje]

**Campos obligatorios**:
- 📍 **Ciudad de origen**: Granada
- 🏁 **Ciudad de destino**: Madrid
- 📅 **Fecha**: 15/12/2025
- ⏰ **Hora de salida**: 10:00
- 💺 **Número de plazas**: 3
- 💰 **Precio por plaza**: 12.00 €

**Campos opcionales**:
- 📝 **Descripción**: "Viaje directo sin paradas. Salida puntual desde el campus."
- 📍 **Dirección exacta de salida**
- 🏁 **Dirección exacta de llegada**

**Paso 3**: Haz clic en **"Publicar Viaje"**

✅ **¡Viaje publicado!** Aparecerá en las búsquedas y empezarás a recibir solicitudes de reserva.

---

## 9. GESTIONAR SOLICITUDES (Como Conductor)

### 9.1 Ver Solicitudes Pendientes

**Opción 1**: Haz clic en el icono de notificaciones (🔔)
- Verás el número de solicitudes pendientes

**Opción 2**: Ve a **"Solicitudes"** en el menú

[CAPTURA: Página de solicitudes pendientes]

### 9.2 Aceptar o Rechazar Solicitudes

Para cada solicitud verás:
- 👤 **Nombre del pasajero**
- ⭐ **Valoración** (número de viajes y estrellas)
- 📝 **Mensaje** del pasajero (si hay)
- 💺 **Plazas solicitadas**
- Botones: **"✅ Aceptar"** y **"❌ Rechazar"**

[CAPTURA: Tarjeta de solicitud con botones]

#### Aceptar una Solicitud

**Paso 1**: Revisa el perfil del pasajero (haz clic en "Ver perfil")

**Paso 2**: Haz clic en **"✅ Aceptar"**

**Paso 3**: El sistema:
- Confirma la reserva
- El pago ya está autorizado (creado al hacer la reserva)
- Descuenta las plazas disponibles
- Actualiza asientos: X/Y disponibles

✅ **El pasajero aparecerá en tu lista** y podrás chatear con él en el chat grupal del viaje.

#### Rechazar una Solicitud

**Paso 1**: Haz clic en **"❌ Rechazar"**

**Paso 2**: (Opcional) Añade un motivo

**Paso 3**: El pasajero recibirá una notificación

---

## 10. CHAT EN TIEMPO REAL

### 10.1 Acceder al Chat

**Opción 1**: Desde **"Mis Viajes"**, haz clic en **"Ver chat"**

**Opción 2**: Desde notificaciones, haz clic en un mensaje no leído

[CAPTURA: Interfaz de chat]

### 10.2 Enviar Mensajes

**Paso 1**: Escribe tu mensaje en el cuadro inferior

**Paso 2**: Haz clic en **"➤"** o presiona **Enter**

✅ **El mensaje se envía instantáneamente** gracias a WebSockets

### 10.3 Funcionalidades del Chat

- ✅ **Mensajes en tiempo real**: Sin necesidad de recargar
- 👁️ **Indicador de lectura**: Doble check (✓✓) cuando el otro usuario lee
- ⌨️ **Indicador de escritura**: "Usuario está escribiendo..."
- 🔔 **Notificaciones**: Banner superior cuando hay mensajes nuevos
- 📝 **Historial**: Todos los mensajes se guardan

### 10.4 Buenas Prácticas en el Chat

- 🙂 Sé amable y respetuoso
- 📞 Intercambia teléfonos para emergencias el día del viaje
- 📍 Confirma el punto exacto de encuentro
- ⏰ Avisa si vas a llegar tarde
- 🚫 No compartas información sensible (dirección de casa, etc.)

---

## 11. VER PASAJEROS (Como Conductor)

### 11.1 Lista de Pasajeros Confirmados

**Paso 1**: Ve a **"Mis Viajes"**

**Paso 2**: Selecciona un viaje donde eres conductor

**Paso 3**: Haz clic en **"Ver pasajeros"**

[CAPTURA: Lista de pasajeros]

Para cada pasajero verás:
- 👤 **Nombre**
- ⭐ **Valoración**
- 💺 **Plazas reservadas**
- 📱 **Teléfono** (si lo compartió)
- 💬 **Botón de chat**

---

## 12. COMPLETAR UN VIAJE (Como Conductor)

### 12.1 Marcar Viaje como Completado

**Cuándo**: Después de que el viaje haya finalizado exitosamente

**Paso 1**: Ve a **"Mis Viajes"**

**Paso 2**: Selecciona el viaje a completar

**Paso 3**: Haz clic en **"✅ Completar Viaje"**

[CAPTURA: Botón completar viaje]

**Paso 4**: Confirma la acción

✅ **El sistema automáticamente**:
1. Captura los pagos de todos los pasajeros
2. Aplica la comisión de UniGO (15%)
3. Transfiere el 85% a tu cuenta Stripe
4. Actualiza el estado del viaje a "Completado"
5. Habilita valoraciones mutuas

### 12.2 Recibir el Pago

Los fondos llegarán a tu cuenta Stripe Connect:
- **Tiempo**: 2-5 días hábiles
- **Comisión UniGO**: 15%
- **Recibes**: 85% del precio total

**Ejemplo**:
- 3 pasajeros × 12€ = 36€ total
- Comisión UniGO (15%): 5.40€
- Recibes: 30.60€

---

## 13. CANCELACIONES

### 13.1 Cancelar una Reserva (Como Pasajero)

**Paso 1**: Ve a **"Mis Reservas"**

**Paso 2**: Selecciona la reserva a cancelar

**Paso 3**: Haz clic en **"Cancelar Reserva"**

[CAPTURA: Botón cancelar con advertencia]

**Paso 4**: Lee las condiciones de cancelación:

**Penalizaciones según tiempo**:
- ✅ **24 horas o más antes**: 0% penalización (reembolso 100%)
- ⚠️ **Menos de 24 horas antes**: 30% penalización (reembolso 70%)

**Nota**: Las tarifas de Stripe se deducen automáticamente del reembolso.

**Paso 5**: Confirma la cancelación

✅ El sistema procesará el reembolso automáticamente:
- Cancela el PaymentIntent en Stripe
- Libera el asiento para otros pasajeros
- Notifica al conductor

### 13.2 Eliminar un Viaje (Como Conductor)

**Paso 1**: Ve a **"Mis Viajes"**

**Paso 2**: Selecciona el viaje a eliminar

**Paso 3**: Haz clic en **"Eliminar Viaje"**

⚠️ **Advertencia**: Solo puedes eliminar viajes sin pasajeros aceptados.

**Paso 4**: Confirma la eliminación

✅ El viaje desaparecerá de las búsquedas
- Aplica la penalización si corresponde
- Notifica a todos los afectados

---

## 14. VALORACIONES

### 14.1 Valorar a un Usuario

**Cuándo**: Después de que un viaje se marque como "Completado"

**Paso 1**: Accede a **"Valorar"** desde:
- Notificaciones
- Detalle del viaje completado

[CAPTURA: Formulario de valoración]

**Paso 2**: Asigna estrellas (1-5)
- ⭐ Muy mala experiencia
- ⭐⭐ Mala experiencia
- ⭐⭐⭐ Experiencia aceptable
- ⭐⭐⭐⭐ Buena experiencia
- ⭐⭐⭐⭐⭐ Excelente experiencia

**Paso 3**: (Opcional) Añade un comentario
- Sé honesto pero respetuoso
- Menciona aspectos positivos y negativos
- Máximo 500 caracteres

**Paso 4**: Haz clic en **"Enviar Valoración"**

✅ La valoración se añadirá al perfil del usuario.

### 14.2 Importancia de las Valoraciones

- 📈 **Reputación**: Usuarios con mejor valoración reciben más solicitudes
- 🔒 **Confianza**: Ayudan a crear una comunidad segura
- 🎯 **Decisión informada**: Los usuarios pueden elegir con quién viajar
- 🏆 **Incentivo**: Fomenta el buen comportamiento

---

## 15. PERFIL DE USUARIO

### 15.1 Ver Mi Perfil

**Paso 1**: Haz clic en tu icono de usuario (esquina superior derecha)

**Paso 2**: Selecciona **"Mi Perfil"**

[CAPTURA: Página de perfil]

Tu perfil muestra:
- 📸 **Avatar** (foto de perfil)
- 📧 **Email** institucional
- ✅ **Estado de verificación**
- ⭐ **Valoración promedio**
- 📊 **Estadísticas**: Viajes completados, cancelados, etc.
- 💬 **Biografía**
- 🚗 **Preferencias** de viaje

### 15.2 Editar Perfil

**Paso 1**: En tu perfil, haz clic en **"✏️ Editar"**

[CAPTURA: Formulario de edición]

**Campos editables**:
- 📸 **Avatar**: Subir foto (máx 5MB)
- 📝 **Nombre completo**
- 📱 **Teléfono**
- 📄 **Biografía**: Cuéntale a otros sobre ti
- 🚗 **Preferencias**: Música, conversación, mascotas, etc.

**Paso 2**: Haz los cambios deseados

**Paso 3**: Haz clic en **"Guardar Cambios"**

✅ Tu perfil se actualizará y será visible para otros usuarios.

### 15.3 Subir un Avatar

**Paso 1**: En editar perfil, haz clic en **"📸 Subir foto"**

**Paso 2**: Selecciona una imagen de tu dispositivo
- Formatos permitidos: JPG, PNG
- Tamaño máximo: 5MB
- Recomendado: 400×400 px

**Paso 3**: La imagen se sube automáticamente

✅ **Tip**: Usa una foto clara de tu rostro para generar confianza.

---

## 16. CHAT EN TIEMPO REAL

### 16.1 Acceder al Chat de Viaje

El chat grupal está disponible cuando:
- **Conductores**: Al menos 1 pasajero aceptado en tu viaje
- **Pasajeros**: Tu reserva ha sido aceptada (estado ACCEPTED)

**Paso 1**: Ve a **"Mis Viajes"**

**Paso 2**: Localiza el viaje activo

**Paso 3**: Haz clic en el botón **"💬 Chat"**

[CAPTURA: Botón de chat en tarjeta de viaje]

### 16.2 Enviar Mensajes

**Paso 1**: Escribe tu mensaje en el campo de texto

**Paso 2**: Haz clic en **"Enviar"** o presiona Enter

**Paso 3**: El mensaje aparecerá instantáneamente para todos los participantes

[CAPTURA: Interfaz de chat con mensajes]

✅ **Nota**: Los mensajes se envían en tiempo real con WebSocket. Si falla la conexión, se usará HTTP automáticamente.

### 16.3 Participantes del Chat

El chat grupal incluye:
- 🚗 **Conductor del viaje**
- 👥 **Todos los pasajeros con estado ACCEPTED**

⚠️ Los pasajeros con reservas PENDING o REJECTED no tienen acceso al chat.

---

## 17. CONFIGURACIÓN

### 17.1 Cambiar Contraseña

**Paso 1**: Ve a **"Configuración"** en el menú

**Paso 2**: Selecciona **"Cambiar contraseña"**

**Paso 3**: Introduce:
- Contraseña actual
- Nueva contraseña (mínimo 8 caracteres)
- Confirmar nueva contraseña

**Paso 4**: Haz clic en **"Actualizar Contraseña"**

✅ Tu contraseña se actualizará y se cerrará la sesión en todos los dispositivos.

### 17.2 Cuenta Stripe Connect (Conductores)

**Para recibir pagos como conductor**:

**Paso 1**: Ve a **"Mi Perfil"**

**Paso 2**: En la sección de pagos, haz clic en **"Configurar Cuenta Stripe"**

**Paso 3**: Completa el formulario de Stripe con:
- Información personal
- Datos bancarios (IBAN)
- Verificación de identidad

**Paso 4**: Stripe verificará tu cuenta (1-2 días)

✅ **Importante**: Debes completar este paso para recibir pagos automáticos al completar viajes.

---

## 18. CONSEJOS DE SEGURIDAD

### 18.1 Antes del Viaje

✅ **Verifica el perfil**: Revisa valoraciones y comentarios  
✅ **Usa el chat**: Comunícate antes del viaje  
✅ **Confirma detalles**: Punto de encuentro, hora exacta  
✅ **Comparte tu viaje**: Dile a un amigo o familiar  
✅ **Revisa la matrícula**: Pide la matrícula del coche (conductores)

### 18.2 Durante el Viaje

✅ **Respeta las normas**: Puntualidad, no fumar si no está permitido  
✅ **Sé educado**: Trata a los demás con respeto  
✅ **Comunica problemas**: Usa el chat si hay cambios  
✅ **Emergencias**: Llama al 112 si hay algún problema grave

### 18.3 Después del Viaje

✅ **Valora honestamente**: Ayuda a otros con tu experiencia  
✅ **Reporta problemas**: Contacta soporte si hubo incidentes  
✅ **Mantén la comunicación**: Hasta confirmar que todo está bien

---

## 19. SOLUCIÓN DE PROBLEMAS

### 19.1 No recibo emails

**Problema**: No llega el código de verificación o notificaciones

**Soluciones**:
1. Revisa la carpeta de **Spam**
2. Añade `noreply@unigo.app` a tus contactos
3. Verifica que tu email esté escrito correctamente
4. Haz clic en **"Reenviar código"**
5. Contacta soporte si persiste

### 19.2 Error al guardar tarjeta

**Problema**: Error al intentar guardar método de pago

**Soluciones**:
1. Verifica que los datos de la tarjeta sean correctos
2. Asegúrate de que la tarjeta esté activa
3. Intenta con otra tarjeta
4. Contacta a tu banco si fue rechazada
5. Si usas tarjetas de prueba (testing), usa: `4242 4242 4242 4242`

### 19.3 El chat no funciona

**Problema**: Los mensajes no se envían en tiempo real

**Soluciones**:
1. Verifica tu conexión a Internet
2. Recarga la página (F5 o Ctrl+R)
3. Cierra sesión y vuelve a iniciar
4. Prueba con otro navegador
5. Limpia caché y cookies

### 19.4 No puedo ver un viaje

**Problema**: Error 404 o viaje no encontrado

**Causas**:
- El viaje fue cancelado por el conductor
- El viaje ya pasó y fue completado
- No tienes permiso para ver ese viaje
- Error temporal del servidor

**Solución**: Intenta buscar viajes similares

---

## 20. PREGUNTAS FRECUENTES (FAQ)

### 20.1 Sobre Pagos

**¿Cuándo se cobra mi tarjeta?**
- Al hacer una reserva, NO se cobra inmediatamente
- Se retiene el dinero (autorización)
- Solo se cobra cuando el conductor marca el viaje como "Completado"

**¿Cuánto cobra UniGO?**
- 15% de comisión sobre cada viaje
- Los conductores reciben el 85%

**¿Es seguro guardar mi tarjeta?**
- Sí, usamos Stripe, líder mundial en pagos
- UniGO nunca ve los datos completos de tu tarjeta
- Cumple con PCI-DSS

### 20.2 Sobre Cancelaciones

**¿Puedo cancelar gratis?**
- Sí, si cancelas con más de 24 horas de antelación
- Menos de 24h: penalizaciones según tabla (ver sección 13)

**¿Qué pasa si el conductor cancela?**
- Recibes reembolso completo
- Si fue con menos de 24h, el conductor paga penalización
- Se te notifica por email y app

### 20.3 Sobre el Chat

**¿El chat es privado?**
- Sí, solo tú y la otra persona pueden ver los mensajes
- UniGO puede acceder para moderación si se reporta abuso

**¿Se guardan los mensajes?**
- Sí, todo el historial se guarda
- Puedes acceder en cualquier momento

### 20.4 Sobre Valoraciones

**¿Puedo cambiar mi valoración?**
- No, una vez enviada no se puede modificar
- Piensa bien antes de valorar

**¿Las valoraciones son anónimas?**
- No, la otra persona verá tu nombre
- Las valoraciones son públicas

---

## 21. SOPORTE Y CONTACTO

### 21.1 Obtener Ayuda

**Opciones de soporte**:

📧 **Email**: soporte@unigo.app  
⏰ **Horario**: Lunes a Viernes, 9:00 - 18:00  
📱 **WhatsApp**: +34 XXX XXX XXX  
💬 **Chat en vivo**: Disponible en la app (esquina inferior derecha)

### 21.2 Reportar un Problema

**Para reportar**:
1. Haz clic en **"Ayuda"** en el menú
2. Selecciona **"Reportar problema"**
3. Describe el problema con detalle
4. Adjunta capturas si es posible
5. Envía el reporte

✅ Responderemos en un máximo de 24 horas.

### 21.3 Reportar un Usuario

**Si experimentas**:
- Comportamiento inapropiado
- Fraude o estafa
- Acoso o discriminación
- Violación de términos de uso

**Pasos**:
1. Ve al perfil del usuario
2. Haz clic en **"⚠️ Reportar"**
3. Selecciona el motivo
4. Describe los hechos
5. Adjunta evidencia (capturas de chat, etc.)
6. Envía el reporte

🔒 **Confidencialidad**: Los reportes son confidenciales. El usuario reportado no sabrá quién hizo el reporte.

---

## 22. TÉRMINOS Y CONDICIONES

Por el uso de UniGO, aceptas:

- Usar la plataforma de forma responsable
- Proporcionar información veraz
- Respetar a otros usuarios
- Cumplir con las leyes de tráfico
- Ser puntual en los viajes
- Pagar las tarifas correspondientes

**Descarga los términos completos**: [Ver términos y condiciones]

---

## 23. CONCLUSIÓN

¡Gracias por usar UniGO! 🎓🚗

Esperamos que esta guía te haya ayudado a entender todas las funcionalidades de la plataforma.

**Recuerda**:
- Sé puntual ⏰
- Sé respetuoso 🙂
- Valora honestamente ⭐
- Comunica claramente 💬
- ¡Disfruta del viaje! 🚗

---

**¡Buen viaje!** 🎉

---

## ANEXO: CAPTURAS DE PANTALLA

*Nota: En la versión PDF final, aquí se incluirían capturas reales de:*

1. Página principal
2. Formulario de registro
3. Verificación de email
4. Dashboard principal
5. Búsqueda de viajes
6. Detalle de viaje
7. Interfaz de chat
8. Solicitudes pendientes
9. Perfil de usuario
10. Formulario crear viaje
11. Vista de pasajeros
12. Notificaciones
13. Configuración
14. Vista móvil (responsive)

---

**Fecha de elaboración**: 04 de Diciembre de 2025  
**Versión del documento**: 2.0  
**Asignatura**: Sistemas Web I  
**Curso**: 2024-2025
