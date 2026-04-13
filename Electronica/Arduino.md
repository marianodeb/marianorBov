
## Comentarios

### comentario de una linea

```
// comentario en una linea
```
### Comentarios de varias lineas

```
/*
comentario:
en varias lineas

*/
```

¡Qué grande! Ya diste el primer paso más importante: **tener el control del hardware desde Linux**. El código que subiste tiene un parpadeo asimétrico (prende rápido y apaga lento), y si lo viste funcionar, es que tu puente entre el AppImage y el chip del Arduino ya está sólido.

Aquí tienes el desglose para tu **Obsidian**, bien organizado para que cuando vuelvas a esto en unos meses (o cuando te quedes sin internet) lo tengas todo claro.

---

## 🛠 Guía de Supervivencia: Arduino en Debian

### 1. Explicación de Comandos de Terminal

#### El "Tubería" o Pipe (`|`)
Antes que nada, el símbolo `|` se llama **pipe**. Su función es agarrar la salida (el texto) del comando de la izquierda y pasárselo como entrada al de la derecha. Es como una cinta transportadora de datos.

#### `dmesg | grep tty`
* **¿Qué hace?**: `dmesg` lee los mensajes directos del Kernel (el corazón del sistema). `grep tty` filtra esos miles de mensajes y solo te muestra los que contienen la palabra "tty".
* **¿Qué buscar?**: Busca líneas que terminen en `ttyUSB0` o `ttyACM0`. Si aparecen, significa que el sistema **físicamente ve la placa**.
* **Fallo común**: Si no sale nada, el problema es el cable USB o el chip de la placa.

#### `sudo dmesg | tail -n 20`
* **¿Qué hace?**: Muestra las **últimas 20 líneas** de lo que pasó en el sistema.
* **¿Qué buscar?**: Conecta el Arduino y tira el comando rápido. Deberías ver mensajes de "New USB device found". Si ves errores de "disconnection" o "error -110", puede que el puerto USB de tu PC tenga poca fuerza o el cable esté fallando.

#### `sudo usermod -a -G dialout $USER`
Este es el comando "mágico" de permisos.
* **`sudo`**: Ejecuta como administrador.
* **`usermod`**: Modifica un usuario.
* **`-a -G`**: Añade (**a**ppend) a un grupo (**G**roup) sin borrar los grupos que ya tenías.
* **`dialout`**: Es el nombre del grupo en Linux que tiene permiso para usar puertos serie (como los que usa Arduino). Antiguamente se usaba para los módems que hacían llamadas telefónicas (de ahí "dial-out").
* **`$USER`**: Es un atajo para no escribir tu nombre; el sistema lo reemplaza por tu usuario actual.


### 2. Checklist: Pasos para subir un Script (Sketch)

Para que no te salte el error de "Permission Denied" nunca más, sigue este orden:

1.  **Conexión Física**: Conecta el Arduino.
2.  **Verificación de Identidad (Opcional si ya anda)**:
    * Tira un `ls /dev/ttyUSB*` o `ls /dev/ttyACM*`. Si el archivo existe, Debian lo reconoce.
3.  **Configuración en el IDE**:
    * **Placa**: `Herramientas -> Placa` -> Selecciona **Arduino Uno**.
    * **Puerto**: `Herramientas -> Puerto` -> Selecciona el que aparezca (ej. `/dev/ttyUSB0`). **Si el puerto sale gris, te falta el permiso o reiniciar sesión.**
4.  **Verificar (El Tilde ✅)**:
    * Compila el código. Esto te dice si escribiste algo mal (un punto y coma que falta, por ejemplo). No toca el Arduino, solo lo traduce en tu PC.
5.  **Subir (La Flecha ➡️)**:
    * Carga el binario a la placa. Aquí es donde se borra lo viejo y entra lo nuevo.


### 3. Tips Extra para tu Obsidian

> [!TIP]
> **El conflicto con BRLTTY**: Si ves que el Arduino se conecta y se desconecta solo cada 2 segundos, es probable que un servicio de Debian llamado `brltty` esté molestando. Si no usas una pantalla braille, bórralo con:
> `sudo apt remove brltty`

