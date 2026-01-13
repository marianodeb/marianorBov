

### Operadores de comparación y tests para archivos en scripts Bash

| Condición | Equivalente |
| --- | --- |
| $a -lt $b | $a < $b |
| $a -gt $b | $a > $b |
| $a -le $b | $a <= $b |
| $a -ge $b | $a >= $b |
| $a -eq $b | $a es igual a $b |
| $a -ne $b | $a no es igual a $b |
| -e $FILE | $FILE existe |
| -d $FILE | $FILE existe y es un directorio |
| -f $FILE | $FILE existe y es un archivo regular |
| -L $FILE | $FILE existe y es un soft link |
| $STRING1 = $STRING2 |  $STRING1 es igual a $STRING2 |
| $STRING1 != $STRING2 |   $STRING1 no es igual a $STRING2 |
| -z $STRING1 | $STRING1 está vacía |


-  -d te permitirá saber si es un directorio y si existe
-  -f lo mismo que en el caso anterior pero para archivos
-  -r en este caso te permite saber si el archivo tiene permiso de lectura
-  -s con esta opción puedes saber si el tamaño del archivo es mayor que cero. Es decir, que no se trata de un archivo vacío
-  -w te permitirá identificar si el archivo tienen permisos de escritura
-  -x lo mismo que en el caso anterior pero para el caso de permisos de ejecución.


### Operadores de comparacion de numeros

| Ejemplo  | Abrev | Palbra Origen |
| --- | --- | --- |
| int1 -eq int2 | iguales que -eq | equal|
| int1 -ne int2 | distintos que -ne | |
| int1 -gt int2 | mayor que  -gt | greater than |
| int1 -ge int2 | mayor o igual que  -ge | greater than or equal |
| int1 -lt int2 | menor que -lt | smaller than |
| int1 -le int2 | menor o igual qeu -le | less than or equal |


### Comparación Numérica
 
| Descripcion | Operador |
| --- | --- |
| Igualdad | == |
| No igualdad | != |
| Menor que | -lt |
| Menor o igual que | -le |
| Mayor que | -gt |
| Mayor o igual que | -ge |

### Comparación de Cadenas:

|  Descripcion | Operador |
| --- | --- |
| Igualdad | == |
| No igualdad | != |
| Cadena no vacía | -n |
| Cadena vacía | -z |

### Comparación de Archivos:

| Descripcion            | Operador |
| ---------------------- | -------- |
| Existe                 | -e       |
| Es un archivo regular  | -f       |
| Es un directorio       | -d       |
| Es un enlace simbólico | -L       |
| archivo con permiso    | -r       |
| archivo con permiso    | -w       |
| archivo con permiso    | -x       |

### operadores Logicos

| operacion | test | []  |
| --------- | ---- | --- |
| and       | -a   | &&  |
| or        | -o   |     |
| not       | !    | !   |

---

## [[CaracteresWild_ER]]


- **Codigo ASCII**
- **Atajos Terminal**
- **Comodines básicos**
- **Expresiones regulares**

---
## Sintaxis 


### if elif else 

statement= sentencia o comandos

```bash
if [ condition ]
then
	statement
fi
```


```bash
if [condicion]
then
	comando
elif [condicion]
	comando
then
fi
```


```bash
if [ condition ]
then
	statement
else
	do this by default
fi
```


```bash
if [ condition ]
then
	statement
elif [ condition ] 
then
	statement 
else
	do this by default
fi
```



```bash
if [ condicion ]; then
  tu codigo
fi
```

## Ejemplos

```bash
if [ $(whoami) = 'root' ]; then
	echo "Tú eres root"
else
	echo "Tú no eres root"
fi
```


```bash
EDAD=$1

if [ $AGE -lt 13 ]; then
	echo "Eres un niño."
elif [ $AGE -lt 20 ]; then
	echo "Eres un adolescente."
elif [ $AGE -lt 65 ]; then
	echo "Eres un adulto."
else
	echo "Eres un adulto mayor."
fi
```


```bash
TEMP=$1

if [ $TEMP -gt 5 ]; then
	if [ $TEMP -lt 15 ]; then
		echo "El clima está frío."
	elif [ $TEMP -lt 25 ]; then
		echo "El clima está bien."
	else
		echo "El clima está caliente."
	fi
else
	echo "Está congelado afuera ..."
fi
```

