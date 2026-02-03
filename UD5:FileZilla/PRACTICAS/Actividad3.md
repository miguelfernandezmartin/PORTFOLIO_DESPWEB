# Creación de usuarios y grupos en VSFTP
## Grupo, usuarios, permisos, directorio raíz y límites de conexión

Este documento describe la configuración de un entorno FTP seguro utilizando **vsftpd** en Ubuntu 24.04.  
Incluye:

- Creación de un grupo con permisos limitados  
- Creación de dos usuarios asociados al grupo  
- Definición de directorio raíz  
- Configuración de permisos (lectura, escritura, borrado)  
- Límites de conexión  
- Explicación de diferencias entre permisos de usuario y permisos de grupo  

---

## 1. Instalación de vsftpd

```bash
sudo apt update
sudo apt install -y vsftpd
sudo systemctl enable vsftpd
sudo systemctl start vsftpd
```
## 2. Crear un grupo con permisos limitados 
   
```bash
sudo groupadd ftp_limited
```

Este grupo será el que controle el acceso a los directorios FTP. 

## 3. Crear usuarios asociados al grupo 

```bash
sudo useradd -m -d /srv/ftp/usuario1 -s /usr/sbin/nologin -G ftp_limited usuario1
sudo passwd usuario1

sudo useradd -m -d /srv/ftp/usuario2 -s /usr/sbin/nologin -G ftp_limited usuario2
sudo passwd usuario2
```

-d define el directorio raíz del usuario. 

-s /usr/sbin/nologin impide acceso SSH. 

-G ftp_limited asigna el grupo. 

## 4. Directorio raíz y permisos 

### Directorio compartido para el grupo 

```bash
sudo mkdir -p /srv/ftp/shared
sudo chown root:ftp_limited /srv/ftp/shared
sudo chmod 770 /srv/ftp/shared
```

Permisos 770 → lectura, escritura y ejecución para propietario y grupo.

### Directorios individuales 

```bash
sudo mkdir -p /srv/ftp/user1/files
sudo chown user1:ftp_limited /srv/ftp/user1/files
sudo chmod 750 /srv/ftp/user1/files

sudo mkdir -p /srv/ftp/user2/files
sudo chown user2:ftp_limited /srv/ftp/user2/files
sudo chmod 750 /srv/ftp/user2/files
```

## 5. Configuración de vsftpd 

### Editar el archivo principal:

```bash
sudo nano /etc/vsftpd.conf
```

### Configurar: 

```conf
listen=YES
listen_ipv6=NO

local_enable=YES
write_enable=YES

# Encerrar usuarios en su directorio
chroot_local_user=YES

# Directorio raíz dinámico
local_root=/srv/ftp/$USER

# Permisos por defecto
local_umask=022

# Limitar acceso solo a usuarios permitidos
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO

# Límites de conexión
max_clients=10
max_per_ip=3
```

## 6. Añadir usuarios permitidos 

```bash
echo "user1" | sudo tee -a /etc/vsftpd.userlist
echo "user2" | sudo tee -a /etc/vsftpd.userlist
```

## 7. Reiniciar servicio 

```bash
sudo systemctl restart vsftpd
```

## 8. Verificación 

```bash
sudo ss -tulpn | grep ftp
```

## 9. Diferencias entre permisos de usuario y permisos de grupo 

| Tipo de Permiso | Qué controla | Ejemplo |
| :--- | :--- | :--- |
| **Usuario (Owner)** | Privilegios individuales sobre carpetas y archivos propios. | `user1` puede leer, escribir y borrar en su carpeta personal `/files`. |
| **Grupo (Group)** | Privilegios compartidos entre los usuarios del mismo grupo. | Tanto `user1` como `user2` pueden trabajar en el directorio `/shared`. |
| **Otros (Others)** | Lo que puede hacer cualquier otro usuario que no esté en el grupo. | **Sin acceso.** Se configura en 0 para que nadie externo vea los datos. |

### Resumen 
Los permisos de usuario definen privilegios individuales.

Los permisos de grupo definen privilegios compartidos entre varios usuarios.

vsftpd respeta los permisos del sistema de archivos Linux.
