## **`uniq`**

---

### **1. Significado**

`uniq` (**Unique**) es un comando para **filtrar o reportar líneas repetidas consecutivas** en un archivo o entrada de texto. Es especialmente útil para analizar logs, listas o datos estructurados, pero requiere que las líneas estén **ordenadas** (usando `sort`) para detectar todas las repeticiones.

---

### **2. Uso**

- Eliminar líneas duplicadas adyacentes.  
- Contar ocurrencias de líneas repetidas.  
- Mostrar solo duplicados o líneas únicas.  
- Comparar segmentos específicos de las líneas (ignorando campos o caracteres).  
- Procesar datos en combinación con `sort`, `cut` u otros comandos.

---

### **3. Sintaxis básica**

```bash
uniq [opciones] [archivo_entrada] [archivo_salida]
```

Si no se especifica un archivo, lee desde la entrada estándar (`stdin`).

---

### **4. Opciones principales**

| Opción | Descripción |  
|--------|-------------|  
| `-c`   | Muestra el **número de repeticiones** al inicio de cada línea. |  
| `-d`   | Muestra **solo las líneas duplicadas** (al menos 2 repeticiones). |  
| `-D`   | Muestra **todas** las líneas duplicadas (no solo una instancia). |  
| `-u`   | Muestra **solo líneas únicas** (no duplicadas). |  
| `-i`   | Ignora mayúsculas/minúsculas al comparar. |  
| `-f N` | Ignora los primeros **N campos** (separados por espacios/tabs). |  
| `-s N` | Ignora los primeros **N caracteres** de cada línea. |  
| `-w N` | Compara solo los primeros **N caracteres** de cada línea. |  

---

### **5. Ejemplos**

#### **Ejemplos simples**

1. **Eliminar duplicados adyacentes**:

```bash
uniq lista.txt  # Si las líneas repetidas están juntas
```

2. **Contar repeticiones**:

```bash
uniq -c lista.txt  
# Ejemplo de salida:  
#   3 manzana  
#   2 pera  
```

3. **Combinar con `sort` para eliminar todos los duplicados**:

```bash
sort frutas.txt | uniq  # Ordena primero, luego elimina dups
```

---

#### **Ejemplos complejos**

1. **Mostrar solo líneas únicas (no repetidas)**:

```bash
sort logs.txt | uniq -u  # Líneas que aparecen una sola vez
```

2. **Ignorar campos al comparar**:

Supongamos que tenemos un archivo con:
   
```text
1 error: conexión fallida  
2 error: conexión fallida  
```
   
```bash
uniq -f 2 errores.txt  # Ignora los primeros 2 campos (números)
# Salida: 1 error: conexión fallida  
```

3. **Identificar IPs repetidas en logs (ignorando puertos)**:

```text
192.168.1.1:8080  
192.168.1.1:3000  
```
   
```bash
cut -d ':' -f1 access.log | sort | uniq -d  # Muestra IPs duplicadas
```

4. **Comparar solo los primeros 3 caracteres**:

```bash
uniq -w 3 datos.txt  # Ej: "abc123" y "abc456" se consideran iguales
```

5. **Mostrar todas las líneas duplicadas**:

```bash
sort datos.txt | uniq -D  # Útil para depurar duplicados masivos
```

---

### **6. Información adicional**

#### **Reglas clave**

- **Requiere líneas ordenadas**: Si las repeticiones no son consecutivas, `uniq` no las detectará. **¡Siempre usa `sort` primero!**  
- **Campos y delimitadores**: Por defecto, los campos se separan por espacios/tabs. Usa `-t` en `sort` o `cut` para cambiar el delimitador.  

#### **Alternativas**

- `sort -u`: Ordena y elimina duplicados en un solo paso.  
- `awk '!seen[$0]++'`: Elimina duplicados sin ordenar (pero usa memoria).  

#### **Casos prácticos**

- **Logs de servidor**:

```bash
cut -d ' ' -f1 access.log | sort | uniq -c | sort -nr  # Top IPs
```
  
- **Listas de correos**:

```bash
sort emails.txt | uniq -i > emails_unicos.txt  # Ignora mayúsculas
```

---

### **7. Comparación entre `uniq` y `sort -u`**

| **`uniq`** | **`sort -u`** |  
|------------|---------------|  
| Elimina **solo duplicados adyacentes**. | Elimina **todos los duplicados** (no requiere que estén juntos). |  
| Ideal para **contar repeticiones** o **filtrar por criterios específicos**. | Más eficiente si solo se necesitan líneas únicas. |  
| Requiere `sort` previo para eliminar todos los duplicados. | No necesita comandos adicionales. |  

---

### **8. Comandos relacionados**

- `sort`: Ordenar líneas.  
- `cut`: Extraer columnas.  
- `wc`: Contar líneas.  

Documentación completa:

```bash
man uniq  
```  

