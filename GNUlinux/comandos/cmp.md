## `cmp` 

### **Instalación** 

El comando `cmp` viene instalado por defecto en la mayoría de las distribuciones de Linux y sistemas Unix, ya que forma parte del paquete **GNU Core Utilities**. No requiere instalación adicional.


### **Definición y significado** 

`cmp` (abreviatura de *compare*) es un comando utilizado para **comparar dos archivos byte por byte**. Su principal función es determinar si dos archivos son idénticos y, en caso de diferencias, mostrar la posición del primer byte que no coincide. Es especialmente útil para archivos binarios, aunque también funciona con texto.

### **Sintaxis básica** 

```bash
cmp [OPCIONES] ARCHIVO1 ARCHIVO2
```

### **Opciones principales** 

| Opción | Descripción |
|--------|-------------|
| `-l`   | Muestra **todas las diferencias** (número de byte y valores en octal). |
| `-s`   | Modo silencioso: **no muestra salida**, solo devuelve el código de salida (0 si son iguales, 1 si difieren). |
| `-i N` | Ignora los primeros **N bytes** de ambos archivos. |
| `-n BYTES` | Limita la comparación a los primeros **BYTES** especificados. |
| `--verbose` | Muestra información detallada (equivalente a `-l` en algunas versiones). |


### **Ejemplos de uso**

#### **Ejemplo simple** 

```bash
cmp archivo1.txt archivo2.txt
```

- **Salida típica**:  

  `archivo1.txt archivo2.txt difieren: byte 12, línea 1 es 150 o 151`  
  (Indica la primera discrepancia en el byte 12).

#### **Ejemplo complejo** 

```bash
cmp -l imagen1.jpg imagen2.jpg
```

- **Salida**:  

```
1023 125 126
2048 300 301
```
  (Muestra todas las diferencias: posición del byte, valor en octal del primer archivo y del segundo).

### **Consejos de uso** 

1. **Para scripts**: Usa `-s` para verificar igualdad en scripts sin salida visible.  

   Ejemplo:  
   
```bash
if cmp -s backup.tar original.tar; then echo "Iguales"; else echo "Diferentes"; fi
```

2. **Archivos binarios**: Prefiere `cmp` sobre `diff` para comparar ejecutables o imágenes, ya que `diff` está diseñado para texto.
3. **Recuperación de datos**: Combínalo con `dd` para identificar corrupción en archivos parcialmente dañados.

### **Información adicional**

- **Diferencia con `diff`**:  

  Mientras `cmp` compara bytes y es ideal para binarios, `diff` analiza líneas de texto y muestra diferencias contextuales .
  
- **Alternativas modernas**:  

  - `comm`: Compara archivos ordenados línea por línea .  
  - `md5sum`: Verifica integridad mediante hashes (útil para confirmar igualdad sin detalles de diferencias) .
  
- **Casos avanzados**:  

  Usa `cmp -i 1024 -n 512` para saltar los primeros 1024 bytes y comparar solo los siguientes 512.

### **Comandos relacionados** 

| Comando | Uso |
|---------|-----|
| `diff`  | Compara archivos de texto línea por línea. |
| `comm`  | Muestra líneas comunes o únicas entre archivos ordenados. |
| `cksum` | Genera checksum para verificar integridad. |



