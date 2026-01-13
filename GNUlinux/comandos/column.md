

## **`column`**

### **1. Definición y significado**  

El comando `column` en sistemas Unix/Linux se utiliza para formatear texto en columnas alineadas, especialmente útil para visualizar datos tabulares en la terminal. Su función principal es organizar la salida de comandos o archivos de texto en columnas legibles, eliminando espacios redundantes y ajustando el ancho automáticamente. Por ejemplo, es ideal para formatear listas de datos separadas por tabulaciones o espacios .

### **2. Instalación (si no viene por defecto)**  

En la mayoría de distribuciones Linux (Debian/Ubuntu, Fedora, etc.), el comando `column` forma parte del paquete `util-linux`, que generalmente está preinstalado. Si no está disponible:  

- **Debian/Ubuntu**:  

```bash
sudo apt-get install util-linux
```

- **Fedora/RHEL**:  

```bash
sudo dnf install util-linux
```

### **3. Sintaxis básica** 
 
```bash
column [opciones] [archivo_entrada]
```

*Ejemplo simple*: 
 
```bash
echo -e "Nombre Edad\nAna 30\nCarlos 25" | column -t
```

### **4. Opciones principales** 

| Opción       | Descripción                                                                 |
|--------------|-----------------------------------------------------------------------------|
| **`-t`**     | Crea una tabla automáticamente, detectando columnas por separadores.       |
| **`-s SEP`** | Define el separador de columnas (por defecto: espacios/tabulaciones).      |
| **`-o STR`** | Especifica el separador de salida entre columnas (ej: `-o " | "`).         |
| **`-c N`**   | Establece el ancho máximo de la terminal para ajustar columnas.            |
| **`-n`**     | Desactiva la fusión de múltiples separadores en uno solo.                  |

### **5. Ejemplos de uso** 
 
- **Ejemplo simple**: Formatear una lista de nombres y edades: 
 
```bash
echo -e "Alice 25\nBob 30\nCharlie 22" | column -t
```

  *Salida*: 
   
```
Alice    25
Bob      30
Charlie  22
```

- **Ejemplo complejo**: Procesar un archivo CSV con separadores personalizados: 
 
```bash
cat datos.csv | column -s "," -t -o " | "
```

  *Explicación*: Usa `,` como separador de entrada y `|` como separador de salida.

### **6. Consejos prácticos**  

- **Combinar con otros comandos**: Útil con `ls`, `ps`, o salidas de scripts para mejorar la legibilidad.  
  Ejemplo: `ls -l | column -t`.  
- **Archivos CSV/TSV**: Usar `-s` para especificar separadores como `,` o `\t` .  
- **Evitar truncamiento**: Si las columnas no caben, ajustar el ancho con `-c` (ej: `-c 120`).  

### **7. Información adicional**  

- **Alternativas modernas**:  

  - `awk`: Ofrece control avanzado sobre el formateo de columnas (ej: `awk '{printf "%-10s %s\n", $1, $2}'`).  
  - `csvkit` (herramientas externas): Especializado en manipulación de CSV/TSV .  
  
- **Relacionados**:  

  - `paste`: Combina líneas de archivos en columnas.  
  - `pr`: Formatea texto en páginas/columnas para impresión.  
  - `expand`: Convierte tabulaciones en espacios .  

### **8. Limitaciones y notas**  

- **Caracteres especiales**: Puede tener problemas con textos que contienen espacios dentro de campos.  
- **No soporte gráfico**: Funciona solo en terminales, no genera tablas HTML o formatos gráficos.  
- **Uso en scripts**: Ideal para salidas rápidas, pero para informes complejos, considere herramientas como `pandoc` o conversores a PDF/Excel .  

### **9. Documentación adicional**  

Para detalles técnicos, ejecute `man column` o visite la [documentación de util-linux](https://man7.org/linux/man-pages/man1/column.1.html). Si necesita manipulación avanzada de tablas, explore `csvkit` o bibliotecas en Python como `pandas` . 

**Nota**: Si su sistema no incluye `column`, verifique si el paquete `util-linux` está instalado o actualizado.
