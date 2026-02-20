# Documentación Final del Proyecto

## 1. Introducción
En este documento se habla de la implementación de un servicio de FTP seguro en entorno **Ubuntu Server** y la integración con el servidor web **Apache**.

---

## 2. Instalación del Servidor
Para la gestión de archivos hemos seleccionado **vsftpd** por su robustez y enfoque en la seguridad.

* **Comando de instalación:** `sudo apt update && sudo apt install vsftpd`
* **Gestión del servicio:** `sudo systemctl restart vsftpd` y `sudo systemctl status vsftpd` para verificar el estado *active (running)*.

---

## 3. Configuración Básica
La configuración se ha realizado editando el archivo `/etc/vsftpd.conf`. Los parámetros más importantes establecidos para garantizar la estabilidad son:

* `anonymous_enable=NO`: Bloqueo total de accesos no identificados.
* `local_enable=YES`: Permite el acceso a los usuarios locales del sistema.
* `write_enable=YES`: Habilitación de permisos de escritura para la subida de archivos.
* `chroot_local_user=YES`: Encarcelamiento de seguridad para restringir al usuario a su propio directorio raíz.
* `allow_writeable_chroot=YES`: Ajuste necesario para permitir la escritura dentro de una jaula chroot.

---

## 4. Usuarios y Permisos
Se ha configurado un entorno donde el usuario FTP tiene acceso directo a la carpeta de publicación web de Apache.

* **Usuario utilizado:** `userseguro` (o `ftpuser`)
* **Directorio vinculado:** `/var/www/html`
* **Ajuste de permisos en el servidor:**
    * Propietario: `userseguro` (para permitir la subida por FTP).
    * Grupo: `www-data` (para permitir la lectura por parte de Apache).
    * Comando: `sudo chown -R userseguro:www-data /var/www/html`

---

## 5. Seguridad (FTPS)
Para evitar la interceptación de credenciales y datos en tránsito, hemos configurado **FTP sobre TLS (FTPS)**:

1. **Generación de certificado:** Creación de un certificado autofirmado mediante OpenSSL en la ruta `/etc/ssl/private/ftp/`.
2. **Configuración SSL en vsftpd:**
    * `ssl_enable=YES`: Activa el soporte para cifrado.
    * `force_local_data_ssl=YES`: Obliga al cifrado de la transferencia de archivos.
    * `force_local_logins_ssl=YES`: Obliga al cifrado de las contraseñas durante el login.

---

## 6. Modos de Conexión
### Modo Activo vs. Pasivo
Se ha priorizado el **Modo Pasivo** para garantizar que la conexión atraviese correctamente el Firewall y el NAT de la red.

* **Configuración Pasiva:**
    * `pasv_min_port=40000`
    * `pasv_max_port=40100`
* **Justificación:** En el modo pasivo, el cliente es quien abre los canales de datos, evitando que el firewall del cliente bloquee la conexión entrante desde el servidor.

---

## 7. Clientes Utilizados
1. **FileZilla Client:** Herramienta principal utilizada para la conexión segura mediante FTPS explícito y validación de certificados.
2. **Consola Linux:** Uso de comandos `systemctl` y `netstat` para auditar el estado del servicio y los puertos.
3. **Navegador Web:** Validación final de la publicación de contenidos mediante el protocolo HTTP.

---

## 8. Integración Web e Informe de Administración
Se ha validado el flujo de despliegue mediante la subida de un archivo `index.html` por FTP y su posterior visualización en el navegador.

* **URL de acceso:** `http://10.0.2.15/index.html`
* **Recomendación de seguridad:** Se recomienda la instalación de **Fail2Ban** para proteger el servidor de ataques de fuerza bruta y realizar copias de seguridad periódicas de la configuración en `/etc/vsftpd.conf`.
