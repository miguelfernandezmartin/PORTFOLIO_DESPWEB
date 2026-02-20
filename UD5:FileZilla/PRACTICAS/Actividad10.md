# Integración de FTP con servidor web

## 1. Introducción
El objetivo de esta práctica es utilizar un servidor FTP como método de subida de contenidos para un servidor web Apache. De esta forma, simulamos un entorno de despliegue real donde un desarrollador sube archivos remotamente para que se publiquen automáticamente en Internet.

---

## 2. Configuración del Directorio de Trabajo
Para que el servidor web Apache pueda servir los archivos que subimos por FTP, debemos vincular el directorio personal del usuario con el **DocumentRoot** de Apache.

### 2.1. Modificación de la ruta en vsftpd
Editamos el archivo de configuración de vsftpd:
`sudo nano /etc/vsftpd.conf`

Añadimos la siguiente línea para que el usuario acceda directamente a la carpeta web:
`local_root=/var/www/html`

Modificamos los permisos de la carpeta donde va a ir la pagina
`sudo chown -R userseguro:www-data /var/www/html`
`sudo chmod -R 755 /var/www/html`

---

## 3. Subida de contenido mediante FileZilla
Utilizamos el cliente **FileZilla** para subir nuestro archivo de prueba.

1.  **Conexión:** Nos conectamos a la IP `10.0.2.15` usando FTPS.
2.  **Transferencia:** Arrastramos el archivo local `index.html` hacia el panel derecho (directorio `/var/www/html`).

**Captura de la transferencia exitosa:**
![Subida de index.html](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD5%3AFileZilla/images/cap1EJ10.png)

---

## 4. Verificación en el Navegador (HTTP)
Una vez subido el archivo, accedemos a la dirección IP del servidor desde un navegador web para comprobar que Apache está sirviendo el contenido correctamente.

* **URL:** `http://10.0.2.15/index.html`

**Captura del sitio web funcionando:**
![Navegador mostrando index.html](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD5%3AFileZilla/images/cap2EJ10.png)

---

## 5. Análisis del Flujo de Trabajo

1.  **Edición:** El archivo `index.html` se crea y edita en el entorno local.
2.  **Cifrado:** FileZilla establece una conexión TLS para proteger el envío del archivo.
3.  **Despliegue:** Al depositar el archivo en `/var/www/html`, Apache lo detecta y lo pone a disposición de las peticiones HTTP entrantes.
