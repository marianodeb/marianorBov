


## **`sed`**



### **1. Definición y significado**

`sed` (**S**tream **ED**itor) es un editor de texto no interactivo que procesa flujos de datos línea por línea. Su principal función es buscar, reemplazar, insertar o eliminar texto usando patrones (incluyendo expresiones regulares). Es ideal para automatizar tareas en scripts o manipular archivos sin abrirlos manualmente .


### **2. Sintaxis**  
La estructura básica es:

```bash
sed [opciones] 'comando' archivo
```  
Ejemplo:  
```bash
sed 's/patrón/reemplazo/g' archivo.txt
```

- **Delimitadores**: Puedes usar `/`, `|`, `:` u otros caracteres para evitar conflictos con texto que contenga `/` .  
- **Scripts**: Permite múltiples comandos con `-e` o leyendo desde un archivo con `-f` .

---

### **3. Todas sus opciones**

| Opción | Descripción |  
|--------|-------------|  
| `-i` | Edita el archivo directamente (sin crear copia). Usa `-i.bak` para crear un backup . |  
| `-n` | Suprime la salida automática (útil con `p` para imprimir solo líneas modificadas) . |  
| `-e` | Permite ejecutar múltiples comandos (ej: `sed -e 's/a/A/' -e 's/b/B/'`) . |  
| `-r` | Habilita expresiones regulares extendidas (ej: `+`, `?`) . |  
| `-f` | Lee comandos desde un archivo externo . |  

---

### **4. Ejemplos**

#### **Simples**

- **Reemplazar primera ocurrencia en cada línea**:

```bash
sed 's/Windows/Linux/' archivo.txt
```
  
- **Reemplazar todas las ocurrencias (global)**:

```bash
sed 's/error/ÉXITO/g' log.txt
```
  
- **Borrar la línea 5**:

```bash
sed '5d' datos.csv
```

#### **Complejos**

- **Reemplazar solo en líneas 10-20**:

```bash
sed '10,20 s/mysql/PostgreSQL/g' config.conf
```
  
- **Ignorar mayúsculas/minúsculas**:

```bash
sed 's/error/OK/gi' reporte.log
```
  
- **Usar múltiples comandos y crear backup**:

```bash
sed -i.bak -e 's/foo/bar/g' -e '/^#/d' script.py
```
  
- **Modificar un rango de líneas que coincidan con un patrón**:

```bash
sed '/START/,/END/ s/draft/final/' documento.txt
```
  

---

### **5. Consejos**

- **Backups**: Siempre usa `-i.bak` para evitar pérdidas de datos .  
- **Pruebas**: Ejecuta sin `-i` primero para ver resultados en terminal .  
- **Delimitadores alternativos**: Si el texto contiene `/`, usa `|` o `#` (ej: `sed 's|/usr/bin|/opt|g'`) .  
- **Combina con `find`**: Para procesar múltiples archivos:

```bash
find . -name "*.html" -exec sed -i 's/old_link/new_link/g' {} \;
```

---

### **6. Información adicional**

- **Historia**: Creado en los 70 por Lee E. McMahon como sucesor de `grep`, influyó en Perl y AWK .  
- **Expresiones regulares**: Soporta `.*` (cualquier carácter), `^` (inicio de línea), `$` (fin de línea), y grupos `\(...\)` .  
- **Limitaciones**: No maneja archivos binarios. Para tareas más complejas (ej: JSON), considera `jq` o `awk` .

---

### **7. Comandos relacionados**

- **`awk`**: Ideal para procesar columnas o datos estructurados .  
- **`grep`**: Búsqueda rápida de patrones (sin edición) .  
- **`perl`**: Ofrece capacidades similares a `sed` pero con sintaxis más poderosa .  

---



`sed` sigue siendo esencial en Unix/Linux, pero para tareas avanzadas (ej: scripts multinivel), se recomienda combinar con `awk` o `Python` .

[ejemplos detallados en los recursos citados](https://geekland.eu/uso-del-comando-sed-en-linux-y-unix-con-ejemplos/).



