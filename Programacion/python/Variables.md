## Variables

### Asignación de Variables

En Python, creas una variable asignándole un valor con el operador `=`.  
**Ejemplos:**  

```python
# Asignación básica
nombre = "Ana"     # String
edad = 25          # Entero
precio = 19.99     # Float
es_estudiante = True  # Booleano

print(nombre)  # Salida: Ana
```

---

### Reasignación de Variables

Puedes cambiar el valor de una variable en cualquier momento:  

```python
# Variable original
contador = 10
print(contador)  # Salida: 10

# Reasignación
contador = 20    # Ahora vale 20
print(contador)  # Salida: 20

# Cambio de tipo de dato (Python es dinámicamente tipado)
contador = "veinte"  
print(contador)  # Salida: veinte
```

---

### Casos Especiales de Asignación

#### 1. Asignación Múltiple 

Asignar varios valores en una línea:  

```python
x, y, z = 1, 2, 3
print(x, y, z)  # Salida: 1 2 3
```

#### 2. Asignación en Cadena

Mismo valor a múltiples variables:  

```python
a = b = c = 0
print(a, b, c)  # Salida: 0 0 0
```

#### 3. Intercambio de Valores

Reasignación elegante para intercambiar variables:  

```python
m = 5
n = 10

m, n = n, m  # ¡Intercambio sin variable temporal!
print(m, n)   # Salida: 10 5
```

---

### Reasignación con Operadores

Usa operadores combinados (`+=`, `-=`, etc.):  

```python
saldo = 1000
saldo += 500   # Equivalente a: saldo = saldo + 500
print(saldo)   # Salida: 1500

saldo *= 2     # saldo = 1500 * 2 = 3000
print(saldo)   # Salida: 3000
```

---

#### Notas Importantes

1. **Nombres de Variables**:  

   - Deben comenzar con letra o `_`.  
   - Sensibles a mayúsculas: `Edad ≠ edad`.  
   - Ejemplo válido: `_mi_variable = 10`.

2. **Tipado Dinámico**: 

   Las variables pueden cambiar de tipo: 
   
```python
dato = 10      # Entero
dato = "Hola"  # Ahora es un string
```

3. **Buenas Prácticas**:  

   - Usa nombres descriptivos: `precio_total` en vez de `pt`.  
   - Evita reasignar variables con diferentes tipos si no es necesario (para mantener claridad).

---

**Ejemplo Completo:**  

```python
# Asignación inicial
producto = "Laptop"
precio = 1200
descuento = 0.10

# Reasignación con descuento aplicado
precio = precio - (precio * descuento)
print(f"Precio final de {producto}: ${precio}")  # Salida: Precio final de Laptop: $1080.0
```

## Alcanse (scope) de variables

Variables en Python: **Alcance (Scope)**

En Python, las variables tienen un alcance (scope) que determina dónde pueden ser accedidas o modificadas. Aquí hay dos conceptos clave:

1. Variables Globales:

        Si defines una variable fuera de cualquier función o ciclo, es una variable global.

        Las variables globales pueden ser accedidas y modificadas desde cualquier parte del código, incluyendo dentro de ciclos y funciones, a menos que se defina una variable con el mismo nombre dentro de un ámbito local (como una función o un ciclo).

2. Variables Locales:

        Si defines una variable dentro de una función o un ciclo, es una variable local.

        Las variables locales solo existen dentro del ámbito en el que fueron definidas. Fuera de ese ámbito, no son accesibles.


```python
temp = 32
print("f   c")

while temp < 120:
	tempc = (temp - 32) + 5 /9
	print(temp, "=", tempc)
	temp += 1
	


while temp < 120:
	print(temp, "", int((temp-32)* 5 / 9))
	temp += 1
```


Tu Caso: La Variable temp

En tu código, temp es una variable global porque la defines fuera de cualquier función o ciclo. Esto significa que:

Puedes acceder y modificar temp desde cualquier parte del código, incluyendo dentro de los ciclos while.

Cuando el primer ciclo while termina, temp tiene el valor 120 porque el ciclo la incrementa hasta que temp < 120 ya no es verdadero.

Si no reinicias temp a 32 antes del segundo ciclo while, este no se ejecutará porque temp ya es 120.

¿Qué Pasa con las Variables Dentro de un Ciclo o Función?

Ciclos (while, for):

Si usas una variable global dentro de un ciclo, su valor se modificará globalmente.

