## 1. Configuración del Servidor (/etc/vsftpd.conf) 
### Edita el archivo de configuración y asegúrate de que los siguientes parámetros estén establecidos:

```bash
# Activar acceso anónimo
anonymous_enable=YES

# Definir el directorio raíz para el usuario anónimo
anon_root=/srv/ftp/publico

# Restricciones de permisos (Solo lectura)
anon_upload_enable=NO
anon_mkdir_write_enable=NO
anon_other_write_enable=NO

# Seguridad adicional
no_anon_password=YES
hide_ids=YES
```

## 2. Creación del Directorio y Permisos de Sistema 
### El directorio debe pertenecer al usuario ftp (creado automáticamente al instalar vsftpd) y no debe tener permisos de escritura para el usuario anónimo en su raíz. 

```bash
# Crear el directorio
sudo mkdir -p /srv/ftp/publico

# Crear un archivo de prueba
echo "Este es un archivo de solo lectura para anonimos" | sudo tee /srv/ftp/publico/nota.txt

# Ajustar permisos (Root es dueño, otros solo leen)
sudo chown root:ftp /srv/ftp/publico
sudo chmod 555 /srv/ftp/publico
```

## 3. Resultado 

En esta captura se puede ver que he entrado con anonymous, aparece la nota que he creado y no puedo crear archivos nuevos. 

![img](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD5%3AFileZilla/images/capEJ4.png)

