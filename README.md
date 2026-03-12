# Hidrosafe

Link de acceso: https://hidrosafe.onrender.com/

Hydrosafe es una plataforma web en la nube orientada al monitoreo de sistemas hidráulicos y al soporte de estrategias de mantenimiento predictivo. La aplicación permite visualizar datos operativos, consultar estados del sistema, revisar históricos, gestionar notificaciones y administrar usuarios desde un panel web.

## Características

- Monitoreo de variables de sensores en tiempo real.
- Visualización del estado general del sistema hidráulico.
- Consulta de históricos por rango de fechas.
- Gestión de perfil de usuario.
- Sistema de autenticación, registro y recuperación de contraseña.
- Módulo de notificaciones y alertas.
- Panel administrativo para gestión de usuarios, alertas y solicitudes.

## Arquitectura

El proyecto está desarrollado como una aplicación web monolítica con Flask. El backend renderiza plantillas HTML con Jinja2 y también expone endpoints JSON para alimentar dinámicamente el dashboard mediante JavaScript en el cliente.

La autenticación y la persistencia de datos se integran con Firebase. Firebase Authentication se usa para la gestión de usuarios, mientras que Firestore almacena información de perfiles, sensores, condiciones del sistema, notificaciones y solicitudes.

## Tecnologías utilizadas

### Backend
- Python 3.11+
- Flask
- Jinja2
- Firebase Admin SDK
- Firestore
- Gunicorn

### Frontend
- HTML5
- CSS3
- JavaScript
- Chart.js

### Despliegue
- Render, con ejecución productiva mediante Gunicorn usando `app:app`.

## Estructura general del proyecto

|   .env
|   .replit
|   admin.py
|   app.py
|   app.py.bak
|   auth.py
|   generated-icon.png
|   main.py
|   package-lock.json
|   package.json
|   Procfile
|   pyproject.toml
|   README.md
|   replit.nix
|   routes.py
|   uv.lock
|
+---static
|   +---css
|   |       custom.css
|   |
|   \---js
|           dashboard.js
|
\---templates
    |   admin_alerts.html
    |   admin_maintenances.html
    |   admin_manage_users.html
    |   admin_panel.html
    |   admin_reports.html
    |   admin_requests.html
    |   base.html
    |   contact.html
    |   dashboard.html
    |   documentation.html
    |   home.html
    |   notifications.html
    |   profile.html
    |   user_requests.html
    |
    \---auth
            forgot_password.html
            login.html
            register.html


## Módulos principales

app.py
Archivo principal de inicialización de la aplicación. Crea la app Flask, configura la clave secreta, inicializa Firebase y registra los blueprints principales.

auth.py
Gestiona autenticación, registro, cierre de sesión y recuperación de contraseña. También consulta Firestore para asociar el rol del usuario autenticado.

routes.py
Contiene las rutas principales del sistema, incluyendo vistas públicas, perfil, notificaciones, dashboard y endpoints de datos para sensores, estado del sistema e histórico.

admin.py
Centraliza la lógica del panel administrativo, con funciones para gestionar usuarios, alertas y solicitudes.

static/js/dashboard.js
Consume endpoints internos mediante fetch() y actualiza dinámicamente indicadores, estados y tablas históricas en el dashboard.

## Flujo de funcionamiento

- El usuario accede a la plataforma desde la interfaz web.
- Puede registrarse o iniciar sesión mediante el módulo de autenticación.
- Al autenticarse, el sistema guarda en sesión el uid, correo y rol del usuario.
- El dashboard consulta datos desde Firestore a través de endpoints internos del backend.
- Si el usuario tiene rol de administrador, puede acceder a funcionalidades adicionales de gestión.

## Colecciones principales en Firestore

El proyecto utiliza Firestore como base de datos documental. Las colecciones principales incluyen:

- usuarios: información de perfil y rol del usuario.
- sensores: datos recientes de sensores asociados al usuario.
- condiciones: estado del sistema e histórico consultable por fechas.
- notificaciones: alertas y mensajes dirigidos a los usuarios.
- solicitudes: requerimientos o tickets enviados por usuarios.

## Endpoints principales

Vistas
/ → página de inicio.
/dashboard → panel principal del usuario autenticado.
/documentation → documentación general.
/profile → perfil del usuario.
/notifications → notificaciones del usuario.
/contact → página de contacto.

Autenticación

/auth/login
/auth/register
/auth/forgot_password
/auth/logout

API interna
/api/sensor_data → último registro de sensores del usuario.
/api/system_status → último estado del sistema.
/api/history_data → histórico por rango de fechas.
/profile/data → datos del perfil.
/profile/update → actualización de perfil.

Administración
/admin/
/admin/manage_users
/admin/alerts
/admin/requests
/admin/reports
/admin/maintenances

## Seguridad
La aplicación implementa autenticación basada en sesión y control de acceso por rol para restringir las secciones administrativas. Además, las consultas de datos operativos se filtran por el uid del usuario autenticado para separar la información entre cuentas.

Antes de usar la aplicación en un entorno productivo, se recomienda revisar y fortalecer la gestión de sesiones, validación de formularios, autenticación y manejo de secretos.

## Estado del proyecto
Hydrosafe se encuentra orientado al monitoreo web de sistemas hidráulicos con integración de servicios cloud y base documental en Firestore. La base funcional del sistema ya incluye autenticación, visualización de datos, consultas históricas, notificaciones y administración.
