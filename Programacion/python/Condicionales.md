## Estructura `match-case` 

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
