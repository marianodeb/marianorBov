##`egrep` 

---

### **1. Significado**

`egrep` (**Extended Global Regular Expression Print**) es una herramienta de búsqueda de texto que utiliza **expresiones regulares extendidas** para localizar patrones en archivos o flujos de datos. Es equivalente a ejecutar `grep -E`, permitiendo el uso de metacaracteres avanzados sin necesidad de escapar caracteres especiales (como `|`, `+`, `?`).

---

### **2. Uso**

- Buscar patrones complejos en archivos de texto.  
- Filtrar salidas de otros comandos mediante tuberías (`|`).  
- Realizar búsquedas recursivas en directorios y subdirectorios.  
- Trabajar con múltiples patrones simultáneamente.  
- Identificar líneas que coincidan con estructuras específicas (ej: direcciones IP, formatos de log, etc.).

---

### **3. Sintaxis básica**

```bash
egrep [opciones] "patrón" [archivo(s)]
```
Ejemplo mínimo:

```bash
egrep "error" log.txt  # Busca "error" en log.txt
```

---

### **4. Opciones principales**

| Opción | Descripción |  
|--------|-------------|  
| `-i`   | Búsqueda insensible a mayúsculas/minúsculas. |  
| `-v`   | Invierte la coincidencia (muestra líneas que **no** contienen el patrón). |  
| `-r` o `-R` | Búsqueda recursiva en directorios. |  
| `-l`   | Muestra solo los nombres de archivos con coincidencias. |  
| `-c`   | Cuenta el número de líneas coincidentes. |  
| `-n`   | Muestra el número de línea de las coincidencias. |  
| `-o`   | Imprime solo la parte del texto que coincide. |  
| `-w`   | Busca palabras completas (evita coincidencias parciales). |  
| `-A n` | Muestra `n` líneas **después** de la coincidencia. |  
| `-B n` | Muestra `n` líneas **antes** de la coincidencia. |  
| `-C n` | Muestra `n` líneas alrededor de la coincidencia. |  
| `--color` | Resalta las coincidencias en color. |  

---

### **5. Ejemplos**

#### **Ejemplos simples**

1. **Búsqueda básica**:

```bash
egrep "hola" archivo.txt  # Busca "hola" en archivo.txt
```
   

2. **Ignorar mayúsculas/minúsculas**:

```bash
egrep -i "EJEMPLO" documento.txt
```
   

3. **Contar coincidencias**:

```bash
egrep -c "warning" sistema.log  # Cuenta líneas con "warning"
```
   

---

#### **Ejemplos complejos**

1. **Búsqueda de múltiples patrones**:

```bash
egrep "error|critical|alert" /var/log/syslog  # Busca 3 términos
```
   

2. **Buscar direcciones IP en un rango específico**:

```bash
egrep "192\.168\.0\.[1-5]" config.ini  # IPs del 1 al 5 en el último octeto
```
   

3. **Usar clases predefinidas para mayúsculas**:

```bash
egrep "[[:upper:]]" texto.txt  # Líneas con al menos una letra mayúscula
```
   

4. **Coincidir líneas que comienzan y terminan con patrones**:

```bash
egrep "^Inicio.*fin$" ejemplo.txt  # Líneas que empiezan con "Inicio" y terminan con "fin"
```
   

5. **Búsqueda recursiva con contexto**:

```bash
egrep -r -C 2 "database" /etc/  # Busca "database" en /etc y muestra 2 líneas alrededor
```
   

---

### **6. Información adicional**

#### **Diferencias clave entre `egrep` y `grep`**

- `egrep` soporta **expresiones regulares extendidas** (como `+`, `?`, `|`), mientras que `grep` básico requiere escapar estos caracteres con `\`.  
- Ejemplo equivalente:

```bash
grep -E "error|warning" log.txt  # Equivalente a egrep
```

#### **Buenas prácticas**

- Usar comillas para patrones con espacios o caracteres especiales: `egrep "mi frase"`.  
- Combinar con `|` para filtrar salidas de comandos: `dmesg | egrep "error"`.  
- Evitar usar `egrep` para archivos binarios; mejor para texto plano.  

#### **Notas de seguridad**

- En algunas distribuciones modernas, `egrep` está obsoleto; se recomienda usar `grep -E`.  

---

### **7. Comandos relacionados**

- `fgrep`: Búsqueda literal (sin interpretar regex).  
- `agrep`: Búsqueda aproximada (tolerante a errores).  
- `rgrep`: Versión recursiva de `grep`.  

Para más detalles, consulta la página del manual:

```bash
man egrep
```


