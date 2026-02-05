

##  [[Variables]]

- Asignación de Variables

- Reasignación de Variables

- Casos Especiales de Asignación

1. Asignación Múltiple 

2. Asignación en Cadena


3. Intercambio de Valores


4. Reasignación con Operadores

### [[Variables#Alcanse (scope) de variables]]

---

## [[Operadores-python]]

1. **Operadores Aritméticos**

2. **Operadores de Asignación**

3. **Operadores de Comparación**

4. **Operadores Lógicos**

5. **Operadores a Nivel de Bits**

6. **Operadores de Pertenencia**

7. **Operadores de Identidad**

8. **Operador Walrus (:=)**  

9. **Operador Ternario**  

10. **Operadores para Cadenas/Secuencias**

## [[Formateo]]

### **`Formateo de strings en Python: +, ",", f-strings, .format()`**  

1. **Concatenación con `+`**  

2. **Concatenación con `,` en `print()`**

3. **Formateo con `.format()`**

4. **f-strings (Python 3.6+)**

**5. f-strings avanzadas: Self-Documenting Expressions (Python 3.8+)**

**a. Incluir expresiones dentro de `{}`**  

**b. Alineación de texto/números**

**c. Formateo de fechas** 
 
**d. Usar `!r`, `!s`, `!a` para conversiones**  

1. **Formato básico de decimales**

2. **Separación de miles con comas**

3. **Formato de porcentaje**

4. **Combinación de formatos (decimales + comas)**

5. **Formato dinámico usando variables**

6. **Manejo de multilínea**

7. **Otros formatos útiles**

**Alineación de texto/números**

**Formato científico**

**Relleno con ceros**

**Formato hexadecimal/binario**

**Formato de fechas**

8. **Formateo condicional**

9. **Truncamiento de cadenas**


---
## [[Python String Methods]]

---

## [[Python Built in Functions]]

---


## [[Listas]]

Una lista en Python es una estructura de datos ordenada y mutable que permite almacenar elementos de diferentes tipos (enteros, strings, otras listas, etc.). Es una de las estructuras más versátiles y utilizadas.

Sintaxis

Se crean con corchetes [] y los elementos se separan por comas.

```python
# Lista vacía
lista_vacia = []

# Lista con elementos
numeros = [1, 2, 3, 4]
mezcla = [10, "hola", True, [5, 6]]
```

Temas:

- Mutabilidad
- Clonación
- List Comprehension
- Side Effects (Efectos Secundarios)
- Desempaquetado Extendido con Asterisco (*)
---
## [[Tuplas]]


---

## [[Diccionarios]]


---

## [[Sets Conjuntos]]


---

## [[Condicionales]]


---

## [[Ciclo FOR]]


### Conceptos clave

- **Iterable**: Es cualquier objeto en Python que puede ser "recorrido" elemento por elemento.  
  *Ejemplos*: listas, tuplas, cadenas, rangos (`range`), diccionarios, etc.  
  *Funcionan porque internamente implementan el método `__iter__()`.

- **Iterar**: Es la acción de recorrer cada elemento del iterable, uno por uno.

- **Variable iterante (o variable de control)**: Es la variable temporal que toma el valor de cada elemento durante cada iteración.  
  *Ejemplo*: `i` en `for i in [1, 2, 3]`.

---

### **Estructura del `for`**

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

### For con funciones: ** numerate() zip() reversed() range()**

### **1. `enumerate()`: Índice + Valor**

### **2. `zip()`: Combinar Múltiples Iterables**

### **3. `reversed()`: Iterar en Orden Inverso**

### **4. `range()`: Generar Secuencias Numéricas**

---

## [[Ciclo WHILE]] 

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


## **5. Emulación de `do-while` en Python**


### `else` en ciclos `for` y `while` en Python



### Ejemplos con `for`


### Ejemplos con `while`


## [[Funciones y Generador]]

En Python, las funciones se definen con la palabra clave `def`, aceptan cero o más parámetros y pueden devolver un valor mediante `return` o producir una secuencia de valores de forma perezosa con `yield`.  

- `return` finaliza inmediatamente la función y envía un valor al llamador.  
- `yield` convierte la función en un generador que produce valores uno a uno, pausando su estado interno entre cada emisión.  


### Sintaxis de definición de funciones  

```python
def nombre_funcion(param1, param2=valor_por_defecto, *args, **kwargs):
    """Docstring opcional que describe lo que hace la función."""
    # cuerpo de la función
    return resultado
```

- Se inicia con `def`, seguido del nombre, paréntesis con parámetros opcionales y dos puntos.  
- El cuerpo va indentado (normalmente 4 espacios) bajo la definición.  
- Opcionalmente incluye un docstring entre triple comillas.  

### Parámetros y argumentos  

- **Parámetros posicionales**: recibidos según su orden.  
- **Parámetros con valor por defecto**: tienen un valor si no se especifica.  
- **`*args`**: tupla con argumentos extra posicionales.  
- **`**kwargs`**: diccionario con argumentos extra nombrados.  

---

### Sintaxis de `return` 
 
```python
def ejemplo_return(x, y):
    resultado = x + y
    return resultado
```

- `return <expresión>` devuelve un único valor y termina la ejecución de la función.  
- Si se omite la expresión, retorna `None`.  
- Cualquier código tras un `return` no se ejecuta.  

