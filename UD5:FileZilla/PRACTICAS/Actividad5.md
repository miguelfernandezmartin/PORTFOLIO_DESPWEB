## 1. Configuración del Rango de Puertos Pasivos 
Para que el modo pasivo funcione correctamente a través de un firewall, debemos definir un rango de puertos fijo.

Edita el archivo de configuración:

```bash
sudo nano /etc/vsftpd.conf
```
Añade o modifica estas líneas al final del archivo:

```bash
pasv_enable=YES
pasv_min_port=40000
pasv_max_port=40100
```

Guarda y reinicia el servicio:

```bash
sudo systemctl restart vsftpd
```

## 2. Pruebas de Conexión (Modo Activo vs Pasivo)
Para documentar tu entrega, realiza las conexiones desde la terminal de tu VirtualBox:

### A. Conexión en Modo Activo 
En este modo, el servidor intenta abrir una conexión de datos hacia el cliente.

```bash
ftp 127.0.0.1
# Login con user1
ftp> passive          # Desactiva el modo pasivo (dirá: Passive mode: off)
ftp> ls               # El servidor intentará conectar a tu puerto 20
```

### B. Conexión en Modo Pasivo
En este modo, el cliente inicia la conexión de datos hacia los puertos que definimos (40000-40100).

```bash
ftp 127.0.0.1
# Login con user1
ftp> passive          # Activa el modo pasivo (dirá: Passive mode: on)
ftp> ls               # El cliente conecta al puerto aleatorio del servidor
```

### No me funciona el login a ftp con el usuario, no sé por qué
![img](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD5%3AFileZilla/images/capEJ5.png)

## 3. Tabla Comparativa

### Comparativa: Modo Activo vs Modo Pasivo

| Característica | Modo Activo (PORT) | Modo Pasivo (PASV) |
| :--- | :--- | :--- |
| **Comando de Control** | El cliente envía el comando `PORT`. | El cliente envía el comando `PASV`. |
| **Conexión de Datos** | Iniciada por el **Servidor** hacia el Cliente. | Iniciada por el **Cliente** hacia el Servidor. |
| **Puertos de Datos** | Servidor usa puerto 20 fijo. | Servidor usa rango dinámico (40000-40100). |
| **Comportamiento Firewall** | El Firewall del cliente suele bloquear la entrada. | El Firewall del cliente lo permite (es salida). |
