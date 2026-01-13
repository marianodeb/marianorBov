| catacter | nombre       | combinacion          | numero hexadecimal |     |
| -------- | ------------ | -------------------- | ------------------ | --- |
| **~**    | virgulilla   | Ctrl + shif + u + 7e | 7e                 |     |
| **\\**   | contra barra | Ctrl + shif + u + 5c | 5c                 |     |
| **\`**   | acento grave | Ctrl + shif + u + 60 | 60                 |     |
| **^**    |              | Ctrl + shif + u + 5e | 5e                 |     |


## Codigo ASCII

![[ASCII.pdf]]


## Atajos Terminal

|conv teclas|accion|
|---|---|
|Ctrl-a|Ir al principio de la linea|
|Ctrl-e|Ir al final de la linea.|
|Ctrl-b|Retroceder un caracter.|
|Alt-b|Retroceder una palabra|
|Ctrl-f|Avanzar un caracter|
|Alt-f |Avanzar una palabra.|
|Alt-] x|Avanzar hasta la siguiente ocurrencia del caracter x.|
|Alt-Ctrl-] x|Retroceder hasta la anterior ocurrencia del caracter x.|
|Ctrl-u|Borrar desde el cursor hasta el principio de la linea|
|Ctrl-k|Borrar desde el cursor hasta el final del linea|
|Ctrl-w|Borrar desde el cursor hasta el principio de la palabra|
|Ctrl-Shift-V|Pega el texto del portapapeles|
|Ctrl-Shift-C|Copia el texto del portapapeles|
|Ctrl-l|borra la pantalla|
|Ctrl-r|Texto|


## Comodines básicos

- **`*`:** Coincide con cualquier secuencia de caracteres, incluyendo una cadena vacía.
    - Ejemplo: `ls *.txt` mostrará todos los archivos con extensión .txt en el directorio actual.
- **`?`:** Coincide con cualquier carácter único.
    - Ejemplo: `ls a?` mostrará los archivos que comienzan con "a" y tienen un carácter más.
- **[`[]`]:** Define un conjunto de caracteres.
    - Ejemplo: `ls [abc].txt` mostrará los archivos que comienzan con "a", "b" o "c" y terminan en .txt.
    - **Rangos:** `[a-z]` coincide con cualquier letra minúscula, `[0-9]` con cualquier dígito.
    - **Negación:** `[^abc]` coincide con cualquier carácter excepto "a", "b" o "c".

**Ejemplos más avanzados:**

- **Combinaciones:** Puedes combinar varios comodines.
    - Ejemplo: `ls [a-z]?[0-9].txt` mostrará archivos con dos caracteres (una letra minúscula seguida de un dígito) y extensión .txt.
- **Inicio y final de línea:**
    - `^`: Coincide con el inicio de una línea.
    - `$`: Coincide con el final de una línea.
    - Ejemplo: `grep '^error' archivo.log` buscará líneas que comiencen con la palabra "error" en el archivo.
- **Comodines en expresiones regulares:**
    - Muchos comandos de Linux (como `grep`, `sed`, `awk`) soportan expresiones regulares más complejas.
    - Por ejemplo, `.` coincide con cualquier carácter (excepto un salto de línea), `+` indica una o más repeticiones del carácter anterior.
    - Ejemplo: `grep 'a.+' archivo.txt` buscará líneas que contengan la letra "a" seguida de uno o más caracteres cualquiera.

**Otros comodines útiles:**

- **`/`:** Separa directorios en rutas.
- **`~`:** Representa el directorio home del usuario.
- **`.`:** Representa el directorio actual.
- **`..`:** Representa el directorio padre.

**Ejemplos prácticos:**

- **Buscar archivos:**
    - `find /home/usuario -name "*.pdf"`: Busca todos los archivos PDF en el directorio home del usuario.
    - `locate *.jpg`: Busca todos los archivos JPG en el sistema (requiere una base de datos actualizada).
- **Renombrar archivos:**
    - `mv *.txt archivos.zip`: Comprime todos los archivos .txt en un archivo ZIP.
- **Eliminar archivos:**
    - **¡Ten mucho cuidado!** `rm *.tmp` eliminará todos los archivos temporales en el directorio actual.

**Importante:**

- **Comprueba siempre antes de ejecutar comandos que puedan eliminar archivos importantes.**
- **Utiliza comillas dobles ("") para proteger espacios y caracteres especiales en nombres de archivos.**
- **Consulta la documentación de cada comando para conocer las opciones específicas y las expresiones regulares soportadas.**

**¿Tienes alguna pregunta más específica sobre el uso de comodines en Linux?**

**Ejemplo:** Si quieres saber cómo buscar todos los archivos que comiencen con "log" y tengan una fecha en formato "AAAA-MM-DD" en el directorio "/var/log", podríamos usar una expresión regular como esta:

```bash
find /var/log -name "log[0-9][0-9][0-9][0-9]-[0-1][0-9]-[0-3][0-9]*"
```


- **Rangos de caracteres:** Además de los rangos numéricos y alfabéticos, puedes combinar rangos: `[a-zA-Z0-9]` coincide con cualquier letra (mayúscula o minúscula) o dígito.
- **Negación:** `[^0-9]` coincide con cualquier carácter que _no_ sea un dígito.
- **Clases de caracteres:** Muchas expresiones regulares ofrecen clases de caracteres predefinidas, como `\d` para dígitos, `\s` para espacios en blanco, `\w` para caracteres alfanuméricos.

**Expresiones regulares más complejas:**

- **Cuantificadores:**
    - `+`: Una o más ocurrencias del carácter anterior.
    - `*`: Cero o más ocurrencias.
    - `?`: Cero o una ocurrencia.
    - `{n}`: Exactamente n ocurrencias.
    - `{n,}`: Al menos n ocurrencias.
    - `{n,m}`: Entre n y m ocurrencias.
- **Alternativas:** `|` separa alternativas. Por ejemplo, `(txt|pdf)` coincide con ".txt" o ".pdf".
- **Agrupación:** `()` agrupa expresiones para aplicar cuantificadores o alternativas.
- **Anclajes:** `^` al inicio de una línea, `$` al final.

**Ejemplos:**

- `find /var/log -name "log[0-9]{8}.txt"`: Busca archivos .txt que comiencen con "log" seguido de 8 dígitos.
- `grep '^[[:upper:]]'` archivo.txt: Busca líneas que comiencen con una letra mayúscula.
- `sed 's/\(hello\)/\U\1/g'` archivo.txt: Convierte todas las ocurrencias de "hello" a mayúsculas.
- `awk '/error/ {print $2}' archivo.log`: Imprime la segunda columna de las líneas que contienen la palabra "error".

**Comodines en otros comandos:**

- **`grep`:** Busca patrones en archivos.
- **`sed`:** Edita archivos de texto.
- **`awk`:** Procesamiento de texto estructurado.
- **`find`:** Busca archivos en el sistema de archivos.
- **`rsync`:** Sincroniza archivos y directorios.
- **`mv`:** Renombra o mueve archivos.
- **`cp`:** Copia archivos.

**Recursos adicionales:**

- **Tutorial detallado:** [https://atareao.es/tutorial/terminal/comodines-y-expresiones-regulares/](https://atareao.es/tutorial/terminal/comodines-y-expresiones-regulares/)
- **Documentación de `grep`:** `man grep`
- **Documentación de `sed`:** `man sed`
- **Documentación de `awk`:** `man awk`

---
### Comodines

- `?`. Representa un único carácter. Así por si ejecutas `ls /dev/sda?` te listará todos los archivos que sean igual a `/dev/sda` mas un único caracter, que puede ser cualquier letra o número. Así en mi caso, ha listado mis unidades, de la `/dev/sda1` a la `/dev/sda7`.
- `*`. Este comodín representa desde nada, hasta cualquier cantidad de caracteres y dígitos. Así, en el ejemplo que he indicado anteriormente, si ejecutados `ls /dev/sd*` te listará `/dev/sda`, `/dev/sda1` a `/dev/sda7` y si tienes otra unidad, `/dev/sdb`, `/dev/sdb1`,…
- `[]`. En este caso, este comodín representa un rango, ya sea de caracteres o de números. Siguiendo con el ejemplo anterior, podemos listar `ls /dev/sda[1-5]`. Ya te puedes hacer una idea de lo que va a listar.
- `{}`. Esto en realidad es mas un conjunto de comodines separados por comas. Igual que en casos anteriores, podrías ejecutar la siguiente orden `ls {sda*,sdb*}`. Ojo con dejar espacios alrededor de la coma, por que te dará un error.
- `[!]`. El funcionamiento de este comodín es similar a `[]`, salvo que representa justo lo contrario. Es decir se trata de listar todo aquello que que no esté en ese rango. Por ejemplo, `ls /dev/sda[!1-5]` te mostrará `/dev/sda6` y `/dev/sda7`. Como te imaginas, esto es en mi caso, en tu equipo seguramente el resultado será otro.
- `\`. Esta es la secuencia de escape y que tienes que tener siempre muy presente. Con este carácter puedes mostrar otros caracteres. Así, si quieres crear el directorio `esta casa` y ejecutas `mkdir esta casa`, te creará dos directorios, `esta` y `casa`. Para hacer lo que quieres, tienes diferentes alternativas, o bien `mkdir "esta casa"` o bien `mkdir esta\ casa`. En esta segunda orden utilizamos `\` para escapar el carácter espacio. Esto ya te lo comenté en el artículo anterior sobre

---

## Expresiones regulares

Las expresiones regulares tienen un potencial increible, pero a diferencia de los comodines necesitan una mayor esfuerzo por tu parte. Por una lado necesitan de una curva de aprendizaje mas o menos pronunciada, y por otro lado, su aplicación no es tan intuitiva como en el caso de los comodines.

A continuación encontrarás algunos de los elementos con los que construir expresiones regulares. Sin embargo, al contrario que con los comodines, dejaré los ejemplos para el final.

- `.`. Representa un solo carácter, es el equivalente a la `?` de los comodines.
- `\`. Se utiliza para escapar caracteres, al igual que en el caso de los comodines.
- `+`. El elemento precedente puede aparecer 1 o mas veces.
- `*`. Es similar al anterior, pero en este caso, el elemento puede aparecer **cero** o mas veces.
- `^` ó `\A`. Dependiendo de su ubicación tiene un significado u otro. Así si lo encuentras al principio se corresponde con que lo que buscamos debe comenzar igual. Si lo encontramos entre corchetes es una negación, como veremos mas adelante.
- `$` ó `\Z`. Es el opuesto al anterior, en tanto en cuanto, cuando lo encuentras al final indica que lo que buscamos tiene que acabar igual.
- `[]`. Especifica un rango, ya sea separado por comas como `[a,b,c]` o bien `[a-c]`.
- `|`. Representa un **o lógico**.
- `[^]`. Como he indicado anteriormente, esta expresión se utiliza para negar rangos.
- `{}`. Indica el número de repeticiones del caracter precedente. Así `a{3}` es equivalente a `aaa`. Pero además `a{3,}` representa 3 ó mas `a`. En el caso de `a{1,5}` se refiere a entre 1 y 5.

Además de estas que son muy parecidas a los comodines, en el caso de las expresiones regulares tenemos mas, como son las siguientes,

- `\s`. Se corresponde con un espacion en blanco.
- `\S`. El contrario del anterior, es decir, cualquier carácter que no sea un espacio en blanco.
- `\d`. Equivale a un dígito.
- `\D`. Cualquier carácter que no sea un dígito.
- `\w`. Se corresponde a cualquier carácter que se pueda utilizar en una palabra. Es equivalente a `[a-zA-Z0-9_]`.
- `\W`. El opuesto al anterior, es decir, es equivalente a `[^a-zA-Z0-9_]`.

Por supuesto, también tiene en cuenta los _caracteres escapados_, que comenté anteriormente, y entre los que cabe citar,

- `\n`. Se corresponde con una línea nueva.
- `\r`. Para retorno de carro.
- `\t`. Representa una tabulación.
- `\0`. Se utiliza para un carácter nulo

Por último queda el rey que es `()` cuyo objetivo es el de capturar todo lo que está en su interior.

#### Algunas expresiones regulares útiles

Indicarte antes de comentarte sobre estos ejemplos de expresiones regulares que, normalmente van delimitados por `//`. Es decir, la expresión regular viene a ser `/expresión-regular/`.

