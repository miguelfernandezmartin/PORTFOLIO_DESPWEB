# Documentación Técnica: Administración y Despliegue de Apache Tomcat

Esta documentación proporciona una guía exhaustiva sobre la arquitectura, configuración, seguridad y despliegue de **Apache Tomcat** en entornos profesionales.

---

##  1. Arquitectura Básica de Tomcat
La arquitectura de Tomcat es jerárquica y se basa en componentes definidos principalmente en el archivo `server.xml`.

* **Server:** El nivel superior de la jerarquía. Representa la instancia completa del contenedor.
* **Service:** Un componente intermedio que agrupa uno o más **Connectors** con un único **Engine**.
* **Connector:** El punto de entrada. Maneja las comunicaciones con el cliente.
    * *HTTP/1.1 (Puerto 8080):* Tráfico web estándar.
    * *AJP (Puerto 8009):* Protocolo binario para comunicación con servidores web frontales.
* **Engine:** El motor de procesamiento que recibe las solicitudes de los conectores y las redirige al Host adecuado.
* **Host:** Permite definir nombres de dominio virtuales (Virtual Hosting).
* **Context:** Representa una aplicación web individual (`.war`).

---

##  2. Configuración del Servidor
La configuración central se encuentra en el directorio `/conf`.

### Archivos de Configuración Esenciales
| Archivo | Función |
| :--- | :--- |
| `server.xml` | Configuración de red, puertos y estructura del servidor. |
| `web.xml` | Parámetros globales para todas las aplicaciones (MIME types, timeouts). |
| `context.xml` | Definición de recursos externos como pools de conexiones a BD (JNDI). |
| `tomcat-users.xml` | Definición de roles y usuarios para las apps de administración. |

---

##  3. Integración con Servidor Web
En producción, se recomienda utilizar un **Proxy Inverso** (Nginx o Apache HTTPD).

**Ventajas:**
1.  **Seguridad:** El servidor Tomcat no se expone directamente a internet.
2.  **SSL/TLS:** La descarga de certificados se gestiona en el proxy.
3.  **Balanceo:** Permite distribuir carga entre varios nodos de Tomcat.

**Configuración sugerida para Nginx:**
```nginx
server {
    listen 80;
    server_name mianuncio.com;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
    }
}
```

##  4. Seguridad Aplicada (Hardening)
Para asegurar una instancia de Tomcat, se deben seguir estas prácticas:

* **Usuario sin privilegios:** Nunca ejecutar Tomcat como `root`. Crear un usuario de sistema dedicado:
    ```bash
    useradd -r -m -U -d /opt/tomcat -s /bin/false tomcat
    ```
* **Eliminar aplicaciones por defecto:** Borrar las carpetas `webapps/examples`, `webapps/docs` y `webapps/ROOT`.
* **Ocultar banners de versión:** Editar el archivo `ServerInfo.properties` para que no muestre la versión en páginas de error 404/500.
* **Seguridad de Cookies:** En `web.xml`, forzar el uso de banderas de seguridad:

```xml
<cookie-config>
    <http-only>true</http-only>
    <secure>true</secure>
</cookie-config>ç
```

##  5. Pruebas de Rendimiento
El monitoreo constante es clave para evitar cuellos de botella.

* **JVM Tuning:** Ajustar la memoria Heap según la carga.
    * `Xms`: Memoria inicial.
    * `Xmx`: Memoria máxima (recomendado no exceder el 80% de la RAM física).
* **Monitoreo de Threads:** Vigilar el `maxThreads` en el conector HTTP (por defecto 200). Si se alcanza el límite, las peticiones se pondrán en cola.
* **Herramientas:** Utilizar **Apache JMeter** para simular usuarios concurrentes y **VisualVM** para detectar fugas de memoria.

---

##  6. Recomendaciones de Administración
* **Rotación de Logs:** Configurar `logrotate` para el archivo `catalina.out` para evitar el llenado del almacenamiento.
* **Actualizaciones:** Mantener la versión de la **JRE (Java Runtime Environment)** actualizada para mitigar vulnerabilidades.
* **Setenv.sh:** No modificar `catalina.sh`. Crear un archivo `bin/setenv.sh` para definir variables personalizadas.

---

##  7. Despliegue en Contenedores (Docker)
El uso de Docker facilita la portabilidad y el escalado horizontal.

**Ejemplo de Dockerfile optimizado:**

```dockerfile
# Usar una imagen ligera de Eclipse Temurin
FROM tomcat:10.1-jdk17-temurin-slim

# Limpiar aplicaciones preinstaladas
RUN rm -rf /usr/local/tomcat/webapps/*

# Copiar el artefacto de la aplicación
COPY app_v1.war /usr/local/tomcat/webapps/ROOT.war

# Ejecutar como usuario no root por seguridad
USER tomcat

EXPOSE 8080
CMD ["catalina.sh", "run"]
```
