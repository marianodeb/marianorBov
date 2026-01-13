## Excepciones en Python

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

```python
try:
    dividendo = 10
    divisor = 0
    resultado = dividendo / divisor
except ZeroDivisionError as error:
    print(f"Error: {error}")  # Error: division by zero
```

#### **2. Múltiples Excepciones**

```python
try:
    lista = [1, 2, 3]
    print(lista[5])  # Índice inválido
    valor = int("abc")  # Conversión inválida
except (IndexError, ValueError) as error:
    print(f"Error detectado: {error}")
```

#### **3. Lectura de Archivo con Finally**

```python
try:
    archivo = open("datos.txt", "r")
    contenido = archivo.read()
except FileNotFoundError:
    print("Archivo no encontrado.")
else:
    print(contenido)
finally:
    archivo.close()  # Siempre se cierra el archivo
```

---

### **Lanzar Excepciones: `raise`**

Puedes **forzar** una excepción con `raise`, útil para validaciones.

```python
def calcular_edad(edad):
    if edad < 0:
        raise ValueError("La edad no puede ser negativa.")
    return edad

try:
    calcular_edad(-5)
except ValueError as e:
    print(e)  # La edad no puede ser negativa.
```

---

### **Excepciones Personalizadas**

Crea una clase heredando de `Exception` para errores específicos.

```python
class MiErrorPersonalizado(Exception):
    pass

try:
    raise MiErrorPersonalizado("¡Algo salió mal!")
except MiErrorPersonalizado as error:
    print(error)  # ¡Algo salió mal!
```

---

### **`assert`: Verificación de Condiciones**

Útil para depuración. Si la condición es `False`, lanza `AssertionError`.

```python
def dividir(a, b):
    assert b != 0, "El divisor no puede ser cero."
    return a / b

dividir(10, 0)  # AssertionError: El divisor no puede ser cero.
```

---

### **Mejores Prácticas**

1. **Especificidad**: Captura excepciones **específicas**, no uses `except` genérico.
2. **Mensajes claros**: Usa `as error` para obtener detalles del error.
3. **Recursos críticos**: Usa `finally` para liberar recursos (archivos, conexiones).
4. **Jerarquía**: Las excepciones más específicas deben ir primero.

---

### **Ejemplo Complejo: Sistema de Login**

```python
class UsuarioNoEncontrado(Exception):
    pass

class ClaveIncorrecta(Exception):
    pass

def login(usuarios, usuario, clave):
    if usuario not in usuarios:
        raise UsuarioNoEncontrado("Usuario no registrado.")
    if usuarios[usuario] != clave:
        raise ClaveIncorrecta("Clave incorrecta.")
    print("¡Bienvenido!")

# Uso
usuarios = {"Alice": "1234", "Bob": "5678"}
try:
    login(usuarios, "Alice", "0000")
except (UsuarioNoEncontrado, ClaveIncorrecta) as e:
    print(f"Error de login: {e}")
else:
    print("Login exitoso.")
finally:
    print("Fin del proceso.")
```

---

### **Resumen Final**

- **`try`/`except`**: Maneja errores de forma controlada.
- **`else`**: Para código que depende del éxito del `try`.
- **`finally`**: Limpieza de recursos.
- **`raise`**: Lanza excepciones personalizadas.
- **Jerarquía**: Captura excepciones de más específicas a generales.

---

