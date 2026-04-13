

## Modulos Paquetes Librerias

### **Definiciones Básicas**


Un módulo es un archivo de Python cuyos objetos (funciones, clases, excepciones, etc.) 
pueden ser accedidos desde otro archivo. Se trata simplemente de una forma de organizar 
grandes códigos.

Un paquete es una carpeta que contiene varios módulos. Siguiendo el ejemplo anterior, 
podemos diseñar un paquete matematica creando una carpeta con la siguiente estructura.

Debe contener siempre un archivo `__init__`.py (por el momento vacío) para que Python 
entienda que se trata de un paquete y no de una simple carpeta.

Python tiene sus propios módulos, los cuales forman parte de su librería de módulos 
estándar, que también pueden ser importados.

PEP 8: importación

La importación de módulos debe realizarse al comienzo del documento, en orden alfabético 
de paquetes y módulos.

Primero deben importarse los módulos propios de Python. Luego, los módulos de terceros 
y finalmente, los módulos propios de la aplicación.

Entre cada bloque de imports, debe dejarse una línea en blanco.

1. **Módulo**  

   - **Qué es**: Un archivo `.py` que contiene código reutilizable (funciones, clases, variables).  
   - **Ejemplo**: `math.py` (módulo de operaciones matemáticas en la biblioteca estándar).  
   - **Uso**: 
    
```python
import math
print(math.sqrt(25))  # Usa la función sqrt del módulo math
```

2. **Paquete** (Mención adicional para claridad)  
   - **Qué es**: Un directorio que agrupa múltiples módulos y/o subpaquetes. Requiere un archivo `__init__.py`.  
   - **Ejemplo**:  
   
```
     mi_paquete/  
     ├── __init__.py  
     ├── modulo1.py  
     └── subpaquete/  
         ├── __init__.py  
         └── modulo2.py
```

3. **Biblioteca/Librería**  

   - **Qué es**: Conjunto de módulos y paquetes organizados para un propósito específico.  
   - **Ejemplos**:  
     - **Biblioteca Estándar**: Colección incluida en Python (ej: `os`, `sys`).  
     - **Bibliotecas Externas**: Instalables via `pip` (ej: `numpy`, `pandas`).  

---

### **🔍 Diferencias Clave**

| **Concepto**      | **Alcance**                | **Estructura**                | **Ejemplo**              |
|--------------------|----------------------------|--------------------------------|--------------------------|
| **Módulo**         | Un solo archivo (.py)      | Funciones/clases individuales | `datetime.py`            |
| **Paquete**        | Directorio con módulos     | Múltiples archivos + `__init__`| `requests/` (biblioteca) |
| **Biblioteca**     | Colección de módulos/paquetes | Puede ser estándar o externa  | `numpy` (científica)     |

---

### **Aclaraciones Importantes**

- **"Biblioteca" vs "Librería"**: Son sinónimos en Python. En español, "librería" se usa más coloquialmente, pero técnicamente ambos se refieren a **libraries**.  
- **No confundir**:  

  - Un **módulo** es como una hoja suelta con código.  
  - Una **biblioteca** es un libro completo (varias hojas/módulos).  

---

### **💡 Ejemplo Práctico**
```python
# Importar un MÓDULO de la BIBLIOTECA estándar
import math
print(math.pi)  # 3.1415...

# Importar una BIBLIOTECA externa (previamente instalada con pip)
import pandas as pd
df = pd.DataFrame()  # Usa el módulo pandas de la biblioteca Pandas
```

---

### **Flujo de Organización**
```
Módulo (.py) → Paquete (directorio) → Biblioteca (colección de paquetes/módulos)
```

---


### **Tipos de Importaciones y Sintaxis**

#### **1. Importar un módulo completo**

- **Sintaxis**:  

```python
import modulo
```
- **Ejemplo**: 
 
```python
import math
print(math.sqrt(16))  # Accedes a la función via el nombre del módulo.
```
- **Cuándo usarlo**:  

  Cuando necesitas múltiples funciones/clases del módulo y quieres evitar conflictos de nombres.

---

#### **2. Importar con alias (renombrar)**

- **Sintaxis**:  

```python
import modulo as alias
```
- **Ejemplo**:  

```python
import numpy as np
array = np.array([1, 2, 3])  # Usas el alias para acceder.
```

- **Cuándo usarlo**:  

  Para acortar nombres largos o evitar colisiones (ej: `pandas as pd`).

---

#### **3. Importar elementos específicos**

