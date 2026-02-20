# Disponibilidad y buenas prácticas

## 1. Optimización y Control de Recursos
En un entorno de producción, es fundamental gestionar el consumo de recursos para prevenir caídas del servicio por saturación o ataques de denegación de servicio (DoS).

* **Gestión de Concurrentes:** Se debe definir un límite máximo de usuarios mediante el parámetro `max_clients=50` para asegurar la estabilidad del hardware.
* **Control de Conexiones por Origen:** Es necesario limitar las conexiones por IP (`max_per_ip=5`) para mitigar intentos de intrusión automatizados.
* **Modelado de Tráfico (QoS):** Se recomienda implementar `local_max_rate` para evitar que un solo usuario monopolice el ancho de banda disponible de la red.
* **Políticas de Expiración:** Configurar `idle_session_timeout` para finalizar conexiones inactivas y optimizar la tabla de estados del servidor.

---

## 2. Auditoría, Logs y Trazabilidad
La capacidad de reconstruir eventos es vital para la seguridad informática y el diagnóstico de errores.

* **Registro de Transferencias:** La activación de `xferlog_enable=YES` es obligatoria para mantener un histórico detallado de la entrada y salida de datos.
* **Auditoría del Protocolo:** Habilitar un registro dual (`dual_log_enable=YES`) permite separar los logs operativos de los del sistema, facilitando su análisis en `/var/log/vsftpd.log`.
* **Mantenimiento de Logs:** Se debe integrar el servicio con `logrotate` para garantizar la rotación de archivos y prevenir el agotamiento del espacio en disco.
* **Sincronización Temporal:** Es imprescindible el uso del protocolo **NTP** para asegurar que todas las trazas de auditoría tengan marcas de tiempo precisas.

---

## 3. Estrategias de Continuidad de Negocio (Backup)
La disponibilidad del servicio no solo reside en su ejecución, sino en la capacidad de recuperación ante desastres.

* **Respaldo de Configuración:** Realizar copias de seguridad periódicas de los archivos de configuración (`/etc/vsftpd.conf`) y de los certificados SSL/TLS.
* **Automatización de Backups:** Programar tareas mediante `cron` para el respaldo de los directorios raíz donde se aloja la información de los usuarios.
* **Arquitectura de Respaldo 3-2-1:**
    * Mantener **3** copias de los datos.
    * Almacenarlas en **2** soportes distintos.
    * Conservar **1** copia en una ubicación física o lógica externa (Off-site/Cloud).

---

## 4. Seguridad de Red: Firewall y NAT
El protocolo FTP requiere una configuración de red específica debido a la separación entre el canal de control y el de datos.

* **Segmentación de Puertos Pasivos:** Se debe acotar un rango de puertos en el archivo de configuración (`pasv_min_port` y `pasv_max_port`).
* **Reglas de Filtrado:** El Firewall debe configurarse para permitir el tráfico exclusivamente en el puerto 21 y en el rango pasivo previamente definido, denegando el resto por defecto.
* **Protección Activa:** Implementar herramientas como **Fail2Ban** para detectar patrones de fuerza bruta y bloquear dinámicamente las direcciones IP atacantes a nivel de red.

---

## 5. Conclusión General
Para garantizar un estándar de seguridad profesional, el uso de **FTPS (FTP sobre TLS)** con cifrado fuerte es innegociable. No obstante, se recomienda evaluar la implementación de **SFTP** en infraestructuras con topologías de red complejas, dado que su gestión a través de firewalls es más eficiente al operar sobre un único flujo de datos seguro.