### Entrada de datos  read

1.
```bas
echo 'introducir el nombre'
read nombre
```

2.
```bash
read -p 'introducir el nombre completo' nombre segundo_nombre apellido
echo 'te llamas: ' $nombre $segundo_nombre $apellido
```


## Bucles

### Case


```bash
case
case $variable in
		patron)
				comandos
						;;
		patron)
				comandos
						;;
		patron)
				comandos
						;;
	*)                                   #es el valor por default, significa que: sino se cumple ninguno de los patrones 
			comandos
					;;
esac
```


### Bucle for      sintaxis

```bash
for varaible in lista
do 
	comando que pueden utilizar $variable
done
```


### Bucle while      sintaxis  while = mientras

```bash
while condicion
do 
	comando
done
```


### Bucle until       sintaxis     until = hasta

```bash
until condicion
do 
	comando
done
```

---


### Condicionales en Bash (if statements)

#### Sintaxis básica:

```bash
if [ condición ]; then
    # código si la condición es verdadera
else
    # código si la condición es falsa
fi
```

#### Ejemplo:

```bash
edad=18

if [ $edad -ge 18 ]; then
    echo "Eres mayor de edad."
else
    echo "Eres menor de edad."
fi
```

#### Operadores de comparación:

- `-eq`: igual a
- `-ne`: no igual a
- `-lt`: menor que
- `-le`: menor o igual que
- `-gt`: mayor que
- `-ge`: mayor o igual que

### Ciclos en Bash (for loops)

#### Sintaxis básica:

```bash
for variable in lista_de_valores; do
    # código a ejecutar
done
```

#### Ejemplo:

```bash
for color in rojo verde azul; do
    echo "El color es $color"
done
```

#### Opciones de iteración:

- Iterar sobre números: `for (( i=1; i<=10; i++ ))`
- Iterar sobre archivos: `for archivo in *.txt`
- Iterar usando `seq`: `for i in $(seq 1 5)`

### Ciclos mientras y hasta en Bash (while y until loops)

#### Sintaxis básica:

```bash
while [ condición ]; do
    # código a ejecutar
done
```

```bash
until [ condición ]; do
    # código a ejecutar
done
```

#### Ejemplo de while:

```bash
contador=1
while [ $contador -le 5 ]; do
    echo "Contador: $contador"
    contador=$((contador + 1))
done
```

#### Ejemplo de until:

```bash
contador=1
until [ $contador -gt 5 ]; do
    echo "Contador: $contador"
    contador=$((contador + 1))
done
```

### Operadores lógicos en Bash

- `&&`: AND lógico
- `||`: OR lógico
- `!`: NOT lógico

#### Ejemplo de operadores lógicos:

```bash
edad=18

if [ $edad -ge 18 ] && [ $edad -le 65 ]; then
    echo "Eres un adulto en edad laboral."
fi

if [ $edad -lt 18 ] || [ $edad -gt 65 ]; then
    echo "No estás en edad laboral."
fi

if ! [ $edad -ge 18 ]; then
    echo "Eres menor de edad."
fi
```

### Operadores aritméticos en Bash

- `+`, `-`, `*`, `/`: Operadores aritméticos básicos
- `%`: Módulo (resto de la división)

#### Ejemplo de operadores aritméticos:

```bash
num1=10
num2=4

# Suma
echo $((num1 + num2))

# Resta
echo $((num1 - num2))

# Multiplicación
echo $((num1 * num2))

# División
echo $((num1 / num2))

# Módulo
echo $((num1 % num2))
```

---

## Escape de caracteres especiales


### **Caracteres que necesitan ser escapados**

