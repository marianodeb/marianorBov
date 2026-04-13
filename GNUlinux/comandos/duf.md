# Comando `duf`: Guía Completa

## 📋 Definición y Significado

**duf** (Disk Usage/Free Utility) es una herramienta moderna para visualizar el uso de disco que reemplaza a los comandos tradicionales `df` y `du`.
Ofrece una salida colorida, ordenada y fácil de leer con información detallada sobre sistemas de archivos montados.

**Características principales:**

- Interfaz colorida y tabular
- Detección automática del tema del terminal (claro/oscuro)
- Ordenación inteligente de resultados
- Filtrado y personalización flexible
- Soporte para JSON y otras salidas estructuradas
- Detección de dispositivos de almacenamiento especiales

## 🔧 Instalación (no viene por defecto en la mayoría de sistemas)

### Método más simple (descarga binario):

```bash
# Linux (descargar y hacer ejecutable)
curl -L https://github.com/muesli/duf/releases/latest/download/duf_$(uname -s)_$(uname -m).tar.gz | tar xz
sudo mv duf /usr/local/bin/

# o usando install.sh
curl -sSf https://raw.githubusercontent.com/muesli/duf/master/install.sh | sh
```

### Ubuntu/Debian (.deb):

```bash
wget https://github.com/muesli/duf/releases/latest/download/duf_$(uname -s)_$(uname -m).deb
sudo dpkg -i duf_*.deb
```

### Fedora/RHEL (.rpm):

```bash
sudo rpm -i https://github.com/muesli/duf/releases/latest/download/duf_$(uname -s)_$(uname -m).rpm
```

### macOS (Homebrew):

```bash
brew install duf
```

### macOS (MacPorts):

```bash
sudo port install duf
```

### Arch Linux (AUR):

```bash
yay -S duf
# o
paru -S duf
```

### Desde código fuente (Go):

```bash
git clone https://github.com/muesli/duf.git
cd duf
go build
sudo mv duf /usr/local/bin/
```

### Docker:

```bash
docker run --rm -it -v /:/host:ro mwendler/duf
```

## 📝 Sintaxis Básica

```bash
duf [opciones] [dispositivos_o_directorios...]
```

## ⚙️ Todas las Opciones Principales

### Opciones de Visualización:

- **`--all`**: Mostrar todos los dispositivos, incluyendo pseudo/duplicados
- **`--inodes`**: Mostrar información de inodos en lugar de espacio en disco
- **`--local`**: Mostrar solo sistemas de archivos locales
- **`--network`**: Mostrar solo sistemas de archivos de red
- **`--fstab`**: Mostrar solo dispositivos de /etc/fstab
- **`--pseudo`**: Mostrar solo sistemas de archivos pseudo (tmpfs, etc.)
- **`--special`**: Mostrar solo dispositivos especiales (loopback, etc.)
- **`--hide <tipos>`**: Ocultar tipos específicos de filesystems
- **`--hide-fs <fs>`**: Ocultar filesystems específicos por tipo
- **`--only <tipos>`**: Mostrar solo tipos específicos de filesystems
- **`--only-fs <fs>`**: Mostrar solo filesystems específicos por tipo
- **`--sort <columna>`**: Ordenar por columna específica

### Opciones de Formato:

- **`--json`**: Salida en formato JSON
- **`--theme <tema>`**: Especificar tema (light, dark, colorful)
- **`--no-color`**: Desactivar colores
- **`--no-wrap`**: Desactivar ajuste de línea
- **`--width <ancho>`**: Especificar ancho de salida
- **`--hide-header`**: Ocultar encabezado de la tabla
- **`--hide-footer`**: Ocultar pie de página de la tabla
- **`--no-shell-escape`**: No escapar caracteres especiales del shell

### Opciones de Configuración:

- **`--config <archivo>`**: Especificar archivo de configuración
- **`--debug`**: Modo de depuración
- **`--version`**: Mostrar versión
- **`--help`**: Mostrar ayuda

## 📊 Ejemplos

### Ejemplos Simples:

1. **Uso básico (similar a `df -h` pero mejorado):**

```bash
duf
```
*Muestra todos los filesystems montados con formato bonito*

2. **Mostrar solo filesystems locales:**

```bash
duf --local
```

3. **Mostrar información de inodos:**

```bash
duf --inodes
```

4. **Mostrar solo dispositivos específicos:**

```bash
duf /dev/sda1 /home
```

5. **Salida JSON para procesamiento:**

```bash
duf --json
```

### Ejemplos Complejos:

1. **Monitoreo específico con filtros:**

```bash
duf --only local --hide-fs tmpfs --sort size
```

2. **Script para alerta de espacio bajo:**

```bash
#!/bin/bash
# Alerta si uso > 90%
duf --json | jq '.[] | select(.usage_percent >= 90) | .mount_point'
```

3. **Comparar antes y después:**

```bash
# Guardar estado
duf --json > estado_antes.json
# Realizar operaciones...
# Comparar
duf --json > estado_despues.json
diff estado_antes.json estado_despues.json
```

4. **Integración en panel de monitoreo:**

```bash
# Formato compacto para dashboards
duf --hide-header --hide-footer --only local --no-wrap
```

5. **Tema personalizado para terminal claro:**

```bash
duf --theme light
```

6. **Filtrar por tipo de filesystem:**

```bash
# Mostrar solo ext4 y xfs
duf --only-fs ext4,xfs

# Ocultar sistemas específicos
duf --hide-fs tmpfs,devtmpfs
```

7. **Monitorizar directorio específico:**

```bash
duf /var/log /home/usuario/Documentos
```

## 🎮 Comandos Interactivos y Uso

### Configuración Personalizada:

