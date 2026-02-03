## 1. Conexión con Cliente ftp (Básico) 
Es el cliente estándar. Utilizaremos al usuario1 creado anteriormente.

```bash
# Iniciar conexión
ftp 127.0.0.1

# 1. Autenticación
# Name: usuario1
# Password: [tu_contraseña]

# 2. Listar archivos
ftp> ls

# 3. Subir un archivo (Upload)
# Primero crea un archivo de prueba en tu local: touch prueba_subida.txt
ftp> put prueba_subida.txt

# 4. Descargar un archivo (Download)
ftp> get archivo_servidor.txt

# 5. Salir
ftp> bye
```

## 2. Conexión con Cliente lftp (Avanzado) 
lftp es más potente porque permite ver el progreso y usar comandos similares a un shell de Linux.

Instalación: sudo apt install lftp

```bash
# Conexión directa
lftp -u usuario1,tu_contraseña 127.0.0.1

# Operaciones:
lftp usuario1@127.0.0.1:~> ls                      # Listar
lftp usuario1@127.0.0.1:~> put imagen.jpg          # Subir
lftp usuario1@127.0.0.1:~> get documento.pdf       # Descargar
lftp usuario1@127.0.0.1:~> exit                    # Salir
```

## 3. Operación Rápida con curl 
curl es ideal para descargar o subir archivos de forma atómica sin entrar en una sesión interactiva.

```bash
# Descargar un archivo
curl -u usuario1:tu_contraseña ftp://127.0.0.1/archivo.txt -o archivo_descargado.txt

# Subir un archivo
curl -T nota.txt -u usuario1:tu_contraseña ftp://127.0.0.1/
```

