## Operadores-python


### 1. **Operadores Aritméticos**

| Operador | Ejemplo       | Resultado |
|----------|---------------|-----------|
| `+`      | `5 + 3`       | `8`       |
| `-`      | `10 - 4`      | `6`       |
| `*`      | `3 * 4`       | `12`      |
| `/`      | `10 / 3`      | `3.333`   |
| `%`      | `10 % 3`      | `1`       |
| `**`     | `2 ** 3`      | `8`       |
| `//`     | `10 // 3`     | `3`       |
| `@`      | Multiplicación de matrices (se usa en bibliotecas como NumPy) |

---

### 2. **Operadores de Asignación**

| Operador | Ejemplo       | Equivalente       |
|----------|---------------|-------------------|
| `=`      | `x = 5`       | Asignación básica |
| `+=`     | `x += 2`      | `x = x + 2`       |
| `-=`     | `x -= 3`      | `x = x - 3`       |
| `*=`     | `x *= 4`      | `x = x * 4`       |
| `/=`     | `x /= 2`      | `x = x / 2`       |
| `%=`     | `x %= 3`      | `x = x % 3`       |
| `**=`    | `x **= 2`     | `x = x ** 2`      |
| `//=`    | `x //= 3`     | `x = x // 3`      |
| `&=`     | `x &= 1`      | `x = x & 1`       |
| `|=`     | `x |= 2`      | `x = x | 2`        |
| `^=`     | `x ^= 3`      | `x = x ^ 3`       |
| `>>=`    | `x >>= 1`     | `x = x >> 1`      |
| `<<=`    | `x <<= 2`     | `x = x << 2`      |

---

### 3. **Operadores de Comparación**

| Operador | Ejemplo          | Resultado |
|----------|------------------|-----------|
| `==`     | `5 == 5`         | `True`    |
| `!=`     | `5 != 3`         | `True`    |
| `>`      | `10 > 5`         | `True`    |
| `<`      | `3 < 2`          | `False`   |
| `>=`     | `7 >= 7`         | `True`    |
| `<=`     | `5 <= 3`         | `False`   |

---

### 4. **Operadores Lógicos**

| Operador | Ejemplo                 | Resultado |
|----------|-------------------------|-----------|
| `and`    | `(5 > 3) and (2 < 4)`   | `True`    |
| `or`     | `(5 < 3) or (2 < 4)`    | `True`    |
| `not`    | `not (5 < 3)`           | `True`    |

---

### 5. **Operadores a Nivel de Bits**

| Operador       | Ejemplo       | Explicación (Binario) |
|----------------|---------------|-----------------------|
| `&` (AND)      | `5 & 3`       | `0101 & 0011 = 0001` → `1` |
| `|` (OR)       | `5 | 3`       | `0101 | 0011 = 0111` → `7` |
| `^` (XOR)     | `5 ^ 3`       | `0101 ^ 0011 = 0110` → `6` |
| `~` (NOT)     | `~5`          | Complemento a dos: `~0101 = 1010` → `-6` |
| `<<` (Shift izquierda) | `5 << 1` | `1010` → `10` |
| `>>` (Shift derecha)   | `5 >> 1` | `0010` → `2` |

---

### 6. **Operadores de Pertenencia**
| Operador   | Ejemplo                 | Resultado |
|------------|-------------------------|-----------|
| `in`       | `"a" in ["a", "b"]`     | `True`    |
| `not in`   | `3 not in [1, 2, 4]`    | `True`    |

---

### 7. **Operadores de Identidad**
| Operador   | Ejemplo                          | Resultado |
|------------|----------------------------------|-----------|
| `is`       | `a = [1, 2]; b = a; a is b`     | `True`    |
| `is not`   | `5 is not "5"`                   | `True`    |

---

### 8. **Operador Walrus (:=)**  

Asigna y retorna un valor en la misma expresión (Python 3.8+):

```python
if (n := len([1, 2, 3])) > 2:
    print(n)  # Salida: 3
```

---

### 9. **Operador Ternario**  

Expresión condicional en una línea:

```python
edad = 20
mayor = "Sí" if edad >= 18 else "No"  # Resultado: "Sí"
```

---

### 10. **Operadores para Cadenas/Secuencias**
| Operador | Ejemplo              | Resultado        |
|----------|----------------------|-----------------|
| `+`      | `"Hola" + "Mundo"`   | `"HolaMundo"`   |
| `*`      | `"Hi" * 3`           | `"HiHiHi"`      |

---

### Ejemplos de Uso en Código:


```python
# Aritméticos
print(10 // 3)  # Resultado: 3

# Pertenencia
frutas = ["manzana", "banana"]
print("pera" not in frutas)  # True

# Operadores de bits
x = 5
x <<= 1  # x = 10 (desplazamiento a la izquierda)

# Operador Walrus
while (entrada := input("Escribe 'salir': ")) != "salir":
    print("Sigue intentando...")
```

---

### Notas Importantes:

- **`is` vs `==`**:  
  `is` compara **identidad** (si son el mismo objeto en memoria), mientras que `==` compara **igualdad de valores**.
- **Operador `@`**: Usado en operaciones avanzadas como multiplicación de matrices (requiere bibliotecas externas).

## Precedencia

### Tabla de Precedencia General (de mayor a menor):

