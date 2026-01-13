

## `aptitude`

### Definición y Significado

`aptitude` es un front-end avanzado para el sistema de gestión de paquetes APT (Advanced Packaging Tool) en sistemas Debian y derivados (como Ubuntu). Combina una interfaz de línea de comandos (CLI) con una interfaz visual interactiva basada en ncurses, ofreciendo más funcionalidades que `apt-get` o `apt`.

Significado: Es una herramienta para instalar, actualizar, eliminar y gestionar paquetes de software, con características como resolución inteligente de dependencias y búsqueda avanzada.

### Sintaxis Básica

```
aptitude [opciones] [comando] [argumentos]
```

### Todas sus Opciones Principales

#### Comandos principales:

- `install` - Instalar paquetes
- `remove` - Eliminar paquetes (deja archivos de configuración)
- `purge` - Eliminar completamente paquetes y sus archivos de configuración
- `update` - Actualizar la lista de paquetes disponibles
- `upgrade` - Actualizar paquetes instalados
- `full-upgrade` - Actualizar el sistema completamente (puede eliminar paquetes si es necesario)
- `search` - Buscar paquetes
- `show` - Mostrar información detallada de un paquete
- `hold` - Bloquear un paquete para evitar actualizaciones
- `unhold` - Desbloquear un paquete
- `forbid-version` - Evitar la instalación de una versión específica
- `reinstall` - Reinstalar un paquete

#### Opciones comunes:

- `-h`, `--help` - Mostrar ayuda
- `-v` - Modo verbose (mostrar más información)
- `-d` - Solo descargar, no instalar
- `-y` - Asumir "sí" a todas las preguntas
- `-f` - Intentar corregir dependencias rotas
- `-q` - Modo silencioso (puede usarse múltiples veces para mayor silencio)
- `-s` - Simular (no realizar cambios reales)
- `-P` - Mostrar siempre el prompt de confirmación
- `--disable-columns` - Desactivar el formato en columnas

#### Opciones para la interfaz visual:

- `--schedule-only` - Programar acciones para más tarde
- `--add-user-tag` - Añadir etiquetas de usuario
- `--remove-user-tag` - Eliminar etiquetas de usuario

### Ejemplos

### Ejemplos simples:

1. Actualizar lista de paquetes:

```bash
sudo aptitude update
```

2. Buscar un paquete:

```bash
aptitude search nginx
```

3. Instalar un paquete:

```bash
sudo aptitude install nginx
```

4. Mostrar información de un paquete:

```bash
aptitude show firefox
```

5. Actualizar todos los paquetes:

```bash
sudo aptitude upgrade
```

### Ejemplos complejos:

1. Actualizar el sistema completamente (puede eliminar paquetes si es necesario):

```bash
sudo aptitude full-upgrade
```

2. Instalar una versión específica de un paquete:

```bash
sudo aptitude install python3=3.8.2-0ubuntu2
```

3. Eliminar un paquete y sus archivos de configuración:

```bash
sudo aptitude purge apache2
```

4. Simular la eliminación de un paquete (sin hacer cambios reales):

```bash
sudo aptitude -s remove libreoffice
```

5. Buscar paquetes que proporcionan un archivo específico:

```bash
aptitude search '~P/usr/bin/htop'
```

### Consejos

1. **Interfaz visual**: Ejecuta `sudo aptitude` sin argumentos para entrar en la interfaz visual interactiva (muy útil para gestionar paquetes).

2. **Resolución de problemas**: `aptitude` tiene mejor resolución de dependencias que `apt-get`. Si tienes problemas con dependencias, prueba con aptitude.

3. **Atajos en la interfaz visual**:

   - `Ctrl+T`: Menú de acciones
   - `+`: Marcar para instalación
   - `-`: Marcar para eliminación
   - `_`: Marcar para purga
   - `u`: Actualizar lista de paquetes
   - `g`: Aplicar cambios
   - `q`: Salir
   - `/`: Buscar

4. **Historial**: `aptitude` mantiene un historial de todas las acciones realizadas, útil para deshacer cambios.

5. **Búsquedas avanzadas**: Usa patrones de búsqueda complejos como `~i` para paquetes instalados, `~U` para actualizables, etc.

### Información Adicional

#### Diferencias con apt/apt-get:

- Mejor manejo de dependencias
- Interfaz interactiva
- Mantiene un historial de acciones
- Permite búsquedas más avanzadas
- Opción de deshacer acciones

#### Comandos relacionados:

1. `apt` - El nuevo front-end recomendado (combina apt-get y apt-cache)
2. `apt-get` - El front-end tradicional
3. `apt-cache` - Para consultar información de paquetes
4. `dpkg` - Herramienta de bajo nivel para manejar paquetes .deb
5. `synaptic` - Interfaz gráfica para gestión de paquetes

#### ¿Está obsoleto?

No está oficialmente obsoleto, pero Canonical (desarrolladores de Ubuntu) recomiendan usar `apt` en su lugar. Sin embargo, `aptitude` sigue siendo útil por sus características avanzadas, especialmente en sistemas Debian.

#### Documentación adicional:

- Manual completo: `man aptitude`
- Guía de usuario: `aptitude --help`
- Documentación oficial en Debian: https://wiki.debian.org/Aptitude

#### Notas importantes:

- Siempre usa `sudo` con aptitude para operaciones que modifican el sistema
- Revisa cuidadosamente las acciones que aptitude propone antes de confirmar
- La interfaz visual es muy útil para resolver conflictos de dependencias
- Puedes usar `aptitude why` para entender por qué un paquete está instalado





