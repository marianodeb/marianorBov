## Ciclo WHILE

### **1. Conceptos clave**

- **Condición**: Expresión booleana que se evalúa al inicio de cada iteración.
- **Cuerpo del ciclo**: Bloque de código que se ejecuta **mientras** la condición sea `True`.
- **Actualización de variables**: Debes modificar las variables involucradas en la condición para evitar bucles infinitos.

---

### **2. Estructura del `while`**

```python
while <condición>:
    # Bloque de código (cuerpo del ciclo)
```

#### **Traducción literal**  

"Mientras la **condición** sea verdadera, ejecuta este código".

---

### **3. ¿Cómo funciona?**

1. **Paso 1**: Evalúa la condición.
   - Si es `True` → Ejecuta el bloque de código.
   - Si es `False` → Sale del ciclo.
2. **Paso 2**: Repite el paso 1 hasta que la condición sea `False`.

---

### **4. Ejemplos visuales**

#### **a. Contador básico**

```python
contador = 0

while contador < 5:
    print(f"Contador: {contador}")
    contador += 1  # Actualización clave
```

- **Salida**:

```
  Contador: 0
  Contador: 1
  Contador: 2
  Contador: 3
  Contador: 4
```

#### **b. Validación de entrada**

```python
respuesta = ""

while respuesta != "salir":
    respuesta = input("Escribe 'salir' para terminar: ").lower()
    print("Respuesta recibida:", respuesta)
```

- El ciclo se repite hasta que el usuario escribe "salir".

---

### **5. Diferencias clave entre `for` y `while`**

| **`for`** | **`while`** |
|-----------|-------------|
| Se usa cuando **sabemos cuántas veces** se ejecutará el ciclo. | Se usa cuando **no conocemos** de antemano cuántas veces se ejecutará. |
| Itera sobre elementos de un iterable. | Depende de una condición booleana. |
| Más seguro (evita bucles infinitos fácilmente). | Riesgo de bucles infinitos si no se actualiza la condición. |

---

### **6. Errores comunes**

#### **a. Bucle infinito**

```python
# ❌ Nunca termina (contador no se actualiza)
contador = 0
while contador < 5:
    print("¡Atrapado!")
```

#### **b. Condición siempre verdadera**

```python
# ❌ "True" nunca cambia (necesitas un 'break')
while True:
    print("Bucle infinito...")
```

---

### **7. Control adicional: `break` y `continue`**

- **`break`**: Termina el ciclo inmediatamente.
- **`continue`**: Salta a la siguiente iteración.

#### **Ejemplo con `break`:**

```python
while True:
    respuesta = input("Escribe 'salir': ")
    if respuesta == "salir":
        break  # Sale del ciclo
    print("Seguimos...")
```

#### **Ejemplo con `continue`:**

```python
numero = 0

while numero < 5:
    numero += 1
    if numero == 3:
        continue  # Salta la iteración actual
    print(numero)
```

- **Salida**: `1 2 4 5` (el 3 se omite).

---

## **Estructura `match-case` (Python 3.10+)**

Python no tiene un `switch-case` tradicional, pero desde la versión 3.10 introdujo `match-case`, similar a un `switch` en otros lenguajes.

### **1. Estructura**

```python
match <variable>:
    case <patrón_1>:
        # Código
    case <patrón_2>:
        # Código
    case _:  # Default
        # Código
```

### **2. Ejemplo**

```python
dia = "martes"

match dia:
    case "lunes":
        print("Inicio de semana")
    case "viernes":
        print("¡Fin de semana!")
    case _:
        print("Día normal")
```

- **Salida**: `Día normal`.

---

### **¿Existen otros ciclos en Python?**

No. Python solo tiene:

1. **`for`**: Para iterar sobre elementos conocidos.
2. **`while`**: Para ejecutar bajo una condición.

Pero se pueden emular otros comportamientos:

### **`do-while` (no existe en Python)**

En otros lenguajes, el `do-while` ejecuta el cuerpo **al menos una vez**. En Python, se puede emular así:

```python
while True:
    # Cuerpo del ciclo (se ejecuta al menos una vez)
    respuesta = input("Escribe 'salir': ")
    if respuesta == "salir":
        break
```

---

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

### **Ejemplo integrador: Menú interactivo**

```python
while True:
    print("\n1. Saludar\n2. Despedir\n3. Salir")
    opcion = input("Elige una opción: ")

    match opcion:
        case "1":
            print("¡Hola! 😊")
        case "2":
            print("Adiós 👋")
        case "3":
            break
        case _:
            print("Opción inválida")
```
---

## **2. Ciclo `while` Anidado**

### **a. Ejemplo Simple: Contador con Retardo**

**Descripción**: Un `while` externo controla intentos, y uno interno simula un retardo.

