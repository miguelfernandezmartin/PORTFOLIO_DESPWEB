# Instalación y uso de Docker en Ubuntu
#### Miguel Fernández Martín

### Introducción
Docker es una herramienta que permite crear, desplegar y ejecutar aplicaciones dentro de contenedores. En este informe veremos cómo instalar Docker Desktop en Ubuntu, cómo ejecutar contenedores web y verificar su funcionamiento.

### 1. Instalación de Docker Desktop en Ubuntu
Para comenzar, debemos actualizar los repositorios e instalar las dependencias necesarias.

```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg
```

![instalacion docker](imagenesVirt/imagen1.png)

A continuación, agregamos la clave GPG de Docker:

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

![clave gpg](imagenesVirt/imagen2.png)

Ahora configuramos el repositorio oficial de Docker:

```bash
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc]   https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
```

![repositorio docker](imagenesVirt/imagen3.png)

Instalamos Docker con el siguiente comando:

```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

![instalacion completa](imagenesVirt/imagen4.png)

### 2. Verificar la instalación
Comprobamos que Docker se está ejecutando correctamente:

```bash
sudo systemctl status docker
```

![estado docker](imagenesVirt/imagen5.png)

Podemos probar la instalación ejecutando una imagen de prueba:

```bash
sudo docker run hello-world
```

![docker hello world](imagenesVirt/imagen6.png)

### 3. Instalación de contenedores web
#### Buscar imágenes disponibles

Podemos buscar imágenes oficiales desde Docker Hub, por ejemplo, Nginx:

```bash
docker search nginx
```

![busqueda nginx](imagenesVirt/imagen7.png)

#### Descargar e iniciar contenedores

Ejecutamos el contenedor Nginx:

```bash
docker run -d -p 8080:80 --name webserver nginx
```

![nginx corriendo](imagenesVirt/imagen8.png)

También podemos ejecutar Tomcat:

```bash
docker run -d -p 8081:8080 --name appserver tomcat
```

![tomcat corriendo](imagenesVirt/imagen9.png)

#### Verificar contenedores activos

```bash
docker ps
```

![contenedores activos](imagenesVirt/imagen10.png)

### 4. Acceder desde el navegador
Abrimos el navegador y comprobamos que los servicios estén funcionando:

- **http://localhost:8080** → muestra la página de bienvenida de Nginx.  
- **http://localhost:8081** → carga el servidor Tomcat.

![nginx navegador](imagenesVirt/imagen11.png)
![tomcat navegador](imagenesVirt/imagen12.png)

### Conclusiones
Docker simplifica el despliegue de aplicaciones al permitir ejecutar servicios en contenedores aislados. Facilita la portabilidad, reduce errores entre entornos y mejora la eficiencia del desarrollo.

### Bibliografía
* [Documentación oficial de Docker](https://docs.docker.com)
* [Docker Hub](https://hub.docker.com)

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