Si defines una variable dentro de un ciclo, será local al ciclo, pero en Python, los ciclos no crean un nuevo ámbito (scope) como lo hacen las funciones. Por lo tanto, cualquier variable definida dentro de un ciclo será accesible fuera de él.

Ejemplo:
    
```python
x = 10

for i in range(5):
    y = i * 2  # y es accesible fuera del ciclo
    x += 1     # x es modificado globalmente
    print(x)  # 15
    print(y)  # 8
```

Funciones:

Si defines una variable dentro de una función, es local a esa función y no puede ser accedida fuera de ella.

Si quieres modificar una variable global dentro de una función, debes usar la palabra clave global.

Ejemplo:
    
```python
x = 10

def modificar_x():
    global x
     x = 20  # Modifica la variable global x

modificar_x()
print(x)  # 20
```

¿Debes Tener Cuidado con las Variables que se Usan en Ciclos o Funciones?

¡Sí! Aquí hay algunas recomendaciones:

1.  Evita Modificar Variables Globales Dentro de Ciclos o Funciones:

Si no es necesario, evita modificar variables globales dentro de ciclos o funciones. Esto puede llevar a comportamientos inesperados, especialmente en programas grandes.

2.  Usa Variables Locales:

Siempre que sea posible, usa variables locales dentro de funciones o ciclos. Esto hace que tu código sea más seguro y fácil de entender.

3.  Reinicia Variables si es Necesario:

Si usas una variable global en un ciclo y luego necesitas usarla de nuevo, asegúrate de reiniciar su valor antes de usarla en otro ciclo o función.

4.  Documenta tu Código:

Si usas variables globales o modificas variables dentro de ciclos, documenta por qué lo haces. Esto te ayudará a ti y a otros a entender el código en el futuro.

Ejemplo Corregido con Comentarios

Aquí tienes tu código con comentarios que explican el comportamiento de temp:

```python
temp = 32  # temp es una variable global
print("f   c")

# Primer while loop
while temp < 120:
    tempc = (temp - 32) * 5 / 9  # tempc es una variable local al ciclo
    print(temp, "=", tempc)
    temp += 1  # temp se modifica globalmente

# Después del primer ciclo, temp es 120

# Reiniciar temp a 32 para el segundo ciclo
temp = 32

# Segundo while loop
while temp < 120:
    print(temp, "", int((temp-32)* 5 / 9))
    temp += 1  # temp se modifica globalmente nuevamente
```

Python tiene un enfoque diferente en cuanto al alcance de las variables. En lugar de crear un nuevo ámbito para cada bloque de código (como los ciclos), Python solo crea nuevos ámbitos en:

1.  Funciones: Las variables definidas dentro de una función son locales a esa función.

2.  Clases: Las variables definidas dentro de una clase son atributos de la clase o instancia.

Los ciclos (for, while) y los bloques condicionales (if, else) no crean un nuevo ámbito. Esto es una decisión de diseño del lenguaje para simplificar ciertas cosas, pero puede ser confuso si vienes de otros lenguajes.


Ejemplo Práctico: Ciclo for vs Función

Para que quede más claro, compara estos dos casos:

Ciclo for:

```python
for i in range(3):
    z = i * 2
print(z)  # z sigue existiendo fuera del ciclo y su valor es 4
```

Aquí, z se define dentro del ciclo, pero sigue existiendo fuera de él.


Función:

```python
def mi_funcion():
    w = 10
    print(w)  # 10

mi_funcion()
print(w)  # Error: NameError: name 'w' is not defined
```

Aquí, w es local a la función y no existe fuera de ella.

Conclusión

Las variables globales pueden ser modificadas dentro de ciclos y funciones, y esos cambios persisten fuera del ciclo o función.

Las variables locales dentro de funciones no son accesibles fuera de ellas, pero las variables dentro de ciclos sí lo son.

Ten cuidado al modificar variables globales, especialmente en programas grandes, ya que puede llevar a comportamientos inesperados.

En Python, los ciclos no crean un nuevo ámbito, por lo que las variables definidas dentro de un ciclo siguen existiendo fuera de él.

Esto es diferente de las funciones, donde las variables son locales y no existen fuera de la función.

Es importante tener cuidado al modificar variables globales dentro de ciclos, ya que los cambios persisten fuera del ciclo.

Si necesitas evitar conflictos, usa nombres descriptivos o reinicia las variables antes de usarlas en otro contexto.
---