- **Sintaxis**:  

```python
from modulo import funcion, clase, variable
```
- **Ejemplo**:  

```python
from math import sqrt, pi
print(sqrt(25))  # No necesitas escribir "math."
print(pi)
```
- **Cuándo usarlo**: 
 
  Cuando solo necesitas unos pocos elementos y quieres escribir menos código.

---

#### **4. Importar todo el contenido de un módulo (⚠️ No recomendado)**

- **Sintaxis**:  

```python
from modulo import *
```
- **Ejemplo**:  

```python
from math import *
print(sqrt(9))  # Todas las funciones están en el espacio global.
```
- **Riesgos**:  

  - Contamina el espacio de nombres (puede sobreescribir variables/funciones tuyas).  
  - Dificulta la lectura (no sabes de dónde viene cada función).  
- **Excepción**:  

  Algunos módulos como `tkinter` lo permiten para facilitar el código.

---

#### **5. Importar desde paquetes**

- **Estructura de paquete**:  

```
  mi_paquete/
  ├── __init__.py
  ├── modulo1.py
  └── subpaquete/
      ├── __init__.py
      └── modulo2.py
```
- **Sintaxis**: 
 
```python
from mi_paquete.subpaquete import modulo2
from mi_paquete.modulo1 import funcion_x
```

- **Ejemplo**: 
 
```python
from sklearn.ensemble import RandomForestClassifier
modelo = RandomForestClassifier()
```

---

#### **6. Importar módulos personalizados (archivos .py en tu proyecto)**

- **Sintaxis**:  

```python
import mi_modulo  # Si está en el mismo directorio.
```
  
- **Si está en otra carpeta**:  

```python
import sys
sys.path.append("ruta/a/la/carpeta")
import mi_modulo
```

---

### **🔍 Diferencias Clave Entre Métodos**

| **Método**                     | **Ventajas**                          | **Desventajas**                      |
|--------------------------------|---------------------------------------|---------------------------------------|
| `import modulo`                | Claridad (sabes de dónde viene todo). | Más código (ej: `modulo.funcion()`).  |
| `from modulo import elemento`  | Código más corto y directo.          | Riesgo de colisiones de nombres.      |
| `import modulo as alias`       | Ideal para nombres largos.            | Requiere recordar el alias.           |
| `from modulo import *`         | Rápido para prototipos.               | **Peligroso** en proyectos grandes.   |

---

### **Importaciones Avanzadas**

#### **1. Importaciones relativas (en paquetes)**

- **Sintaxis**:  

```python
from . import modulo          # Mismo nivel.
from ..subpaquete import algo  # Nivel superior.
```
- **Ejemplo**:  

  Si estás en `mi_paquete/subpaquete/modulo2.py`:  
  
```python
from .. import modulo1  # Importa modulo1 desde mi_paquete.
```

#### **2. Importar módulos dinámicamente**

- **Usando `importlib` (útil para plugins)**:  

```python
import importlib
mi_modulo = importlib.import_module("nombre_del_modulo")
mi_modulo.funcion()
```

---

### **💡 Mejores Prácticas**

1. **Evita `import *`**, excepto en scripts pequeños o entornos interactivos.  
2. **Usa alias estándar**:  

```python
import pandas as pd
import numpy as np
```
   
3. **Organiza imports**:  

   - Primero bibliotecas estándar.  
   - Luego bibliotecas externas.  
   - Finalmente módulos locales.
     
```python
# Correcto
import os
import sys

import pandas as pd

from mi_proyecto import utils
```

---

### **Errores Comunes**

1. **Módulo no encontrado**:  

   - ¿Instalaste la biblioteca? (`pip install nombre`).  
   - ¿El archivo está en la misma carpeta o en `sys.path`?  

2. **Importaciones circulares**:  

   - Módulo A importa Módulo B, que a su vez importa Módulo A.  

3. **Confundir paquetes con módulos**:  

   - Un paquete es un directorio, **no** se puede importar directamente (ej: `import mi_paquete/` ❌).

---

### **Ejemplo Integrador**

```python
# Importar biblioteca estándar
import os

# Importar con alias
import pandas as pd

# Importar elemento específico
from matplotlib import pyplot as plt

# Importar desde un paquete externo
from sklearn.model_selection import train_test_split

# Importar módulo personalizado
import mis_funciones as mf

# Uso
df = pd.DataFrame(mf.leer_archivo("datos.csv"))
plt.plot(df["x"], df["y"])
```

---

