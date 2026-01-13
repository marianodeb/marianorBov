## Ciclo FOR


### **1. Conceptos clave**

- **Iterable**: Es cualquier objeto en Python que puede ser "recorrido" elemento por elemento.  
  *Ejemplos*: listas, tuplas, cadenas, rangos (`range`), diccionarios, etc.  
  *Funcionan porque internamente implementan el método `__iter__()`.

- **Iterar**: Es la acción de recorrer cada elemento del iterable, uno por uno.

- **Variable iterante (o variable de control)**: Es la variable temporal que toma el valor de cada elemento durante cada iteración.  
  *Ejemplo*: `i` en `for i in [1, 2, 3]`.

---

### **2. Estructura del `for`**

```python
for <variable_iterante> in <iterable>:
    # Bloque de código
```

#### **Traducción literal**  

"**Para cada elemento** (variable_iterante) **en** el iterable, ejecuta este código".

---

### **3. ¿Cómo funciona?**

1. **Paso 1**: Python obtiene un **iterador** del iterable (llama a `__iter__()`).
2. **Paso 2**: En cada ciclo, el iterador devuelve el siguiente elemento (llama a `__next__()`).
3. **Paso 3**: El valor se asigna a la variable iterante.
4. **Paso 4**: Se ejecuta el bloque de código.
5. **Paso 5**: Se repite hasta que no hay más elementos (se lanza `StopIteration`).

- **Iterable**: Colección de elementos (lista, cadena, etc.).
- **Iterar**: Recorrer cada elemento.
- **Variable iterante**: Representa el elemento actual en cada ciclo.

---

### **4. Ejemplos visuales**

#### **a. Con una lista**

```python
frutas = ["manzana", "banana", "naranja"]

for fruta in frutas:
    print(fruta)
```

- **Iterable**: `frutas` (lista).
- **Variable iterante**: `fruta`.
- **Proceso**:

  - 1ª iteración: `fruta = "manzana"` → imprime "manzana".
  - 2ª iteración: `fruta = "banana"` → imprime "banana".
  - 3ª iteración: `fruta = "naranja"` → imprime "naranja".

#### **b. Con un rango**

```python
for numero in range(3):
    print(numero)
```

- **Iterable**: `range(3)` (genera 0, 1, 2).
- **Variable iterante**: `numero`.
- **Salida**:  

```
  0
  1
  2
```

#### **c. Con una cadena**

```python
for letra in "Hola":
    print(letra)
```

- **Iterable**: `"Hola"` (cadena).
- **Variable iterante**: `letra`.
- **Salida**:  
  ```
  H
  o
  l
  a
  ```

---

### **5. Analogía con indización**

Imagina que el ciclo `for` hace esto automáticamente:

```python
lista = [10, 20, 30]
indice = 0

while indice < len(lista):
    elemento = lista[indice]
    print(elemento)
    indice += 1
```

- El `for` evita manejar índices manualmente.

---

### **6. Puntos clave**

- **No se modifica el iterable original** (a menos que lo hagas explícitamente).
- **La variable iterante** puede tener cualquier nombre (`i`, `item`, `elemento`, etc.).
- **El iterable puede ser complejo**: listas de listas, diccionarios, etc.

---

### **7. Errores comunes**

```python
# ❌ Creer que "i" son los índices
for i in ["a", "b", "c"]:
    print(i)  # Imprime "a", "b", "c" (no 0, 1, 2).

# ✅ Si necesitas índices, usa enumerate():
for indice, valor in enumerate(["a", "b", "c"]):
    print(indice, valor)  # 0 a, 1 b, 2 c
```

---

### **Resumen**

- **Iterable**: Colección de elementos (lista, cadena, etc.).
- **Iterar**: Recorrer cada elemento.
- **Variable iterante**: Representa el elemento actual en cada ciclo.

--- 

### For con funciones: ** numerate() zip() reversed() range()**


### **1. `enumerate()`: Índice + Valor**

**¿Qué hace?**  

`enumerate()` devuelve pares de valores `(índice, elemento)` de un iterable. Es perfecto cuando necesitas tanto el índice como el valor en cada iteración.

#### **Ejemplo Simple:**

```python
frutas = ["manzana", "banana", "naranja"]

# Sin enumerate (usando range(len(...))):
for i in range(len(frutas)):
    print(f"Índice: {i}, Fruta: {frutas[i]}")

# Con enumerate (más limpio y eficiente):
for indice, fruta in enumerate(frutas):
    print(f"Índice: {indice}, Fruta: {fruta}")
```

**Salida (ambos casos):**

```
Índice: 0, Fruta: manzana
Índice: 1, Fruta: banana
Índice: 2, Fruta: naranja
```

#### **Ejemplo Complejo:**

Imagina que tienes una lista de estudiantes y quieres mostrar su posición en un ranking, pero solo si su calificación es mayor a 70:

