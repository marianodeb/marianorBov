 `awk` es una herramienta poderosa para el procesamiento de texto y datos en sistemas Unix y Linux. Es un lenguaje de programación orientado a patrones que permite realizar operaciones sobre textos, normalmente en formato de columnas.

`awk` es una herramienta para manipular y analizar archivos de texto. Funciona leyendo líneas de entrada y procesándolas según los patrones y acciones especificados.

### Sintaxis Básica

```bash
awk 'patrón {acción}' archivo
```

- **`patrón`**: Expresión regular que se usa para seleccionar las líneas que serán procesadas.
- **`acción`**: Código que se ejecuta para las líneas que coinciden con el patrón.
- **`archivo`**: Archivo de entrada. Si no se especifica, `awk` lee desde la entrada estándar.

```bash
awk 'program' archivo
```

Donde:

    program es el conjunto de instrucciones que especifican cómo procesar el archivo.
    archivo es el archivo de entrada.

Aquí tienes una guía completa y detallada sobre `awk`, incluyendo opciones, ejemplos y su uso en diversas situaciones.

### Opciones Comunes

#### 1. **`-f archivo`**

   Especifica un archivo que contiene el programa `awk`. Esto permite escribir scripts `awk` más largos y complejos en un archivo separado.

```bash
awk -f programa.awk archivo
```

#### 2. **`-v nombre=valor`**

Define variables de `awk` desde la línea de comandos.

```bash
awk -v FS="," '{print $1}' archivo.csv
```

#### 3. **`-F delimitador`**

Define el delimitador de campos. El valor por defecto es espacio o tabulación.

```bash
awk -F":" '{print $1}' archivo.txt
```

#### 4. **`-W compat`**

   Activa la compatibilidad con la versión anterior de `awk` (para GNU `awk`).

```bash
awk -W compat 'BEGIN {print "Compatibilidad activada"}'
```

#### 5. **`-W `**

Otras opciones de compatibilidad pueden ser especificadas con `-W`, como `posix`, `traditional`, y `gawk` para la versión GNU de `awk`.

```bash
awk -W traditional 'BEGIN {print "Modo tradicional"}'
```

### Uso Básico y Ejemplos

#### 1. **Imprimir Columnas Específicas**

Imprime la primera columna del archivo.

```bash
awk '{print $1}' archivo.txt
```

#### 2. **Uso de Delimitador Personalizado**

Imprime la primera columna de un archivo CSV usando coma como delimitador.

```bash
awk -F"," '{print $1}' archivo.csv
```

#### 3. **Filtrar Línea por Patrón**
Imprime líneas que contienen el patrón "texto".
 
```bash
awk '/texto/' archivo.txt
```

#### 4. **Condiciones de Patrón**
 
Imprime la línea si el valor de la segunda columna es mayor que 50.

```bash
awk '$2 > 50' archivo.txt
```

#### 5. **Formato de Salida**

Imprime el nombre y el valor en formato tabulado.

```bash
awk '{printf "%s\t%s\n", $1, $2}' archivo.txt
```

#### 6. **Uso de Variables de `awk`**

Define una variable `FS` para cambiar el delimitador de campos.

```bash
awk -v FS=":" '{print $1}' archivo.txt
```

#### 7. **Acción en el Bloque `BEGIN` y `END`**

Imprime un mensaje al inicio y al final del procesamiento.

```bash
awk 'BEGIN {print "Inicio"} {print $1} END {print "Fin"}' archivo.txt
```

#### 8. **Operaciones Matemáticas**

Calcula la suma de los valores en la segunda columna.

```bash
awk '{suma += $2} END {print suma}' archivo.txt
```

#### 9. **Formatear Salida**

Imprime las columnas en un formato alineado.
```bash
awk '{printf "%-10s %-10s\n", $1, $2}' archivo.txt
```

#### 10. **Uso de Funciones Integradas**

