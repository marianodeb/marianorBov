

## 1. ¿Qué es un Decorador?

Un decorador es una función que recibe otra función como entrada, le añade alguna funcionalidad "envolviéndola" y devuelve una versión mejorada de la misma.

**La Regla de Oro:** Se usan para no repetir código. Si tenés 10 funciones que necesitan hacer lo mismo al principio o al final (como loguear datos o verificar permisos), usás un decorador.

---

## Ejemplos Sencillos (Nivel Semilla)

### Ejemplo 1: El Saludador (Básico)

Este decorador simplemente avisa antes de ejecutar la función.

```python
def mi_decorador(func):
    def envoltura():
        print("Antes de ejecutar la función...")
        func()
        print("Después de ejecutar la función.")
    return envoltura

@mi_decorador
def saludar():
    print("¡Hola, Huerta!")

saludar()
```

- **Explicación:** `mi_decorador` envuelve a `saludar`. El `@` hace que cuando llames a `saludar()`, en realidad estés llamando a `envoltura()`.

- **Resultado:**

```  
Antes de ejecutar la función...
¡Hola, Huerta!
Después de ejecutar la función.
```


### Ejemplo 2: El Formateador de Texto

Para poner guiones alrededor de un mensaje.

```python
def con_guiones(func):
    def wrapper():
        print("-" * 20)
        func()
        print("-" * 20)
    return wrapper

@con_guiones
def aviso():
    print("COSECHA LISTA")

aviso()
```

- **Explicación:** Útil para separar visualmente bloques en la terminal.

- **Resultado:**

```
--------------------
COSECHA LISTA
--------------------
```


### Ejemplo 3: Contador de Ejecuciones

Para saber cuántas veces se activó una función.

```python
def contador(func):
    def wrapper():
        wrapper.veces += 1
        print(f"La función se ejecutó {wrapper.veces} veces")
        return func()
    wrapper.veces = 0
    return wrapper

@contador
def regar():
    print("Regando las plantas...")

regar()
regar()
```

- **Explicación:** Agregamos una propiedad `.veces` a la envoltura para llevar la cuenta.

- **Resultado:**

```
La función se ejecutó 1 veces
Regando las plantas...
La función se ejecutó 2 veces
Regando las plantas...
```

### Ejemplo 4: Conversor a Mayúsculas

Modifica el resultado de una función que devuelve texto.


```python
def gritar(func):
    def wrapper():
        resultado = func()
        return resultado.upper()
    return wrapper

@gritar
def obtener_hortaliza():
    return "tomate cherry"

print(obtener_hortaliza())
```

- **Explicación:** Aquí el decorador captura el `return` de la función original y lo transforma.

- **Resultado:** `TOMATE CHERRY`

### Ejemplo 5: El "Simulador de Carga" (Timing)

Añade un retraso artificial (útil para pruebas).


```python
import time

def pausa(func):
    def wrapper():
        print("Procesando datos...")
        time.sleep(2) # Pausa de 2 segundos
        return func()
    return wrapper

@pausa
def guardar():
    print("Datos guardados en huerta.db")

guardar()
```

- **Explicación:** Simula una operación pesada antes de ejecutar la acción real.

---

## Ejemplos Complejos (Nivel Cosecha)

### Ejemplo 6: Decoradores con Argumentos (`*args` y `**kwargs`)

Este es vital porque permite decorar funciones que reciben parámetros (como tu función de eliminar por ID).


```python
def log_seguro(func):
    def wrapper(*args, **kwargs):
        print(f"Ejecutando {func.__name__} con datos: {args}")
        return func(*args, **kwargs)
    return wrapper

@log_seguro
def calcular_total(kilos, precio):
    return kilos * precio

print(f"Total: {calcular_total(5, 1200)}")
```

- **Explicación:** `*args` captura cualquier cantidad de argumentos. Esto permite que el decorador sirva para CUALQUIER función, tenga los parámetros que tenga.

- **Resultado:**

```
Ejecutando calcular_total con datos: (5, 1200)
 Total: 6000
```
 

### Ejemplo 7: El Validador de Datos (Tipo Flask)

Simula un control de seguridad antes de dejarte hacer algo.

```python
def solo_numeros_positivos(func):
    def wrapper(valor):
        if valor < 0:
            return "ERROR: No podés cosechar kilos negativos."
        return func(valor)
    return wrapper

@solo_numeros_positivos
def registrar_kilos(k):
    return f"Se registraron {k} kg exitosamente."

print(registrar_kilos(10))
print(registrar_kilos(-5))
```

