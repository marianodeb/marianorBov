
### **Comando `bc`**

`bc` (***Basic Calculator***) es un lenguaje de programación y calculadora de precisión arbitraria utilizado en sistemas Unix/Linux para realizar **cálculos matemáticos avanzados**, incluyendo operaciones con decimales, funciones trigonométricas, lógicas y algebraicas. Es ideal para cálculos complejos que requieren alta precisión o para integrar matemáticas en scripts de shell.

---

#### **¿Cómo utilizarlo?**  

- **Propósito principal:**  

  - Realizar operaciones matemáticas desde la terminal o scripts.  
  - Trabajar con números de **precisión arbitraria** (sin límite de dígitos).  
  - Ejecutar funciones personalizadas o predefinidas (ej: seno, logaritmo).  
- **Modos de uso:**  
  - **Interactivo:** Ejecutar `bc` y escribir operaciones directamente.  
  - **Por línea de comandos:** Enviar cálculos mediante pipes (ej: `echo "5+3" | bc`).  
  - **Scripts:** Ejecutar un archivo con código `bc`.  

---

#### **Sintaxis**  

```bash
bc [opciones] [archivo...]
```

#### **Opciones comunes**  

| Opción | Descripción                                                                 |
|--------|-----------------------------------------------------------------------------|
| `-l`   | Carga la **biblioteca matemática estándar** (funciones como `sin`, `sqrt`).|
| `-q`   | Modo silencioso (no muestra el banner de bienvenida).                      |
| `-i`   | Modo interactivo forzado.                                                  |
| `-v`   | Muestra la versión de `bc`.                                                |

---

#### **Ejemplos**  

1. **Operaciones básicas (suma, resta, multiplicación, división)**  

```bash
echo "5 + 3 * 2" | bc
```

**Salida:**  
   
```
11
```

2. **División con decimales (usando `scale`)**  

```bash
echo "scale=2; 10/3" | bc
```

**Salida:**  
   
```
3.33  # `scale` define el número de decimales.
```

3. **Funciones matemáticas avanzadas (con `-l`)**  

```bash
echo "s(3.1415)" | bc -l  # Calcula el seno de π (casi 0).
```
   
**Salida:** 
    
```
.00000000926535
```

4. **Trabajar con variables**
  
```bash
echo "n=5; n^2" | bc  # Elevar al cuadrado.
```
   
**Salida:**  
   
```
25
```

5. **Script en `bc` (archivo `calculo.bc`)**  

```bash
# Contenido de calculo.bc
scale=4
a=15.5
b=3.2
a / b
```
Ejecutar:  
   
```bash
bc -q calculo.bc
```

**Salida:** 
 
```
4.8437
```

6. **Conversión de bases numéricas (hexadecimal a decimal)** 
 
```bash
echo "ibase=16; FF" | bc  # FF en hex = 255 en decimal.
```
   
**Salida:**  
   
```
255
```

---

#### **Notas importantes** 
 
- **Precisión decimal:**  

- Usa `scale` para definir los decimales en divisiones (por defecto es 0).  
  
```bash
echo "scale=10; 22/7" | bc  # Aproximación de π.
```

- **Funciones disponibles con `-l`:**  

  - `s(x)`: Seno.  
  - `c(x)`: Coseno.  
  - `a(x)`: Arcotangente.  
  - `l(x)`: Logaritmo natural.  
  - `e(x)`: Exponencial.  
  
- **Sintaxis avanzada:**  

  - Permite definir funciones, bucles (`for`, `while`) y condicionales (`if`).  

---

#### **Consejos**  

- **Integración con scripts bash:**  

```bash
area=$(echo "scale=2; 3.1416 * 5^2" | bc)
echo "Área del círculo: $area"
```
  
**Salida:**  
  
```
Área del círculo: 78.53
```

- **Calculadora interactiva:**  

```bash
bc -l -q  # Inicia en modo interactivo con funciones matemáticas.
> 4 * atan(1)  # Calcula π (3.14159265358979323844).
```

**Tip adicional:** Usa `Ctrl + D` para salir de `bc` en modo interactivo.
