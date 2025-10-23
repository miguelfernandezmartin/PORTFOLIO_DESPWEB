

## Requerimientos Mínimos para Implantar una Aplicación Web

### Requisitos de Hardware y Software 💻

#### **Hardware (Servidor)**
 **CPU**  2 núcleos.  
 **RAM**  4 GB.  
 **Almacenamiento**  100 GB SSD.  

#### **Software**
* **Sistema Operativo:** Linux (ej. Ubuntu Server).
* **Lenguaje/Runtime:** Versión estable requerida (ej. Node.js, PHP, Python).
* **Base de Datos:** SGBD adecuado (ej. MySQL, PostgreSQL).

***

### Infraestructura de Red 🌐

* **Direccionamiento:** IP pública estática.
* **DNS:** Configuración del registro 'A' al servidor.
* **Firewall:** Apertura de puertos esenciales (80/HTTP y 443/HTTPS).
* **Opcional/Recomendado:** Uso de CDN (Content Delivery Network).

***

### Configuración del Servidor Web y de Aplicaciones ⚙️

* **Servidor Web:** Software (ej. Nginx o Apache) para servir contenido.
* **Virtual Hosts:** Configuración para el dominio específico.
* **Proxy Inverso:** Configuración para conectar el Servidor Web con el Servidor de Aplicaciones (donde corre la lógica).

***

### Seguridad y Mantenimiento 🛡️

#### **Seguridad**
* **Cifrado:** Certificado **SSL/TLS** (HTTPS) obligatorio.
* **Parches:** Aplicación constante de parches de seguridad (SO y software).
* **Defensa:** Uso de Firewall y, preferiblemente, WAF (Web Application Firewall).

#### **Mantenimiento**
* **Backups:** Políticas de copia de seguridad automática (BD y archivos).
* **Monitorización:** Herramientas para vigilar el rendimiento (CPU, RAM, errores).
* **Logs:** Gestión de registros para análisis y detección de fallos.