Crea `~/.config/duf/duf.toml`:
```toml
[general]
# Tema: dark, light, colorful
theme = "dark"
show_header = true
show_footer = true

[sorting]
# Columnas: mountpoint, size, used, avail, usage, filesystem, type
column = "mountpoint"
descending = false

[filter]
only_mounted = true
hide_loop = true
hide_special = false
hide_fs_types = ["tmpfs", "devtmpfs"]
show_local = true
show_network = false
```

### Columnas Disponibles para Ordenar:

- `mountpoint`: Punto de montaje
- `size`: Tamaño total
- `used`: Espacio usado
- `avail`: Espacio disponible
- `usage`: Porcentaje usado
- `filesystem`: Dispositivo/filesystem
- `type`: Tipo de filesystem

## 💡 Consejos Prácticos

1. **Para monitoreo diario:** Configura un alias en tu `.bashrc`:

```bash
alias df='duf --theme dark --only local'
```

2. **En scripts:** Usa `--json` para procesamiento programático:

```bash
duf --json | jq -r '.[] | select(.usage_percent > 80) | .mount_point'
```

3. **Para presentaciones:** Usa `--theme light` si proyectas en pantalla clara

4. **En servidores headless:** Usa `--no-color` si no hay soporte de color

5. **Monitoreo remoto:**

```bash
ssh usuario@servidor "duf --json" | jq ...
```

6. **Configuración persistente:** Crea archivo de configuración para tus preferencias

## 🔍 Información Adicional

### Columnas que Muestra duf:

1. **Device**: Dispositivo/filesystem
2. **Size**: Tamaño total
3. **Used**: Espacio usado
4. **Avail**: Espacio disponible
5. **Use%**: Porcentaje de uso
6. **Type**: Tipo de filesystem
7. **Mount point**: Punto de montaje

### Diferencias con `df` tradicional:

- **Visual**: Colores y formato tabular
- **Inteligente**: Oculta filesystems irrelevantes por defecto
- **Flexible**: Filtrado y ordenación avanzada
- **Moderno**: Soporte JSON, temas, etc.

### Archivo de Configuración:

Ubicaciones buscadas (en orden):

1. `--config` especificado
2. `$XDG_CONFIG_HOME/duf/duf.toml`
3. `~/.config/duf/duf.toml`
4. `/etc/duf/duf.toml`

### Alternativas y Herramientas Relacionadas:

1. **`df` tradicional:**

   ```bash
   df -h  # Formato humano
   df -i  # Información de inodos
   ```

2. **`pydf`**: Versión Python de df con colores

```bash
# Instalación: sudo apt install pydf
   pydf
```

3. **`dust`**: Para uso de directorios (complementa duf)

```bash
# Para ver espacio por directorio
dust /path
```

4. **`ncdu`**: Interfaz interactiva para uso de disco

5. **`lsblk`**: Información de bloques y particiones

```bash
lsblk -f  # Con información de filesystem
```

6. **`baobab`/`Filelight`**: Herramientas gráficas

### Rendimiento:

- `duf` es más lento que `df` por el procesamiento adicional
- Para scripts críticos de rendimiento, usar `df`
- Para monitoreo humano, `duf` es superior

## 🚀 Uso Avanzado

### Script de Alerta Automática:

```bash
#!/bin/bash
# alerta-duf.sh
THRESHOLD=80

while read -r line; do
    mount=$(echo "$line" | jq -r '.mount_point')
    usage=$(echo "$line" | jq -r '.usage_percent')
    
    if (( $(echo "$usage > $THRESHOLD" | bc -l) )); then
        echo "ALERTA: $mount al ${usage}% de uso"
    fi
done < <(duf --json | jq -c '.[]')
```

### Integración con Prometheus/Grafana:

```bash
# Exportar métricas en formato prometheus
duf --json | jq -r '
  .[] | 
  "duf_size_bytes{mount=\"\(.mount_point)\"} \(.size_bytes)" +
  "\nduf_used_bytes{mount=\"\(.mount_point)\"} \(.used_bytes)" +
  "\nduf_usage_percent{mount=\"\(.mount_point)\"} \(.usage_percent)"
'
```

### Dashboard en Terminal con watch:

```bash
# Actualizar cada 2 segundos
watch -n 2 -c duf --theme dark --only local
```

### Combinar con otras herramientas:

```bash
# Espacio total usado por filesystems ext4
duf --json --only-fs ext4 | jq 'map(.used_bytes) | add' | numfmt --to=si
```

## 📚 Recursos Adicionales

1. **Repositorio oficial:** https://github.com/muesli/duf
2. **Documentación completa:** https://github.com/muesli/duf/blob/master/README.md
3. **Issues y contribuciones:** En el repositorio de GitHub
4. **Comunidad:** Discussions en GitHub del proyecto

## 🎯 Comparación y Recomendación

**`duf` vs `df` tradicional:**
- ✅ **duf**: Mejor visualización, filtros, JSON, temas
- ✅ **df**: Más rápido, disponible en todos los sistemas, mejor para scripts

**¿Cuándo usar cada uno?**
- **Usa `duf` para:** Monitoreo manual, dashboards, situaciones donde la legibilidad es importante
- **Usa `df` para:** Scripts de sistema, sistemas minimalistas, máxima compatibilidad

**Recomendación:** Instala `duf` como reemplazo visual de `df` en tus estaciones de trabajo y servidores de desarrollo. Para producción crítica, mantén scripts usando `df` por compatibilidad y rendimiento, pero usa `duf` para diagnóstico manual.

**Comandos complementarios:** Usa `dust` para análisis de directorios y `ncdu` para limpieza interactiva, junto con `duf` para visión general del sistema.