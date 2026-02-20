# Uso del navegador como cliente FTP

## 1. Intento de Acceso mediante Navegador Web
Se ha intentado acceder al servidor FTP utilizando un navegador web mediante la URL `ftp://10.0.2.15`. 

![Conexion fallida](https://github.com/miguelfernandezmartin/PORTFOLIO_DESPWEB/blob/main/UD5%3AFileZilla/images/cap1EJ9.png)  

**Resultado de la prueba:** La conexión **no fue exitosa**. Esto se debe a que los navegadores actuales han dejado de dar soporte nativo al protocolo FTP por razones de seguridad.
He probado a abrir el servidor desde el explorador de archivos y tampoco me ha dejado acceder.

---

## 2. Comparativa: Navegador vs. Cliente Dedicado (FileZilla)

| Característica | Navegador Web | Cliente Dedicado (FileZilla) |
| :--- | :--- | :--- |
| **Soporte FTPS/SFTP** | Nulo o muy limitado | Soporte completo y configurable |
| **Subida de archivos** | No permitida generalmente | Soporte total (Drag & Drop) |
| **Seguridad** | Inseguro (texto plano si funciona) | Cifrado de alto nivel (TLS 1.2/1.3) |
| **Interfaz** | Muy simple (estilo carpetas) | Panel dual (local/remoto) y cola de transferencia |
| **Diagnóstico** | No muestra errores técnicos | Consola de comandos en tiempo real |

---

## 3. Conclusión Técnica
Tras las pruebas realizadas, se concluye que el uso de un **cliente dedicado como FileZilla es indispensable** en entornos profesionales o configuraciones seguras. 
