# Seguridad en el repositorio

Este documento explica por qué ciertos archivos están excluidos del control de versiones mediante `.gitignore`.

## Archivos sensibles
- **`.env`, claves privadas y certificados (`.key`, `.pem`)**: contienen credenciales, tokens y configuraciones que no deben ser expuestos públicamente, ya que comprometerían la seguridad del sistema.
- **Archivos de configuración local** (`*.local.php`, `*.local.yaml`): almacenan ajustes específicos de cada entorno (desarrollo, producción). No deben compartirse para evitar filtraciones o configuraciones incorrectas en otros entornos.

## Archivos temporales
- **Logs (`*.log`) y temporales (`*.tmp`)**: contienen información sensible como errores internos o trazas de ejecución. Subirlos podría exponer detalles del sistema.
- **Archivos del sistema operativo** (`.DS_Store`, `Thumbs.db`): no tienen relevancia para el código fuente y pueden contener metadatos innecesarios.

## Dependencias
- **`node_modules/` y `vendor/`**: son directorios grandes que contienen librerías externas. No se suben porque pueden reinstalarse fácilmente desde los gestores de dependencias (`npm`, `composer`), evitando así riesgos de manipulación de paquetes ya instalados.

## Archivos binarios
- **Compilados y ejecutables (`*.exe`, `*.dll`, `*.class`, etc.)**: no deben versionarse porque son generados automáticamente a partir del código fuente. Además, pueden ser vectores de malware si se distribuyen por error.

## Archivos de IDE y pruebas
- **Configuraciones de editores (`.idea/`, `.vscode/`)**: son específicas de cada desarrollador y no deben compartirse.
- **Resultados de pruebas (`coverage/`, `tests/output/`)**: contienen datos intermedios que no tienen valor para el repositorio.

---

En resumen, excluir estos archivos protege:
1. **La confidencialidad** de credenciales y configuraciones.  
2. **La integridad** del repositorio, evitando la inclusión de archivos no confiables.  
3. **La portabilidad**, ya que cada entorno puede regenerar dependencias y configuraciones locales.  