- **Caracteres alfabéticos**. `/^[a-zA-Z]*$/`. Estos patrones son los mas sencllos de utilizar, sin embargo es un buen comienzo.
- **Caracteres en minúsculas**. `/^([a-z]*$` Igual que en el caso anterior, pero esta vez en minúculas.
- **Números**. `/^[0-9]*$/`. La tercera opción pero solo para dígitos. Sin embargo, a partir de ahora, la cosa se va a ir complicando.
- **Nombre de usuario**. `/^[a-z0-9_-]{3,16}$/`. En este caso, el nombre de usuario debe tener una longitud mínima de tres caracteres y máxima de 16. Solo puede estar compuesto por letras minúsculas, números, además de `_` y `-`. Podrías incluir también las mayúsculas de la siguiente forma, `/^[a-zA-Z0-9_-]{3,16}$/`.
- **Contraseña**. Esto es muy similar al anterior, pero, por un lado podemos considerar cambiar la longitud mínima y máxima de la contraseña, y por otro lado incluir algunos otros caracteres. Así podría ser algo como `[a-zA-Z0-9_-$!¡@?¿=;:]{8,20}$/`. Hemos aumentado la longitud mínima a `8` y la máxima a `20` y además hemos incorporado algunos caracteres mas o menos extraños como pueden ser`$!¡@?¿=;:`.
- **Correo electrónico**. Este patrón ya tiene un poco mas de dificultad. `/^([a-z0-9_\.-]+)@([a-z0-9_\.-])\.([a-z\.]{2,6})$/`. Se divide en tres grupos diferenciados, tipo `antes@despues.fin`. Los dos primeros admiten letras, números, además de `_`, `-` y `.`. Mientras que el último solo admite letras y el `.`, pero además con una longitud mínima de 2 y máxima de 6.
- **Dirección web**. Otro patrón realmente interesante, `/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/`
- **Código postal**. `[0-9]{5}(\-?[0-9]{4})?$`
- **Para direcciones IP**. Prepárate, que este es un buen chorizo `/^(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$`. Con esto nos aseguramos que cada uno de los grupos es número comprendido entre 0 y 255.
- **Etiquetas html**. Esta es muy interesante y seguro que la utilizarás en mas de una ocasión. Se trata de un patrón para etiquetas html. `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`
- **Tarjetas de crédito**. Como ves las cosas se van complicando, pero las posibilidades son realmente espectaculares. Puedes hacer casi cualquier cosa que te puedas imaginar, tan solo es cuestión de estudiarlo con el suficiente detalle. `/^(?:4[0-9]{12}(?:[0-9]{3})?|5[1-5][0-9]{14}|6011[0-9]{12}|622((12[6-9]|1[3-9][0-9])|([2-8][0-9][0-9])|(9(([0-1][0-9])|(2[0-5]))))[0-9]{10}|64[4-9][0-9]{13}|65[0-9]{14}|3(?:0[0-5]|[68][0-9])[0-9]{11}|3[47][0-9]{13})*$/`.
- **Fechas**. Al fin y al cabo, se pueden establecer expresiones regulares que nos ayuden en todas nuestras taresm y simjplifiquen el trabajo. `'#^((19|20)?[0-9]{2}[- /.](0?[1-9]|1[012])[- /.](0?[1-9]|[12][0-9]|3[01]))*$#`
- **Imágenes**. `/[^\s]+(?=\.(jpg|gif|png))\.\2)`