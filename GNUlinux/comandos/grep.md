
## GREP

Herramienta para buscar **patrones de texto** en archivos o flujos de entrada usando **expresiones regulares**. Esencial para filtrar logs, procesar datos y depurar código.

**g** globally search
**r** regular expresision
**p** print matching lines

---

### **Sintaxis Básica**

```bash
grep [OPCIONES] "PATRÓN" ARCHIVO(S)
```

| Componente    | Descripción                                                                 |
|---------------|-----------------------------------------------------------------------------|
| `OPCIONES`    | Modifican el comportamiento de búsqueda (ej: `-i` para ignorar mayúsculas). |
| `PATRÓN`      | Texto o expresión regular a buscar.                                         |
| `ARCHIVO(S)`  | Archivo(s) donde se buscará. Si no se especifica, lee de la entrada estándar. |

---

### **🔍 Opciones Clave**

| Opción | Descripción                                                                 |
|--------|-----------------------------------------------------------------------------|
| `-i`   | Ignora mayúsculas/minúsculas.                                               |
| `-v`   | Muestra líneas que **NO** coinciden con el patrón.                          |
| `-r`   | Busca recursivamente en **todos los archivos** de un directorio.            |
| `-n`   | Muestra el número de línea donde se encontró la coincidencia.               |
| `-l`   | Solo lista los **nombres de archivos** que contienen el patrón.             |
| `-c`   | Cuenta el número de líneas coincidentes por archivo.                        |
| `-A N` | Muestra **N líneas después** de la coincidencia (Contexto posterior).       |
| `-B N` | Muestra **N líneas antes** de la coincidencia (Contexto anterior).          |
| `-C N` | Muestra **N líneas alrededor** de la coincidencia.                          |
| `-E`   | Habilita **expresiones regulares extendidas** (equivalente a `egrep`).      |
| `-w`   | Busca palabras completas (evita coincidencias parciales).                  |
| `--color` | Resalta el texto coincidente en color (útil en terminales).               |

---

### **Ejemplos Prácticos**

#### **1. Búsqueda básica en un archivo**

```bash
grep "error" sistema.log
```

**Salida:**

```
2023-10-01 ERROR: Disco lleno.
2023-10-02 error crítico en el servidor.
```

---

#### **2. Ignorar mayúsculas (`-i`) y mostrar números de línea (`-n`)**

```bash
grep -in "timeout" app.log
```

**Salida:**

```
45: 2023-10-01 WARNING: Connection TIMEOUT.
89: 2023-10-02 Error: Timeout en la API.
```

---

#### **3. Buscar en todos los archivos de un directorio (`-r`)**

```bash
grep -r "TODO" ~/proyecto/
```

**Salida:**

```
/home/user/proyecto/app.js: // TODO: Implementar validación.
/home/user/proyecto/README.md: TODO: Agregar documentación.
```

---

#### **4. Mostrar líneas alrededor de una coincidencia (`-C`)**

```bash
grep -C 2 "excepción" debug.log
```

**Salida** (muestra 2 líneas antes y después de la coincidencia):

```
Línea 10: Inicio del proceso.
Línea 11: Validando datos...
Línea 12: **excepción**: División por cero.
Línea 13: Reintentando operación.
Línea 14: Error persistente.
```

---

#### **5. Filtrar procesos en ejecución (combinado con `ps`)**

```bash
ps aux | grep "firefox"
```

**Salida:**

```
usuario  1234  0.5  2.1 987654 32100 ?  Sl   10:00  /usr/lib/firefox
```

---

#### **6. Contar líneas coincidentes (`-c`)**

```bash
grep -c "200 OK" access.log
```

**Salida:**

```
142
```

---

### **🔍 Uso de Expresiones Regulares**

| Patrón        | Descripción                                      | Ejemplo                  |
|---------------|--------------------------------------------------|--------------------------|
| `^inicio`     | Líneas que **comienzan** con "inicio".           | `grep "^start" file.txt` |
| `fin$`        | Líneas que **terminan** con "fin".               | `grep "end$" file.txt`   |
| `a.b`         | Coincide con "a" + cualquier carácter + "b".     | `grep "a.x" file.txt`    |
| `[aeiou]`     | Cualquier vocal.                                 | `grep "[AEIOU]" file.txt`|
| `[0-9]`       | Cualquier dígito.                                | `grep "ID[0-9]" file.txt`|
| `\d`          | Dígito (solo con `-P` para Perl regex).          | `grep -P "\d+" file.txt` |