> [!NOTE]
> **Consumo de Energía**: Tu bomba de lavarropas consume mucha corriente. El Arduino solo puede dar "órdenes" (señales de 5V con muy poca fuerza). Para mover motores o bombas, vas a necesitar un **Relé** o un **Transistor**. Nunca conectes la bomba directo a los pines del Arduino o lo vas a cocinar.




### Un detalle de tu código:
En tu código pusiste tres veces `digitalWrite(LED_BUILTIN, LOW);` seguidas con diferentes `delay`.
Como el LED ya está apagado (`LOW`) desde la primera vez, el Arduino simplemente se queda esperando sin hacer nada hasta que pasan los 3 segundos totales. ¡Funciona perfecto, pero con una sola vez que lo pongas al final alcanza!

¿Te gustaría que te ayude a armar un esquema de cómo conectarías un sensor de humedad para esos 5 bancales que tienes? Sería un buen paso antes de que te quedes sin conexión.



¡Qué grande! Ya diste el primer paso más importante: **tener el control del hardware desde Linux**. El código que subiste tiene un parpadeo asimétrico (prende rápido y apaga lento), y si lo viste funcionar, es que tu puente entre el AppImage y el chip del Arduino ya está sólido.

Aquí tienes el desglose para tu **Obsidian**, bien organizado para que cuando vuelvas a esto en unos meses (o cuando te quedes sin internet) lo tengas todo claro.


##  Guía de Supervivencia: Arduino en Debian

### 1. Explicación de Comandos de Terminal

#### `dmesg | grep tty`
* **¿Qué hace?**: `dmesg` lee los mensajes directos del Kernel (el corazón del sistema). `grep tty` filtra esos miles de mensajes y solo te muestra los que contienen la palabra "tty".
* **¿Qué buscar?**: Busca líneas que terminen en `ttyUSB0` o `ttyACM0`. Si aparecen, significa que el sistema **físicamente ve la placa**.
* **Fallo común**: Si no sale nada, el problema es el cable USB o el chip de la placa.

#### `sudo dmesg | tail -n 20`
* **¿Qué hace?**: Muestra las **últimas 20 líneas** de lo que pasó en el sistema.
* **¿Qué buscar?**: Conecta el Arduino y tira el comando rápido. Deberías ver mensajes de "New USB device found". Si ves errores de "disconnection" o "error -110", puede que el puerto USB de tu PC tenga poca fuerza o el cable esté fallando.

#### `sudo usermod -a -G dialout $USER`
Este es el comando "mágico" de permisos.
* **`sudo`**: Ejecuta como administrador.
* **`usermod`**: Modifica un usuario.
* **`-a -G`**: Añade (**a**ppend) a un grupo (**G**roup) sin borrar los grupos que ya tenías.
* **`dialout`**: Es el nombre del grupo en Linux que tiene permiso para usar puertos serie (como los que usa Arduino). Antiguamente se usaba para los módems que hacían llamadas telefónicas (de ahí "dial-out").
* **`$USER`**: Es un atajo para no escribir tu nombre; el sistema lo reemplaza por tu usuario actual.


### 2. Checklist: Pasos para subir un Script (Sketch)

Para que no te salte el error de "Permission Denied" nunca más, sigue este orden:

1.  **Conexión Física**: Conecta el Arduino.
2.  **Verificación de Identidad (Opcional si ya anda)**:
    * Tira un `ls /dev/ttyUSB*` o `ls /dev/ttyACM*`. Si el archivo existe, Debian lo reconoce.
3.  **Configuración en el IDE**:
    * **Placa**: `Herramientas -> Placa` -> Selecciona **Arduino Uno**.
    * **Puerto**: `Herramientas -> Puerto` -> Selecciona el que aparezca (ej. `/dev/ttyUSB0`). **Si el puerto sale gris, te falta el permiso o reiniciar sesión.**
4.  **Verificar (El Tilde ✅)**:
    * Compila el código. Esto te dice si escribiste algo mal (un punto y coma que falta, por ejemplo). No toca el Arduino, solo lo traduce en tu PC.
5.  **Subir (La Flecha ➡️)**:
    * Carga el binario a la placa. Aquí es donde se borra lo viejo y entra lo nuevo.


### 3. Tips

> [!TIP]
> **El conflicto con BRLTTY**: Si ves que el Arduino se conecta y se desconecta solo cada 2 segundos, es probable que un servicio de Debian llamado `brltty` esté molestando. Si no usas una pantalla braille, bórralo con:
> `sudo apt remove brltty`