```python
estudiantes = [
    ("Ana", 85),
    ("Luis", 60),
    ("Carlos", 92),
    ("Marta", 78)
]

for posicion, (nombre, calificacion) in enumerate(estudiantes, start=1):  # start=1 para que el ranking empiece en 1
    if calificacion > 70:
        print(f"Ranking {posicion}: {nombre} - {calificacion} puntos")
```

**Salida:**

```
Ranking 1: Ana - 85 puntos
Ranking 3: Carlos - 92 puntos
Ranking 4: Marta - 78 puntos
```

**Nota:**  

- Usamos `start=1` para que el ranking comience en 1 (por defecto es 0).
- Desempaquetamos `(nombre, calificacion)` dentro de la tupla que contiene `enumerate`.

---

### **2. `zip()`: Combinar Múltiples Iterables**

**¿Qué hace?**  

`zip()` permite iterar sobre varios iterables en paralelo, emparejando elementos en tuplas. Útil para procesar datos relacionados.

#### **Ejemplo Simple:**

```python
nombres = ["Alice", "Bob", "Charlie"]
edades = [25, 30, 35]

for nombre, edad in zip(nombres, edades):
    print(f"{nombre} tiene {edad} años")
```

**Salida:**

```
Alice tiene 25 años
Bob tiene 30 años
Charlie tiene 35 años
```

#### **Ejemplo Complejo:**

Procesar datos de estudiantes (nombres, notas, cursos) y mostrar un resumen:

```python
nombres = ["Ana", "Luis", "Carlos"]
notas = [85, 60, 92]
cursos = ["Matemáticas", "Historia", "Física"]

for nombre, nota, curso in zip(nombres, notas, cursos):
    if nota >= 70:
        estado = "APROBADO"
    else:
        estado = "REPROBADO"
    print(f"{nombre} ({curso}): {nota} -> {estado}")
```

**Salida:**

```
Ana (Matemáticas): 85 -> APROBADO
Luis (Historia): 60 -> REPROBADO
Carlos (Física): 92 -> APROBADO
```

---

### **3. `reversed()`: Iterar en Orden Inverso**

**¿Qué hace?**  

`reversed()` devuelve un iterador que recorre el iterable en orden inverso.

#### **Ejemplo Simple:**

```python
numeros = [10, 20, 30, 40]

for num in reversed(numeros):
    print(num)
```

**Salida:**

```
40
30
20
10
```

#### **Ejemplo Complejo:**

Procesar una lista de tareas en orden inverso y mostrar su prioridad:

```python
tareas = ["Hacer ejercicio", "Estudiar Python", "Comprar víveres"]

for i, tarea in enumerate(reversed(tareas), start=1):
    print(f"Prioridad {i}: {tarea}")
```

**Salida:**

```
Prioridad 1: Comprar víveres
Prioridad 2: Estudiar Python
Prioridad 3: Hacer ejercicio
```

---

### **4. `range()`: Generar Secuencias Numéricas**

Ya lo conoces, pero un ejemplo avanzado:

#### **Ejemplo Complejo:**

Generar una tabla de multiplicar para números pares:

```python
numero = 2

# range(inicio, fin, paso):
for i in range(2, 21, 2):  # Números pares del 2 al 20
    print(f"{numero} x {i//2} = {i}")
```

**Salida:**

```
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
...
2 x 10 = 20
```

---

### **¿Cuándo usar cada uno?**

| **Función**    | **Uso Típico**                                                                 |
|----------------|-------------------------------------------------------------------------------|
| `enumerate()`  | Necesitas el índice y el valor (ej: rankings, procesar elementos con posición). |
| `zip()`        | Combinar datos de varias listas (ej: nombres + edades, coordenadas x/y).       |
| `reversed()`   | Iterar en orden inverso (ej: procesar eventos históricos, pilas).              |
| `range()`      | Generar secuencias numéricas (ej: bucles controlados por contador).             |

---

### **Conclusión:**

- **`enumerate()`** es clave cuando necesitas índices y valores.
- **`zip()`** es ideal para trabajar con múltiples listas relacionadas.
- **`reversed()`** y **`range()`** ofrecen control sobre el orden y la secuencia de iteración.

**¡Practica combinándolos!** Por ejemplo:

```python
# Combinando enumerate y zip:
lista1 = ["a", "b", "c"]
lista2 = [1, 2, 3]

for indice, (letra, numero) in enumerate(zip(lista1, lista2)):
    print(f"Índice: {indice}, Letra: {letra}, Número: {numero}")
```

**Salida:**

```
Índice: 0, Letra: a, Número: 1
Índice: 1, Letra: b, Número: 2
Índice: 2, Letra: c, Número: 3
```

## **1. Ciclo `for` Anidado**

### **a. Ejemplo Simple: Tabla de Multiplicar**

**Descripción**: Dos ciclos `for` anidados para generar una tabla de multiplicar básica.

```python
for i in range(1, 4):      # Ciclo externo (filas)
    for j in range(1, 4):  # Ciclo interno (columnas)
        print(f"{i} x {j} = {i * j}")
    print("-----")         # Separador
```

**Salida**:

