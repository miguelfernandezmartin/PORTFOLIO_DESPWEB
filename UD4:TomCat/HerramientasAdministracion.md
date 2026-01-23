# Tomcat: Herramientas de Administración — Manager y Host Manager

## 1. Acceso a las Interfaces de Administración

### 1.1 Acceso a Tomcat Manager

URL: https://localhost:8443/manager/html 

Credenciales:
- Usuario con rol `manager-gui`

---

### 1.2 Acceso a Host Manager

URL: https://localhost:8443/host-manager/html 

Credenciales:
- Usuario con rol `admin-gui`

---

## 2. Herramienta Tomcat Manager

### Descripción
Tomcat Manager es una aplicación web que permite administrar las aplicaciones desplegadas en el servidor Tomcat sin necesidad de reiniciarlo.

### Funciones Principales
- Despliegue de aplicaciones web (.war)
- Recarga de aplicaciones
- Parada e inicio de aplicaciones
- Eliminación de aplicaciones
- Visualización de sesiones activas

### Uso Principal
Administración y mantenimiento de aplicaciones web durante el desarrollo y producción.

---

## 3. Herramienta Host Manager

### Descripción
Host Manager es una herramienta de administración utilizada para gestionar hosts virtuales en Tomcat.

### Funciones Principales
- Creación de hosts virtuales
- Eliminación de hosts
- Configuración de dominios
- Gestión de rutas de aplicaciones por host

### Uso Principal
Administración de múltiples dominios o entornos en un server

---

## 4. Fichas Descriptivas

### Ficha: Tomcat Manager
- Tipo: Herramienta de administración de aplicaciones
- Función principal: Gestión de aplicaciones web
- Acceso: /manager/html
- Operaciones clave: Desplegar, recargar, iniciar y detener aplicaciones

---

### Ficha: Host Manager
- Tipo: Herramienta de administración de hosts virtuales
- Función principal: Gestión de dominios y hosts
- Acceso: /host-manager/html
- Operaciones clave: Crear y eliminar hosts virtuales

---

## 5. Conclusión

Las herramientas Manager y Host Manager permiten administrar de forma eficiente aplicaciones y hosts en Apache Tomcat 10, facilitando el despliegue, mantenimiento y organización de entornos web.