Usa la función `length()` para imprimir la longitud de cada línea.
```bash
awk '{print length($0)}' archivo.txt
```

### Ejemplos Avanzados

#### 1. **Leer y Escribir Archivos**

Lee un archivo y escribe en otro archivo.

```bash
awk '{print $1}' archivo.txt > salida.txt
```

#### 2. **Contar Líneas que Coinciden con un Patrón**

Cuenta cuántas líneas contienen el patrón "error".

```bash
awk '/error/ {count++} END {print count}' archivo.txt
```

#### 3. **Reemplazo de Texto**

Reemplaza "antiguo" por "nuevo" en un archivo.

```bash
awk '{gsub(/antiguo/, "nuevo"); print}' archivo.txt
```

#### 4. **Agrupación y Resumen**

Imprime la suma de la tercera columna agrupada por la primera columna.

```bash
awk '{suma[$1] += $3} END {for (i in suma) print i, suma[i]}' archivo.txt
```

#### 5. **Usar `awk` con Entrada Estándar**

Usa `echo` para pasar datos a `awk` directamente.

```bash
echo -e "uno dos\ntres cuatro" | awk '{print $2}'
```

### Ejemplos de Scripts en Archivo

#### 1. **Archivo `programa.awk`**

Contenido del archivo `programa.awk`:

```awk
BEGIN { print "Inicio del Programa" }
/patrón/ { print $1 }
END { print "Fin del Programa" }
```
 
Ejecutar el script:

```bash
awk -f programa.awk archivo.txt
```

#### 2. **Script para Calcular Promedio**

Contenido del archivo `promedio.awk`:

```
    awk
   {
     suma += $1
     conteo++
   }
   END {
     if (conteo > 0) {
       print suma / conteo
     } else {
       print "No hay datos"
     }
   }
   ```
   Ejecutar el script:
   ```bash
   awk -f promedio.awk archivo.txt
```

### Resumen de las Opciones

- **`-f archivo`**: Ejecutar un programa `awk` desde un archivo.
- **`-v nombre=valor`**: Definir variables de `awk` desde la línea de comandos.
- **`-F delimitador`**: Establecer el delimitador de campos.
- **`-W compat`**: Activar compatibilidad con versiones anteriores.
- **`-W`**: Otras opciones de compatibilidad (`posix`, `traditional`, `gawk`).

Espero que esta guía detallada te ayude a comprender y usar `awk` de manera efectiva. Si tienes alguna pregunta específica o necesitas más ejemplos, no dudes en preguntar.


### Funciones de salida

print: Imprime datos (con separador de campo definido por OFS).
printf: Imprime datos con formato, similar a la función printf de C.

### Funciones de cadenas de texto

length: Devuelve la longitud de una cadena o campo.
substr(s, i, n): Extrae una subcadena desde la posición i con longitud n.
index(s, t): Devuelve la posición de la primera aparición de t en s.
tolower(s): Convierte una cadena a minúsculas.
toupper(s): Convierte una cadena a mayúsculas.
split(s, a, sep): Divide la cadena s en el arreglo a usando sep como separador.
match(s, r): Encuentra coincidencias basadas en expresiones regulares.

### Funciones numéricas

sqrt(x): Devuelve la raíz cuadrada de x.
sin(x), cos(x), atan2(y, x): Funciones trigonométricas.
log(x): Logaritmo natural de x.
exp(x): Devuelve e^x.
int(x): Devuelve la parte entera de x.
rand(): Devuelve un número aleatorio entre 0 y 1.
srand(x): Inicializa la semilla para rand.

### Estructuras de control

if: Condicional.
for: Bucles (tanto for tradicional como for-in para arreglos).
while: Bucle mientras.
do-while: Bucle hacer-mientras.

---


Sintaxis básica

```bash
awk 'program' archivo
```

Donde:

    program es el conjunto de instrucciones que especifican cómo procesar el archivo.
    archivo es el archivo de entrada.

Un ejemplo básico:

```bash
awk '{print $1}' archivo.txt
```

Esto imprime la primera columna de cada línea del archivo archivo.txt.
Partes principales de un programa awk

    Patrón (pattern): Condición para seleccionar líneas.
    Acción (action): Lo que se ejecuta en las líneas seleccionadas.
    Estructura: { patrón { acción } }.

Ejemplo:

```bash
awk '/error/ {print $0}' archivo.log
```

Esto selecciona las líneas que contienen la palabra "error" y las imprime.
Opciones comunes de awk

    -F: Define el separador de campos (por defecto, el espacio o tabulación).

```bash
awk -F"," '{print $2}' archivo.csv
```

Esto selecciona la segunda columna de un archivo CSV.

-v: Define variables desde la línea de comandos.

```bash
awk -v var=10 '{print $1 + var}' archivo.txt
```

Construcciones comunes en awk

    Variables predefinidas:
        $0: La línea completa.
        $1, $2, ...: Campos individuales.
        NR: Número de línea actual.
        NF: Número total de campos en la línea actual.

    Condiciones:

```bash
awk '$3 > 50 {print $1, $3}' archivo.txt
```

Imprime la primera y tercera columna de las líneas donde la tercera columna es mayor a 50.

Ciclos y bloques:

```bash
awk 'BEGIN {print "Inicio"} {print $1} END {print "Fin"}' archivo.txt
```

Esto imprime un mensaje antes y después de procesar las líneas del archivo.

---

## Segunda definicion 


## **Definición y Funcionamiento de `awk`**

### **¿Qué es `awk`?**

- **Propósito:** Procesar y analizar archivos de texto estructurados (por columnas) mediante patrones y acciones.
- **Funcionamiento:** 
  - Lee un archivo línea por línea.
  - Divide cada línea en **campos** (columnas) usando un delimitador (espacio, coma, etc.).
  - Ejecuta acciones basadas en **patrones** (condiciones o expresiones regulares).
- **Fortalezas:** 
  - Manipulación de columnas.
  - Cálculos matemáticos.
  - Generación de informes formateados.
  - Uso de variables, bucles y funciones.

---

## **Sintaxis Básica**

```bash
awk 'PATRÓN { ACCIÓN }' archivo(s)
```

- **`PATRÓN`**: Condición para ejecutar la acción (opcional). Ej: `NR > 5`, `/error/`.
- **`ACCIÓN`**: Comandos a ejecutar si el patrón coincide. Ej: `print $1`.
- Si no se especifica patrón, la acción se aplica a **todas las líneas**.

---

### **Conceptos Clave**

#### **1. Variables integradas**

| Variable | Descripción |
|----------|-------------|
| **`$0`** | Toda la línea actual. |
| **`$1, $2, ..., $n`** | Campos (columnas) 1, 2, ..., n. |
| **`NR`** | Número de línea actual (Número de Registro). |
| **`NF`** | Número de campos en la línea actual. |
| **`FS`** | Delimitador de campos (Field Separator). Por defecto: espacio/tab. |
| **`OFS`** | Delimitador de salida (Output Field Separator). Por defecto: espacio. |

#### **2. Patrones comunes**

- **`BEGIN`**: Ejecuta la acción antes de procesar el archivo.
- **`END`**: Ejecuta la acción después de procesar el archivo.
- **`/expresión regular/`**: Filtra líneas que coinciden con la regex.
- **`condición lógica`**: Ej: `NR == 1`, `$3 > 100`.

#### **3. Acciones comunes**

- **`print`**: Imprime texto o campos.
- **`printf`**: Imprime con formato personalizado.
- **Cálculos**: Operaciones matemáticas (`+`, `-`, `*`, `/`).
- **Estructuras de control**: `if`, `for`, `while`.

---

### **⚙️ Opciones Principales**

