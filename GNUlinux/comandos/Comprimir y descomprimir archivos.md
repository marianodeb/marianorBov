
## TAR `gzip`, `bzip2`, `xz`, etc

Diferencias entre **empaquetar** y **comprimir**, dos conceptos clave que, aunque a menudo se usan juntos, cumplen funciones distintas. 

---

### **1. Empaquetar: Unir archivos en un solo contenedor**

- **Qué hace**: Agrupa múltiples archivos y directorios en un único archivo (llamado *tarball* en el caso de `.tar`), **sin reducir su tamaño**. Es como meter ropa en una maleta: todo queda organizado, pero la maleta no pesa menos .
  - **Herramienta estrella**: `tar` (Tape Archive), creado originalmente para almacenar datos en cintas magnéticas .
  - **Ejemplo**:  
  
```bash
tar -cvf archivo.tar directorio/  # Crea un archivo .tar
```
  - **Ventajas**:  
  
    - Mantiene permisos, estructura de directorios y metadatos (como fechas de modificación) .  
    - Es esencial para copias de seguridad o transferencias de múltiples archivos .

---

### **2. Comprimir: Reducir el tamaño de los datos**

- **Qué hace**: Aplica algoritmos para eliminar redundancias y **disminuir el espacio ocupado**. Es como usar una aspiradora para compactar la ropa en la maleta .

  - **Herramientas comunes**: `gzip`, `bzip2`, `xz`, etc.  
  - **Ejemplo**:  
  
```bash
gzip archivo.tar  # Comprime el archivo .tar → archivo.tar.gz
```
    
  - **Formatos resultantes**:  
    - `.tar.gz` (combinación de `tar` + `gzip`).  
    - `.tar.bz2` (más compresión pero más lento, usando `bzip2`) .

---

### **3. Diferencias clave** 

| **Característica**       | **Empaquetar (tar)**                | **Comprimir (gzip, etc.)**         |
|--------------------------|--------------------------------------|-------------------------------------|
| **Propósito**            | Organizar múltiples archivos en uno | Reducir el tamaño de un archivo     |
| **Altera el tamaño**     | No (incluso puede aumentar ligeramente) | Sí (reduce significativamente) |
| **Metadatos**            | Conserva permisos y estructura       | No añade metadatos adicionales      |
| **Uso típico**           | Copias de seguridad, agrupación      | Transferencia eficiente, ahorro de espacio |

---

### **4. ¿Por qué se usan juntos (ej. .tar.gz)?** 
- **Tar** solo empaqueta, pero no comprime. Para optimizar el espacio, primero se empaqueta con `tar` y luego se comprime con herramientas como `gzip`:  

```bash
tar -czvf archivo.tar.gz directorio/  # Empaqueta Y comprime en un paso
```

- **Ventaja**: Combina la organización de `tar` con la eficiencia de `gzip`. En sistemas Unix/Linux, es el formato estándar para distribuir software .

---

### **5. Ejemplos de otros formatos y sus usos**

- **.zip**: Empaqueta y comprime en un solo paso (común en Windows) .  
- **.tar.xz**: Mayor compresión que `gzip`, pero más lento (ideal para distribuciones Linux) .  
- **.7z**: Alta compresión con cifrado, pero requiere más recursos .

---

### **Conclusión**

- **Empaquetar ≠ Comprimir**, pero son **complementarios**.  
- **`tar`** es el rey del empaquetado en Linux, mientras que **`gzip`/`bzip2`** son los magos de la compresión.  
- Para dominar el arte, recuerda:  
  > *"Primero empaqueta con `tar`, luego comprime con tu algoritmo favorito"* .


---

### Comandos para Comprimir Archivos

#### 1. `tar`

**Sintaxis:**
```bash
tar opciones archivo_destino archivo_origen(s)
```

**Opciones Comunes:**

