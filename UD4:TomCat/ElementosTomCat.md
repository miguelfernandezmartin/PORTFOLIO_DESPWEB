# Componentes y Funcionamiento de Apache Tomcat
![img](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD4%3ATomCat/tomCat.webp)

## Componentes principales de Tomcat

### 1. Catalina
- Es el **contenedor de servlets** de Tomcat.
- Implementa la especificación **Jakarta Servlet** y **Jakarta JSP**.
- Administra aplicaciones web, sesiones, seguridad y manejo de servlets.

### 2. Coyote
- Es el **conector HTTP** de Tomcat.
- Recibe peticiones HTTP y las convierte en objetos Request/Response.
- Soporta otros protocolos como AJP.

### 3. Jasper
- Es el **motor de JSP** de Tomcat.
- Compila archivos JSP en servlets Java.
- Gestiona recompilación cuando un JSP cambia.

### 4. Manager y Host Manager

#### Manager
- Administra aplicaciones web: deploy, recargar, iniciar/detener y eliminar.

#### Host Manager
- Gestiona **virtual hosts** en Tomcat.

---

## Estructura básica de directorios
![img](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD4%3ATomCat/arbolTomCat.png)


---

## Flujo interno de funcionamiento

### 1. Recepción de la petición
- Coyote recibe la solicitud HTTP.

### 2. Procesamiento en el contenedor
- Coyote crea Request/Response y los envía a Catalina.
- Catalina identifica host, aplicación y servlet.

### 3. Ejecución del servlet
- Jasper compila JSP cuando corresponde.

### 4. Generación de la respuesta
- Catalina envía el resultado a Coyote.
- Coyote responde al cliente.

### 5. Despliegue de aplicaciones
- Tomcat detecta .war o carpetas dentro de `webapps/`.

