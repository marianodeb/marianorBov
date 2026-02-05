# Comando `ncdu`: Guía Completa

## 📋 Definición y Significado
**ncdu** (NCurses Disk Usage) es una herramienta de análisis de uso de disco basada en la interfaz **ncurses** (biblioteca para crear interfaces de texto en terminales). Es una alternativa interactiva y más amigable a comandos como `du` y `df`.

**Características principales:**
- Interfaz interactiva con navegación mediante teclado
- Muestra el uso de disco de directorios y archivos
- Permite eliminar archivos/directorios directamente desde la interfaz
- Actualización en tiempo real al eliminar contenido
- Exportación de resultados

## 🔧 Instalación (si no viene por defecto)

### Ubuntu/Debian:
```bash
sudo apt update
sudo apt install ncdu
```

### CentOS/RHEL/Fedora:
```bash
sudo yum install ncdu
# o
sudo dnf install ncdu
```

### macOS (Homebrew):
```bash
brew install ncdu
```

### Arch Linux:
```bash
sudo pacman -S ncdu
```

### Desde código fuente:
```bash
wget https://dev.yorhel.nl/download/ncdu-2.3.tar.gz
tar -xzf ncdu-2.3.tar.gz
cd ncdu-2.3
./configure
make
sudo make install
```

## 📝 Sintaxis Básica
```bash
ncdu [opciones] [directorio]
```

## ⚙️ Todas las Opciones Principales

### Opciones de Modo:
- **Sin opciones**: Modo interactivo por defecto
- **`-q`**: Modo silencioso (no muestra porcentajes durante escaneo)
- **`-f ARCHIVO`**: Importa resultados escaneados previamente
- **`-o ARCHIVO`**: Exporta resultados a archivo (sin interfaz interactiva)
- **`--si`**: Modo interactivo usando unidades SI (1k = 1000)
- **`-0`**: Modo no interactivo, salida para procesamiento

### Opciones de Visualización:
- **`-x`**: No cruzar límites de filesystem
- **`--exclude PATRÓN`**: Excluir archivos que coincidan con patrón
- **`--exclude-from ARCHIVO`**: Excluir patrones desde archivo
- **`--exclude-caches`**: Excluir directorios con CACHEDIR.TAG
- **`--follow-symlinks`**: Seguir enlaces simbólicos
- **`-L`**: Seguir enlaces simbólicos (mismo que --follow-symlinks)

### Opciones de Salida:
- **`-v`**: Modo verbose
- **`-h`**: Mostrar ayuda
- **`-V`**: Mostrar versión

## 📊 Ejemplos

### Ejemplos Simples:

1. **Escaneo interactivo del directorio actual:**
```bash
ncdu
```

2. **Escaneo de un directorio específico:**
```bash
ncdu /var/log
```

3. **Escaneo excluyendo archivos temporales:**
```bash
ncdu --exclude '*.tmp' /home/usuario
```

4. **Exportar resultados a archivo:**
```bash
ncdu -o resultados.txt /home
```

5. **Cargar resultados desde archivo:**
```bash
ncdu -f resultados.txt
```

### Ejemplos Complejos:

1. **Escaneo remoto por SSH:**
```bash
ssh usuario@servidor "ncdu -o - /" | ncdu -f -
```
*Nota: Escanea sistema remoto y muestra resultados localmente*

2. **Comparar dos directorios:**
```bash
ncdu -o viejo.txt /directorio/viejo
# Hacer cambios...
ncdu -o nuevo.txt /directorio/viejo
# Comparar diferencias manualmente
```

3. **Excluir múltiples patrones:**
```bash
ncdu --exclude '*.log' --exclude '*.tmp' --exclude 'cache/' /var
```

4. **Escaneo con límite de filesystem:**
```bash
ncdu -x /  # No escaneará /home si está en partición diferente
```

5. **Monitorear cambios en tiempo real:**
```bash
watch -n 60 "ncdu -1x /directorio | head -20"
```

## 🎮 Comandos en Modo Interactivo

### Navegación:
- **`↑/↓`**: Moverse entre elementos
- **`→`**: Entrar en directorio
- **`←`**: Salir de directorio
- **`n`**: Ordenar por nombre
- **`s`**: Ordenar por tamaño
- **`C`**: Ordenar por número de items

