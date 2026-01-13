
P30   19/09 21/09
P48   22/09  
P65   23/09  
p75   24/09
p     30/09

## Comodines

| comodin                      | singificado                                                                       |     |
| ---------------------------- | --------------------------------------------------------------------------------- | --- |
| *                            | caulquier caracter                                                                |     |
| ?                            | caulquier caracter individual                                                     |     |
| [catacter]                   | cualquier caracter que sea miembro del gurpo caracter                             |     |
| [!catacter]                  | cualquier caracter que no sea miembro del grupo caracter                          |     |
| \[\[:calass:\]\]             | cualquier caracter que sea mienmbro de una clase especifica                       |     |
| \[:alnum:\]                  | cualquier caracter alfanumerico                                                   |     |
| \[:alpha\]                   | cualquier caracter alfabetico                                                     |     |
| \[:digit:\]                  | cualquier numerico                                                                |     |
| \[:lower:\]                  | caulquier letra minuscula                                                         |     |
| \[:upper:\]                  | cualquier letra mayuscula                                                         |     |
| data???                      | todos los archivos que empiezan por data seguido de exactamente 3 caracteres      |     |
| \[abc\]*                     | todos los archivos que empiezan por: a, b, c                                      |     |
| backup.\[0-9\]\[0-9\]\[0-9\] | todos los archivos que empiezan por backup. seguido de exactamente tres numeros   |     |
| \[\[:upper:\]\]\*            | todos los archivos que empizan por una letra mayuscula                            |     |
| \[!\[:digit:\]\]\*           | todo lso archivos que no empiezan por un numero                                   |     |
| \*\[\[:lower:\]123\]         | todos los archivos que terminan por una letra minuscula o por los numeros 1, 2, 3 |     |




---

## ln enlaces 

enlaces comando ln
enlaces duros
ln ruta_delarchivo ruta_y_nombre_del_archivo
enlaces simbolico
ln -s ruta_delarchivo ruta_y_nombre_del_archivo

---

***type*** - indica como se intrepreta el nombre de un comando
***which*** - muestra la localizacion de un ejecutable
***help*** - ofrece ayuda para funciones del shell
***man*** - muestra el manual de un comando
***apropos*** - muestra una lista de comandos apropiados
***info*** - muestra informacion sobre un comando
***whatis*** - muestra una descripcion muy breve de un comando

---

## alias

Se puede agregar un comando tras otro usando ";" 
 para saber si el alias esta libre utilizar el comando type

crear alias
alias nombre='string_del_comando'
ejemplo 
$alias foo='cd /usr; ls; cd -'
eliminar alias
$unalias foo

--- 

## cat

cat - concatenando archivos con cat si encontramos varios archivos como : 
movie.mpeg.001 movie.mpeg.002 ... movie.mpeg.099 
se podria unir con este coamnado:
cat movie.mpeg.0* > movie.mpeg

--- 

## uniq

elimina las lineas repetidas sucesivas. para ordenarlas se utiliza primero el comando $sort
ejemplo: 

$ ls /bin /usr/bin | sort | uniq -d | less

---

## wc

Muestra el numero de lineas, palabras y bytes wc (word count - contador de palabras)
ejemplo
$wc arcvhivo.txt

---

## grep

Busca patrones
ejemplo

$grep patron archivo.txt

---

## Aritmetica en la terminal

La expaion aritmetica solo soprta enteros 
$((EXPRESION))

| Operador | Descripcion    |
| -------- | -------------- |
| +        | Suma           |
| -        | Resta          |
| *        | Multiplicacion |
| /        | Division       |
| %        | Modulo - resto |
| **       | Potencia       |

ejemplo 5 al cuadrado por 3:

$echo $(($((5\*\*2))\*3))
o 
$echo $(((5\*\*2)\*3))

---

## Expasion con llaves

$echo Front-{A,B,C}-Back