- **Explicación:** El decorador actúa como un **filtro**. Si la condición no se cumple, ni siquiera deja que la función original se ejecute.

- **Resultado:**


```
Se registraron 10 kg exitosamente.
ERROR: No podés cosechar kilos negativos.
```
### Ejemplo 8: El Decorador con Configuración (Triple Nivel)

Este es como el `@app.route('/')`. Recibe un parámetro _dentro_ del decorador.



```python
def repetidor(veces):
    def decorador_real(func):
        def wrapper(*args, **kwargs):
            for _ in range(veces):
                func(*args, **kwargs)
        return wrapper
    return decorador_real

@repetidor(veces=3)
def alarma():
    print("¡Revisar la humedad!")

alarma()
```

- **Explicación:** Es una función que devuelve un decorador, que a su vez devuelve una envoltura. Es el nivel máximo de flexibilidad. Así es como Flask sabe que vos pusiste `/` o `/consultas`.
    
- **Resultado:**
    


```
¡Revisar la humedad!
¡Revisar la humedad!
¡Revisar la humedad!
```


---

- **Palabra clave:** El decorador **envuelve** (wrap).

- **Uso en Flask:** No los inventamos nosotros, usamos los que Flask ya hizo (`@app.route`) para conectar la URL con el código Python.

- **Orden:** Si ponés varios decoradores, se ejecutan de arriba hacia abajo (el de más arriba envuelve a todos los demás).

---
## Parámetros vs. Argumentos

### 1. Definiciones Técnicas

- **Parámetro:** Es la **variable** que definís en la declaración de la función. Es el "hueco" o "contenedor" que espera recibir un dato. Vive dentro de la definición de la función (`def`).

- **Argumento:** Es el **valor real** (el dato) que le enviás a la función cuando la llamás (la ejecutás). Es lo que llena el hueco.

### 2. La Analogía del Formulario

Imagina que estás diseñando un formulario de papel para un trámite:

- **El Parámetro:** Es la etiqueta que dice **"Nombre: __________"**. El espacio vacío está diseñado para recibir algo, pero todavía no tiene contenido.

- **El Argumento:** Es lo que el usuario escribe con la birome: **"Juan"**. Es el dato concreto que viaja al sistema.


> **Otra analogía rápida:** El Parámetro es el **Estacionamiento** (el lugar reservado). El Argumento es el **Auto** (lo que ocupa ese lugar).

### 3. Explicación Visual del Flujo

Cuando llamás a una función, Python hace una **asignación automática**:

`Parámetro = Argumento`

### 4. Ejemplos Prácticos

#### Ejemplo 1: El básico de cocina


```python
# 'ingrediente' es el PARÁMETRO (el hueco)
def preparar_ensalada(ingrediente):
    print(f"Picando {ingrediente}...")

# "Tomate" es el ARGUMENTO (el valor real)
preparar_ensalada("Tomate") 
```

#### Ejemplo 2: Múltiples datos

```python
# 'hortaliza' y 'gramos' son PARÁMETROS
def registrar_cosecha(hortaliza, gramos):
    kilos = gramos / 1000
    print(f"Cosechaste {kilos}kg de {hortaliza}")

# "Lechuga" y 2500 son los ARGUMENTOS
registrar_cosecha("Lechuga", 2500)
```

#### Ejemplo 3: Argumentos por nombre (Keyword Arguments)

Python te permite ser muy específico para no confundirte el orden.


```python
def configurar_riego(zona, duracion_minutos):
    print(f"Regando {zona} por {duracion_minutos} min.")

# Aquí pasamos los argumentos aclarando a qué parámetro van
configurar_riego(duracion_minutos=15, zona="Huerta Norte")
```

### 5. ¿Por qué es importante esto para tu App de Flask?

En tu archivo `app.py`, esto se ve todo el tiempo. Mirá esta función que hicimos:

```python
@app.route('/eliminar/<int:id>')
def eliminar(id): # <--- 'id' es el PARÁMETRO
    ...
```

Cuando vos en el navegador hacés clic en el botón de borrar de la fila 5, Flask llama a la función así: `eliminar(5)`.

- El **5** es el **Argumento**.

- Ese **5** entra en el parámetro **id** para que la base de datos sepa exactamente qué fila borrar.

### Resumen para tus notas:

- **Parámetro:** El nombre en la receta (`def`).

- **Argumento:** El ingrediente real que tirás a la olla (`llamada`).