|Nombre|Simbolo|
|---|---|
|1. Paréntesis `()`|
|2. Exponente `**`|
|3. Operadores unarios |(`-x`, `+x`, `~x`)|
|4. Multiplicación/División |(`*`, `/`, `//`, `%`)|
|5. Suma/Resta |(`+`, `-`)|
|6. Desplazamiento bits |(`<<`, `>>`)|
|7. AND bit a bit |(`&`)|
|8. XOR bit a bit |(`^`)|
|9. OR bit a bit |(`|`)|
|10. Comparaciones |(`<`, `>`, `<=`, `>=`, `==`, `!=`, `is`, `in`, etc.)|
|11. NOT lógico |(`not`)|
|12. AND lógico |(`and`)|
|13. OR lógico |(`or`)|
|14. Ternario |(`if-else`)|
|15. Asignación |(`=`, `+=`, `:=`, etc.)|

### 1. Operadores Aritméticos
**Precedencia (de mayor a menor):**
1. `()` (paréntesis)
2. `**` (exponenciación)
3. `-x` (negación unaria), `+x` (positivo unario)
4. `*`, `/`, `//`, `%` (multiplicación, división, división entera, módulo)
5. `+`, `-` (suma, resta)

**Ejemplos:**
```python
# Simple
print(3 + 5 * 2)    # 13 (no 16)
print(2 ** 3 * 2)   # 16 (2^3=8 * 2)

# Complejo
valor = 10 + 2 ** 3 * (5 - 3) // 4  # 10 + 8*2//4 = 10+4=14
print(valor)
```

### 2. Operadores de Asignación
**Precedencia:** Muy baja (se evalúan al final)
`=`, `+=`, `-=`, `*=`, etc.

**Ejemplos:**
```python
# Simple
x = 5 + 3  # Primero suma, luego asigna
x *= 2 + 3 # x = x * (2+3)

# Complejo
a, b = 10, 5
a += b ** 2  # a = 10 + 25 = 35
```

### 3. Operadores de Comparación
**Precedencia:** Todos iguales (se evalúan de izquierda a derecha)
`==`, `!=`, `<`, `>`, `<=`, `>=`, `is`, `is not`, `in`, `not in`

**Ejemplos:**
```python
# Simple
print(5 + 3 < 10)  # True (8 < 10)

# Complejo (encadenamiento)
edad = 25
print(18 <= edad <= 30)  # True (18<=25 y 25<=30)
```

### 4. Operadores Lógicos
**Precedencia (de mayor a menor):**
1. `not`
2. `and`
3. `or`

**Ejemplos:**
```python
# Simple
print(not True and False)  # False

# Complejo
a, b, c = 10, 5, 7
print(a > b and (b < c or c == 7))  # True
```

### 5. Operadores a Nivel de Bits
**Precedencia (de mayor a menor):**
1. `~` (NOT)
2. `<<`, `>>` (desplazamiento)
3. `&` (AND)
4. `^` (XOR)
5. `|` (OR)

**Ejemplos:**
```python
# Simple
print(8 >> 1 + 1)  # 8 >> 2 = 2 (no 4)

# Complejo
valor = 0b1010 & 0b1100 | 0b0011  # 0b1000 | 0b0011 = 0b1011 (11)
print(bin(valor))
```

### 6. Operadores de Pertenencia
**Precedencia:** Igual que comparación
`in`, `not in`

**Ejemplos:**
```python
# Simple
print('a' in 'apple')  # True

# Complejo
lista = [1, [2,3], 4]
print(2 in lista[1])  # True
```

### 7. Operadores de Identidad
**Precedencia:** Igual que comparación
`is`, `is not`

**Ejemplos:**
```python
# Simple
a = [1,2]
b = a
print(a is b)  # True

# Complejo
print(type("hola") is str and 5 is not None)  # True
```

### 8. Operador Walrus (:=)
**Precedencia:** Mayor que lógicos, menor que aritméticos

**Ejemplos:**
```python
# Simple
if (n := len("Hola")) > 3:
    print(n)  # 4

# Complejo
while (entrada := input("Diga 'stop': ")) != "stop":
    print(entrada)
```

### 9. Operador Ternario
**Precedencia:** Muy baja (necesita paréntesis)
`x if cond else y`

**Ejemplos:**
```python
# Simple
edad = 20
status = "Mayor" if edad >= 18 else "Menor"

# Complejo
precio = 100
descuento = precio * 0.2 if precio > 50 else precio * 0.1
```

### 10. Operadores para Cadenas/Secuencias
**Precedencia:** Igual que aritméticos
`+` (concatenación), `*` (repetición)

**Ejemplos:**
```python
# Simple
print("A" + "B" * 3)  # ABBB

# Complejo
nombre = "Ana"
saludo = ("Hola " + nombre + "! ") * 2  # "Hola Ana! Hola Ana! "
```

### Tabla de Precedencia General (de mayor a menor):
1. Paréntesis `()`
2. Exponente `**`
3. Operadores unarios (`-x`, `+x`, `~x`)
4. Multiplicación/División (`*`, `/`, `//`, `%`)
5. Suma/Resta (`+`, `-`)
6. Desplazamiento bits (`<<`, `>>`)
7. AND bit a bit (`&`)
8. XOR bit a bit (`^`)
9. OR bit a bit (`|`)
10. Comparaciones (`<`, `>`, `<=`, `>=`, `==`, `!=`, `is`, `in`, etc.)
11. NOT lógico (`not`)
12. AND lógico (`and`)
13. OR lógico (`or`)
14. Ternario (`if-else`)
15. Asignación (`=`, `+=`, `:=`, etc.)

**Ejemplo final combinado:**
```python
resultado = 2 ** 3 * 4 + (5 if 10 > 5 and not False else 0)  # 8*4 +5 = 37
print(resultado)
```

