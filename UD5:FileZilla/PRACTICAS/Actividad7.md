# FileZilla: Pruebas con clientes gráficos

## 1. Preparación e Instalación
Para realizar las pruebas gráficas, instalamos el cliente FileZilla en nuestro sistema Ubuntu. Abrimos la terminal y ejecutamos:

`sudo apt update && sudo apt install filezilla -y`

Una vez completada la instalación, iniciamos el entorno gráfico con el comando: `filezilla`

---

## 2. Conexión Rápida
Voy a usar la barra superior de **Conexión Rápida** para un acceso inmediato al servidor. 

Introducimos los siguientes parámetros en los campos correspondientes:

* **Servidor:** `10.0.2.15` (IP de la Máquina Virtual)
* **Nombre de usuario:** `usuario1`
* **Contraseña:** `[Contraseña]`
* **Puerto:** `21`

Al pulsar el botón **Conexión rápida**, aceptaremos el certificado (si aparece) y verificaremos que el panel derecho ("Sitio remoto") muestra el contenido del servidor.

![Uso de Conexión Rápida](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD5%3AFileZilla/images/cap1Ej7.png)

---

## 3. Pruebas de Transferencia de Datos
Realizamos un flujo bidireccional de archivos para confirmar que los permisos de escritura y lectura son correctos:

### ⬆️ Subida (Local a Remoto)
Seleccionamos un archivo de nuestra carpeta personal y lo arrastramos hacia el directorio del servidor.


### ⬇️ Descarga (Remoto a Local)
Arrastramos un fichero desde el servidor hacia nuestro escritorio o carpeta local.

![Log de Operaciones](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD5%3AFileZilla/images/cap2EJ7.png)
