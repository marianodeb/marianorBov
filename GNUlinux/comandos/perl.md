

## `perl`


### **1. Definición y Significado**

**Perl** (Practical Extraction and Reporting Language) es un lenguaje de programación interpretado, creado por **Larry Wall** en 1987. Destaca por su potencia en:

- **Procesamiento de texto** (manejo avanzado de expresiones regulares).  
- **Automatización de tareas** (scripts para sistemas UNIX/Linux).  
- **Flexibilidad**: Combina características de lenguajes como C, sed, awk y sh.  

Su filosofía es *"There's more than one way to do it"* (TMTOWTDI), lo que lo hace versátil pero a veces complejo.

---

### **2. Sintaxis Básica**

El comando `perl` se usa desde la terminal para ejecutar scripts o código inline:

```bash
perl [opciones] [archivo.pl] [argumentos]
```

Ejemplo básico:

```bash
perl -e 'print "Hola, mundo!\n";'
```

---

### **3. Opciones Principales**

| **Opción** | **Descripción** |  
|------------|-----------------|  
| `-e 'código'` | Ejecuta código Perl directamente (ejemplo: `perl -e 'print "Hola"`). |  
| `-w` | Habilita advertencias (warnings) para detectar errores. |  
| `-c` | Verifica la sintaxis de un script sin ejecutarlo. |  
| `-n` | Lee la entrada línea por línea (como un bucle `while (<>) { ... }`). |  
| `-p` | Similar a `-n`, pero imprime cada línea automáticamente. |  
| `-l` | Elimina saltos de línea al leer y los añade al imprimir. |  
| `-a` | Divide líneas en el array `@F` (modo "auto-split"). |  
| `-F` | Define el separador para `-a` (ejemplo: `-F':'` para dividir por `:`). |  
| `-M[módulo]` | Carga un módulo (ejemplo: `-MData::Dumper`). |  
| `-I[ruta]` | Añade directorios a la ruta de búsqueda de módulos. |  

---

### **4. Ejemplos**

#### **Simples**

- **Hola Mundo**:

```bash
perl -e 'print "Hola, mundo!\n";'
```

- **Contar líneas de un archivo** (como `wc -l`):

```bash
perl -lne 'END { print $. }' archivo.txt
```  

#### **Complejos**

- **Reemplazar texto en un archivo** (como `sed`):

```bash
perl -pi -e 's/foo/bar/g' archivo.txt
```

- **Filtrar líneas con regex y guardar en otro archivo**:

```bash
perl -ne 'print if /error/i' log.txt > errores.txt
```

- **Script para procesar CSV** (`archivo.pl`):

```perl
  #!/usr/bin/perl -w
  use strict;
  use Text::CSV;
  my $csv = Text::CSV->new({ binary => 1 });
  open my $fh, "<", "datos.csv" or die $!;
  while (my $row = $csv->getline($fh)) {
      print "Nombre: $row->[0], Edad: $row->[1]\n";
  }
  close $fh;
```

---

### **5. Consejos**

- **Usa `strict` y `warnings`**: Evitan errores comunes.

```perl
#!/usr/bin/perl
use strict;
use warnings;
```

- **Aprovecha CPAN**: Repositorio gigante de módulos (ej: `cpan install JSON`).  
- **Perl one-liners**: Ideales para tareas rápidas en la terminal (como `sed` o `awk`).  
- **Regex es tu aliado**: Perl es el rey de las expresiones regulares.  

---

### **6. Información Adicional**

- **Perl vs Perl 6/Raku**: **Perl 6** se convirtió en **Raku** (un lenguaje separado). **Perl 5** sigue activo y se actualiza (versión estable actual: 5.38).  
- **Alternativas**: Python o Ruby son más populares hoy para scripting, pero Perl sigue siendo clave en sistemas heredados.  
- **Documentación**:  
  - `perldoc`: Comando para ver documentación (ej: `perldoc perlrun` para opciones del intérprete).  
  - Sitio oficial: [https://www.perl.org](https://www.perl.org).  

---

### **7. Comandos Relacionados**

- `sed` / `awk`: Para procesamiento de texto (Perl los incluye y supera).  
- `python`: Alternativa moderna para scripting.  
- `grep`: Búsqueda de patrones (Perl puede hacerlo con `-n`/`-p`).  

---