- `-c`: Crea un nuevo archivo tar.
- `-x`: Extrae archivos de un archivo tar.
- `-f`: Especifica el nombre del archivo tar.
- `-z`: Utiliza gzip para comprimir/decomprimir.
- `-j`: Utiliza bzip2 para comprimir/decomprimir.
- `-J`: Utiliza xz para comprimir/decomprimir.
- `-v`: Muestra el progreso de la operación (verbose).
- `-C directorio`: Cambia al directorio antes de ejecutar la operación.

**Ejemplos:**

- Crear un archivo tar de un directorio y comprimirlo con gzip:

```bash
tar -czvf archivo.tar.gz directorio/
```

- Extraer un archivo tar comprimido con gzip:

```bash
tar -xzvf archivo.tar.gz
```

#### 2. `gzip`

**Explicación:**

`gzip` es un programa de compresión de archivos que se utiliza comúnmente con `tar` para comprimir archivos individuales.

**Sintaxis:**

```bash
gzip opciones archivo(s)
```

**Opciones Comunes:**

- `-d`: Descomprime archivos.
- `-r`: Comprime recursivamente directorios.
- `-v`: Muestra el progreso de la operación (verbose).

**Ejemplos:**

- Comprimir un archivo:

```bash
gzip archivo.txt
```

- Descomprimir un archivo comprimido con gzip:

```bash
gzip -d archivo.txt.gz
```

#### 3. `bzip2`

**Explicación:**

`bzip2` es otra herramienta de compresión que generalmente produce archivos más pequeños que gzip, pero a costa de una velocidad de compresión más lenta.

**Sintaxis:**

```bash
bzip2 opciones archivo(s)
```

**Opciones Comunes:**

- `-d`: Descomprime archivos.
- `-k`: Conserva los archivos originales después de la compresión/descompresión.
- `-v`: Muestra el progreso de la operación (verbose).

**Ejemplos:**

- Comprimir un archivo:

```bash
bzip2 archivo.txt
```

- Descomprimir un archivo comprimido con bzip2:

```bash
bzip2 -d archivo.txt.bz2
```

#### 4. `xz`

**Explicación:**

`xz` es una utilidad de compresión que ofrece una tasa de compresión muy alta y es utilizada principalmente para archivos grandes.

**Sintaxis:**

```bash
xz opciones archivo(s)
```

**Opciones Comunes:**

- `-d`: Descomprime archivos.
- `-k`: Conserva los archivos originales después de la compresión/descompresión.
- `-v`: Muestra el progreso de la operación (verbose).

**Ejemplos:**

- Comprimir un archivo:

```bash
xz archivo.txt
```

- Descomprimir un archivo comprimido con xz:

```bash
xz -d archivo.txt.xz
```

### Comandos para Descomprimir Archivos

Para descomprimir archivos comprimidos, generalmente los comandos son similares a los utilizados para comprimir, pero con opciones específicas para descomprimir.

#### Descomprimir con `tar`

- Extraer un archivo tar:

```bash
tar -xvf archivo.tar
```

- Extraer un archivo tar comprimido con gzip:

```bash
tar -xzvf archivo.tar.gz
```

- Extraer un archivo tar comprimido con bzip2:

```bash
tar -xjvf archivo.tar.bz2
```

- Extraer un archivo tar comprimido con xz:

```bash
tar -xJvf archivo.tar.xz
```

#### Descomprimir con `gzip`

- Descomprimir un archivo comprimido con gzip:

```bash
gzip -d archivo.txt.gz
```

#### Descomprimir con `bzip2`

- Descomprimir un archivo comprimido con bzip2:

```bash
bzip2 -d archivo.txt.bz2
```

#### Descomprimir con `xz`

- Descomprimir un archivo comprimido con xz:

```bash
xz -d archivo.txt.xz
```

---

### Archivos y Ficheros comprimidos

```
bunzip2 file1.bz2: descomprime in fichero llamado ‘file1.bz2’.
```

