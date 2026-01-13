## POO


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

### **Analogía**  

Imagina un **videojuego**:  

- **Clase**: Como un "molde" para crear enemigos (con atributos: vida, daño; y métodos: atacar, moverse).  
- **Objeto**: Cada enemigo concreto en el juego (uno tiene vida = 100, otro vida = 80).  
- **Modularización**: Diseñar por separado los sistemas de combate, sonido y gráficos.  
- **Encapsulamiento**: El jugador no ve el código interno del daño, solo el resultado.  
- **Herencia**: Un "JefeFinal" hereda de "Enemigo" pero tiene habilidades extra.  
- **Polimorfismo**: Tanto el jugador como un NPC pueden "moverse", pero de forma distinta.  

---

### **Ejemplo en Python**  

```python
# Clase abstracta (Abstracción)
class Vehiculo:
    def __init__(self, marca):
        self.marca = marca  # Propiedad

    def acelerar(self):  # Método abstracto (Polimorfismo)
        pass

# Herencia
class Coche(Vehiculo):
    def acelerar(self):
        print(f"{self.marca} acelera a 120 km/h")

class Bicicleta(Vehiculo):
    def acelerar(self):
        print(f"{self.marca} pedalea a 20 km/h")

# Objetos
mi_coche = Coche("Toyota")
mi_bici = Bicicleta("BMX")

# Polimorfismo en acción
for vehiculo in [mi_coche, mi_bici]:
    vehiculo.acelerar()
```

**Salida:**  

```
Toyota acelera a 120 km/h  
BMX pedalea a 20 km/h  
```

---

### **¿Por qué usar POO?**  

- **Organización**: Divide problemas complejos en partes más pequeñas (objetos).  
- **Reutilización**: Evita código repetido con herencia y módulos.  
- **Flexibilidad**: El polimorfismo y encapsulamiento facilitan cambios futuros.  

Es como construir un reloj: cada pieza (objeto) tiene una función específica, pero trabajan juntas para lograr un objetivo común. 

### **1. Clase**  

**Analogía:** Un plano arquitectónico de una casa.  
**Definición:** Es una plantilla que define la estructura (propiedades) y comportamiento (métodos) común para todos los objetos creados a partir de ella.  
**Ejemplo:**  

```python
class Perro:
    def __init__(self, nombre):
        self.nombre = nombre  # Propiedad

    def ladrar(self):  # Método
        print("¡Guau!")
```

---

### **2. Objeto**  

**Analogía:** Una casa construida a partir del plano.  
**Definición:** Es una instancia concreta de una clase. Tiene valores únicos para sus propiedades.  
**Ejemplo:**  

```python
mi_perro = Perro("Firulais")  # Objeto de la clase Perro
```

---

### **3. Modularización**  

**Analogía:** Un lego construido por piezas independientes (ruedas, ventanas, etc.).  
**Definición:** Dividir un programa en partes más pequeñas (módulos/clases) para facilitar el mantenimiento.  
**Ejemplo:**  

```python
# Módulo "geometria.py"
class Circulo:
    def __init__(self, radio):
        self.radio = radio

class Cuadrado:
    def __init__(self, lado):
        self.lado = lado
```

---

### **4. Encapsulamiento**  

**Analogía:** Una cápsula de medicamento: oculta su contenido y solo permite acceder a él mediante instrucciones.  
**Definición:** Restringir el acceso directo a ciertos datos o métodos (usando `_` o `__` en Python).  
**Ejemplo:**  

```python
class CuentaBancaria:
    def __init__(self):
        self.__saldo = 0  # Propiedad privada

    def depositar(self, monto):  # Método público
        self.__saldo += monto
```

---

### **5. Herencia**  

**Analogía:** Un hijo hereda características de sus padres, pero puede tener habilidades adicionales.  
**Definición:** Una clase (hija) puede heredar propiedades y métodos de otra clase (padre).  
**Ejemplo:**  

```python
class Animal:  # Clase padre
    def respirar(self):
        print("Respirando")

class Gato(Animal):  # Clase hija
    def maullar(self):
        print("Miau")
```

---

### **6. Polimorfismo**  

**Analogía:** Un botón "encender": en un TV lo activa, en una lámpara enciende la luz.  
**Definición:** Métodos con el mismo nombre pero comportamientos diferentes en clases distintas.  
**Ejemplo:**  

```python
class Pajaro:
    def sonido(self):
        print("¡Pío!")

class Vaca:
    def sonido(self):
        print("¡Muu!")

# Uso polimórfico:
for animal in [Pajaro(), Vaca()]:
    animal.sonido()
```

---

### **7. Métodos**  

**Analogía:** Acciones que puede realizar una persona (correr, saltar).  
**Definición:** Funciones definidas dentro de una clase que describen su comportamiento.  
**Ejemplo:**  

```python
class Telefono:
    def llamar(self, numero):  # Método
        print(f"Llamando al {numero}")
```

---

### **8. Propiedades/Atributos**  

**Analogía:** Características de un auto (color, modelo, velocidad).  
**Definición:** Variables que almacenan el estado de un objeto.  
**Ejemplo:**  

```python
class Auto:
    def __init__(self, color):
        self.color = color  # Atributo

mi_auto = Auto("rojo")
print(mi_auto.color)  # Salida: "rojo"
```

---

### **9. Mensajes**  

**Analogía:** Enviar una carta: solicitas una acción al destinatario.  
**Definición:** Comunicación entre objetos mediante la invocación de métodos.  
**Ejemplo:**  

```python
mi_perro.ladrar()  # Mensaje: "Ejecuta el método ladrar"
```

---

### **10. Constructor (`__init__`)**  

**Analogía:** Preparar una nueva habitación de hotel con toallas y jabón antes de que llegue un huésped.  
**Definición:** Método especial que se ejecuta al crear un objeto para inicializar sus atributos.  
**Ejemplo:**  

```python
class Libro:
    def __init__(self, titulo, autor):  # Constructor
        self.titulo = titulo
        self.autor = autor

libro = Libro("Cien años de soledad", "García Márquez")
```

---

### **Componentes clave de una clase**  

- **Atributos:** Variables que almacenan datos (`self.nombre`).  
- **Métodos:** Funciones que definen acciones (`ladrar()`).  
- **Constructor:** `__init__`, inicializa el objeto.  
- **Herencia:** Reutiliza código de una clase padre.  
- **Encapsulamiento:** Protege datos sensibles.  



