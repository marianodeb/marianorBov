

## CUT

---

## **Definición y Funcionamiento del Comando `cut`**

### **¿Qué hace `cut`?**

- **Propósito:** Extraer secciones específicas de cada línea de un archivo o entrada estándar.
- **Funcionamiento:** Divide cada línea en "campos" (columnas) usando un delimitador (como `,`, `:`, o `TAB`), o selecciona rangos de caracteres/bytes, y muestra solo las partes especificadas.
- **Uso típico:** Procesar datos estructurados (CSV, logs, etc.), extraer columnas, o analizar salidas de otros comandos.

---

## **Opciones Principales**



| Opción | Descripción |
|--------|-------------|
| `-f` o `--fields` | Selecciona **campos** (columnas) por número o rango. |
| `-d` o `--delimiter` | Define el **delimitador** entre campos (por defecto: `TAB`). |
| `-c` o `--characters` | Selecciona **caracteres** específicos por posición. |
| `-b` o `--bytes` | Selecciona **bytes** específicos por posición. |
| `--complement` | Invierte la selección (muestra todo **excepto** lo especificado). |
| `-s` o `--only-delimited` | Omite líneas que **no contienen el delimitador**. |



| Opción       | Descripción con parametro                                                     |
|--------------|-----------------------------------------------------------------------------|
| `-f N`       | Selecciona el campo (columna) número `N` (ej: `-f1` para la primera columna). |
| `-d 'X'`     | Define `X` como delimitador entre campos (por defecto es `TAB`).            |
| `-c N-M`     | Selecciona caracteres desde la posición `N` hasta `M`.                      |
| `-b N-M`     | Selecciona bytes desde la posición `N` hasta `M`.                           |
| `--complement`| Muestra todo **excepto** los campos/caracteres seleccionados.               |
| `-s`         | Omite líneas que **no contienen el delimitador**.                            |
| `--output-delimiter` | Cambia el delimitador de salida (ej: `--output-delimiter=";"`). |

---

## **Ejemplos Detallados con Archivos**

### **1️⃣ Ejemplo Simple: Extraer la Primera Columna de un CSV**

**Archivo `empleados.csv`:**

```csv
Nombre,Edad,Departamento
Ana,28,Marketing
Luis,35,IT
Marta,42,Finanzas
```

**Comando:**

```bash
cut -d ',' -f1 empleados.csv
```

**Salida:**

```
Nombre
Ana
Luis
Marta
```

**Explicación:**

- `-d ','`: Usa la coma como delimitador.
- `-f1`: Selecciona la primera columna.

---

### **2️⃣ Ejemplo Intermedio: Extraer Rangos de Caracteres**

**Archivo `mensajes.txt`:**

```txt
[ERROR] 2023-10-01: Fallo de conexión.
[INFO] 2023-10-02: Usuario autenticado.
```

**Comando:**

```bash
cut -c 2-6,12-21 mensajes.txt
```

**Salida:**

```
ERROR 2023-10-01
INFO 2023-10-02
```

**Explicación:**

- `-c 2-6`: Caracteres de la posición 2 a 6 (`ERROR` o `INFO`).
- `-c 12-21`: Caracteres de la posición 12 a 21 (fecha).

---

### **3️⃣ Ejemplo Avanzado: Filtrar y Combinar con `grep`**

**Archivo `servidor.log`:**

```log
[192.168.1.1] GET /index.html 200
[192.168.1.2] POST /login 404
[192.168.1.3] GET /contact 200
```

**Comando:**

```bash
grep "404" servidor.log | cut -d ' ' -f1,4
```

**Salida:**

```
[192.168.1.2] 404
```

**Explicación:**

- `grep "404"`: Filtra líneas con error 404.
- `-d ' '`: Usa espacio como delimitador.
- `-f1,4`: Selecciona la IP y el código de error.

---

### **4️⃣ Ejemplo con `--complement` (Exclusión)**

**Archivo `datos.txt`:**

```txt
A:B:C:D:E
1:2:3:4:5
```

**Comando:**

```bash
cut -d ':' --complement -f2-4 datos.txt
```

**Salida:**

```
A:E
1:5
```

**Explicación:**

- `--complement` excluye los campos 2, 3 y 4.
- Muestra solo los campos 1 y 5.

---

### **5️⃣ Ejemplo con Delimitador Personalizado en Salida**

**Archivo `clientes.txt`:**

```txt
Juan Perez|juan@email.com|México
Maria Lopez|maria@email.com|España
```

**Comando:**

```bash
cut -d '|' -f1,3 --output-delimiter=" - " clientes.txt
```

**Salida:**

```
Juan Perez - México
Maria Lopez - España
```

**Explicación:**

- `--output-delimiter=" - "`: Cambia el separador de salida.

---

### **6️⃣ Ejemplo con `-s` (Ignorar Líneas sin Delimitador)**

**Archivo `mix.txt`:**

```txt
Esta línea no tiene delimitador
Nombre;Apellido;Edad
Ana;García;30
```

**Comando:**

```bash
cut -d ';' -s -f2 mix.txt
```

**Salida:**

```
Apellido
García
```

**Explicación:**

- `-s`: Omite la primera línea (no contiene `;`).

---

## **⚠️ Notas Clave**

1. **Delimitador por Defecto:** Si no usas `-d`, `cut` espera `TAB`.
2. **Rangos:** 
   - `-f2-4`: Campos 2, 3 y 4.
   - `-f-3`: Campos 1, 2 y 3.
3. **Errores Comunes:** Si un archivo tiene campos variables, `cut` puede no ser la mejor herramienta (mejor usar `awk`).

---

## **Casos de Uso Reales**

- Extraer columnas de un CSV.
- Procesar logs para obtener IPs o códigos de estado.
- Limpiar salidas de comandos como `ps`, `df`, o `lsblk`.