```
bzip2 file1: comprime un fichero llamado ‘file1’.
```

```
gunzip file1.gz: descomprime un fichero llamado ‘file1.gz’.
```

```
gzip file1: comprime un fichero llamado ‘file1’.
```

```
gzip -9 file1: comprime con compresión máxima.
```

```
rar a file1.rar test_file: crear un fichero rar llamado ‘file1.rar’.
```

```
rar a file1.rar file1 file2 dir1: comprimir ‘file1’, ‘file2’ y ‘dir1’ simultáneamente.
```

```
rar x file1.rar: descomprimir archivo rar.
```

```
unrar x file1.rar: descomprimir archivo rar.
```

```
tar -cvf archive.tar file1: crear un tarball descomprimido.
```

```
tar -cvf archive.tar file1 file2 dir1: crear un archivo conteniendo ‘file1’, ‘file2′ y’dir1’.
```

```
tar -tf archive.tar: mostrar los contenidos de un archivo.
```

```
tar -xvf archive.tar: extraer un tarball.
```

```
tar -xvf archive.tar -C /tmp: extraer un tarball en / tmp.
```

```
tar -cvfj archive.tar.bz2 dir1: crear un tarball comprimido dentro de bzip2.
```

```
tar -xvfj archive.tar.bz2: descomprimir un archivo tar comprimido en bzip2
```

```
tar -cvfz archive.tar.gz dir1: crear un tarball comprimido en gzip.
```

```
tar -xvfz archive.tar.gz: descomprimir un archive tar comprimido en gzip.
```

```
zip file1.zip file1: crear un archivo comprimido en zip.
```

```
zip -r file1.zip file1 file2 dir1: comprimir, en zip, varios archivos y directorios de forma simultánea.
```

```
unzip file1.zip: descomprimir un archivo zip.
```

---


Desempaquetar ficheros .tar

tar -xvf archivo.tar
-x: indica a tar que descomprima el fichero.tar
-v: indica a tar que muestre lo que va desempaquetando
-f: indica a tar que el siguiente argumento es el nombre del fichero a desempaquetar
Ver contenido de un archivo .tar
tar -tf archivo.tar
-t: lista el contenido del fichero .tar
-f: indica a tar que el siguiente argumento es el nombre del fichero a ver

Ficheros .zip

zip archivo.zip fichero_a_comprimir
zip mariano.zip mariano.txt
Descomprimir
unzip archivo.zip
unzip mariano.zip
Ver contenido
unzip -v archivo.zip

Ficheros .rar

rar -a archivo.rar ficheros
Descomprimir ficheros .rar
unrar -x archivo.rar
Ver contenido
unrar -v archivo.rar
unrar -l archivo.rar

Fichero gz

gzip -9 fichero
-9: le indica a gz que utilice el mayor factor de compresión posible
Descomprimir gz
gzip -d fichero.gz
-d: indica descomprimir

Fichero bz2

bzip fichero
Descomprimir gz
bzip2 -d fichero.bz2
Nota: Tanto el compresor gzip como bzip2, sólo comprimen ficheros, no directorios, para comprimir directorios (carpetas), se debe de usar en combinación con tar.

Ficheros tar.gz

tar -czfv archivo.tar.gz fichero
-z: indica que use el compresor gzip

Descomprimir tar.gz

tar -xzvf archivo.tar.gz
-z: indica a tar que esta comprimido con gzip

Ver contenido tar.gz

tar -tzf archivo.tar.gz
Ficheros tar.bz2

para comprimir en tar.bz2 usaremos un truco, mediante el uso del parámetro pipeline (|Esto permite hacer que dos programas trabajen juntos.

tar -c ficheros | bzip2 > archivo.tar.bz2

Descomprimir ficheros tar.bz2

bzip2 -dc archivo.tar.bz2 | tar -xv
Ver contenido .tar.bz2
bzip2 dc archivo.tar.bz2 | tar -t


