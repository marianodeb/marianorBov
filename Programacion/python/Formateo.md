## Formateo 

### **`Formateo de strings en Python: +, ",", f-strings, .format()`**  

#### 1. **Concatenación con `+`**  

- **Funciona solo entre strings**: Si intentas concatenar un string con un número, genera un error.  
- **Ejemplo simple**:  
   
```python
nombre = "Luis"  
saludo = "Hola " + nombre  # Correcto: "Hola Luis"  
```

- **Ejemplo complejo (error)**:  
```python  
edad = 30  
mensaje = "Tienes " + edad + " años"  # Error: TypeError (int + str)  
```

- **Solución**: Convertir números a string con `str()`:

```python
mensaje = "Tienes " + str(edad) + " años"  # Correcto: "Tienes 30 años"  
```

---

#### 2. **Concatenación con `,` en `print()`**

- **Ejemplo simple**:
```python  
print("Nombre:", "Ana", "| Edad:", 25)  # Salida: "Nombre: Ana | Edad: 25"  
```

- **Ejemplo complejo**: 
    
```python  
producto = "teclado"  
precio = 49.99  
print("Producto:", producto, "| Precio:", precio, "| Stock:", 10)  
# Salida: "Producto: teclado | Precio: 49.99 | Stock: 10"  
```

---

#### 3. **Formateo con `.format()`**
 
- **Ejemplo simple**:
   
```python  
mensaje = "Bienvenido, {}".format("María")  # "Bienvenido, María"  
```
     
- **Ejemplo complejo** (múltiples variables y formato numérico):
```python  
nombre = "Carlos"  
promedio = 95.6789  
texto = "Alumno: {} | Promedio: {:.2f}%".format(nombre, promedio)  
# Resultado: "Alumno: Carlos | Promedio: 95.68%"  
```

---

#### 4. **f-strings (Python 3.6+)**

- **Ejemplo simple**:

```python  
ciudad = "Madrid"  
print(f"Vives en {ciudad}")  # "Vives en Madrid"  
```

- **Ejemplo complejo** (operaciones y funciones dentro del string):

```python
horas_trabajadas = 8  
tarifa = 20  
total = f"Salario: ${horas_trabajadas * tarifa} | IVA: ${horas_trabajadas * tarifa * 0.16:.2f}"  
# Resultado: "Salario: $160 | IVA: $25.60"  
```

---


### **5. f-strings avanzadas: Self-Documenting Expressions (Python 3.8+)**

Una característica poderosa de las f-strings es la capacidad de **mostrar automáticamente el nombre de la variable y su valor** usando `=`, lo que simplifica la depuración y reduce redundancia.  

#### **Ejemplo básico**:

```python  
y = 10  
x = 30  
print(f"{y=} | {x=} | {x + y=}")  
```
**Salida**:

`y=10 | x=30 | x + y=40`  

#### **Ejemplo complejo** (combinado con formateo numérico):

```python  
temperatura = 25.5  
humedad = 0.75  
print(f"{temperatura=:.1f}°C | {humedad=:.0%}")  
```

**Salida**:
  
`temperatura=25.5°C | humedad=75%`  

---

### **Más tips avanzados con f-strings**:  

#### **a. Incluir expresiones dentro de `{}`**  


```python  

# Simple:  

print(f"Total: {5 * 10}")  # Salida: "Total: 50"  

# Complejo:  
precio = 99.99  
descuento = 0.2  
print(f"Pagar: ${precio * (1 - descuento):.2f}")  # Salida: "Pagar: $79.99"  
```

#### **b. Alineación de texto/números**

```python
# Simple:  
nombre = "Ana"  
print(f"{nombre:>10}")  # Alineado a la derecha (10 caracteres de espacio).  

# Complejo:  
productos = [("Manzana", 2.5), ("Banana", 1.8)]  
for nombre, precio in productos:  
    print(f"{nombre:<15} ${precio:>5.2f}")  # Nombre a la izquierda, precio a la derecha.  
```  
**Salida**:

```python
Manzana          $ 2.50  
Banana           $ 1.80  
```

#### **c. Formateo de fechas** 
 
