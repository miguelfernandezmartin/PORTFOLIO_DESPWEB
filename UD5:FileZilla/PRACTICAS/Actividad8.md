# Configuración FTP seguro

## 1. Creación del Certificado de Seguridad (TLS)
Para garantizar la privacidad de las credenciales, generamos un certificado autofirmado que cifrará el canal de comunicación:

`sudo mkdir -p /etc/ssl/private/ftp`

`sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/ftp/vsftpd.key -out /etc/ssl/private/ftp/vsftpd.crt`

Tras la generación, restringimos el acceso a la clave privada por seguridad:

`sudo chmod 600 /etc/ssl/private/ftp/vsftpd.key`

---

## 2. Parametrización para el cifrado explícito
Modifico el fichero de configuración principal para habilitar las capas de seguridad:

`sudo nano /etc/vsftpd.conf`

Dentro del archivo, validamos que los siguientes parámetros estén activos y correctamente definidos:

* **Escucha:** `listen=YES` / `listen_ipv6=NO`
* **Acceso:** `anonymous_enable=NO` / `local_enable=YES` / `write_enable=YES`
* **Seguridad:** `chroot_local_user=YES` / `ssl_enable=YES`
* **Cifrado forzado:** `force_local_data_ssl=YES` / `force_local_logins_ssl=YES`
* **Rutas:** `rsa_cert_file=/etc/ssl/private/ftp/vsftpd.crt` / `rsa_private_key_file=/etc/ssl/private/ftp/vsftpd.key`
* **Protocolos:** `ssl_tlsv1=YES` (Desactivando SSLv2 y SSLv3 por ser obsoletos)

---

## 3. Aplicación de cambios y verificación
Para que el servidor reconozca los nuevos parámetros, reiniciamos el demonio y comprobamos su estado actual:

`sudo systemctl restart vsftpd`

`sudo systemctl status vsftpd`

---

## 4. Gestión del Usuario de Pruebas
Creamos una cuenta de usuario específica y preparamos su árbol de directorios con los permisos correspondientes:

`sudo adduser userseguro`

Establecemos su carpeta de trabajo y ajustamos el propietario:

`sudo mkdir -p /home/userseguro/ftp`

`sudo chown userseguro:userseguro /home/userseguro/ftp`

---

## 5. Validación de acceso mediante FileZilla
Iniciamos el cliente gráfico y configuramos los parámetros de red. Es fundamental seleccionar "Usar FTP explícito sobre TLS" para que el servidor acepte la conexión:

![Captura Interfaz](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD5%3AFileZilla/images/cap1EJ8.png)

Al establecer el enlace, el software nos solicitará aceptar el certificado generado. Una vez aceptado, se confirma el túnel cifrado:

![Captura Conexión Segura](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD5%3AFileZilla/images/cap2EJ8.png)
