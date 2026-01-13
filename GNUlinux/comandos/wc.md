
## WC

`wc` se utiliza para contar líneas, palabras, bytes y caracteres en archivos o entrada estándar.

---

## **Sintaxis básica:**

```bash
wc [OPCIONES] [ARCHIVO...]
```

Si no se especifica un archivo, `wc` lee desde la entrada estándar (stdin).

---

## **🔧 Opciones principales:**

| Opción | Descripción |
|--------|-------------|
| `-l`    | Cuenta **líneas**. |
| `-w`    | Cuenta **palabras**. |
| `-c`    | Cuenta **bytes**. |
| `-m`    | Cuenta **caracteres** (diferente de `-c` en Unicode). |
| `-L`    | Muestra la longitud de la **línea más larga**. |
| `--help` | Muestra ayuda. |
| `--version` | Muestra la versión. |

Si no se especifica ninguna opción, `wc` muestra **líneas, palabras y bytes** (en ese orden).

---

## **Ejemplos:**

### **1️⃣ Ejemplos básicos:**
#### **Contar líneas, palabras y bytes de un archivo:**

```bash
wc archivo.txt
```

**Salida:**  

`10  25 120 archivo.txt`  

*(10 líneas, 25 palabras, 120 bytes)*

#### **Contar solo líneas (`-l`):**

```bash
wc -l archivo.txt
```

**Salida:**  

`10 archivo.txt`

#### **Contar palabras (`-w`):**

```bash
wc -w archivo.txt
```

**Salida:**  

`25 archivo.txt`

---

### **2️⃣ Ejemplos intermedios:**
#### **Contar líneas de múltiples archivos:**

```bash
wc -l *.txt
```

**Salida:**  

```
10 archivo1.txt
15 archivo2.txt
25 total
```

#### **Usar `wc` con tuberías (`|`):**

```bash
cat archivo.txt | wc -w
```

**Salida:**  

`25` *(palabras en `archivo.txt`)*

#### **Contar archivos en un directorio:**

```bash
ls | wc -l
```

**Salida:**  

`5` *(si hay 5 archivos en el directorio)*

---

### **3️⃣ Ejemplos avanzados:**

#### **Encontrar la línea más larga en un archivo (`-L`):**

```bash
wc -L archivo.txt
```

**Salida:**  

`45` *(la línea más larga tiene 45 caracteres)*

#### **Contar caracteres en lugar de bytes (`-m`):**

```bash
echo "café" | wc -c  # Bytes (puede ser 5 por UTF-8)
echo "café" | wc -m  # Caracteres (4)
```

**Salida:**  

```
5  (bytes)
4  (caracteres)
```

#### **Contar palabras en todos los archivos `.log` (usando `xargs`):**

```bash
find . -name "*.log" | xargs wc -w
```

**Salida:**  

```
100 archivo1.log
200 archivo2.log
300 total
```

#### **Ignorar espacios en blanco al contar líneas (`grep` + `wc`):**

```bash
grep -v '^$' archivo.txt | wc -l
```

**Salida:**  

`8` *(líneas no vacías)*

---

### **Conclusión:**

- `wc` es muy útil para conteos rápidos en archivos o texto.
- Se combina bien con otros comandos (`grep`, `find`, `cat`, `xargs`, etc.).
- Las opciones más usadas son `-l` (líneas), `-w` (palabras) y `-c` (bytes).


