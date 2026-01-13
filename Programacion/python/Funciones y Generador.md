## Funciones 

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

---

### Ejemplos básicos con `return`  

### 1. Suma de lista  

```python
def sumar_lista(lista):
    total = 0
    for num in lista:
        total += num
    return total

print(sumar_lista([1, 2, 3, 4]))  # Salida: 10
```

Este ejemplo acumula valores en `total` y lo devuelve al terminar.  

### 2. Factorial (recursivo)  

```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

print(factorial(5))  # Salida: 120
```

Aquí cada llamada usa `return` para enviar el resultado recursivo y finalizar la función actual.  

---

### Ejemplos básicos con `yield`  

### 1. Contar hasta n  

```python
def contar_hasta(n):
    i = 1
    while i <= n:
        yield i
        i += 1

for número in contar_hasta(3):
    print(número)
# Salida: 1 2 3
```

Cada `yield` produce un valor y pausa la función, sin cargar toda la secuencia en memoria.  

### 2. Factoriales intermedios 
 
```python
def factoriales(n):
    resultado = 1
    for i in range(1, n + 1):
        resultado *= i
        yield resultado

print(list(factoriales(4)))  # Salida: [1, 2, 6, 24]
```

Útil cuando necesitas cada paso del cálculo sin calcularlo todo de antemano.  

### 3. Pipeline de transformación  

```python
def leer_lineas(archivo):
    with open(archivo) as f:
        for linea in f:
            yield linea.strip()

def filtrar_vacias(lineas):
    for linea in lineas:
        if linea:
            yield linea

def a_mayusculas(lineas):
    for linea in lineas:
        yield linea.upper()

# Uso:
for linea in a_mayusculas(filtrar_vacias(leer_lineas('datos.txt'))):
    print(linea)
```

Cada generador procesa elemento a elemento, facilitando la construcción de pipelines sin cargar todo en memoria.  

---

### Uso de `return` y `yield`

En Python, las instrucciones `return` y `yield` se usan para devolver valores desde una función, pero su comportamiento y uso son muy distintos. Mientras que `return` finaliza por completo la ejecución de la función y envía de una sola vez un valor (o `None` si no se especifica), `yield` convierte la función en un **generador** que produce una secuencia de valores **perezosamente**, pausando y reanudando su estado interno en cada llamada, lo que resulta en un uso más eficiente de la memoria y en la capacidad de manejar flujos de datos potencialmente infinitos. A continuación veremos una comparación detallada, ejemplos sencillos y un ejemplo más complejo que ilustra las ventajas de los generadores.

¿Qué hace `return`?  
La instrucción `return` termina la ejecución de la función y devuelve un **único** valor al llamador; después de un `return`, la función no sigue ejecutándose bajo ninguna circunstancia.  

```python
def cuadrado(n):
    return n * n
    # Código aquí nunca se ejecuta
```

- Si no se especifica valor, retorna `None`.  
- No mantiene estado interno entre invocaciones: cada llamada es independiente.  

####  ¿Qué hace `yield`?  

El uso de `yield` en lugar de `return` convierte la función en un **generador**, que al invocarse no ejecuta el cuerpo completo, sino que devuelve un **objeto generador** que produce valores bajo demanda citeturn0search5. 
 
- Al llegar a `yield`, la función **pausa** su ejecución, **preserva** todas sus variables locales y el punto de ejecución citeturn1search1.  
- La siguiente llamada a `next()` (o iteración en un `for`) **reanuda** justo después del `yield`, hasta el siguiente `yield` o hasta que termine la función.  
- Cuando el generador agota sus `yield`, lanza `StopIteration`.  

### Comparación directa  

| Característica        | `return`                                | `yield` (generador)                                                                             |
| --------------------- | --------------------------------------- | ----------------------------------------------------------------------------------------------- |
| Estado tras devolver  | Destruye el contexto de la función      | Conserva variables locales y posición de ejecución citeturn1search1                          |
| Cantidad de valores   | Uno solo                                | Múltiples, uno por cada `yield` citeturn0search2                                             |
| Uso de memoria        | Carga todo en memoria si devuelve lista | Pares de “valor–pausa”, ideal para grandes flujos citeturn0search9                           |
| Finalización          | Inmediata al `return`                   | Al terminar el cuerpo o al lanzar `return` sin valor dentro de un generador citeturn1search1 |
| Protocolo de iterador | No                                      | Sí; implementa `__iter__()` y `__next__()` automáticamente citeturn1search0                  |

### Ejemplos sencillos  

#### Ejemplo 1: secuencia de números  

```python
def contar_hasta(n):
    i = 1
    while i <= n:
        yield i
        i += 1

for num in contar_hasta(3):
    print(num)
# Salida: 1 2 3
```

- Cada `yield` pausa la función tras devolver `i` citeturn0search2.

### Ejemplo 2: factorial iterativo vs generador  
**Con `return`:**  

```python
def factorial(n):
    resultado = 1
    for i in range(1, n+1):
        resultado *= i
    return resultado
```

**Con `yield`:** (devuelve factoriales intermedios)
  
```python
def factoriales(n):
    resultado = 1
    for i in range(1, n+1):
        resultado *= i
        yield resultado

for val in factoriales(4):
    print(val)
# Salida: 1 2 6 24
```

- Útil cuando necesitamos cada paso del cálculo, sin calcular todo de antemano citeturn0search6.

### Ejemplo 3: “pipeline” simple de transformación  

```python
def leer_lineas(archivo):
    with open(archivo) as f:
        for linea in f:
            yield linea.strip()

def filtrar_vacias(lineas):
    for linea in lineas:
        if linea:
            yield linea

def en_mayusculas(lineas):
    for linea in lineas:
        yield linea.upper()

# Uso:
for linea in en_mayusculas(filtrar_vacias(leer_lineas('datos.txt'))):
    print(linea)
```

- Cada generador procesa línea a línea, sin cargar todo el archivo en memoria citeturn0search1.

### Ejemplo más complejo: coroutine con `send()` y `close()` 
 
Los generadores también pueden **recibir** datos y controlar excepciones internamente:
  
```python
def acumulador():
    total = 0
    try:
        while True:
            x = yield total
            total += x
    except GeneratorExit:
        print(f"Finalizado con total={total}")

gen = acumulador()
print(next(gen))     # Inicia el generador, imprime 0
print(gen.send(5))   # Envía 5, imprime 5
print(gen.send(10))  # Envía 10, imprime 15
gen.close()          # Llama a GeneratorExit, imprime mensaje de finalización
```

- `yield` devuelve `total` y recibe el valor enviado por `send()` como resultado de la expresión `yield` citeturn0search3turn0search13.  
- `close()` dispara `GeneratorExit`, permitiendo limpieza en bloque `finally` o capturar la excepción citeturn0search13.  

### Conclusión  

- Usa **`return`** cuando tu función deba devolver **un único valor** y finalizar inmediatamente.  
- Usa **`yield`** para convertir tu función en un **generador**, ideal para **secuencias** de datos, **procesamiento en pipeline** y **uso eficiente de memoria** en flujos grandes o infinitos.  
- Los generadores ofrecen además capacidades avanzadas de **comunicación bidireccional** (`send`, `throw`, `close`) y de **delegación** (`yield from`) para componer flujos complejos de manera elegante.

