
## **Comando `head`**

#### **¿Qué es?**  

`head` es un comando en sistemas Unix/Linux que **muestra las primeras líneas o bytes de un archivo** (por defecto, las primeras 10 líneas). Es útil para:  
- Previsualizar el inicio de archivos grandes (ej: logs, CSVs).  
- Verificar encabezados de archivos (ej: columnas de una tabla).  
- Integrarse con otros comandos para filtrar información.

---

### **Sintaxis básica**  

```bash
head [OPCIONES] [ARCHIVO1] [ARCHIVO2] ...
```

---

### **Opciones principales**  

| Opción | Descripción |  
|--------|-------------|  
| `-n N` | Muestra las **primeras `N` líneas** (ej: `-n 5`). |  
| `-c N` | Muestra los **primeros `N` bytes** (ej: `-c 100`). |  
| `-v`   | **Muestra el nombre del archivo** antes del contenido. |  
| `-q`   | **Oculta el nombre del archivo** (útil para múltiples archivos). |  

---

### **Ejemplos simples**  

#### 1. **Ver las primeras 10 líneas de un archivo**  

```bash
head archivo.log
```

#### 2. **Mostrar las primeras 5 líneas**  

```bash
head -n 5 datos.csv
```

**Salida**:  

```
ID,Nombre,Edad
1,Ana,28
2,Luis,34
3,Carla,22
4,Pedro,45
```

#### 3. **Ver los primeros 100 bytes de un binario**  

```bash
head -c 100 imagen.jpg
```

#### 4. **Mostrar contenido de múltiples archivos**  

```bash
head -n 3 archivo1.txt archivo2.txt
```

**Salida**:  

```
==> archivo1.txt <==
Línea 1
Línea 2
Línea 3

==> archivo2.txt <==
Primera línea
Segunda línea
Tercera línea
```

---

### **Ejemplos avanzados**  

#### 1. **Ignorar las últimas `N` líneas**  

```bash
head -n -5 archivo.log  # Muestra todo excepto las últimas 5 líneas.
```

**Nota**: No todas las versiones de `head` soportan números negativos.

#### 2. **Combinar con `ls` para ver los archivos más recientes**  

```bash
ls -t | head -n 3  # Muestra los 3 archivos modificados más recientemente.
```

#### 3. **Extraer encabezados de un CSV**  

```bash
head -n 1 ventas.csv
```

**Salida**:  

```
Fecha,Producto,Cantidad,Precio
```

#### 4. **Usar con `grep` para filtrar y mostrar inicio**  

```bash
grep "ERROR" sistema.log | head -n 10  # Primeros 10 errores.
```

#### 5. **Ver inicio de un archivo comprimido (con `zcat`)**  

```bash
zcat access.log.gz | head -n 20  # Primeras 20 líneas del log comprimido.
```

---

### **Casos de uso comunes**  

- **Monitorizar logs en tiempo real**:  

```bash
tail -f /var/log/syslog | head -n 25  # Primeras 25 líneas del stream.
```

- **Verificar formato de archivos**:  

```bash
head config.json  # ¿Tiene un encabezado válido?
```

- **Depurar scripts**:  

```bash
head -n 15 script.sh  # Revisar las primeras líneas de código.
```

---

### **Errores frecuentes**  

1. **Confundir `head` con `tail`**:  

- `head` muestra el **inicio** del archivo.  
- `tail` muestra el **final** (y puede seguir cambios en tiempo real con `-f`).  

2. **Usar `head` en archivos binarios**:  

```bash
head imagen.png  # Muestra caracteres ilegibles (no útil).
```

---

### **Consejos**

- **Para archivos enormes**:  

  `head` es más rápido que `cat`, ya que no carga todo el archivo en memoria.  

- **Integración con `awk` o `cut`**:  

```bash
head -n 50 datos.csv | awk -F ',' '{print $2}'  # Segunda columna de las primeras 50 líneas.
```

---

### **Resumen de opciones clave**  

| Propósito               | Comando Ejemplo             |  
|-------------------------|-----------------------------|  
| **Ver inicio de archivo** | `head -n 20 archivo.txt`   |  
| **Previsualizar CSV**   | `head -n 1 datos.csv`       |  
| **Filtrar con pipes**   | `ls -l | head -n 5`           |  

**Tip**: Si necesitas ver el final de un archivo, recuerda que `tail` es tu mejor aliado. ¡Dominar ambos comandos te dará control total sobre tus archivos! 
