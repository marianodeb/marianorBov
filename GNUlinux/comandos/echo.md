
## `echo`

---

### **1. Significado**

`echo` es un comando utilizado para **mostrar mensajes en la terminal** o **enviar datos a archivos o otros comandos**. Es una herramienta básica pero poderosa en scripts de shell para interactuar con el usuario o depurar código.

---

### **2. Uso**

- Imprimir texto o variables en la terminal.  
- Redirigir texto a archivos.  
- Generar mensajes de salida en scripts.  
- Validar variables o resultados de comandos.  
- Combinar con tuberías (`|`) para procesar texto.

---

### **3. Sintaxis básica**

```bash
echo [opciones] "cadena_de_texto"
```

---

### **4. Opciones principales**

| Opción | Descripción |  
|--------|-------------|  
| `-e`   | Habilita la interpretación de **secuencias de escape** (ej: `\n`, `\t`). |  
| `-E`   | Desactiva las secuencias de escape (comportamiento predeterminado en algunos shells). |  
| `-n`   | Elimina el salto de línea al final del mensaje. |  

---

### **5. Ejemplos**

#### **Ejemplos simples**

1. **Texto básico**:

```bash
echo "Hola Mundo"  
```

2. **Imprimir variables**:

```bash
nombre="Juan"  
echo "Bienvenido, $nombre"  # Resultado: Bienvenido, Juan  
```

3. **Redirigir a un archivo**:

```bash
echo "Línea 1" > archivo.txt  
```

---

#### **Ejemplos complejos**

1. **Secuencias de escape con `-e`**:

```bash
   echo -e "Línea 1\nLínea 2\tTabulador"  
# Salida:  
# Línea 1  
# Línea 2    Tabulador  
```

2. **Color en texto (ANSI escape codes)**:

```bash
echo -e "\e[31mTexto en rojo\e[0m"  # \e[31m activa color rojo  
```

3. **Combinar con comandos**:

```bash
echo "Fecha actual: $(date)"  # Usa la salida del comando `date`  
```

4. **Eliminar salto de línea (`-n`)**:

```bash
echo -n "Progreso: 50%"; echo " completado"  
# Salida: Progreso: 50% completado  
```

---

### **6. Diferencia entre comillas dobles (`" "`) y simples (`' '`)**

| **Comillas Dobles (`" "`)** | **Comillas Simples (`' '`)** |  
|-----------------------------|------------------------------|  
| Permiten **expansión de variables** (`$VAR`). | **No expanden variables** (ej: `$VAR` se imprime literalmente). |  
| Interpretan **secuencias de escape** (si se usa `echo -e`). | Ignoran secuencias de escape (todo es texto literal). |  
| Permiten **subcomandos** (`$(comando)`). | Tratan `$(comando)` como texto. |  
| Útiles para cadenas con espacios o caracteres especiales. | Ideales para texto con `$`, `"`, o `!`. |  

#### **Ejemplos**:

- Con comillas dobles:

```bash
echo "Usuario: $USER, Ruta: $(pwd)"  # Expande variables y comandos  
```

- Con comillas simples:

```bash
echo 'Usuario: $USER, Ruta: $(pwd)'  # Imprime literalmente: Usuario: $USER, Ruta: $(pwd)  
```

---

### **7. Información adicional**

#### **Consideraciones clave**:

- **Variables sin comillas**: Si no usas comillas, `echo` elimina espacios múltiples y no maneja caracteres especiales (ej: `*`).

```bash
echo Hola   Mundo       # Imprime "Hola Mundo" (espacios reducidos)  
```

- **Portabilidad**: El comportamiento de `echo` varía entre shells (Bash, Zsh, etc.). Para scripts robustos, usa `printf`.  

- **Seguridad**: Usa siempre comillas para evitar errores con espacios o caracteres especiales en variables:

```bash
texto="Texto con * y espacios"  
echo "$texto"  # Correcto  
echo $texto     # ¡Error! El * se expande como archivos del directorio.  
```

#### **Alternativa recomendada**:

Para mayor control (especialmente en scripts), usa `printf`:

```bash
printf "Nombre: %s\nEdad: %d\n" "Juan" 25  # Formatea texto como en C  
```

---

### **8. Comandos relacionados**

- `printf`: Versión avanzada para formatear texto.  
- `cat`: Mostrar contenido de archivos.  
- `read`: Leer entrada del usuario.  

Para ver todas las opciones:

```bash
help echo  # En Bash (depende del shell)  
```