Los patrones a expandir con llaves deben contener un prefijo llamado preámbulo y un sufijo
llamado postcript. La expresión entre llaves debe contener una lista de cadenas separadas por comas
o un rango de números enteros o caracteres individuales. El patrón no debe contener espacios en
blanco. Aquí hay un ejemplo usando un rango de números enteros:

$echo numer_{1...5}

Los numeros enteros tambien pueden tener ceros a la izquieda asi:
$echo {01...15}

Rango de letras:

$echo {Z...A}
o
$echo {A...z}

Las  expasione con llaves pueden ser anidadas:

$echo a{A,{1,2},B{3,4}}b

Epansiones con mkdir
ejemplo:

$mkdri {2022...2024}-{1...12}

---

## Secuencia de escape

| Secuencia de escape | Significado                                                  |
| ------------------- | ------------------------------------------------------------ |
| \a                  | Tono ("Alerta"- hace que el ordenador pite)                  |
| \b                  | Retroceder un espacio                                        |
| \n                  | Nueva linea. En sistemas como unix, produce unsalto de linea |
| \r                  | Retorno de carro                                             |
| \t                  | Tabulacion                                                   |

---

## Movimiento del cursor

| Teclas | Accion                                                              |
| ------ | ------------------------------------------------------------------- |
| Ctrl a | Mueve el cursor al principio de la linea                            |
| Ctrl e | Mueve el cursor al final de la linea                                |
| Ctrl f | Mueve el cursor un caracter hacia adelante; igual que la flecha der |
| Ctrl b | Mueve el cursor un caracter ahcia atras; igual flecha izq           |
| Alt f  | Mueve el cursor hacia adelante una palabra                          |
| Alt b  | Mueve el cursor hacia detras una palabra                            |
| Ctrl l | Limpia la pantalla                                                  |

---

## Modificando el texto en la terminal

| Teclas | Accion                                                                                            |
| ------ | ------------------------------------------------------------------------------------------------- |
| Ctrl d | Borra un caracter en la localizacion del cursor                                                   |
| Ctrl t | Traspasa (intercambia) el caracter en la localizacion del cursor con el que le precede            |
| Alt t  | Trasla palabra en la localizacion del cursor con la que le precede                                |
| Alt l  | Convierte los caracteres desde la localizacion del cursor hasta el final de la plabra a minuscula |
| Alt u  | Convierte los caracteres desde la localizacion del cursor hasta el final de la palbra a mayuscula |

---

## Cortar y pegar

| Teclas         | Accion                                                                                                                                                                   |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Ctrl k         | Kill (corta) el texto desde la localizacion del cursor al final de lal ineas                                                                                             |
| Ctrl u         | Kill (corta) el texto desde la localizacion del cursor hasta el principio de la linea                                                                                    |
| Altl d         | Kill (corta) el texto desde la localizacion del cursor hasta el final de la palabra                                                                                      |
| Altl Retroceso | Kill (corta)  el texto desde la localizacion del cursor hasta el principio de la palbra actaul. Si el cursor esta al principio de una palabra, corta la palabra anterior |
| Ctrl y         | Yank (pega) texto del kill-ring y lo coloca en la localizacion del cursor                                                                                                |

---

## Atajos para manipular comando history

| Tecla  | Accion                                                                                                                                                    |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ctrl p | Se mueve a la anterior entrada de historial. Miama accion que la flecha hacia arriba                                                                      |
| Ctrl n | Se mueve a la siguiente entrada del historial. Misma accion que la flecha hacia abajo                                                                     |
| Alt <  | Se mueve al principio (arriba) del historial                                                                                                              |
| Alt >  | Se mueve al final (abajo) del histrial, p.ej., la actual linea de comandos                                                                                |
| Ctrl r | Busqueda incremental inversa. Busqueda incrementalmente desde el actual comando hacia arriba en el historial                                              |
| Alt p  | Busqueda inversa, no incremental. Con esta conmbinacion de teclas, escribes las palabras a buscar y presionas enter antes de que busqueda se realice      |
| Alt n  | Busqueda hacia delante,no incremental                                                                                                                     |
| Ctrl o | Ejecuta el elemento actual en el historial y avanza al siguiente. Esto es practico si estas intentando reejecutar una secuencia de comandos del historial |