| Opción | Descripción |
|--------|-------------|
| `-F`   | Define el delimitador de campos. Ej: `-F ","`. |
| `-v`   | Define una variable. Ej: `-v var=valor`. |
| `-f`   | Lee el script desde un archivo. Ej: `-f script.awk`. |
| `--sandbox` | Ejecuta en modo seguro (sin acceso al sistema). |

---

### **Ejemplos Prácticos**

### **1️⃣ Ejemplos Básicos**

#### **Imprimir la primera columna de un archivo:**
```bash
awk '{print $1}' archivo.txt
```

#### **Imprimir la primera y tercera columna usando coma como delimitador:**
```bash
awk -F ',' '{print $1, $3}' datos.csv
```

#### **Mostrar líneas donde la tercera columna es mayor a 100:**
```bash
awk '$3 > 100 {print $0}' ventas.txt
```

---

### **2️⃣ Ejemplos Intermedios**

#### **Sumar valores de una columna:**
```bash
awk -F ',' '{sum += $2} END {print "Total:", sum}' ventas.csv
```

#### **Imprimir el número de líneas de un archivo:**
```bash
awk 'END {print NR}' archivo.txt
```

#### **Filtrar líneas que contienen una palabra (como `grep`):**
```bash
awk '/error/ {print}' sistema.log
```

#### **Imprimir el último campo de cada línea:**
```bash
awk '{print $NF}' archivo.txt
```

---


### **1️⃣ Ejemplo Básico: Imprimir una Columna**

**Archivo `empleados.csv`:**

```csv
Nombre,Edad,Departamento
Ana,28,Marketing
Luis,35,IT
Marta,42,Finanzas
```

**Comando:**

```bash
awk -F ',' '{print $2}' empleados.csv
```

**Salida:**

```
Edad
28
35
42
```

**Explicación:**

- `-F ','`: Define la coma como delimitador de columnas.
- `{print $2}`: Imprime la segunda columna (Edad).

---

### **2️⃣ Filtrar Líneas por Valor de Columna**

**Archivo `ventas.txt`:**

```txt
ProductoA 150
ProductoB 200
ProductoC 75
ProductoD 300
```

**Comando (Mostrar productos con ventas > 100):**

```bash
awk '$2 > 100 {print $1}' ventas.txt
```

**Salida:**

```
ProductoA
ProductoB
ProductoD
```

**Explicación:**

- `$2 > 100`: Filtra líneas donde la segunda columna sea mayor a 100.
- `{print $1}`: Imprime el nombre del producto.

---

### **3️⃣ Sumar Valores de una Columna**

**Archivo `ventas.csv`:**

```csv
Manzanas,50
Peras,30
Plátanos,20
```

**Comando (Sumar la segunda columna):**

```bash
awk -F ',' '{sum += $2} END {print "Total:", sum}' ventas.csv
```

**Salida:**

```
Total: 100
```

**Explicación:**

- `{sum += $2}`: Acumula la suma de la columna 2.
- `END`: Ejecuta la acción al final del procesamiento.

---

### **4️⃣ Contar Líneas con Patrones**

**Archivo `sistema.log`:**

```log
[INFO] Servicio iniciado.
[ERROR] Disco lleno.
[WARNING] Alto uso de CPU.
[ERROR] Conexión fallida.
```

**Comando (Contar errores):**

```bash
awk '/ERROR/ {count++} END {print "Errores:", count}' sistema.log
```

**Salida:**

```
Errores: 2
```

**Explicación:**

- `/ERROR/`: Filtra líneas que contienen "ERROR".
- `{count++}`: Incrementa el contador por cada coincidencia.

---

### **5️⃣ Formatear Salida con `printf`**

**Archivo `notas.txt`:**

```txt
Juan 90
Ana 85
Luis 78
```

**Comando (Tabla formateada):**

```bash
awk 'BEGIN {printf "%-10s %-10s\n", "Nombre", "Nota"} {printf "%-10s %-10d\n", $1, $2}' notas.txt
```

**Salida:**