## 🛠 Guía de Supervivencia: Arduino en Debian

### 1. Explicación de Comandos de Terminal

#### El "Tubería" o Pipe (`|`)
Antes que nada, el símbolo `|` se llama **pipe**. Su función es agarrar la salida (el texto) del comando de la izquierda y pasárselo como entrada al de la derecha. Es como una cinta transportadora de datos.

#### `dmesg | grep tty`
* **¿Qué hace?**: `dmesg` lee los mensajes directos del Kernel (el corazón del sistema). `grep tty` filtra esos miles de mensajes y solo te muestra los que contienen la palabra "tty".
* **¿Qué buscar?**: Busca líneas que terminen en `ttyUSB0` o `ttyACM0`. Si aparecen, significa que el sistema **físicamente ve la placa**.
* **Fallo común**: Si no sale nada, el problema es el cable USB o el chip de la placa.

#### `sudo dmesg | tail -n 20`
* **¿Qué hace?**: Muestra las **últimas 20 líneas** de lo que pasó en el sistema.
* **¿Qué buscar?**: Conecta el Arduino y tira el comando rápido. Deberías ver mensajes de "New USB device found". Si ves errores de "disconnection" o "error -110", puede que el puerto USB de tu PC tenga poca fuerza o el cable esté fallando.

#### `sudo usermod -a -G dialout $USER`
Este es el comando "mágico" de permisos.
* **`sudo`**: Ejecuta como administrador.
* **`usermod`**: Modifica un usuario.
* **`-a -G`**: Añade (**a**ppend) a un grupo (**G**roup) sin borrar los grupos que ya tenías.
* **`dialout`**: Es el nombre del grupo en Linux que tiene permiso para usar puertos serie (como los que usa Arduino). Antiguamente se usaba para los módems que hacían llamadas telefónicas (de ahí "dial-out").
* **`$USER`**: Es un atajo para no escribir tu nombre; el sistema lo reemplaza por tu usuario actual.


### 2. Checklist: Pasos para subir un Script (Sketch)

Para que no te salte el error de "Permission Denied" nunca más, sigue este orden:

1.  **Conexión Física**: Conecta el Arduino.
2.  **Verificación de Identidad (Opcional si ya anda)**:
    * Tira un `ls /dev/ttyUSB*` o `ls /dev/ttyACM*`. Si el archivo existe, Debian lo reconoce.
3.  **Configuración en el IDE**:
    * **Placa**: `Herramientas -> Placa` -> Selecciona **Arduino Uno**.
    * **Puerto**: `Herramientas -> Puerto` -> Selecciona el que aparezca (ej. `/dev/ttyUSB0`). **Si el puerto sale gris, te falta el permiso o reiniciar sesión.**
4.  **Verificar (El Tilde ✅)**:
    * Compila el código. Esto te dice si escribiste algo mal (un punto y coma que falta, por ejemplo). No toca el Arduino, solo lo traduce en tu PC.
5.  **Subir (La Flecha ➡️)**:
    * Carga el binario a la placa. Aquí es donde se borra lo viejo y entra lo nuevo.


### 3. Tips

> [!TIP]
> **El conflicto con BRLTTY**: Si ves que el Arduino se conecta y se desconecta solo cada 2 segundos, es probable que un servicio de Debian llamado `brltty` esté molestando. Si no usas una pantalla braille, bórralo con:
> `sudo apt remove brltty`

---

# 📑 Programación en Arduino: Variables, Constantes y Pines

## 1. Fundamentos de Variables
Una **variable** es un espacio en la memoria RAM del microcontrolador donde almacenamos datos que pueden cambiar durante la ejecución del programa.

### Tipos de Datos (Tabla Maestra)
En microcontroladores como Arduino o ESP32, elegir el tipo de dato correcto es vital para no agotar la memoria.

