

## **`comm`**

### **1. Definición y significado**  

El comando `comm` es una herramienta de Unix/Linux utilizada para comparar dos archivos de texto **ordenados línea por línea**, identificando las líneas comunes y las exclusivas de cada archivo. Genera tres columnas de salida:  
- **Columna 1**: Líneas presentes solo en el primer archivo.  
- **Columna 2**: Líneas presentes solo en el segundo archivo.  
- **Columna 3**: Líneas comunes en ambos archivos.  
Es útil para análisis de datos, verificación de diferencias en logs o bases de datos, y scripts de automatización .

### **2. Instalación (si no viene por defecto)**  

`comm` forma parte del paquete **GNU Core Utilities** (`coreutils`), que suele estar preinstalado en distribuciones Linux y sistemas Unix. Si no está disponible:  
- **Debian/Ubuntu**:  

```bash
sudo apt-get install coreutils
```

- **Fedora/RHEL**:  

```bash
sudo dnf install coreutils
```

En sistemas macOS, está incluido por defecto .

### **3. Sintaxis básica**  

```bash
comm [OPCIONES] archivo1 archivo2
```

**Requisito previo**: Ambos archivos deben estar **ordenados** (usar `sort` antes de ejecutar `comm`) .

### **4. Opciones principales**  

| Opción          | Descripción                                                                 |  
|-----------------|-----------------------------------------------------------------------------|  
| **`-1`**        | Suprime la primera columna (líneas exclusivas del archivo1).                |  
| **`-2`**        | Suprime la segunda columna (líneas exclusivas del archivo2).                |  
| **`-3`**        | Suprime la tercera columna (líneas comunes).                                |  
| **`--check-order`** | Verifica que los archivos estén ordenados (si no, muestra error).           |  
| **`--nocheck-order`** | Omite la verificación de orden (útil si los archivos ya están ordenados).   |  
| **`--output-delimiter=STR`** | Personaliza el separador entre columnas (por defecto: tabulaciones).       |  

### **5. Ejemplos de uso**  

- **Ejemplo simple**: Comparar dos archivos ordenados y mostrar todas las columnas: 
 
```bash
comm archivo1.txt archivo2.txt
```

  *Salida*: 
   
```
  Línea solo en archivo1
          Línea solo en archivo2
                  Línea común
```

- **Ejemplo complejo**: Mostrar solo las líneas comunes (suprimir columnas 1 y 2): 
 
```bash
comm -12 archivo1.txt archivo2.txt
```

  *Uso típico*: Encontrar intersecciones entre listas de usuarios o datos .

- **Personalizar delimitadores**:
  
```bash
comm --output-delimiter=" | " archivo1.txt archivo2.txt
```

  *Resultado*: Separa columnas con ` | ` en lugar de tabulaciones .

### **6. Consejos prácticos**  

- **Ordenar archivos**: Siempre ordena los archivos con `sort` antes de usar `comm`:

```bash
sort archivo1.txt -o archivo1_sorted.txt
sort archivo2.txt -o archivo2_sorted.txt
comm archivo1_sorted.txt archivo2_sorted.txt
```

- **Combina con `sort -u`**: Para eliminar duplicados antes de la comparación .  
- **Usar en scripts**: Ideal para automatizar comparaciones simples sin necesidad de herramientas complejas .  

### **7. Información adicional**  

- **Alternativas modernas**:  

  - `diff`: Detecta diferencias línea por línea con más detalle (muestra cambios específicos) .  
  - `awk` o `grep`: Para comparaciones más flexibles o filtrar patrones complejos .  
  - `csvkit` (para archivos CSV): Herramientas especializadas en datos tabulares .  
  
- **Limitaciones**:  

  - No funciona con archivos no ordenados (a menos que se use `--nocheck-order`).  
  - No soporta comparaciones recursivas de directorios.  

### **8. Comandos relacionados**  

- **`sort`**: Ordena archivos para prepararlos para `comm` .  
- **`diff`**: Compara archivos mostrando diferencias detalladas .  
- **`cmp`**: Compara archivos a nivel de bytes (útil para binarios) .  
- **`grep`**: Busca patrones en archivos, útil para filtrados previos .  

### **9. Notas técnicas**  

- **Historia**: Desarrollado originalmente para sistemas Unix, `comm` es parte del estándar POSIX y sigue siendo relevante por su simplicidad .  
- **Uso avanzado**: En modo scripting, combínalo con `cut` o `sed` para procesar salidas. Por ejemplo, extraer solo líneas únicas de un archivo:  

```bash
comm -23 archivo1_sorted.txt archivo2_sorted.txt
```

**Referencia adicional**: Consulta la página del manual con `man comm` o visita [GNU Core Utilities Documentation](https://www.gnu.org/software/coreutils/manual/html_node/comm-invocation.html) para detalles técnicos .
