Claro, aquí tienes la sintaxis básica, opciones comunes y ejemplos de los comandos `cat`, `head` y `tail` en sistemas Unix/Linux:

### 1. `cat`

**Sintaxis:**
```bash
cat [opciones] [archivo(s)]
```

**Opciones Comunes:**
- `-n`: Numera las líneas de salida.
- `-b`: Numera las líneas no vacías de salida.
- `-E`: Muestra un `$` al final de cada línea.
- `-T`: Muestra caracteres de tabulación como `^I`.

**Ejemplos:**
- Mostrar el contenido completo de un archivo:
  ```bash
  cat archivo.txt
  ```

- Mostrar el contenido de varios archivos:
  ```bash
  cat archivo1.txt archivo2.txt
  ```

- Numera las líneas de un archivo:
  ```bash
  cat -n archivo.txt
  ```

### 2. `head`

**Sintaxis:**
```bash
head [opciones] [archivo(s)]
```

**Opciones Comunes:**
- `-n NUM`: Muestra las primeras NUM líneas (por defecto 10).
- `-c NUM`: Muestra los primeros NUM bytes del archivo.
- `-q`: Suprime encabezados de nombre de archivo si se muestran más de un archivo.

**Ejemplos:**
- Mostrar las primeras 10 líneas de un archivo:
  ```bash
  head archivo.txt
  ```

- Mostrar las primeras 5 líneas de varios archivos:
  ```bash
  head -n 5 archivo1.txt archivo2.txt
  ```

- Mostrar los primeros 100 bytes de un archivo:
  ```bash
  head -c 100 archivo.txt
  ```

### 3. `tail`

**Sintaxis:**
```bash
tail [opciones] [archivo(s)]
```

**Opciones Comunes:**
- `-n NUM`: Muestra las últimas NUM líneas (por defecto 10).
- `-f`: Muestra las últimas líneas y se queda en espera de nuevas líneas (útil para logs en tiempo real).
- `-c NUM`: Muestra los últimos NUM bytes del archivo.

**Ejemplos:**
- Mostrar las últimas 10 líneas de un archivo:
  ```bash
  tail archivo.txt
  ```

- Mostrar las últimas 20 líneas de varios archivos:
  ```bash
  tail -n 20 archivo1.txt archivo2.txt
  ```

- Mostrar las últimas 200 bytes de un archivo:
  ```bash
  tail -c 200 archivo.txt
  ```

- Mostrar las últimas líneas de un archivo y seguir en tiempo real (útil para logs):
  ```bash
  tail -f archivo.log
  ```