| Tipo de Dato | Memoria | Rango de Valores | Uso Sugerido |
| :--- | :--- | :--- | :--- |
| `bool` | 1 byte | `true` (1) o `false` (0) | Estados lógicos (encendido/apagado). |
| `byte` | 1 byte | 0 a 255 | **Números de pines**, valores de sensores de 8 bits. |
| `char` | 1 byte | -128 a 127 o un carácter | Almacenar una letra (ej. 'A'). |
| `int` | 2 bytes | -32,768 a 32,767 | Contadores y números enteros generales. |
| `unsigned int` | 2 bytes | 0 a 65,535 | Valores que nunca serán negativos. |
| `long` | 4 bytes | -2,147,483,648 a ... | Números enteros muy grandes. |
| `unsigned long`| 4 bytes | 0 a 4,294,967,295 | **Tiempos con `millis()`** y cálculos de reloj. |
| `float` | 4 bytes | ±3.4e38 (con decimales) | Sensores de precisión (Temp, Humedad). |

> [!WARNING]
> **Diferencia Crítica:** Evita el uso excesivo de `String` (con S mayúscula). Para manejar texto de forma eficiente, usa arrays de caracteres: `char miTexto[] = "Hola";`.


## 2. Constantes y Definición de Pines
Las constantes no cambian su valor. Usarlas para definir pines evita errores accidentales y hace el código legible.

### ¿`const` o `#define`?
* **`const byte` (Recomendado):** Respeta los tipos de datos y es más seguro. El compilador te avisará si intentas cambiarlo por error.
* **`#define` (Tradicional):** Es un reemplazo de texto antes de compilar. No ocupa memoria RAM, pero es más difícil de depurar.

**Ejemplo de buenas prácticas:**
```cpp
const byte PIN_BOMBA = 8;   // Uso 'byte' porque el pin no supera 255 (ahorra RAM)
const float UMBRAL_RIEGO = 35.5; 
```


## 3. Ámbito de las Variables (Scope)
* **Globales:** Declaradas fuera de `setup()` y `loop()`. Se pueden usar en todo el programa.
* **Locales:** Declaradas dentro de una función. Solo existen mientras esa función se ejecuta.
* **Static (Avanzado):** Una variable local que **no pierde su valor** al terminar la función. Útil para contadores internos.


## 4. Control de Pines (Hardware I/O)

### Configuración en `setup()`
Antes de usar un pin, hay que decirle a Arduino qué hará:
```cpp
void setup() {
  pinMode(PIN_BOMBA, OUTPUT); // Envía energía
  pinMode(2, INPUT);          // Recibe señal de un sensor/botón
}
```

### Funciones de Interacción
1.  **Digitales (Todo o nada):**
    * `digitalWrite(pin, estado);` -> Envía `HIGH` (5V/3.3V) o `LOW` (0V).
    * `digitalRead(pin);` -> Lee si hay voltaje (`HIGH`) o no (`LOW`).
2.  **Analógicas (Escalas):**
    * `analogRead(pin);` -> Lee voltajes de 0 a 5V y los traduce de **0 a 1023**.
    * `analogWrite(pin, valor);` -> Genera una señal **PWM** (simula voltaje) de **0 a 255**.




## 5. Ejemplo Práctico Integrador
Este código resume cómo organizar las notas para un proyecto real (como tu sistema de riego):

```cpp
// 1. Definición de constantes (Pines y Ajustes)
const byte PIN_SENSOR = A0;
const byte PIN_RELE = 7;
const int LIMITE_HUMEDAD = 400;

// 2. Variables Globales
int lecturaActual = 0;

void setup() {
  pinMode(PIN_RELE, OUTPUT);
  // Los pines analógicos son INPUT por defecto
}

void loop() {
  // Uso de variable local para procesar el dato
  lecturaActual = analogRead(PIN_SENSOR);

  if (lecturaActual < LIMITE_HUMEDAD) {
    digitalWrite(PIN_RELE, HIGH); // Activa riego
  } else {
    digitalWrite(PIN_RELE, LOW);  // Apaga riego
  }
  delay(1000); // Pausa de 1 segundo
}
```

---

# 📑 Estructuras de Control: Guía Práctica de Sintaxis

## 1. El Bloque Condicional (`if`, `else if`, `else`)
Se usa para bifurcar el camino del programa. En Arduino, el "elif" de Python se escribe como **`else if`**.

### Sintaxis
```cpp
if (condicion) {
  // Código si es verdadero
} else if (otra_condicion) {
  // Código si la anterior falló pero esta es verdadera
} else {
  // Código si nada de lo anterior se cumplió
}
```

### 3 Ejemplos
1.  **`if` simple (Seguridad):**
    ```cpp
    if (temperatura > 100) {
      digitalWrite(PIN_ALARMA, HIGH); // Solo actúa si hay peligro
    }
    ```
