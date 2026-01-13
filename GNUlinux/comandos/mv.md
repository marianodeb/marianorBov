## `mv`

### **Definición y Significado**

`mv` (**m**o**v**e) es un comando para **mover o renombrar archivos y directorios** en sistemas Linux/Unix. Funciona de dos maneras:  

1. **Mover**: Llevar un archivo/directorio de una ubicación a otra.  
2. **Renombrar**: Cambiar el nombre de un archivo/directorio en la misma ubicación.

---

### **Sintaxis**

```bash
mv [OPCIONES] <origen> <destino>
```

- **`<origen>`**: Archivo(s) o directorio(s) a mover/renombrar.  
- **`<destino>`**:

  - Si es un **directorio**: Los archivos se moverán allí.  
  - Si es un **nombre nuevo**: El origen se renombrará.

---

### **Opciones Principales**

| Opción | Descripción |  
|--------|-------------|  
| `-i`   | Pregunta antes de sobrescribir un archivo (**modo interactivo**). |  
| `-v`   | Muestra detalles de lo que se está haciendo (**verbose**). |  
| `-n`   | **No sobrescribe** archivos existentes. |  
| `-u`   | Mueve solo si el origen es **más reciente** que el destino. |  
| `-b`   | Crea un **backup** de los archivos que se sobrescriben (agrega `~` al nombre). |  
| `-f`   | **Fuerza** la operación (ignora advertencias y sobrescribe). |  
| `-t <directorio>` | Especifica el directorio destino **al inicio** (útil para múltiples archivos). |  

---

### **Ejemplos Simples**  

1. **Renombrar un archivo**:

```bash
mv informe.txt informe_final.txt
```

2. **Mover un archivo a otro directorio**:

```bash
mv foto.jpg ~/Imágenes/
```

3. **Mover múltiples archivos a un directorio**:

```bash
mv *.txt documentos/
```

---

### **Ejemplos Complejos**

1. **Mover archivos con confirmación y detalles** (`-i` + `-v`):

```bash
mv -iv *.log /var/logs/
```

2. **Mover archivos y crear backup si existen** (`-b`):

```bash
mv -b config.conf /etc/
# Si /etc/config.conf existe, se guardará como /etc/config.conf~
```

3. **Usar `-t` para mover múltiples archivos**:

```bash
mv -t /backup/ archivo1 archivo2 archivo3
```

4. **Mover solo archivos actualizados** (`-u`):

```bash
mv -u *.html /var/www/  # Solo mueve los HTML modificados recientemente
```

---

### **Consejos de Uso**

1. **¡Cuidado con sobrescribir!**

   - Usa `-i` para evitar borrar archivos por accidente.  
   - Ejemplo: `alias mv='mv -i'` (agrégalo a tu `.bashrc` para hacerlo permanente).  

2. **Verifica rutas**:

   - Si el directorio destino no existe, `mv` renombrará el archivo como si fuera un nuevo nombre.  

3. **Usa `-v` en scripts**:

   - Para saber qué hizo `mv` en operaciones críticas.  

4. **Espacios en nombres**:

   - Usa comillas si hay espacios: `mv "mi documento.pdf" "nuevo nombre.pdf"`.

---

### **Información Adicional**

- **Permisos**: Necesitas permisos de escritura en el directorio origen y destino.

- **Directorios vs. Archivos**:

  - Si mueves un directorio, todos sus contenidos se moverán.
  
- **Entre sistemas de archivos**:

  - Si mueves un archivo entre particiones/dispositivos, `mv` copia y borra el original (como `cp` + `rm`).
  
- **Enlaces simbólicos**:

  - `mv` no sigue enlaces simbólicos; mueve el enlace, no el archivo al que apunta.
  
- **Exit Codes**:

  - `0`: Éxito.  
  - `1`: Error (ej: archivo no encontrado).  



