
## `find`

### **¿Qué es el comando `find`?**

Es una herramienta poderosa en sistemas Unix/Linux para **buscar archivos y directorios en tiempo real** dentro del sistema de archivos. A diferencia de `locate`, `find` no usa una base de datos, por lo que es más lento pero extremadamente flexible y preciso.

### **Sintaxis General**

```bash
find [ruta...] [expresión]
```

- **`[ruta...]`**: Directorio(s) donde buscar (ej: `/home`, `.` para el directorio actual).
- **`[expresión]`**: Combinación de opciones, tests y acciones que definen la búsqueda.

---

## **Componentes Clave de la Expresión**

1. **Opciones**: Configuran el comportamiento general (ej: `-maxdepth`).
2. **Tests**: Filtran resultados por atributos (ej: `-name`, `-size`).
3. **Acciones**: Ejecutan comandos sobre los resultados (ej: `-print`, `-exec`).

---

## **Opciones Principales**

### **1. Búsqueda por Nombre**

- **`-name "patrón"`**: Busca por nombre (sensible a mayúsculas).

```bash
find /home -name "documento.txt"
```

- **`-iname "patrón"`**: Ignora mayúsculas/minúsculas.

```bash
find . -iname "*.JPG"
```

---

### **2. Búsqueda por Tipo de Archivo**

- **`-type [f|d|l]`**: Filtra por tipo:

  - `f`: Archivos regulares.
  - `d`: Directorios.
  - `l`: Enlaces simbólicos.
  
```bash
find /var/log -type f -name "*.log"
```

---

### **3. Búsqueda por Tamaño**

- **`-size [+/-]N[c|k|M|G]`**:

  - `+N`: Archivos mayores que `N`.
  - `-N`: Archivos menores que `N`.
  - Unidades: `c` (bytes), `k` (KB), `M` (MB), `G` (GB).
  
```bash
find / -size +100M    # Archivos > 100 MB
find . -size -10k     # Archivos < 10 KB
```

---

### **4. Búsqueda por Fechas**

- **`-mtime [+/-]N`**: Modificación hace `N` días.

```bash
find /backup -mtime -7  # Modificados en los últimos 7 días
```

- **`-atime [+/-]N`**: Último acceso.

```bash
find /home -atime +30  # No accedidos en 30 días
```

---

### **5. Búsqueda por Permisos**

- **`-perm [modo]`**: Filtra por permisos (octal o simbólico).

```bash
find . -perm 644        # Archivos con permisos 644
find /etc -perm -u=r    # Legibles por el dueño
```

---

### **6. Búsqueda por Usuario/Grupo**

- **`-user [nombre]`**: Archivos del usuario especificado.

```bash
find /var -user www-data
```

- **`-group [nombre]`**: Archivos del grupo especificado.

```bash
find /home -group developers
```

---

### **7. Búsqueda por Profundidad**

- **`-maxdepth N`**: Limita la profundidad de búsqueda.

```bash
find / -maxdepth 3 -name "*.conf"
```

---

## **Acciones para Procesar Resultados**

### **1. `-print`**

Muestra los resultados (acción por defecto).

```bash
find ~/Documents -name "*.pdf" -print
```

---

### **2. `-exec`**

Ejecuta un comando sobre cada resultado.

- **Sintaxis**: `-exec comando {} \;` (donde `{}` es el archivo actual).

```bash
find . -name "*.tmp" -exec rm {} \;  # Eliminar archivos .tmp
find /var/log -type f -exec chmod 644 {} \;  # Cambiar permisos
```

---

### **3. `-delete`**

Elimina archivos encontrados.

```bash
find /tmp -name "*.cache" -delete
```

---

### **4. `-ok`**

Como `-exec`, pero pide confirmación antes de ejecutar.

```bash
find . -name "*.bak" -ok rm {} \;
```

---

## **Ejemplos Prácticos**

### **1. Buscar archivos vacíos**

```bash
find /home -type f -empty
```

### **2. Encontrar archivos modificados hoy**

```bash
find . -type f -mtime 0
```

### **3. Buscar directorios con permisos 777**

```bash
find / -type d -perm 777
```

### **4. Buscar archivos de más de 1 GB y listarlos**

```bash
find / -size +1G -exec ls -lh {} \;
```

### **5. Buscar archivos .log y comprimirlos**

```bash
find /var/log -name "*.log" -exec gzip {} \;
```

---

## **Expresiones Avanzadas**

### **1. Combinar múltiples condiciones**

- **AND implícito** (separando tests):

```bash
find . -name "*.jpg" -size +1M  # JPG > 1 MB
```

- **OR explícito** (`-o`):

```bash
find / -name "*.mp3" -o -name "*.mp4"
```

- **Negación** (`-not` o `!`):

```bash
find . -type f ! -name "*.txt"
```

---

### **2. Buscar y copiar archivos**

```bash
find /home -name "*.docx" -exec cp {} /backup \;
```

---

### **3. Buscar archivos y redirigir resultados**

```bash
find /etc -type f -name "*.conf" > lista_configuraciones.txt
```

---

### **Consideraciones de Seguridad**

- **Evita inyección de comandos**: Usa `-exec` con `\;` y no con `&&`.
- **Citas en patrones**: Usa comillas para patrones con espacios o caracteres especiales:

```bash
find . -name "archivo con espacios.txt"
```

---

### **Comparación `find` vs `locate`**

| **Característica**      | **`find`**                          | **`locate`**                      |
|--------------------------|-------------------------------------|-----------------------------------|
| Velocidad                | Lento (busca en tiempo real)        | Rápido (usa base de datos)        |
| Actualización            | Siempre actualizado                 | Depende de `updatedb`             |
| Complejidad              | Alta (múltiples opciones)           | Baja (búsquedas simples)          |
| Uso de recursos          | Alto (escanea directorios)          | Bajo (consulta base de datos)     |
| Flexibilidad             | Muy flexible (permite acciones)     | Limitada                          |

---

### **Conclusión**

- Usa **`find`** cuando necesites:
  - Búsquedas en tiempo real.
  - Filtrar por atributos avanzados (tamaño, fecha, permisos).
  - Ejecutar acciones sobre los resultados (eliminar, modificar, etc.).
- **`locate`** es mejor para búsquedas rápidas y simples.


