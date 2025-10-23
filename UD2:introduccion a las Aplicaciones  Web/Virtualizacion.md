# INSTALACIÓN DOCKER DESKTOP EN UBUNTU

## Escritorio ubuntu desktop
![Actualización de repositorios](imagenes/cap1.png)  

## Actualiza repositorios

![Actualización de repositorios](imagenes/cap2.png)  
Se actualizan los paquetes del sistema para asegurar versiones recientes.

---

## INSTALAR DEPENDENCIAS NECESARIAS

![Instalación de dependencias](imagenes/cap3.png)  
Se instalan herramientas necesarias como `curl` y certificados.

---

## AGREGAR CLAVE GPG DE DOCKER

![Agregar clave GPG](imagenes/cap4.png)  
Se descarga y guarda la clave GPG para verificar la autenticidad de Docker.

---

## AGREGAR REPOSITORIO OFICIAL DE DOCKER

![Agregar repositorio Docker](imagenes/cap5.png)  
Se añade el repositorio oficial de Docker a las fuentes de APT.

---

## INSTALAR DOCKER

![Inicio de instalación de Docker](imagenes/cap6.png)  
Se inicia la instalación de Docker y sus componentes principales.

---

## VERIFICAR LA INSTALACIÓN

![Instalación en progreso](imagenes/cap7.png)  
Docker se descarga desde el repositorio y se instala en el sistema.

---

## PROBAR DOCKER CON UNA IMAGEN DE PRUEBA

![Instalación finalizada](imagenes/cap8.png)  
La instalación se completa sin errores y Docker queda listo para usarse.

---

# INSTALACIÓN DE CONTENEDORES EN SERVIDOR WEB

## BUSCAR IMÁGENES DISPONIBLES

![Buscar imagen nginx](imagenes/cap9.png)  
Se buscan imágenes relacionadas con Nginx en Docker Hub.

![Buscar imagen tomcat](imagenes/cap10.png)  
Se buscan imágenes relacionadas con Tomcat en Docker Hub.

---

## DESCARGAR E INICIAR CONTENEDORES

![Ejecutar contenedor Tomcat](imagenes/cap11.png)  
Se descarga y lanza un contenedor Tomcat en segundo plano.

![Ejecutar contenedor Nginx](imagenes/cap12.png)  
Se descarga y lanza un contenedor Nginx en segundo plano.

---

## VERIFICAR CONTENEDORES ACTIVOS

![Contenedores activos](imagenes/cap13.png)  
Se listan los contenedores en ejecución y sus puertos asignados.

---

## ABRIR EN EL NAVEGADOR

![Página de bienvenida Nginx](imagenes/cap14.png)  
Se accede al contenedor Nginx desde el navegador y muestra la página por defecto.

![Error 404 en Tomcat](imagenes/cap15.png)  
Se accede al contenedor Tomcat, pero no hay contenido desplegado aún.



## Requerimientos Mínimos para Implantar una Aplicación Web

### Requisitos de Hardware y Software 

#### **Hardware (Servidor)**
 **CPU**  2 núcleos.  
 **RAM**  4 GB.  
 **Almacenamiento**  100 GB SSD.  

#### **Software**
* **Sistema Operativo:** Linux (ej. Ubuntu Server).
* **Lenguaje/Runtime:** Versión estable requerida (ej. Node.js, PHP, Python).
* **Base de Datos:** SGBD adecuado (ej. MySQL, PostgreSQL).

***

### Infraestructura de Red 

* **Direccionamiento:** IP pública estática.
* **DNS:** Configuración del registro 'A' al servidor.
* **Firewall:** Apertura de puertos esenciales (80/HTTP y 443/HTTPS).
* **Opcional/Recomendado:** Uso de CDN (Content Delivery Network).

***

### Configuración del Servidor Web y de Aplicaciones 

* **Servidor Web:** Software (ej. Nginx o Apache) para servir contenido.
* **Virtual Hosts:** Configuración para el dominio específico.
* **Proxy Inverso:** Configuración para conectar el Servidor Web con el Servidor de Aplicaciones (donde corre la lógica).

***

### Seguridad y Mantenimiento 

#### **Seguridad**
* **Cifrado:** Certificado **SSL/TLS** (HTTPS) obligatorio.
* **Parches:** Aplicación constante de parches de seguridad (SO y software).
* **Defensa:** Uso de Firewall y, preferiblemente, WAF (Web Application Firewall).

#### **Mantenimiento**
* **Backups:** Políticas de copia de seguridad automática (BD y archivos).
* **Monitorización:** Herramientas para vigilar el rendimiento (CPU, RAM, errores).
* **Logs:** Gestión de registros para análisis y detección de fallos.