### Acciones:
- **`d`**: Eliminar elemento seleccionado
- **`i`**: Mostrar información del elemento
- **`r`**: Recalcular tamaño
- **`g`**: Mostrar/Ocultar porcentajes
- **`?`**: Mostrar ayuda

### Búsqueda:
- **`/`**: Buscar por patrón (regex)
- **`n`**: Siguiente coincidencia en búsqueda
- **`N`**: Coincidencia anterior en búsqueda

## 💡 Consejos Prácticos

1. **Para análisis inicial:** Comienza con `ncdu /` para ver todo el sistema
2. **Uso en producción:** Usa `-x` para evitar escanear filesystems montados
3. **Exportar para análisis posterior:** `ncdu -o informe.txt /ruta`
4. **Identificar espacio perdido:** Busca directorios grandes inesperados
5. **Limpiar espacio:** Usa `d` para eliminar directamente desde ncdu
6. **Comparar snapshots:** Exporta resultados antes y después de limpiezas

## 🔍 Información Adicional

### Formatos de Exportación:
ncdu guarda en formato JSON cuando exporta con `-o`. Puedes procesarlo con otras herramientas:
```bash
ncdu -o datos.json /directorio
jq '.' datos.json  # Si tienes jq instalado
```

### Limitaciones Conocidas:
- No maneja bien archivos con nombres que contienen saltos de línea
- En sistemas con millones de archivos, puede consumir mucha memoria
- Los enlaces duros se cuentan múltiples veces (por diseño)

### Alternativas y Herramientas Relacionadas:

1. **`du` + `sort`:** La alternativa clásica
   ```bash
   du -sh * | sort -h
   ```

2. **`dust`:** Alternativa moderna en Rust
   ```bash
   # Instalación: cargo install du-dust
   dust /directorio
   ```

3. **`gt5`:** Similar con historial de diferencias

4. **`baobab`:** Versión gráfica para GNOME

5. **`Filelight`:** Visualización gráfica radial para KDE

6. **`diskus`:** Más rápido pero menos funcionalidades
   ```bash
   # Instalación: cargo install diskus
   diskus /directorio
   ```

### Rendimiento Comparativo:
- `ncdu`: Buen balance entre características y velocidad
- `dust`: Más rápido, interfaz similar
- `du`: Más rápido para scripts, menos amigable

## 🚀 Uso Avanzado

### Script para limpieza automatizada:
```bash
#!/bin/bash
# Encuentra directorios mayores a 1GB y exporta resultado
TARGET="/"
THRESHOLD="1073741824"  # 1GB en bytes

ncdu -x $TARGET -o /tmp/scan.txt
# Procesar resultados con otros comandos...
```

### Integración con cron para monitoreo:
```bash
# En crontab: 0 2 * * * /ruta/script-monitor.sh
#!/bin/bash
ncdu -o /var/log/disk-usage-$(date +%Y%m%d).json /
```

### Personalizar unidades:
```bash
# Mostrar en megabytes
ncdu | while read line; do
    # Procesar línea para convertir unidades
    echo "$line"
done
```

## 📚 Recursos Adicionales

1. **Página oficial:** https://dev.yorhel.nl/ncdu
2. **Repositorio Git:** https://g.blicky.net/ncdu.git/
3. **Wiki Arch Linux:** https://wiki.archlinux.org/title/Ncdu
4. **Guías de rendimiento:** Útil para servidores con mucho almacenamiento

## 🎯 Conclusión

**`ncdu`** sigue siendo una herramienta excelente y ampliamente utilizada. No ha sido sustituida por completo, pero tiene alternativas modernas como **`dust`** que ofrecen mejor rendimiento en algunos casos. Para la mayoría de usuarios, `ncdu` ofrece el mejor balance entre funcionalidad, usabilidad y disponibilidad.

**Recomendación:** Instala y prueba tanto `ncdu` como `dust` para ver cuál se adapta mejor a tu flujo de trabajo. Para scripting, `du` tradicional sigue siendo la mejor opción, mientras que para análisis interactivo `ncdu` es difícil de superar.
