
Renombrar archivos en Linux con el comando rename
Con este comando, vas a tener cierto control. Varias configuraciones en Linux lo tienen incluido por defecto. Aun así, si no lo tienes instalado, lo puede instalar en unos simples pasos a través de este comando.

```bash
sudo apr install rename
```
La sintaxis básica de este comando se visualiza así:

```bash
rename 's/old-name/new-name' files
```

Veamos un ejemplo, en el cual crearemos una carpeta nueva titulada filetorename. Además, empleando el comando touch, generaremos cinco archivos.

```bash
mkdir filetorename
cd filetorename
touch file{1..5}.txt
ls
```

Si lo que quieres es renombrar un solo archivo llamado file1.txt, se tendría que ver así:

```bash
rename 's/file1/newfile1/' file.txt
```

modificar la extensión de los archivos a .php, puedes hacerlo de la siguiente manera:

```bash
rename 's/.txt/.php' *.txt
ls
```

Eliminar del nombre del fichero caracteres especiales que no están entre la letra y la z (a-z) . Dejando en el nombre del fichero solo caracteres alfanuméricos.
Ejemplo:
mi-fichero.txt por mifichero.txt

```bash
rename -v -n 'v/[^a-z]'*.*
```

Modifica nombres de archivo a mayúsculas:

```bash
rename 'y/a-z/A-Z'*
```

Modifica nombres de archivo a minúsculas:

```bash
rename 'A-Z/a-z'*
```

Reemplazar espacios con guiones bajos en los nombres de archivos:

```bash
rename 'y//_/'*
```

```bash
rename -v'y/(/_/'*
```

renombrar "(" por "\_"    <'/cambia esto/ por esto /'>

```bash
rename 's/ _720p_24fps_H264-192kbit_AAC//g' *.mp4
```


Lo que se hiizo fue: renombrar '/\_720p_24fps_H264-192kbit_AAC/por esto/'


Con (-n) siimula la operacion y muestra como quedaria sin realizar los cambios

```bash
rename -n 's/new/test' new.txt
```

salida:

```bash
rename(new.txt, test.txt)
```


forzar rename -f si es que existe el archivo


**$rename 's/new/test/' new.txt**


salida:

```bash
new.txt not renamed: test.txt already exists
```

```bash
rename -f 's/new/test/' new.txt
```

salida: La operación se completó sin problemas y test.txt se sobrescribió.

Renombrar un grupo de imágenes con nombres diferentes. Si tenemos un grupo de imágenes (por ejemplo PNG) a las que les queremos añadir una información en la parte final del nombre de la imagen antes de la extensión.
Ejemplo:
nombreimagen.png por nombreimagen_150x150.png
```bash
rename -v -n 's/.png/_150x150.png/' *.png
```
Vamos a suponer que queremos reemplazar los guiones bajos por guiones medios ("\_" por "\-") en los nombres de nuestros archivos de un directorio determinado.

```bash
rename -v -n 's/_/-/' *.jpg
```

Añadir texto al inicio del nombre del fichero. Con el carácter ^ le indicamos al comando rename que se sitúe en el comienzo del nombre del fichero y ahí inserte o ejecute la segunda parte.
Ejemplo:
leccion 1.doc,
leccion 2.doc ...
por
tema - leccion 1.doc,
tema - leccion 2.doc ..

```bash
rename -v -n 's/^/tema–/' *.doc
```

Si queremos eliminar varios caracteres antes de un punto de corte determinado.
Ejemplo:
texto1_abc_001_small.jpg,
texto2_abc_002_small.jpg,
texto3_abc_003_small.jpg
por:
texto1_small.jpg,
texto2_small.jpg,
texto3_small.jpg
Utilizamos para el corte la cadena "\_small" y le decimos que nos elimine los 8 caracteres (\\w) anteriores, o los reemplace por lo que indiquemos en la segunda parte del comando rename.

```bash
rename -v -n 's/w{8}/_small/_small/'*jpg
```

reemplazar desde un punto determinado de corte, pero respetando un número concreto de caracteres numéricos antes de la parte donde se produce el corte. Para este caso usamos el elemento "$1" en la cadena de la parte derecha, para que nos coja esa variable obtenida de la parte izquierda.  Viendo el ejemplo se entenderá mejor.
Ejemplo:

texto1_uno001_small.jpg,
texto2_otro002_small.jpg,
texto3_cualquiera003_small.jpg ...
por:
texto1_uno_ADD-001_small.jpg,
texto2_otro_ADD-002_small.jpg,
texto3_cualquiera_ADD-003_small.jpg ...

Utilizamos para el corte la cadena "\_small" y le decimos que nos guarde los 3 caracteres numéricos (\\d) anteriores (001, 002, 003...) utilizando el $1 en la segunda parte del comando (la expresión de la derecha) Nos añadirá o modificara lo indicado en la segunda parte del comando rename justo antes de esos 3 caracteres reservados antes del corte.

```bash
rename -v -n 's/(w{3})_small/_ADD–$1_small/' *.jpg
```

A continuación dejo un listado explicando (en inglés) las expresiones regulares que se pueden utilizar con este comando rename:

^  _matches the beginning of the line_   (coincide con el comienzo de la línea)

$  _matches the end of the line_    
	(coincide con el final de la línea)

.  _Matches any single character _  
	(Coincide con cualquier carácter)

(_character_)\*  _match arbitrarily many occurences of_ (_character_) 
	(coincide arbitrariamente con muchas apariciones de carácter)

(character)?  Match 0 or 1 instance of (character) 
	(Coincide con 0 o 1 instancia de caracter)