```
Nombre      Nota       
Juan        90        
Ana         85        
Luis        78        
```

**Explicación:**

- `BEGIN`: Define el encabezado antes de procesar el archivo.
- `%-10s`: Formatea texto en 10 caracteres alineado a la izquierda.

---

### **6️⃣ Procesar Múltiples Campos con Condiciones**

**Archivo `datos.csv`:**

```csv
2023-01-05,200,ClienteA
2023-01-05,150,ClienteB
2023-01-06,300,ClienteC
```

**Comando (Filtrar ventas > 200 y mostrar fecha y cliente):**

```bash
awk -F ',' '$2 > 200 {print $1, $3}' datos.csv
```

**Salida:**

```
2023-01-06 ClienteC
```

**Explicación:**

- `$2 > 200`: Solo líneas donde la segunda columna (ventas) > 200.
- `{print $1, $3}`: Imprime fecha (col1) y cliente (col3).

---

### **7️⃣ Usar Variables Personalizadas**

**Archivo `temperaturas.txt`:**

```txt
Madrid 25
Barcelona 28
Valencia 30
```

**Comando (Convertir °C a °F):**

```bash
awk '{fahrenheit = ($2 * 9/5) + 32; print $1, fahrenheit "°F"}' temperaturas.txt
```

**Salida:**

```
Madrid 77°F
Barcelona 82.4°F
Valencia 86°F
```

**Explicación:**

- `fahrenheit = ...`: Calcula la conversión.
- `print ... "°F"`: Formatea la salida con símbolo.

---

### **8️⃣ Generar Informe con Encabezado y Totales**

**Archivo `stock.txt`:**

```txt
ProductoA 50
ProductoB 30
ProductoC 20
```

**Comando:**

```bash
awk 'BEGIN {print "Producto\tStock"; total=0} 
     {print $1 "\t\t" $2; total += $2} 
     END {print "----------------\nTotal:\t\t" total}' stock.txt
```

**Salida:**

```
Producto    Stock
ProductoA   50
ProductoB   30
ProductoC   20
----------------
Total:      100
```

**Explicación:**

- `BEGIN`: Encabezado inicial.
- `total += $2`: Suma acumulativa.
- `END`: Total final.

---

### **9️⃣ Filtrar por Longitud de Campo**

**Archivo `usuarios.txt**:**

```txt
juan 25
maria 30
pedro 42
ana 28
```

**Comando (Usuarios con nombres de 4 letras):**

```bash
awk 'length($1) == 4 {print $1}' usuarios.txt
```

**Salida:**

```
juan
pedro
```

**Explicación:**

- `length($1) == 4`: Filtra nombres con 4 caracteres.

---

### **Script en Archivo (`-f`)**

**Archivo `script.awk`:**

```awk
BEGIN {
    FS = ",";
    print "Inicio del informe:";
}
{
    printf "%-10s: %d\n", $1, $2;
}
END {
    print "-------------------";
    print "Registros procesados:", NR;
}
```

**Ejecución:**

```bash
awk -f script.awk datos.csv
```

**Salida (si `datos.csv` tiene 3 líneas):**

```
Inicio del informe:
2023-01-05: 200
2023-01-05: 150
2023-01-06: 300
-------------------
Registros procesados: 3
```

---

## **⚠️ Errores Comunes**

1. **Olvidar el delimitador (`-F`)**: Si los campos no están separados por espacios/tabs, define `-F`.
2. **No inicializar variables**: Si usas variables numéricas, inicialízalas en `BEGIN`.
3. **Confundir `print` y `printf`**: `printf` no añade saltos de línea automáticos.

---

## **Casos de Uso Reales**

- **Logs de servidores**: Filtrar errores, calcular estadísticas.
- **CSV/TSV**: Generar informes, filtrar datos.
- **Datos científicos**: Cálculos matemáticos rápidos.
- **Formateo de texto**: Convertir datos a tablas legibles.

---



