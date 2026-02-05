# Comando `stat` - Guía Completa

## 📖 **Definición y Significado**

`stat` es un comando en sistemas Unix/Linux que muestra información detallada (metadatos) sobre archivos y sistemas de archivos. Su nombre proviene de "status" o "estadísticas". Proporciona información como:
- Permisos y propiedad
- Tamaños (en bytes y bloques)
- Fechas de acceso, modificación y cambio
- Número de inodo
- Tipo de archivo
- Información del dispositivo

## 🔧 **Instalación**

**Ubuntu/Debian:**

```bash
# Viene instalado por defecto en la mayoría de distribuciones
# Si no está presente:
sudo apt-get install coreutils
```

**CentOS/RHEL/Fedora:**

```bash
# Generalmente viene por defecto
# Si es necesario:
sudo yum install coreutils
```

**macOS:**

```bash
# Viene preinstalado
# Versión BSD (diferente de GNU/Linux)
```

## 📝 **Sintaxis Básica**

```bash
stat [OPCIONES]... ARCHIVO...
```

## ⚙️ **Todas las Opciones (GNU stat)**

### **Opciones de Formato:**

```bash
-L, --dereference     Seguir enlaces simbólicos
-f, --file-system     Mostrar info del sistema de archivos en lugar del archivo
-c, --format=FORMATO  Usar el formato especificado
--printf=FORMATO      Similar a --format pero interpreta secuencias de escape
-t, --terse           Mostrar en formato conciso
```

### **Opciones de Información:**

```bash
--help     Mostrar ayuda
--version  Mostrar versión
```

## 📊 **Formatos Especiales**

### **Secuencias de formato para --format/--printf:**

**Para archivos:**

```
%a  Permisos en octal
%A  Permisos en formato legible
%b  Bloques asignados
%B  Tamaño en bytes por bloque
%d  Número de dispositivo en decimal
%D  Número de dispositivo en hexadecimal
%f  Modo en hexadecimal
%F  Tipo de archivo
%g  ID del grupo propietario
%G  Nombre del grupo propietario
%h  Número de enlaces duros
%i  Número de inodo
%m  Punto de montaje
%n  Nombre del archivo
%N  Nombre con comillas (→ enlace simbólico)
%o  Tamaño de bloque I/O óptimo
%s  Tamaño total en bytes
%t  Número de dispositivo mayor en hexadecimal
%T  Número de dispositivo menor en hexadecimal
%u  ID del usuario propietario
%U  Nombre del usuario propietario
%w  Hora de creación (nacimiento)
%W  Hora de creación como segundos desde Epoch
%x  Hora del último acceso
%X  Hora del último acceso en segundos desde Epoch
%y  Hora de última modificación
%Y  Hora de última modificación en segundos desde Epoch
%z  Hora del último cambio
%Z  Hora del último cambio en segundos desde Epoch
```

**Para sistemas de archivos:**

```
%a  Bloques libres disponibles para usuarios no root
%b  Bloques de datos totales
%c  Bloques de inodos totales
%d  Bloques de inodos libres
%f  Bloques libres
%i  Número de inodos libres
%l  Longitud máxima de nombres de archivo
%n  Nombre del archivo
%s  Tamaño de bloque
%S  Tamaño de bloque fundamental
%t  Tipo de sistema de archivos en hexadecimal
%T  Tipo de sistema de archivos en texto legible
```

## 📚 **Ejemplos Prácticos**

### **Ejemplos Simples:**

1. **Información básica de un archivo:**

```bash
stat archivo.txt
```

2. **Información de múltiples archivos:**

```bash
stat archivo1.txt archivo2.txt
```

3. **Información concisa:**

```bash
stat -t /etc/passwd
```

4. **Seguir enlaces simbólicos:**

```bash
stat -L /usr/bin/python
```

### **Ejemplos Complejos:**

1. **Formato personalizado:**

```bash
# Solo mostrar nombre, tamaño y fecha de modificación
stat --format='Nombre: %n, Tamaño: %s bytes, Modificado: %y' archivo.txt

# Formato con tabulaciones
stat -c $'%n\t%s\t%y' *.txt
```

2. **Información del sistema de archivos:**

```bash
# Info del sistema de archivos donde está el archivo
stat -f /home/usuario/

# Formato personalizado para sistema de archivos
stat -f --format='Sistema: %T, Bloques libres: %f, Tamaño bloque: %s' /
```

3. **Script para monitorear cambios:**

```bash
#!/bin/bash
# Monitorear cambios en un archivo
ARCHIVO="/var/log/syslog"
ESTADO_ANTERIOR=$(stat -c %Y "$ARCHIVO")

while true; do
    ESTADO_ACTUAL=$(stat -c %Y "$ARCHIVO")
    if [ "$ESTADO_ANTERIOR" != "$ESTADO_ACTUAL" ]; then
        echo "El archivo $ARCHIVO ha sido modificado"
        ESTADO_ANTERIOR="$ESTADO_ACTUAL"
    fi
    sleep 5
done
```