2.  **`if / else` (Estado Binario):**
    ```cpp
    if (digitalRead(PIN_BOTON) == HIGH) {
      encenderBomba();
    } else {
      apagarBomba();
    }
    ```
3.  **`if / else if / else` (Niveles de Tanque):**
    ```cpp
    if (nivelAgua < 10) {
      estado = "Vacio";
    } else if (nivelAgua < 90) {
      estado = "Ok";
    } else {
      estado = "Lleno";
    }
    ```

---

## 2. Selector Múltiple (`switch` / `case`)
Ideal para cuando una sola variable puede tener muchos estados distintos. Es mucho más ordenado que usar 10 `if` seguidos.

### Sintaxis
```cpp
switch (variable) {
  case 1:
    // Acción para valor 1
    break;
  case 2:
    // Acción para valor 2
    break;
  default:
    // Si no es ni 1 ni 2
    break;
}
```

### 3 Ejemplos
1.  **Menú de Usuario:**
    ```cpp
    switch (botonPresionado) {
      case 'U': subirMenu(); break;
      case 'D': bajarMenu(); break;
      case 'E': seleccionar(); break;
    }
    ```
2.  **Semáforo de Estados:**
    ```cpp
    switch (faseSemaforo) {
      case 0: color = "Rojo"; break;
      case 1: color = "Amarillo"; break;
      case 2: color = "Verde"; break;
    }
    ```
3.  **Control de Motores (Dirección):**
    ```cpp
    switch (comandoBluetooth) {
      case 'F': avanzar(); break;
      case 'B': retroceder(); break;
      case 'S': detener(); break;
    }
    ```

---

## 3. Bucle Determinado (`for`)
Repite un bloque de código un número exacto de veces.

### Sintaxis
`for (inicio; condicion; incremento) { ... }`

### 3 Ejemplos
1.  **Parpadeo de Alerta (SOS):**
    ```cpp
    for (int i = 0; i < 3; i++) {
      digitalWrite(LED, HIGH); delay(200);
      digitalWrite(LED, LOW);  delay(200);
    }
    ```
2.  **Limpiar Sensores (Promediado):**
    ```cpp
    long suma = 0;
    for (int i = 0; i < 10; i++) {
      suma += analogRead(A0); // Suma 10 lecturas para sacar promedio
    }
    ```
3.  **Recorrer los 5 Bancales:**
    ```cpp
    for (int pin = 2; pin <= 6; pin++) {
      digitalWrite(pin, LOW); // Apaga todos los relés del pin 2 al 6
    }
    ```

---

## 4. Bucle Indeterminado (`while`)
Repite mientras la condición sea verdadera. **¡Cuidado!** Si la condición nunca cambia a falso, el Arduino se queda "trabado".

### Sintaxis

```cpp
while (condicion) {
  // Repetir hasta que condicion sea false
}
```

### 3 Ejemplos
1.  **Esperar a que se suelte un botón:**

```cpp
while (digitalRead(BOTON) == HIGH) {
// No hace nada, solo espera a que el usuario suelte el Determinado
}
```

2.  **Llenado de Seguridad (Presostato):**
```cpp
    while (sensorPresion == LOW) {
      digitalWrite(PIN_BOMBA, HIGH);
      sensorPresion = digitalRead(PIN_ENTRADA); // Actualiza la variable
    }
```
3.  **Calentamiento de Sensor:**
```cpp
    while (millis() < 5000) {
      // El programa no hace nada durante los primeros 5 segundos 
      // para dejar que los sensores se estabilicen
    }
```
##  Info de Oro

### Los Operadores Lógicos (Para condiciones complejas)
A veces un `if` no es suficiente y necesitas combinar condiciones:

1. **`&&` (Y / AND):** `if (humedad < 30 && esDeNoche == true)` -> Se deben cumplir **ambas**.
2. **`||` (O / OR):** `if (boton == HIGH || emergencia == true)` -> Se cumple si **cualquiera** de las dos es verdadera.
3. **`!` (NO / NOT):** `if (!estaLloviendo)` -> Invierte el valor (si no está lloviendo).


aca va la imagen de compuertas_arduino