---

## Expasion del historial

| Secuencia | Accion                                                                            |
| --------- | --------------------------------------------------------------------------------- |
| !!        | Repite el ultimo comando. Probablemente es mas facil pulsa la fecha y luego enter |
| !numero   | Repite el elemento del historial numero                                           |
| !texto    | Repite el ultimo elemento del historial que empiece con texto                     |
| !?        | Repite el ultimo elemento del historial que contanga texto                        |

---

## Comando para manipular permisos

***id***– Muestra la identidad del usuario
***chmod*** – Cambia el modo de un archivo
***umask*** – Establece los permisos por defecto
***su*** – Ejecuta un shell como otro usuario
***sudo*** – Ejecuta un comando como otro usuario
***chown*** – Cambia el propietario de un archivo
***chgrp*** – Cambia la propiedad de grupo de un archivo
***passwd*** – Cambia la contraseña de un usuario

---

## Tipos de archivos

| Atributo | Tipo de archivo                                                                                                                    |     |                                                                                                                                                                                                              |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------- | --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| d        | Directorio                                                                                                                         |     |                                                                                                                                                                                                              |
| l        |                                                                                                                                    | e   | nlace simbolico. Con los enlaces simbolicos, el resto de los atributos del archvio son "rwxrwxrwx" y que son valores de relleno. Los atributos reales son los del archivo al que el enlace simbolico apunta. |
| c        | Aarchivo de caracter especial. Se refiere a un dispositivo que soporta datos como una cadena de bytes, como un terminal o un modem |     |                                                                                                                                                                                                              |
| b        | Archivo de bloque especial. Se refiere a un dispositivo que soporta datos en bloques, como un disco duro o una unidad de CD        |     |                                                                                                                                                                                                              |

| Propietario | Grupo | Mundo |
| ----------- | ----- | ----- |
| rwx         | rwx   | rwx   |

| Atributo | Archivo                                                | Directorio                                                                                                                             |                                                                                                            |
| -------- | ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| r        | Permite que sea abierto y leido                        | Permite que el contenido del directorio sea listado si el atributo de x tambien esta configurado                                       |                                                                                                            |
| w        |                                                        | Permite que sea escrito o truncado, no permite renombrar o borrar.Borrar, renombrar viene determidada por los atributos del directorio | Permite crear, borrar y nombrar archivos dentro de un directorio si el atributo x tambien esta establecido |
| x        | Permite que sea tratado como un programa y ejecutarlo. | Permite entrar en el directorio, ejemplo: cd directorio                                                                                |                                                                                                            |

---

##Modos de archivos en BInario y Octal

| Octal | Binario | Modo de archvio |
| ----- | ------- | --------------- |
| 0     | 000     | ---             |
| 1     | 001     | --x             |
| 2     | 010     | -w-             |
| 3     | 011     | -wx             |
| 4     | 100     | r--             |
| 5     | 101     | r-x             |
| 6     | 110     | rw-             |
|7|111|wrx|

---

## Notacion simbolica de chmod

| Simbolo | Significado                                                                        |
| ------- | ---------------------------------------------------------------------------------- |
| u       | Abreviatura de "usuario" pero significa el propietario del archivo o el directorio |
| g       | El grupo del propietario                                                           |
| o       | Abreviatura de "otros", pero se refiere al mundo                                   |
| a       | Abreviatura de "all" (todos). Es la combinacion de "u", "g", y "o"                 |

---

## Comando chown - cambia el grupo

Sintaxis 

$chown \[propietario\]\[:\[grupo\]\] archivo

```bash
$sudo chown propietario:grupo archivo_directorio
$sudo chown cambia_propietario archivo_directorio
$sudo chown :cambia_grupo archivo_directorio
$sudo chown propietario: archivo_directorio \#cambia propietario y grupo al nuevo propietario
```
---
