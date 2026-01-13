
## SORT
---

## **Definición y Funcionamiento del Comando `sort`**

### **¿Qué hace `sort`?**

- **Propósito:** Ordenar líneas de texto en un archivo o entrada estándar, ya sea alfabética, numéricamente o por criterios personalizados.
- **Funcionamiento:** Por defecto, ordena lexicográficamente (como en un diccionario). Puede manejar:
  - **Orden numérico** (enteros o decimales).
  - **Orden inverso** (de Z a A, o de mayor a menor).
  - **Ignorar mayúsculas/minúsculas**.
  - **Eliminar duplicados**.
  - **Ordenar por columnas específicas** (útil para datos estructurados).

---

## **Sintaxis Básica**

```bash
sort [OPCIONES] [ARCHIVO...]
```

---

## **⚙️ Opciones Principales**


| Opción          | Descripción                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| `-n` o `--numeric-sort` | Ordena numéricamente (ej: `10` > `2`).                                      |
| `-r` o `--reverse`      | Orden inverso (descendente).                                                |
| `-k` o `--key`          | Define una clave/columna específica para ordenar (ej: `-k2` para la columna 2). |
| `-t` o `--field-separator` | Define el delimitador entre campos (ej: `-t ','` para CSV).               |
| `-u` o `--unique`       | Elimina líneas duplicadas (muestra solo valores únicos).                    |
| `-f` o `--ignore-case`  | Ignora diferencias entre mayúsculas y minúsculas.                           |
| `-o` [archivo]          | Guarda la salida en un archivo (en lugar de mostrarla).                      |
| `-m` o `--merge`        | Fusiona múltiples archivos ya ordenados (sin reordenar).                     |
| `-c` o `--check`        | Verifica si un archivo ya está ordenado (no muestra salida si lo está).      |
| `--debug`               | Muestra información de depuración (útil para entender el orden aplicado).   |

---

### **Ejemplos Detallados con Archivos**

#### **1️⃣ Ejemplo Básico: Orden Alfabético**

**Archivo `frutas.txt`:**

```txt
Mango
Banana
manzana
Pera
```

**Comando:**

```bash
sort frutas.txt
```

**Salida:**

```
Banana
manzana
Mango
Pera
```

**Explicación:**

- Orden lexicográfico (las minúsculas van después de las mayúsculas en ASCII).

---

#### **2️⃣ Ignorar Mayúsculas (`-f`)**

**Comando:**

```bash
sort -f frutas.txt
```

**Salida:**

```
Banana
Mango
manzana
Pera
```

**Explicación:**

- `-f` ignora diferencias entre `Mango` y `manzana`.

---

#### **3️⃣ Orden Numérico (`-n`)**

**Archivo `numeros.txt`:**

```txt
10
2
150
25
```

**Comando:**

```bash
sort -n numeros.txt
```

**Salida:**

```
2
10
25
150
```

**Explicación:**

- Sin `-n`, ordenaría como texto: `10`, `150`, `2`, `25`.

---

#### **4️⃣ Orden por Columna Específica (Usando `-k`)**

**Archivo `empleados.csv`:**

```csv
Juan,28,IT
Ana,35,Marketing
Luis,22,Finanzas
```

**Comando (Ordenar por edad - columna 2):**

```bash
sort -t ',' -n -k2 empleados.csv
```

**Salida:**

```
Luis,22,Finanzas
Juan,28,IT
Ana,35,Marketing
```

**Explicación:**

- `-t ','`: Delimitador es coma.
- `-n -k2`: Ordena numéricamente por la segunda columna.

---

### **5️⃣ Eliminar Duplicados (`-u`)**

**Archivo `colores.txt`:**

```txt
Rojo
Azul
Rojo
Verde
```

**Comando:**

```bash
sort -u colores.txt
```

**Salida:**

```
Azul
Rojo
Verde
```

**Explicación:**

- `-u` elimina las líneas repetidas (solo funciona si el archivo está ordenado).

---

#### **6️⃣ Orden Inverso (`-r`)**

**Comando:**

```bash
sort -nr numeros.txt
```

**Salida:**

```
150
25
10
2
```

**Explicación:**

- `-nr`: Orden numérico inverso (de mayor a menor).

---

#### **7️⃣ Ordenar por Múltiples Columnas**

**Archivo `ventas.csv`:**

```csv
2023-01-05,200,ClienteA
2023-01-05,150,ClienteB
2023-01-06,200,ClienteC
```

**Comando (Ordenar por fecha y monto):**

```bash
sort -t ',' -k1,1 -k2nr ventas.csv
```

**Salida:**

```
2023-01-05,200,ClienteA
2023-01-05,150,ClienteB
2023-01-06,200,ClienteC
```

**Explicación:**

- `-k1,1`: Ordena primero por la primera columna (fecha).
- `-k2nr`: Luego ordena por la segunda columna numéricamente en reversa.

---

#### **8️⃣ Guardar Resultado en un Archivo (`-o`)**

**Comando:**

```bash
sort -n numeros.txt -o numeros_ordenados.txt
```

**Contenido de `numeros_ordenados.txt`:**

```
2
10
25
150
```

---

#### **9️⃣ Combinar con `cut` y `grep` (Ejemplo Avanzado)**

**Archivo `servidor.log`:**

```log
192.168.1.1 [ERROR] 404
192.168.1.2 [INFO] 200
192.168.1.3 [ERROR] 500
```

**Comando (Extraer IPs con errores y ordenar):**

```bash
grep "ERROR" servidor.log | cut -d ' ' -f1 | sort -u
```

**Salida:**

```
192.168.1.1
192.168.1.3
```

**Explicación:**

- `grep`: Filtra líneas con "ERROR".
- `cut`: Extrae la primera columna (IPs).
- `sort -u`: Ordena y elimina duplicados.

---

### **Errores Comunes y Tips**

1. **Orden Numérico vs. Lexicográfico:** Si usas `sort` sin `-n` para números, `10` aparecerá antes que `2`.
2. **Delimitadores:** Si no defines `-t`, `sort` usa espacios/tabs por defecto.
3. **Claves Compuestas:** Usa `-k inicio,final` para rangos de columnas (ej: `-k2,3`).

---

## **Casos de Uso Reales**

- Ordenar registros CSV por fecha, ID, etc.
- Procesar logs para identificar patrones.
- Limpiar listas de datos eliminando duplicados.