### **1. Llamar métodos de un módulo**

#### **Caso 1: Importar el módulo completo**

```python
# Importar el módulo math
import math

# Llamar al método sqrt (raíz cuadrada)
resultado = math.sqrt(25)  # Sintaxis: módulo.método()
print(resultado)  # 5.0
```

#### **Caso 2: Importar solo el método**

```python
from math import sqrt

# Llamar directamente al método
resultado = sqrt(9)  # Sintaxis: método()
print(resultado)  # 3.0
```

---

### **2. Llamar elementos de una biblioteca (ej: `requests`)**

#### **Ejemplo con biblioteca externa:**

```python
# Importar toda la biblioteca
import requests

# Usar un método de la biblioteca
response = requests.get("https://api.example.com")  # Sintaxis: biblioteca.método()
print(response.status_code)
```

#### **Alternativa con alias:**

```python
import requests as req  # Alias común

response = req.get("https://api.example.com")  # Sintaxis: alias.método()
```

---

### **3. Llamar elementos de un paquete (ej: `numpy`)**

#### **Estructura del paquete `numpy`:**

```
numpy/
├── __init__.py
├── random/
│   ├── __init__.py
│   └── random.py
└── linalg/
    └── ...
```

#### **Ejemplo de uso:**

```python
# Importar el paquete numpy (biblioteca)
import numpy as np

# Llamar un método del submódulo random
numeros_aleatorios = np.random.rand(3)  # Sintaxis: alias.submódulo.método()
print(numeros_aleatorios)  # Ej: [0.42, 0.15, 0.87]

# Usar otro submódulo (linalg)
matriz = np.array([[1, 2], [3, 4]])
determinante = np.linalg.det(matriz)  # Sintaxis: alias.submódulo.método()
print(determinante)  # -2.0
```

---

### **4. Llamar elementos de un paquete personalizado**

#### **Estructura de tu proyecto:**

```
mi_proyecto/
├── main.py
└── mi_paquete/
    ├── __init__.py
    ├── herramientas.py
    └── subpaquete/
        ├── __init__.py
        └── graficos.py
```

#### **Ejemplo de uso desde `main.py`:**

```python
# Importar un módulo del paquete
from mi_paquete.herramientas import sumar

# Llamar directamente al método
resultado = sumar(5, 3)  # Sintaxis: método()
print(resultado)  # 8

# Importar un submódulo de un subpaquete
from mi_paquete.subpaquete import graficos

# Usar una clase del submódulo
grafico = graficos.GraficoBarras()  # Sintaxis: submódulo.Clase()
grafico.dibujar()
```

---

### **5. Diferencias clave en sintaxis**

| **Elemento**        | **Ejemplo de Import**               | **Ejemplo de Llamado**           |
|----------------------|--------------------------------------|-----------------------------------|
| **Módulo completo**  | `import math`                       | `math.sqrt(25)`                  |
| **Método específico**| `from math import sqrt`             | `sqrt(9)`                        |
| **Paquete (submódulo)** | `import numpy as np`             | `np.random.rand(3)`              |
| **Clase en módulo**  | `from mi_paquete import Herramientas` | `herramienta = Herramientas()` |
| **Método de clase**  | `herramienta = Herramientas()`      | `herramienta.calcular()`         |

---

### **6. Casos especiales**

#### **Importar todo un módulo (NO recomendado):**

```python
from math import *  # Importa todos los métodos/variables

print(sqrt(16))  # Funciona, pero contamina el espacio de nombres
print(pi)        # 3.1415...
```

#### **Importaciones relativas (dentro de paquetes):**

En `mi_paquete/subpaquete/graficos.py`:

```python
# Importar un módulo del mismo paquete padre
from ..herramientas import sumar  # ".." sube un nivel

resultado = sumar(10, 20)  # Usa el módulo herramientas
```

---

### **Resumen de Reglas**

1. **Módulos**:  

   - `import modulo` → `modulo.metodo()`.  
   - `from modulo import metodo` → `metodo()`.  

2. **Paquetes**:  

   - Se accede a través de su estructura jerárquica:  
     `paquete.subpaquete.modulo.metodo()`.  

3. **Bibliotecas**:  

   - Trátalas como paquetes (ej: `numpy` es un paquete que contiene submódulos como `random` o `linalg`).  

4. **Métodos**:  

   - Siempre se llaman con paréntesis: `metodo()`, `Clase.metodo_estatico()`, o `objeto.metodo_instancia()`.  