```python  
from datetime import datetime  
fecha = datetime.now()  
print(f"{fecha:%d/%m/%Y %H:%M}")  # Salida: "15/07/2024 14:30" (ejemplo).  
```

#### **d. Usar `!r`, `!s`, `!a` para conversiones**  

```python  
texto = "Hola"  
print(f"{texto!r}")  # Muestra la representación con comillas: 'Hola'  
```

---

### **Comparativa de métodos (actualizada)**:  

| Característica                | `+` | `,` en `print()` | `.format()` | `f-strings` |  
|-------------------------------|-----|-------------------|-------------|-------------|  
| Auto-documentación (`x=`)     | ❌  | ❌                | ❌          | ✅ (3.8+)   |  
| Soporta expresiones           | ❌  | ❌                | ✅          | ✅          |  
| Formateo numérico avanzado    | ❌  | ❌                | ✅          | ✅          |  
| Legibilidad                   | Baja| Media            | Alta        | Muy Alta    |  


---


### 1. **Formato básico de decimales**

```python
numero = 3.14159265
print(f"Número redondeado: {numero:.2f}")  # Salida: 3.14
```

---

### 2. **Separación de miles con comas**

```python
valor = 1234567.89
print(f"Valor formateado: {valor:,.2f}")  # Salida: 1,234,567.89
```

---

### 3. **Formato de porcentaje**

```python
puntuacion = 0.8745
print(f"Tasa de éxito: {puntuacion:.2%}")  # Salida: 87.45%
```

---

### 4. **Combinación de formatos (decimales + comas)**


```python
valor = 9876543.21
print(f"Valor combinado: ${valor:,.2f}")  # Salida: $9,876,543.21
```

---

### 5. **Formato dinámico usando variables**

```python
ancho = 10
precision = 3
numero = 42.56789
print(f"Formato dinámico: {numero:{ancho}.{precision}f}")  # Salida:     42.568
```

---

### 6. **Manejo de multilínea**

```python
nombre = "Cuchuflyto"
edad = 20
ciudad = "Biurzaco"
info = f"""
Nombre: {nombre}
Edad:   {edad}
Ciudad: {ciudad}
"""
print(info)
# Salida:
# Nombre: Cuchuflyto
# Edad:   20
# Ciudad: Biurzaco
```

---

### 7. **Otros formatos útiles**

#### **Alineación de texto/números**

```python
texto = "Hola"
numero = 42
print(f"Texto alineado: |{texto:>10}|")  # Alineado a la derecha (10 caracteres)
print(f"Número alineado: |{numero:<10}|")  # Alineado a la izquierda
```

```
Salida:
Texto alineado: |      Hola|
Número alineado: |42        |
```

#### **Formato científico**

```python
numero = 12345.6789
print(f"Notación científica: {numero:.2e}")  # Salida: 1.23e+04
```

#### **Relleno con ceros**

```python
numero = 42
print(f"Relleno con ceros: {numero:05}")  # Salida: 00042
```

#### **Formato hexadecimal/binario**

```python
numero = 255
print(f"Hex: {numero:#x}")  # Salida: 0xff
print(f"Bin: {numero:b}")   # Salida: 11111111
```

#### **Formato de fechas**

```python
from datetime import datetime
hoy = datetime.now()
print(f"Fecha: {hoy:%d/%m/%Y}")  # Salida: 21/10/2023 (ejemplo)
```

---

### 8. **Formateo condicional**

```python
temperatura = 23.456
print(f"Temperatura: {temperatura:.1f}°C") if temperatura < 100 else print(f"Peligro: {temperatura:.0f}°C")
```

---

### 9. **Truncamiento de cadenas**

```python
texto_largo = "Python es increíble"
print(f"Texto truncado: {texto_largo:.5}")  # Salida: Pytho...
```

---

### Tips adicionales:

- Usa `:` dentro de `{}` para aplicar formato.
- Los símbolos como `,` (miles), `%` (porcentaje), o `e` (científico) modifican el tipo de salida.
- Puedes combinar múltiples símbolos (ej: `,.2f` para miles + 2 decimales).