\[abcdef\]  _Match any character enclosed in_ \[\] (_in this instance_, a b c d e or f) _ranges of_ characters such as \[a-z\] are permitted. The behaviour of this deserves more description. 
	(Coincide con cualquier carácter encerrado en \[\] (en este caso, a b c d e of) se permiten rangos de caracteres como \[a-z\]. El comportamiento de esto merece más descripción.)

\[\^abcdef\]	Match any character NOT enclosed in \[\] (in this instance, any character other than a b c d e or f) 
	Coincide con cualquier carácter NO incluido en \[\] (en este caso, cualquier carácter que no sea a b c d e o f)


(character){m,n}	Match m-n repetitions of (character) 
	(Coincide con m-n repeticiones de carácter)

(character){m,}	Match m or more repetitions of (character) 
	(Coincide con m o más repeticiones de carácter)

(character){,n}	Match n or less (possibly 0) repetitions of (character) 
	(Coincide con n o menos (posiblemente 0) repeticiones de carácter)
	
(character){n}	Match exactly n repetitions of (character) 
	(Coincide exactamente con n repeticiones de carácter)

(expression)	Group operator.
 	Backreference – matches nth group
expression1|expression2	Matches expression1 or expression 2. Works with GNU sed, but this feature might not work with other forms of sed.

\w	matches any single character classified as a “word” character (alphanumeric or “\_”)
(coincide con cualquier carácter clasificado como carácter de “palabra” (alfanumérico o “\_”))

\\W	matches any non-“word” character 
	(coincide con cualquier carácter que no sea "palabra")

\\s	matches any whitespace character (space, tab, newline) 
	(coincide con cualquier carácter de espacio en blanco (espacio, tabulación, nueva línea))

\\S	matches any non-whitespace character
	(coincide con cualquier carácter que no sea un espacio en blanco)

\\d	matches any digit character, equiv. to \[0-9\]
	(coincide con cualquier carácter de dígito, equivalente. a \[0-9\])

\\D	matches any non-digit character
	(coincide con cualquier carácter que no sea un dígito)

---

El comando `rename` en sistemas Unix/Linux se utiliza para renombrar múltiples archivos de acuerdo con un patrón especificado. Es importante tener en cuenta que hay diferentes versiones de `rename` con variaciones en su sintaxis y funcionalidad dependiendo del sistema operativo. 

### Sintaxis básica de `rename`

La sintaxis general de `rename` puede variar entre distintas implementaciones, pero la más común es:

```bash
rename opciones 'expresión_de_búsqueda' 'expresión_de_reemplazo' archivos
```

- `opciones`: Son parámetros opcionales que modifican el comportamiento de `rename`.
- `'expresión_de_búsqueda'`: Es una expresión regular que especifica qué partes de los nombres de archivo serán modificadas.
- `'expresión_de_reemplazo'`: Es la cadena que reemplazará las partes encontradas por la expresión de búsqueda.
- `archivos`: Son los archivos que se van a renombrar.

### Ejemplos de uso común

#### Ejemplo 1: Renombrar archivos con un prefijo

```bash
rename 's/^prefijo/nuevo_prefijo/' archivo*
```

Esto renombrará todos los archivos que empiecen con `archivo` y tengan un prefijo `prefijo`, reemplazando `prefijo` con `nuevo_prefijo`.

#### Ejemplo 2: Cambiar la extensión de archivos

```bash
rename 's/.old$/.new/' *.old
```

Este comando cambiará la extensión de todos los archivos `.old` por `.new`.

### Uso de wildcards (comodines)

Los wildcards en `rename` se utilizan principalmente para seleccionar conjuntos de archivos sobre los cuales aplicar las operaciones de renombrado.

#### Ejemplo 3: Renombrar archivos con wildcards

```bash
rename 's/IMG00(\d+)/Image_$1/' IMG00*.jpg
```

En este ejemplo, se renombrarán todos los archivos `IMG00X.jpg` a `Image_X.jpg`, donde `X` es un número.

### Opciones útiles de `rename`

Las opciones específicas pueden variar según la implementación de `rename`, pero algunas comunes son:

- `-v`: Modo verboso (verbose), muestra los nombres de los archivos renombrados.
- `-n`: Modo simulación (dry-run), muestra qué archivos se renombrarían sin realizar cambios.
- `-f`: Forzar (force), sobrescribe archivos existentes sin pedir confirmación.

### Implementaciones específicas de `rename`

Es importante destacar que hay diferentes versiones de `rename` dependiendo del sistema operativo. Por ejemplo:

- **Perl rename (`prename`)**: Utiliza sintaxis similar a expresiones regulares de Perl.
- **Util-linux rename (`rename.ul`)**: Implementación más básica que puede tener una sintaxis diferente.

### Ejemplo específico con Perl `rename` (prename)

```bash
prename 's/\.txt$/\.bak/' *.txt
```

Este comando cambiará la extensión de todos los archivos `.txt` a `.bak`.

### Consideraciones adicionales

- **Backups**: Antes de realizar cambios masivos con `rename`, considera hacer una copia de seguridad de los archivos afectados, especialmente si no estás completamente seguro de los patrones y efectos que tendrán las expresiones regulares utilizadas.
- **Pruebas**: Utiliza el modo simulación (`-n` o `--dry-run`) para verificar qué cambios se realizarán antes de ejecutar `rename` en modo normal.

Espero que estos ejemplos y explicaciones te ayuden a comprender mejor cómo utilizar el comando `rename` en tu sistema Unix/Linux. Si tienes más preguntas o necesitas ejemplos adicionales, no dudes en preguntar.