---
## Generador

### Sintaxis de `yield`  

```python
def ejemplo_yield(n):
    for i in range(n):
        yield i
```

- Al usar `yield`, la función pasa a ser un **generador** en lugar de una función normal.  
- Cada vez que iteras (p. ej. con `next()` o un bucle `for`), la función se reanuda justo después del `yield` hasta el siguiente `yield` o el fin de la función.  

### 3. Pipeline de transformación  

### Ejemplo más complejo: coroutine con `send()` y `close()` 
 
Los generadores también pueden **recibir** datos y controlar excepciones internamente:

---

## [[Excepciones]] 

#### **¿Qué es una excepción?**

Una **excepción** es un error que ocurre durante la ejecución de un programa, interrumpiendo su flujo normal. Por ejemplo, dividir por cero, acceder a un índice inexistente en una lista, o abrir un archivo que no existe.

**Analogía**: Imagina que estás cocinando y sigues una receta. Si falta un ingrediente esencial (como la harina), se produce un "error" y debes manejar la situación (usar un sustituto o cancelar la receta). Las excepciones son como esos imprevistos que debes anticipar y manejar.

---

### **Sintaxis Básica: `try` - `except`**

El bloque `try` permite **probar** un código que podría generar una excepción. Si ocurre un error, el bloque `except` lo **captura** y maneja.

```python
try:
    # Código que podría generar una excepción
    resultado = 10 / 0
except ZeroDivisionError:
    # Manejo de la excepción
    print("¡No puedes dividir por cero!")
```

---

### **Partes de un Bloque de Excepciones**

1. **`try`**: Contiene el código a probar.
2. **`except`**: Maneja la excepción si ocurre.
3. **`else`**: Se ejecuta si **no hubo excepciones**.
4. **`finally`**: Siempre se ejecuta, haya o no excepciones.

```python
try:
    numero = int(input("Ingresa un número: "))
except ValueError:
    print("¡Eso no es un número válido!")
else:
    print(f"El cuadrado es: {numero ** 2}")
finally:
    print("Proceso finalizado.")
```

---

### **Tipos Comunes de Excepciones**

- **`ValueError`**: Valor inapropiado (ej: convertir texto a número).
- **`IndexError`**: Índice fuera de rango en una lista.
- **`KeyError`**: Clave no encontrada en un diccionario.
- **`FileNotFoundError`**: Archivo no encontrado.
- **`TypeError`**: Operación con tipo incorrecto.

---

### **Ejemplos Detallados**

#### **1. Ejemplo Simple: División por Cero**

#### **2. Múltiples Excepciones**

#### **3. Lectura de Archivo con Finally**

### **Lanzar Excepciones: `raise`**

### **Excepciones Personalizadas**

Crea una clase heredando de `Exception` para errores específicos.

### **`assert`: Verificación de Condiciones**

Útil para depuración. Si la condición es `False`, lanza `AssertionError`.

---

## [[Decoradores]]

---

## [[POO]]

### **Definición de POO**  

Es un **paradigma de programación** que organiza el código en estructuras llamadas **"objetos"**, los cuales representan entidades del mundo real. Estos objetos contienen:  

- **Propiedades** (datos o características).  
- **Métodos** (acciones o comportamientos).  

La POO se basa en cuatro pilares:  

1. **Encapsulamiento**: Proteger los datos internos de un objeto, exponiendo solo lo necesario.  
2. **Herencia**: Reutilizar y extender funcionalidades de clases existentes.  
3. **Polimorfismo**: Permitir que objetos de diferentes clases respondan de forma única a un mismo mensaje.  
4. **Abstracción**: Simplificar la complejidad ocultando detalles irrelevantes.  

---

### **1. Clase**  

**Definición:** Es una plantilla que define la estructura (propiedades) y comportamiento (métodos) común para todos los objetos creados a partir de ella.  


### **2. Objeto**  

**Definición:** Es una instancia concreta de una clase. Tiene valores únicos para sus propiedades.  

### **3. Modularización**  

**Definición:** Dividir un programa en partes más pequeñas (módulos/clases) para facilitar el mantenimiento.  

### **4. Encapsulamiento**  

**Definición:** Restringir el acceso directo a ciertos datos o métodos (usando `_` o `__` en Python).  

### **5. Herencia**  

**Definición:** Una clase (hija) puede heredar propiedades y métodos de otra clase (padre).  

### **6. Polimorfismo**  

**Definición:** Métodos con el mismo nombre pero comportamientos diferentes en clases distintas.  

### **7. Métodos**  

**Definición:** Funciones definidas dentro de una clase que describen su comportamiento.  

### **8. Propiedades/Atributos**  

**Definición:** Variables que almacenan el estado de un objeto.  

### **9. Mensajes**  

**Definición:** Comunicación entre objetos mediante la invocación de métodos.  

### **10. Constructor (`__init__`)**  

**Definición:** Método especial que se ejecuta al crear un objeto para inicializar sus atributos.  

---

## [[modulosPython]]

Un módulo es un archivo de Python cuyos objetos (funciones, clases, excepciones, etc.)  pueden ser accedidos desde otro archivo. Se trata simplemente de una forma de organizar grandes códigos.

---

## [[EntornoVirtualesPython]]

---












