# Instalación y configuración de vsftpd en Ubuntu 24.04

## Introducción
En esta documentación se describe el proceso de instalación y configuración del servidor FTP **vsftpd** en un sistema **Ubuntu 24.04**.  
vsftpd (Very Secure FTP Daemon) es el servidor FTP más utilizado en sistemas GNU/Linux por su seguridad y simplicidad.

El objetivo es:
- Instalar el servidor FTP
- Acceder a la consola de administración
- Configurar el puerto de escucha
- Configurar la dirección IP
- Habilitar el inicio automático del servicio

---

## 1. Instalación de vsftpd

Primero se actualizan los repositorios del sistema:

```bash
sudo apt update
```

A continuación, se instala el servidor **vsftpd**:

```bash
sudo apt install vsftpd -y
```

Una vez instalado, se puede comprobar la versión:

```bash
vsftpd -version
```

---

## 2. Acceso a la consola de administración

En Ubuntu, la administración del servicio se realiza mediante **systemd**.

### Comprobar el estado del servicio
```bash
sudo systemctl status vsftpd
```

### Comandos básicos de administración
```bash
sudo systemctl start vsftpd
sudo systemctl stop vsftpd
sudo systemctl restart vsftpd
```

El archivo de configuración principal del servidor es:

```
/etc/vsftpd.conf
```

Para editarlo:
```bash
sudo nano /etc/vsftpd.conf
```

---

## 3. Configuración del servidor

### 3.1 Configuración del puerto de escucha

En el archivo `vsftpd.conf` se define el puerto FTP:

```ini
listen_port=21
```

En este caso se ha utilizado el puerto FTP estándar **21**.

---

### 3.2 Configuración de la dirección IP

Para indicar en qué interfaces de red escucha el servidor:

```ini
listen_address=0.0.0.0
```

El valor `0.0.0.0` indica que el servidor acepta conexiones desde todas las interfaces de red disponibles.

---

### 3.3 Inicio automático del servicio

Para que el servidor FTP se inicie automáticamente al arrancar el sistema:

```bash
sudo systemctl enable vsftpd
```

Se puede comprobar con:
```bash
systemctl is-enabled vsftpd
```

---

## 4. Aplicación de cambios

Después de modificar la configuración, es necesario reiniciar el servicio:

```bash
sudo systemctl restart vsftpd
```

---

## 5. Verificación del funcionamiento

Para comprobar que el servidor está escuchando correctamente en el puerto configurado:

```bash
sudo ss -tulpn | grep ftp
```

Salida obtenida:

![img](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD5%3AFileZilla/images/capEJ1.png)

Esto confirma que:
- El servicio **vsftpd** está activo
- Escucha en el puerto **21**
- Acepta conexiones desde cualquier interfaz de red

---

## Conclusión

Se ha instalado y configurado correctamente el servidor FTP **vsftpd** en Ubuntu 24.04, cumpliendo los requisitos de:
- Instalación del servicio
- Configuración del puerto de escucha
- Configuración de la dirección IP
- Activación del inicio automático

El servidor queda listo para su uso y para la creación de usuarios FTP según las necesidades del sistema.