```
1 x 1 = 1
1 x 2 = 2
1 x 3 = 3
-----
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
-----
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9
-----
```

---

### **b. Ejemplo Complejo: Procesamiento de Matriz**

**Descripción**: Calcular el promedio de cada fila y columna en una matriz.

```python
matriz = [
    [5, 3, 2],
    [8, 1, 7],
    [4, 6, 9]
]

# Promedio por fila
for fila in matriz:
    promedio = sum(fila) / len(fila)
    print(f"Promedio fila: {promedio:.1f}")

# Promedio por columna (usando índices)
for col in range(len(matriz[0])):
    suma_columna = 0
    for fila in matriz:
        suma_columna += fila[col]
    promedio = suma_columna / len(matriz)
    print(f"Promedio columna {col + 1}: {promedio:.1f}")
```

**Salida**:

```
Promedio fila: 3.3
Promedio fila: 5.3
Promedio fila: 6.3
Promedio columna 1: 5.7
Promedio columna 2: 3.3
Promedio columna 3: 6.0
```

---

### `else` en ciclos `for`

En Python, el bloque `else` **puede usarse después de un ciclo `for` o `while`**, y **solo se ejecuta si el ciclo termina normalmente**, es decir, **sin que ocurra un `break`**.

---

### ¿Cuándo se ejecuta el `else`?

- ✅ **Sí se ejecuta** si el ciclo termina sin interrupciones.
- ❌ **No se ejecuta** si el ciclo es interrumpido por un `break`.
- 🔁 **Sí se ejecuta** incluso si hubo `continue`.
- 🟡 El ciclo puede tener cero iteraciones y el `else` se ejecutará si no hay `break`.

---

### Ejemplos con `for`

#### Caso 1: El ciclo **termina normalmente** (se ejecuta el `else`)

```python
for i in range(3):
    print(i)
else:
    print("El ciclo for terminó normalmente")
```

**Salida:**

```
0
1
2
El ciclo for terminó normalmente
```

---

### Caso 2: El ciclo **se interrumpe con `break`** (no se ejecuta el `else`)

```python
for i in range(5):
    if i == 3:
        break
    print(i)
else:
    print("El ciclo for terminó normalmente")
```

**Salida:**

```
0
1
2
```

---

#### Caso útil: búsqueda en lista

```python
numeros = [1, 3, 5, 7]

for n in numeros:
    if n == 4:
        print("Número encontrado")
        break
else:
    print("Número no encontrado")
```

**Salida:**

```
Número no encontrado
```

---

### ✅ Resumen en tabla

| Ciclo      | ¿Se puede usar `else`? | ¿Cuándo se ejecuta el `else`?                  |
|------------|-------------------------|------------------------------------------------|
| `for`      | Sí                      | Si el ciclo termina sin `break`               |
| `while`    | Sí                      | Si el ciclo termina sin `break`               |

---

---

## **3. Ciclos `for` y `while` Combinados**

### **Ejemplo: Búsqueda en Lista con Reintentos**

**Descripción**: Un `while` controla reintentos, y un `for` busca elementos.

```python
productos = ["manzana", "banana", "naranja"]
busqueda_exitosa = False
reintentos = 0

while not busqueda_exitosa and reintentos < 3:
    buscado = input("Buscar producto: ").lower()
    
    for producto in productos:
        if producto == buscado:
            print(f"¡Encontrado: {producto}!")
            busqueda_exitosa = True
            break  # Termina el for
    
    if not busqueda_exitosa:
        reintentos += 1
        print("Producto no encontrado. Intenta de nuevo.")

if reintentos == 3:
    print("Límite de búsquedas alcanzado.")
```

**Salida** (ejemplo):

```
Buscar producto: pera
Producto no encontrado. Intenta de nuevo.
Buscar producto: mango
Producto no encontrado. Intenta de nuevo.
Buscar producto: banana
¡Encontrado: banana!
```

### **Resumen de ciclos y estructuras de control**

| **Estructura** | **Uso principal** |
|----------------|--------------------|
| `for` | Iterar sobre elementos de listas, cadenas, etc. |
| `while` | Repetir código mientras una condición sea verdadera. |
| `match-case` | Comparar una variable con múltiples patrones (similar a `switch`). |

---

### **Mejores prácticas**

- **`for`**: Úsalo cuando trabajes con colecciones (listas, diccionarios, etc.).
- **`while`**: Úsalo cuando dependas de una condición dinámica (ej: entrada de usuario).
- **Evita bucles infinitos**: Asegúrate de actualizar variables en el `while`.
- **`match-case`**: Ideal para simplificar múltiples condiciones `if-elif-else`.

---

- **`for` anidados**: Útiles para matrices, tablas, o datos multidimensionales.
- **`while` anidados**: Ideales para reintentos, temporizadores, o flujos complejos.
- **Combinaciones**: Usa `while` para control global y `for` para iteraciones específicas.
- **`match-case`**: Simplifica decisiones múltiples dentro de ciclos.
- **Errores comunes**: Siempre actualiza variables en `while` para evitar bucles infinitos.



