# APACHE HTTPS

---

## 1. INVESTIGACIÓN

### 1.1. Funcionamiento del protocolo HTTPS
HTTPS funciona añadiendo una capa de seguridad (SSL/TLS) al protocolo HTTP, cifrando la comunicación entre tu navegador y el sitio web. Esto hace que los datos, como contraseñas o información bancaria, viajen ilegibles para terceros, usando un par de claves (pública y privada) para encriptar y desencriptar la información, asegurando que sea privada y auténtica.

---

### 1.2. Tipos de certificados SSL/TLS
El certificado digital es la pieza central que permite el cifrado y la autenticación.  
Los certificados SSL/TLS permiten cifrar la comunicación entre un cliente (como un navegador) y un servidor web. Existen distintos tipos:

#### Certificados autofirmados
Un certificado creado y firmado por la misma entidad que lo usa (por ejemplo, tú mismo en tu servidor).

**Características:**
- No son emitidos por terceros confiables.
- Los navegadores los marcan como no seguros.
- Se usan para entornos internos o pruebas (desarrollo, intranet).

**Ventajas:**
- Gratuitos.
- Fácil de crear.

**Desventajas:**
- No confiables para usuarios externos.
- Generan advertencias de seguridad.
- No sirven para sitios públicos.

#### Certificados emitidos por una CA confiable
Certificados emitidos por una Autoridad de Certificación (Certificate Authority), como Let's Encrypt o DigiCert.

**Características:**
- Firmados digitalmente por una entidad confiable.
- Los navegadores los aceptan sin advertencias.
- Usados en producción para sitios accesibles públicamente.

**Ventajas:**
- Reconocidos y confiables.
- Dan confianza a usuarios.
- Validan la identidad del servidor.

**Desventajas:**
- Algunos son de pago.
- Pueden requerir verificación de dominio o empresa.

---

## 2. EJECUCIÓN TÉCNICA

### 2.1. Instalar y verificar estado de Apache2
![Estado de Apache2](p1.png)

---

### 2.2. Habilitar SSL y headers
Habilito el SSL y los headers, luego reinicio Apache2.  
![Habilitar SSL y headers](p2.png)

---

### 2.3. Generación de certificado SSL/TLS

#### A. Certificado autofirmado
Creo el directorio para los certificados y genero un certificado autofirmado válido por 365 días.  
![Certificado autofirmado](p3.png)

---

### 2.4. Configurar VirtualHost HTTPS

#### Crear archivo de configuración SSL
![Archivo de configuración SSL](p4.png)

#### Habilitar sitio
![Habilitar sitio](p5.png)

#### Verificar escucha en puerto 443
![Verificar puerto 443](p6.png)

#### Redirigir de HTTP a HTTPS
![Redirección HTTP a HTTPS](p7.png)

#### Recargar Apache
![Recargar Apache](p8.png)

#### Validar funcionamiento
![Validar HTTPS](p9.png)

#### Confirmación de HTTPS
![Confirmación HTTPS](p10.png)

#### Comprobación con curl
![Comprobación curl](p11.png)

---

## Conclusiones
- Apache2 fue instalado y funciona correctamente, confirmado mediante `systemctl` y `configtest`.
- Los módulos SSL y headers se habilitaron correctamente para manejar conexiones cifradas y políticas de seguridad.
- Se generó un certificado autofirmado, útil para pruebas internas y entornos de desarrollo.
- Se configuró un VirtualHost para el puerto 443 con la ubicación correcta del certificado y permisos adecuados.
- No se utilizó Certbot; el proceso fue completamente manual, permitiendo un control total y comprensión del funcionamiento de SSL/TLS en Apache.
- La estructura de archivos quedó ordenada y funcional.
- Se probó la configuración con navegador y `curl`, confirmando que el sitio responde correctamente por HTTPS.