#### **Ejemplo: Buscar direcciones IP**

```bash
grep -E "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b" log.txt
```

**Explicación:**  

Busca patrones como `192.168.1.1` usando una expresión regular extendida (`-E`).

---

### **Errores Comunes y Tips**

1. **Wildcards vs. Expresiones Regulares**:

   - Los comodines como `*` y `?` funcionan diferente en `grep` (son parte de regex):
     - `*` significa "cero o más repeticiones del carácter anterior".
     - `?` significa "cero o una repetición del carácter anterior".
   - Para buscar cualquier carácter, usa `.*` (ej: `grep "a.*b"`).

2. **Archivos Binarios**:

   - `grep` puede mostrar salidas extrañas en archivos binarios. Usa `-a` para forzar la lectura como texto.

3. **Búsqueda Inversa Útil**:

```bash
# Excluir comentarios en un script:
grep -v "^#" script.sh
```

---

### **Casos de Uso Avanzados**

- **Buscar en múltiples patrones**:

```bash
grep -e "error" -e "warning" sistema.log
```

- **Extraer emails de un archivo**:

```bash
grep -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b" users.txt
```

- **Buscar y reemplazar (con `sed`)**:

```bash
grep -l "old_string" *.txt | xargs sed -i 's/old_string/new_string/g'
```

---

## **Conclusión**

`grep` es una navaja suiza para el procesamiento de texto. Combínalo con `|`, `awk`, `sed`, o `xargs` para flujos de trabajo avanzados.


---

---


El comando `grep` es una herramienta poderosa en sistemas Unix/Linux que se utiliza para buscar patrones dentro de archivos o para filtrar texto basado en patrones específicos. 

### Sintaxis básica de `grep`

La sintaxis general de `grep` es la siguiente:

```
grep opciones patrón archivo(s)
```

- `opciones`: Son parámetros opcionales que modifican el comportamiento de `grep`.
- `patrón`: Es la cadena de texto o expresión regular que `grep` buscará dentro del archivo.
- `archivo(s)`: Son los archivos en los cuales `grep` realizará la búsqueda. Si no se especifican archivos, `grep` busca en la entrada estándar (por ejemplo, la salida de otro comando).

### Ejemplos de uso común

#### Ejemplo 1: Búsqueda de una palabra en un archivo

```bash
grep "palabra" archivo.txt
```
Esto buscará la palabra "palabra" dentro del archivo `archivo.txt` y mostrará todas las líneas que contienen esa palabra.

#### Ejemplo 2: Búsqueda recursiva en directorios

```bash
grep -r "patrón" directorio/
```
Con la opción `-r` (o `-R`), `grep` buscará recursivamente en todos los archivos bajo el directorio especificado (`directorio/` en este caso).

#### Ejemplo 3: Búsqueda de patrones con expresiones regulares

```bash
grep "^inicio" archivo.txt
```
Este comando buscará líneas que comiencen con "inicio" dentro de `archivo.txt`. El símbolo `^` en una expresión regular denota el inicio de una línea.

### Uso de wildcards (comodines)

Los wildcards son caracteres especiales que permiten buscar patrones más generales. Algunos ejemplos:

- `*`: Representa cualquier secuencia de caracteres.
- `?`: Representa un solo carácter.

#### Ejemplo 4: Uso de wildcards

```bash
grep "abc*" archivo.txt
```
Esto buscará cualquier línea que contenga "abc" seguido de cero o más caracteres en `archivo.txt`.

#### Ejemplo 5: Uso de comodín `?`

```bash
grep "a?c" archivo.txt
```
Esto buscará líneas que contengan una "a", seguida de cualquier carácter, seguida de una "c" en `archivo.txt`.

### Opciones útiles de `grep`

- `-i`: Realiza la búsqueda de manera insensible a mayúsculas y minúsculas.
- `-v`: Invierte la búsqueda, mostrando las líneas que NO contienen el patrón.
- `-l`: Muestra solo los nombres de los archivos que contienen el patrón, en lugar de las líneas.
- `-c`: Muestra solo el número de líneas que contienen el patrón en cada archivo, en lugar de las líneas mismas.