### El Peligro del `;` (Punto y Coma)
Nunca pongas `;` inmediatamente después del paréntesis de un `if`, `for` o `while`.
* ❌ `if (x == 10); { ... }` -> El Arduino creerá que el `if` termina ahí y ejecutará el código siempre.
* ✅ `if (x == 10) { ... }`

---

Esta es una de las partes más importantes de la programación. Las **funciones** te permiten dividir un código gigante en piezas pequeñas, reutilizables y fáciles de entender. Para tu sistema de riego o el llenado de baldes, las funciones son las que harán que tu código no sea un caos.


## Funciones en Arduino (C++)

Una **función** es un bloque de código independiente que realiza una tarea específica. En lugar de escribir 20 veces lo mismo en el `loop()`, creas una función y la "llamas" cuando la necesites.

## 1. Funcionamiento y Anatomía
Toda función tiene tres partes principales: el **tipo de retorno**, el **nombre** y los **parámetros**.

### Declaración de una Función

```c++
tipoDeRetorno nombreFuncion(tipo parametro1, tipo parametro2) {
  // Cuerpo de la función (el código que se ejecuta)
  return valor; // Opcional, solo si el tipo de retorno no es 'void'
}
```

**`void`**: Se usa cuando la función realiza una acción (como encender un LED) pero no devuelve ningún número o dato de vuelta.
**`int`, `float`, `bool`**: Se usan cuando la función hace un cálculo y te "devuelve" el resultado.

## 2. Parámetros vs. Argumentos (Diferencias)

Es común confundirlos, pero técnicamente son distintos:

* **Parámetro:** Es la variable que definimos en la **declaración** de la función (el "espacio reservado").
* **Argumento:** Es el valor real que le enviamos a la función cuando la **llamamos**.

> [!TIP]
> **Analogía:** El **parámetro** es el molde de un bizcocho, y el **argumento** es el sabor (chocolate, vainilla) que viertes en el molde.


## 3. Llamar a una función
Llamar a una función es simplemente escribir su nombre seguido de paréntesis (y los argumentos si los tiene) en cualquier parte del `setup()` o `loop()`.


## 4. Ejemplos Prácticos

### Ejemplo 1: Función sin retorno ni parámetros (`void`)
Ideal para tareas repetitivas simples.
```cpp
// Declaración
void parpadearAlerta() {
  digitalWrite(13, HIGH);
  delay(100);
  digitalWrite(13, LOW);
  delay(100);
}

void loop() {
  if (sensorPeligro == HIGH) {
    parpadearAlerta(); // Llamada a la función
  }
}
```

### Ejemplo 2: Función con Parámetros (Uso de Argumentos)
Aquí enviamos datos a la función para que sea flexible.
```cpp
// El parámetro es 'pin' y 'tiempo'
void encenderLuz(byte pin, int tiempo) {
  digitalWrite(pin, HIGH);
  delay(tiempo);
  digitalWrite(pin, LOW);
}

void loop() {
  encenderLuz(8, 500);  // 8 y 500 son los ARGUMENTOS
  encenderLuz(13, 1000); // Reutilizamos la misma función para otro pin
}
```

### Ejemplo 3: Función con Retorno (`return`)
Útil para procesar datos de tus sensores de riego.
```cpp
// Esta función devuelve un booleano (true/false)
bool necesitaRiego(int lecturaHumedad) {
  if (lecturaHumedad < 300) {
    return true; 
  } else {
    return false;
  }
}

void loop() {
  int valor = analogRead(A0);
  // Guardamos el resultado de la función en una variable
  bool estado = necesitaRiego(valor); 
  
  if (estado) { 
    digitalWrite(BOMBA, HIGH); 
  }
}
```


## 💡 Información Muy Útil

### 1. El Orden Importa (pero no siempre)
En Arduino (gracias a su pre-procesador), puedes declarar tus funciones **debajo** del `loop()`, y el programa las encontrará igual. Esto ayuda a mantener el `loop()` arriba para que sea lo primero que leas.

### 2. Variables Locales dentro de Funciones
Cualquier variable que declares dentro de una función **muere** cuando la función termina. Si quieres que un valor sobreviva, debes usar el tipo de retorno o una variable global.

### 3. Reutilización de Código
Si notas que estás copiando y pegando el mismo bloque de código para tus 5 bancales de riego, es una señal de que **necesitas una función**.



