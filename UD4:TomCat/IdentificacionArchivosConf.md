# Configuración de Apache Tomcat
## Archivos clave y mapa visual de dependencias

En Apache Tomcat, varios archivos ubicados en el directorio `conf/` controlan el
funcionamiento del servidor, la seguridad y el comportamiento de las aplicaciones web.

---

## 1. server.xml

### Función
Configura la **infraestructura interna del servidor Tomcat**.
Define cómo Tomcat escucha peticiones y gestiona las conexiones.

### Qué se puede configurar
- Puertos del servidor
- Conectores (HTTP, HTTPS, AJP)
- Protocolos de comunicación
- SSL / TLS (certificados)
- Rendimiento (hilos, timeouts)

> ⚠️ Un error en este archivo puede impedir que Tomcat arranque.

---

## 2. web.xml

### Función
Archivo de **configuración web global por defecto** para todas las aplicaciones.

### Qué se puede configurar
- Servlets por defecto
- Filtros (encoding, seguridad)
- Mapeo de URLs
- Gestión de sesiones
- Páginas de error
- Archivos de bienvenida

> Cada aplicación puede sobrescribirlo con su propio `WEB-INF/web.xml`.

---

## 3. tomcat-users.xml

### Función
Gestiona los **usuarios y roles internos de Tomcat**.

### Qué se puede configurar
- Usuarios
- Contraseñas
- Roles
- Asignación usuario–rol

Se utiliza principalmente para:
- Tomcat Manager
- Host Manager

> ❌ No recomendado para entornos de producción.

---

## 4. context.xml

### Función
Define el **contexto global por defecto** para las aplicaciones web.

### Qué se puede configurar
- DataSources (JDBC)
- Recursos JNDI
- Pools de conexiones
- Parámetros comunes

> Puede sobrescribirse con `META-INF/context.xml` en cada aplicación.

---

## Mapa visual de dependencias
                     ┌─────────────────────────┐
                     │      server.xml         │
                     │  Infraestructura        │
                     │  - Puertos              │
                     │  - Conectores           │
                     │  - SSL / HTTPS          │
                     └───────────┬─────────────┘
                                 │
                                 ▼
                ┌─────────────────────────────────┐
                │            TOMCAT               │
                │        (Servidor Web)           │
                └───────────┬───────────┬─────────┘
                            │           │
                            │           │
    ┌───────────────────────▼───┐   ┌───▼───────────────────────┐
    │        web.xml            │   │     tomcat-users.xml      │
    │ Configuración web global  │   │ Usuarios y roles          │
    │ - Servlets                │   │ - Usuarios                │
    │ - Filtros                 │   │ - Contraseñas             │
    │ - Sesiones                │   │ - Roles                   │
    │ - Páginas de error        │   └─────────────┬─────────────┘
    └───────────────┬──────────┘                 │
                    │                            │
                    ▼                            ▼
    ┌────────────────────────────────────────────────────┐
    │                Aplicaciones Web                    │
    │                                                    │
    │  WEB-INF/web.xml        META-INF/context.xml       │
    │  (config propia)        (recursos propios)         │
    └───────────────┬───────────────────────┬──────────┘
                    │                       │
                    ▼                       ▼
          ┌───────────────────┐   ┌─────────────────────────┐
          │    context.xml    │   │   Recursos compartidos  │
          │ Contexto global   │   │ - JDBC                  │
          │ - DataSources     │   │ - JNDI                  │
          │ - Pools           │   │ - Pools de conexión     │
          └───────────────────┘   └─────────────────────────┘