En Bash, algunos caracteres tienen un significado especial y deben ser escapados (con una barra invertida `\`) si quieres que se traten como texto literal. Aquí tienes una lista de los principales:

1. **Espacio**: Si un argumento contiene espacios, debe estar entre comillas o escapado.

```bash
echo "Hola Mundo"  # Correcto
echo Hola\ Mundo   # Correcto (espacio escapado)
```

2. **`$`**: Indica una variable o expansión de comandos.

```bash
echo "El valor es \$10"  # Escapado para imprimir literalmente $
```

3. **`"` y `'`**: Las comillas tienen un significado especial en Bash.

```bash
echo "Esto es una \"comilla\""  # Escapado dentro de comillas dobles
echo 'Esto es una \'comilla\''  # No funciona, mejor usar comillas dobles
```

4. **`\`**: La barra invertida en sí misma debe escaparse si quieres que se trate como un carácter literal.

```bash
echo "Esto es una barra invertida: \\"
```

5. **`` ` ``**: El acento grave (backtick) se usa para ejecutar comandos.

```bash
echo "El resultado es \`ls\`"  # Escapado para imprimir literalmente
```

6. **`[ ]`, `{ }`, `( )`**: Estos caracteres tienen significados especiales en Bash (expansiones, listas, etc.).

```bash
echo "Los corchetes \[\] se escaparon"
```

7. **`*`, `?`**: Son comodines en Bash.

```bash
echo "El asterisco \* no es un comodín aquí"
```

8. **`&`, `|`, `;`**: Son operadores de control en Bash.

```bash
echo "El símbolo \& no ejecuta en segundo plano"
```

---

### **Cuándo escapar caracteres**

Debes escapar caracteres especiales cuando:

1. **No estás usando comillas**: Si no usas comillas, Bash interpretará los caracteres especiales.

```bash
echo Hola\ Mundo  # Espacio escapado
```

2. **Dentro de comillas dobles `"`**: Algunos caracteres (como `$`, `` ` ``, y `\`) siguen teniendo significado dentro de comillas dobles, así que debes escaparlos si quieres que sean literales.

```bash
echo "El precio es \$10"
```

3. **Dentro de comillas simples `'`**: No necesitas escapar caracteres, pero no puedes incluir comillas simples dentro de una cadena entre comillas simples.

```bash
echo 'Esto es $10'  # $ se trata como texto literal
```

---

### **Cuándo usar comillas simples `'` o dobles `"`**

1. **Comillas simples `'`**:

   - Todo dentro de comillas simples se trata como texto literal.
   - No se interpretan variables (`$VAR`), comandos (`` `comando` ``), o caracteres especiales.
   - No puedes incluir una comilla simple dentro de una cadena entre comillas simples.
   ```bash
   echo 'Hola $USER'  # Imprime literalmente "Hola $USER"
   ```

2. **Comillas dobles `"`**:

   - Permiten la expansión de variables (`$VAR`) y comandos (`` `comando` `` o `$(comando)`).
   - Algunos caracteres especiales (como `$`, `` ` ``, y `\`) siguen teniendo significado, así que debes escaparlos si quieres que sean literales.
   ```bash
   echo "Hola $USER"  # Imprime "Hola tu_usuario"
   echo "El precio es \$10"  # Escapa $ para imprimir literalmente
   ```

3. **Sin comillas**:

   - Solo se recomienda para cadenas simples sin espacios o caracteres especiales.
   - Bash interpretará espacios, comillas, y otros caracteres especiales.
   ```bash
   echo Hola  # Correcto
   echo Hola Mundo  # Incorrecto (se interpreta como dos argumentos)
   ```

---

### **Ejemplos prácticos**

1. **Escapar caracteres especiales**:

```bash
echo "El precio es \$10 y el comando es \`ls\`"
```

2. **Usar comillas simples**:

```bash
echo 'El precio es $10 y el comando es `ls`'
```

3. **Usar comillas dobles con expansión de variables**:

```bash
nombre="Juan"
echo "Hola $nombre, hoy es $(date)"
```

4. **Escapar comillas dentro de comillas**:

```bash
echo "Esto es una \"comilla\" dentro de comillas dobles"
echo 'Esto es una \'comilla\' dentro de comillas simples'  # No funciona
echo 'Esto es una '"'"'comilla'"'"' dentro de comillas simples'  # Correcto
```

---

### **Resumen**

- **Escapa caracteres especiales** cuando no estás usando comillas o cuando usas comillas dobles `"`.
- **Usa comillas simples `'`** para cadenas literales donde no necesitas expansión de variables o comandos.
- **Usa comillas dobles `"`** cuando necesitas expandir variables o comandos dentro de la cadena.