```python
intentos = 0
max_intentos = 2

while intentos < max_intentos:
    print(f"Intento {intentos + 1}")
    segundos = 3
    while segundos > 0:  # Retardo de 3 segundos
        print(f"  Esperando... {segundos}")
        segundos -= 1
    intentos += 1
```

**Salida**:

```
Intento 1
  Esperando... 3
  Esperando... 2
  Esperando... 1
Intento 2
  Esperando... 3
  Esperando... 2
  Esperando... 1
```

---

### **b. Ejemplo Complejo: Juego de Adivinanza con Límites**

**Descripción**: Un juego donde el usuario debe adivinar un número, con pistas y límite de intentos.

```python
import random

numero_secreto = random.randint(1, 20)
intentos = 0
max_intentos = 3

while intentos < max_intentos:
    intentos += 1
    print(f"Intento {intentos}/{max_intentos}")
    guess = int(input("Adivina el número (1-20): "))
    
    if guess == numero_secreto:
        print("¡Correcto! 🎉")
        break
    else:
        # Pista: Mayor o menor
        if guess < numero_secreto:
            print("El número es mayor.")
        else:
            print("El número es menor.")
        
        # Ciclo interno para mostrar "pistas visuales"
        pistas = 0
        while pistas < abs(numero_secreto - guess):
            print("*", end="")
            pistas += 1
        print("\n")

if intentos == max_intentos:
    print(f"¡Perdiste! El número era {numero_secreto}.")
```

**Salida** (ejemplo):

```
Intento 1/3
Adivina el número (1-20): 10
El número es mayor.
**********

Intento 2/3
Adivina el número (1-20): 15
El número es menor.
*****

Intento 3/3
Adivina el número (1-20): 12
¡Correcto! 🎉
```

### `else` en ciclos `while` 

En Python, el bloque `else` **puede usarse después de un ciclo `for` o `while`**, y **solo se ejecuta si el ciclo termina normalmente**, es decir, **sin que ocurra un `break`**.

---

### ¿Cuándo se ejecuta el `else`?

- ✅ **Sí se ejecuta** si el ciclo termina sin interrupciones.
- ❌ **No se ejecuta** si el ciclo es interrumpido por un `break`.
- 🔁 **Sí se ejecuta** incluso si hubo `continue`.
- 🟡 El ciclo puede tener cero iteraciones y el `else` se ejecutará si no hay `break`.

---

### Ejemplos con `while`

#### Caso 1: `while` termina normalmente

```python
x = 0
while x < 3:
    print(x)
    x += 1
else:
    print("El ciclo while terminó normalmente")
```

**Salida:**

```
0
1
2
El ciclo while terminó normalmente
```

---

### Caso 2: `while` se interrumpe con `break`

```python
x = 0
while x < 5:
    if x == 2:
        break
    print(x)
    x += 1
else:
    print("El ciclo while terminó normalmente")
```

**Salida:**

```
0
1
```
---

### ✅ Resumen en tabla

| Ciclo      | ¿Se puede usar `else`? | ¿Cuándo se ejecuta el `else`?                  |
|------------|-------------------------|------------------------------------------------|
| `for`      | Sí                      | Si el ciclo termina sin `break`               |
| `while`    | Sí                      | Si el ciclo termina sin `break`               |

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
---

### **4. `match-case` dentro de un `while` (Python 3.10+)**

### **Ejemplo: Sistema de Comandos con Menú**

**Descripción**: Un menú interactivo que usa `while` para ejecutarse y `match-case` para gestionar opciones.

```python
while True:
    print("\n--- Menú ---")
    print("1. Ver hora")
    print("2. Calcular 2+2")
    print("3. Salir")
    
    opcion = input("Elige una opción: ")
    
    match opcion:
        case "1":
            from datetime import datetime
            print(f"Hora actual: {datetime.now().strftime('%H:%M:%S')}")
        case "2":
            print("2 + 2 = 4")
        case "3":
            print("Saliendo...")
            break
        case _:
            print("Opción inválida. Usa 1, 2 o 3.")
```

**Salida** (ejemplo):

```
--- Menú ---
1. Ver hora
2. Calcular 2+2
3. Salir
Elige una opción: 1
Hora actual: 14:30:45

--- Menú ---
1. Ver hora
2. Calcular 2+2
3. Salir
Elige una opción: 3
Saliendo...
```

---

## **5. Emulación de `do-while` en Python**

### **Ejemplo: Validación de Entrada con Ejecución Inicial**

**Descripción**: Ejecutar código al menos una vez, aunque la condición sea falsa.

```python
while True:
    numero = int(input("Ingresa un número entre 1 y 10: "))
    
    if 1 <= numero <= 10:
        print("Número válido ✅")
        break
    else:
        print("Inválido. Intenta de nuevo.")
```

**Salida** (ejemplo):

```
Ingresa un número entre 1 y 10: 15
Inválido. Intenta de nuevo.
Ingresa un número entre 1 y 10: 7
Número válido ✅
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