4. **Comparar metadatos de dos archivos:**

```bash
#!/bin/bash
# Comparar metadatos de dos archivos
comparar_archivos() {
    echo "Comparando $1 y $2"
    echo "====================="
    
    for campo in %s %U %G %a %y; do
        valor1=$(stat --format="$campo" "$1")
        valor2=$(stat --format="$campo" "$2")
        
        case $campo in
            "%s") nombre="Tamaño";;
            "%U") nombre="Usuario";;
            "%G") nombre="Grupo";;
            "%a") nombre="Permisos";;
            "%y") nombre="Modificación";;
        esac
        
        if [ "$valor1" = "$valor2" ]; then
            echo "✓ $nombre: IGUAL ($valor1)"
        else
            echo "✗ $nombre: DIFERENTE"
            echo "  $1: $valor1"
            echo "  $2: $valor2"
        fi
    done
}

comparar_archivos archivo1.txt archivo2.txt
```

5. **Encontrar archivos modificados recientemente:**

```bash
# Archivos modificados en las últimas 24 horas
find /var/log -type f -mtime -1 -exec stat -c '%y %n' {} \;

# Ordenados por fecha de modificación
find /etc -type f -exec stat -c '%Y %n' {} \; | sort -n
```

## 💡 **Consejos Prácticos**

1. **Para scripting**, usa `-c` o `--format` para obtener datos específicos
2. **Los tiempos** se muestran en tres formas:
   - `Access`: último acceso (lectura)
   - `Modify`: última modificación del contenido
   - `Change`: último cambio de metadatos (permisos, propiedad)

3. **Diferencia entre `stat` de GNU y BSD** (macOS):
   ```bash
   # GNU/Linux
   stat -c %s archivo
   
   # macOS/BSD
   stat -f %z archivo
   ```

4. **Usa `stat` con `xargs`** para procesar múltiples archivos:
   ```bash
   find . -name "*.log" -print0 | xargs -0 stat -c "%s %n"
   ```

## 🔄 **Comandos Relacionados y Alternativas**

### **Comandos Similares:**

- **`ls -l`** - Información básica (menos detallada)
- **`file`** - Determina tipo de archivo
- **`find -printf`** - Similar formato a stat
- **`du`** - Uso de espacio en disco
- **`df`** - Espacio libre en sistemas de archivos

### **Alternativas Modernas:**

1. **`exa`** (reemplazo moderno de `ls`):
   ```bash
   exa -l --git --time-style=long-iso
   ```

2. **`bat`** (con preview de archivos):
   ```bash
   bat --metadata filename.txt
   ```

3. **Con `Python`** (para mayor flexibilidad):
   ```python
   import os, stat, time
   info = os.stat('archivo.txt')
   print(time.ctime(info.st_mtime))
   ```

## 📋 **Información Adicional**

### **Códigos de Salida:**

- `0` - Éxito
- `1` - Error

### **Limitaciones:**

- No muestra contenido del archivo
- En sistemas de archivos antiguos, algunos campos pueden estar vacíos
- El tiempo de "nacimiento" (birth time) no está soportado en todos los sistemas de archivos

### **Variables de Entorno:**

- `LANG`, `LC_ALL` - Afectan a la localización de salida
- `TZ` - Zona horaria para las fechas

### **Compatibilidad:**

- GNU `stat` es más completo que BSD `stat`
- Para scripts portables, considerar usar `ls -l` o `find -printf`

## 🎯 **Casos de Uso Avanzados**

1. **Auditoría de seguridad:**
```bash
# Verificar permisos de archivos sensibles
stat -c "%a %U %G %n" /etc/passwd /etc/shadow /etc/sudoers
```

2. **Backup diferencial:**
```bash
# Usar mtime para backups incrementales
stat -c %Y archivo_datos.db > .ultimo_backup
```

3. **Detección de intrusiones:**
```bash
# Monitorear cambios en binarios críticos
CRITICOS="/bin/bash /usr/bin/sudo /usr/sbin/sshd"
for bin in $CRITICOS; do
    stat -c "%n %a %U %G %y" "$bin" >> /var/log/binarios_baseline.log
done
```

4. **Análisis forense:**
```bash
# Recopilar metadatos de todo un directorio
find /directorio/ -type f -exec stat -c "%i|%A|%U|%G|%s|%y|%n" {} \; > metadatos.csv
```

## 🚀 **Mejores Prácticas**

1. **En scripts**, siempre validar que el archivo existe antes de usar `stat`
2. **Para eficiencia**, evita llamar `stat` múltiples veces en bucles
3. **Usa formato específico** en lugar de parsear la salida por defecto
4. **Considera `lstat`** si no quieres seguir enlaces simbólicos

El comando `stat` sigue siendo relevante y ampliamente usado, especialmente en scripts y administración de sistemas, por su precisión y capacidad de formateo de salida.
