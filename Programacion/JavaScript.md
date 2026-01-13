
Definiendo variables 

### **Diferencias entre `let`, `var`, y `const` en JavaScript**

#### 1. **Ámbito (Scope):**

- **`var`**: Tiene ámbito de función (solo es accesible dentro de la función donde se declara). Si se declara fuera de una función, es global.

```javascript
  function ejemploVar() {
    var x = 10;
    if (true) {
      var x = 20; // Sobrescribe la variable anterior.
    }
    console.log(x); // 20
  }
```

- **`let`** y **`const`**: Tienen ámbito de bloque (solo son accesibles dentro del bloque `{}` donde se declaran).

```javascript
  function ejemploLet() {
    let y = 10;
    if (true) {
      let y = 20; // Variable diferente.
      console.log(y); // 20
    }
    console.log(y); // 10
  }
```

#### 2. **Reasignación y redeclaración:**

- **`var`**:
  - Puede ser **redeclarada** en el mismo ámbito.
  - Puede ser **reasignada**.
  
```javascript
var z = 10;
var z = 20; // Válido.
z = 30; // Válido.
```

- **`let`**:

  - No puede ser **redeclarada** en el mismo ámbito.
  - Puede ser **reasignada**.
  
```javascript
let a = 10;
a = 20; // Válido.
// let a = 30; // Error: no se puede redeclarar.
```

- **`const`**:
  - No puede ser **redeclarada**.
  - No puede ser **reasignada** (pero si es un objeto o array, sus propiedades pueden modificarse).
  
```javascript
  const b = 10;
  // b = 20; // Error: no se puede reasignar.
  const objeto = { nombre: "Juan" };
  objeto.nombre = "Pedro"; // Válido.
```

#### 3. **Hoisting (Elevación):**

- **`var`**: Es elevada (hoisted) e inicializada con `undefined`.

```javascript
console.log(c); // undefined
var c = 5;
```

- **`let`** y **`const`**: Son elevadas pero no inicializadas. Acceder antes de declarar causa un error.

```javascript
console.log(d); // Error: no se puede acceder antes de la inicialización.
let d = 5;
```



Definir variables con `var` se las puede acceder de cualquier lado. Se puede cambiar el valor luego de definirla.
Definir variables con `let` solo se puede acceder en el bloque donde se definio ejemplo bloque if. No se puede cambiar el valor de la variable luego de definirla.
Definir variables con `const` estas se definen una vez y no se pueden cambiar.

```js
const email = "elpcihichi@gmail.com";
var nombre = "pacualinio";
var edad = 22;
var presenteOno = true;
var apellido = "Rogelinio";
var mascotas = "Gatillo";
var estatura = 1.80;
```

```js
alert("hola " + nombre + "!!!");
```

```js
console.log("Nombre: " + nombre + " tipo de dato: " + typeof nobmre );
console.log("Edad: " + edad  + " tipo de dato: " + typeof edad);
console.log("Presente: " + presenteOno  + " tipo de dato: " + typeof presenteOno);
console.log("Apellido: " + apellido  + " tipo de dato: " + typeof apellido);
console.log("Mascota: " + mascotas  + " tipo de dato: " + typeof mascotas);
console.log("Estatura: " + estatura  + " tipo de dato: " + typeof estatura);
console.log("email: " + email + " tipo de dato: " + typeof email);
```

Ejemolo de la definicion de una variable con let en un bloque if

```
if (true) {
    let nombrelet = "variable definida con let";
}
```

esto dara une error: console.log(nombrelet)

### **Resumen**

- Usa `const` por defecto para valores que no cambian.
- Usa `let` si necesitas reasignar una variable.
- Evita `var` por su ámbito impredecible.

---

### **Formas de concatenar en JavaScript**

#### 1. **Operador `+`**:

```javascript
let nombre = "Ana";
let edad = 25;
let mensaje = "Hola, soy " + nombre + " y tengo " + edad + " años.";
console.log(mensaje); // "Hola, soy Ana y tengo 25 años."
```

#### 2. **Template Literals (Backticks `` ` ``)**:

```javascript
let mensaje = `Hola, soy ${nombre} y tengo ${edad} años.`;
console.log(mensaje); // "Hola, soy Ana y tengo 25 años."
```

#### 3. **Método `concat()`**:

```javascript
let saludo = "Hola".concat(", ", nombre, "!");
console.log(saludo); // "Hola, Ana!"
```

#### 4. **Concatenar arrays con `join()`**:

```javascript
let palabras = ["Hola", "mundo"];
let frase = palabras.join(" "); // Une elementos con un espacio.
console.log(frase); // "Hola mundo"
```

#### 5. **Concatenar arrays con `concat()`**:

```javascript
let arr1 = [1, 2];
let arr2 = [3, 4];
let arr3 = arr1.concat(arr2);
console.log(arr3); // [1, 2, 3, 4]
```

---

## Comentarios

EN linea : // escribir comentario

```js
var suma = 7 + 3;
console.log(suma);
// esto es un comentario en una linea
```

En varias lineas: /* escricbir comentario */

```js

var suma = 7 + 3;
console.log(suma);
/* esto es un 
 comentario en 
 varias lineas*/

```

---

### Caracteres de escape

Caracteres de escape  en JavaScript, ordenados y con una breve definición:

| Carácter de Escape | Definición                                                                                                   | Ejemplo en JavaScript                 | Resultado                                           |
| ------------------ | ------------------------------------------------------------------------------------------------------------ | ------------------------------------- | --------------------------------------------------- |
| `\'`               | Comilla simple. Se usa para incluir una comilla simple dentro de una cadena delimitada por comillas simples. | `'Esto tiene una \'comilla simple\''` | `Esto tiene una 'comilla simple'`                   |
| `\"`               | Comilla doble. Se usa para incluir una comilla doble dentro de una cadena delimitada por comillas dobles.    | `"Esto tiene una \"comilla doble\""`  | `Esto tiene una "comilla doble"`                    |
| `\\`               | Barra invertida. Se usa para incluir una barra invertida literal.                                            | `'Esto tiene una \\'`                 | `Esto tiene una \`                                  |
| `\n`               | Nueva línea. Inserta un salto de línea.                                                                      | `"Primera línea\nSegunda línea"`      | `Primera línea` <br> `Segunda línea`                |
| `\r`               | Retorno de carro. Mueve el cursor al inicio de la línea actual (en algunos sistemas se combina con `\n`).    | `"Texto\rInicio"`                     | Depende del sistema (puede sobrescribir)            |
| `\t`               | Tabulador horizontal. Inserta un espacio de tabulación.                                                      | `"Columna 1\tColumna 2"`              | `Columna 1       Columna 2`                         |
| `\b`               | Retroceso (Backspace). Borra el carácter precedente.                                                         | `"Texto\bError"`                      | `TextoError`                                        |
| `\f`               | Salto de página (Form Feed). Avanza a la siguiente página (poco común en navegadores modernos).              | `"Página 1\fPágina 2"`                | Depende del sistema (puede no tener efecto visible) |
| `\v`               | Tabulador vertical. Inserta un espacio de tabulación vertical (poco común).                                  | `"Línea 1\vLínea 2"`                  | Depende del sistema (puede no tener efecto visible) |
| `\0`               | Carácter nulo. Representa el carácter nulo (código ASCII 0).                                                 | `"Texto\0Final"`                      | `Texto` (lo que sigue puede no mostrarse)           |
| `\xHH`             | Carácter con código hexadecimal HH (dos dígitos hexadecimales).                                              | `"Carácter \\x41"`                    | `Carácter A`                                        |
| `\uHHHH`           | Carácter Unicode con código HHHH (cuatro dígitos hexadecimales).                                             | `"Símbolo \\u00A9"`                   | `Símbolo ©`                                         |
| `\u{HHHHH}`        | Carácter Unicode con código HHHHH (uno a seis dígitos hexadecimales) - ECMAScript 6 (ES2015).                | `"Emoji \\u{1F600}"`                  | `Emoji 😀`                                          |

**Notas importantes:**

* Los caracteres de escape siempre comienzan con una barra invertida (`\`).
* Se utilizan dentro de cadenas de texto (delimitadas por comillas simples o dobles).
* Algunos caracteres de escape como `\r`, `\f`, y `\v` tienen un comportamiento que puede variar dependiendo del entorno (navegador, consola, etc.).
* Los códigos hexadecimales y Unicode te permiten representar una gama mucho más amplia de caracteres.




---

### Operadores de comaparacion


|descripcion|operador|
|---|---|
|igualdad ==|
|Desigualdad (distinto) !=|
|Igualdad estricta ===|
|Desigualdad estricta !==|
|Mayor y menor > <|
|Mayor o igual menor o igual >= <=|

### Operadores matematicos


|operador|descripcio|
|---|---|
|+| suma|
|-| resta| 
|*| multiplicacion|
|++| incremeta|
|--| decrementa| 
|%| resto de la division|

```js
var suma = 7 + 3;
console.log(suma);
```

```js
var resta = 10 - 4;
console.log(resta);
```

```js
var multip = 3 * 7;
console.log(multip);
```

```js
var div = 10 / 2;
console.log(div);
```

```js
var resto = 10 % 3;
console.log(resto);
```

### Operadores de comaparacion

```js
console.log(4 == 7 , "falso");

console.log(4 > 7 , "falso");

console.log(4 < 7 , "verdad");

console.log(4 >= 7 , "falso");

console.log(4 <= 7 , "verdad");

console.log(4 != 7 , "verdad");
```

```js
var edad = 19;
var dni = true;
// operador and
console.log(edad >= 18 && dni == true );
//operador or
console.log(edad >= 19 || dni == true);
```
---

Claro, los **operadores unarios** en JavaScript son aquellos que actúan sobre un **solo operando** (variable, valor o expresión). Vamos a explorarlos, comparando con Python donde sea relevante, ya que algunos no existen o funcionan de manera diferente.

---

### **Principales Operadores Unarios en JavaScript**

#### 1. **`+` (Conversión a número)**

   - Convierte un valor a tipo `number`.
   - Si el valor no es convertible, retorna `NaN`.
   
```javascript
console.log(+ "42");      // 42 (número)
console.log(+ "Hola");    // NaN
console.log(+ true);      // 1
console.log(+ false);     // 0
```

   **Comparación con Python**:
   
   En Python no existe este operador unario para conversión. Se usa `int()` o `float()`:

```python
print(int("42"))  # 42
```

---

#### 2. **`-` (Negación)**

   - Convierte el valor a número y luego lo niega.
   
```javascript
console.log(- "10");      // -10
console.log(- true);      // -1
```

---

#### 3. **`++` (Incremento) y `--` (Decremento)**

   - Aumentan o disminuyen el valor de una variable en 1.
   - **Prefijo**: Primero incrementa/decrementa, luego retorna el valor.
   - **Sufijo**: Primero retorna el valor, luego incrementa/decrementa.

```javascript
let x = 5;
console.log(++x); // 6 (pre-incremento)
console.log(x++); // 6 (post-incremento, x ahora es 7)

let y = 3;
console.log(--y); // 2 (pre-decremento)
```

   **Comparación con Python**:
   Python no tiene estos operadores. Se usa `x += 1` o `x -= 1`:
   ```python
   x = 5
   x += 1  # 6
   ```

---

#### 4. **`!` (NOT lógico)**

   - Convierte el valor a booleano y lo niega.
   - Valores **falsy** en JavaScript: `false`, `0`, `""`, `null`, `undefined`, `NaN`.

```javascript
console.log(!true);        // false
console.log(!0);           // true
console.log(!"Hola");      // false (porque "Hola" es truthy)
```

   **Comparación con Python**:
   
   En Python se usa `not`:
   
```python
print(not True)  # False
```

---

#### 5. **`typeof`**
   - Retorna el tipo de dato de una variable o valor como string.

```javascript
   console.log(typeof 42);          // "number"
   console.log(typeof "Hola");      // "string"
   console.log(typeof true);        // "boolean"
   console.log(typeof undefined);   // "undefined"
   console.log(typeof null);        // "object" (¡Cuidado! Es un error histórico de JS)
```

   **Comparación con Python**:
   
   En Python se usa `type()`:
   
```python
print(type(42))  # <class 'int'>
```

---

#### 6. **`void`**

   - Evalúa una expresión y retorna `undefined`.
   - Se usa para evitar que una expresión retorne un valor.
   
```javascript
console.log(void 0);             // undefined
console.log(void (5 + 3));       // undefined
```

   **Uso común**: En enlaces HTML para evitar navegación:
   
```html
<a href="javascript:void(0)">Haz clic</a>
```

---

#### 7. **`delete`**

   - Elimina una propiedad de un objeto o un elemento de un array (pero no modifica la longitud del array).

```javascript
const obj = { a: 1, b: 2 };
delete obj.a;
console.log(obj); // { b: 2 }

const arr = [1, 2, 3];
delete arr[1];    // Elimina el valor en la posición 1 (queda [1, empty, 3])
```

   **Comparación con Python**:
   
   En Python se usa `del`:
   
```python
dicc = {"a": 1, "b": 2}
del dicc["a"]
```

---

#### 8. **`~` (Bitwise NOT)**

   - Invierte los bits de un número.
   
```javascript
console.log(~5); // -6 (equivale a -(x + 1))
```

   **Uso avanzado**: Chequear si un elemento existe en un string/array (antiguo enfoque):
   
```javascript
   if (~"Hola".indexOf("a")) { // Si no encuentra, retorna -1 → ~-1 = 0 (falsy)
     console.log("Existe");
   }
```

---

### **Diferencias Clave con Python**

1. **Operadores de incremento/decremento**: Python no tiene `++` o `--`.
2. **Operador `typeof`**: En Python se usa `type()`.
3. **Delete vs Del**: En Python `del` elimina variables o elementos, en JS `delete` solo propiedades de objetos.
4. **Valores Truthy/Falsy**: Los valores considerados como `falsy` difieren entre ambos lenguajes.

---

### **¿Cuándo Usarlos?**

- **`+` y `-`**: Para conversiones rápidas a número.
- **`++` y `--`**: En bucles o contadores (pero evita usarlos en expresiones complejas).
- **`!`**: Para negar condiciones de manera concisa.
- **`typeof`**: Para validar tipos de datos (útil en funciones).
- **`void`**: Casos muy específicos (como enlaces HTML).

Si vienes de Python, estos operadores pueden parecer extraños al principio, pero son fundamentales para escribir código conciso en JavaScript. 😊

---

## Prompt

Prompt es una función en JavaScript que muestra un cuadro de diálogo en el navegador, solicitando al usuario que ingrese un valor. El valor ingresado por el usuario se devuelve como una cadena de texto.

```js
let nombre = prompt("Por favor, ingresa tu nombre:");
```

--
##Condicionales

Sintaxis if else - if anidado

```js
if (condicion) {
// codigo que se ejecuta si la condicion se cumple
}
```


```js
if (condición) {
    // Código a ejecutar si la condición es verdadera
} else {
    // Código a ejecutar si la condición es falsa
}
```

Ejemplo 

```js
var aprobe = true;

if (aprobe == true) {
    console.log("puedo salir");
}
else {
    console.log("negativo a salir");
}
```

If Anidado

Estructura condicional dentro de otra.

```javascript
if (condición1) {
    // Código si condición1 es verdadera
    if (condición2) {
        // Código si condición2 también es verdadera
    }
} else if (condición3) {
    // Código si condición1 es falsa pero condición3 es verdadera
} else {
    // Código si todas las condiciones anteriores son falsas
}
```

**Ejemplo:**

```javascript
let edad = 18;
let esMiembro = true;

if (edad >= 18) {
    if (esMiembro) {
        console.log("Acceso permitido al área VIP.");
    } else {
        console.log("Acceso solo a la zona general.");
    }
} else {
    console.log("Acceso denegado: Menor de edad.");
}
```



Sintaxis switch

```
switch (expresión) {
    case valor1:
        // Código a ejecutar si expresión === valor1
        break;
    case valor2:
        // Código a ejecutar si expresión === valor2
        break;
    default:
        // Código a ejecutar si no coincide ningún caso
}
```

---


---

### While

Ejecuta un bloque mientras se cumpla una condición (verificación al inicio).

```javascript
while (condición) {
    // Código a ejecutar
    // Modificar variable de control para evitar bucles infinitos
}
```

**Ejemplo:**

```javascript
let contador = 0;

while (contador < 5) {
    console.log("Contador: " + contador);
    contador++;
}
```

---

### 3. **For**

Bucle con inicialización, condición e incremento/decremento.

```javascript
for (inicialización; condición; expresiónFinal) {
    // Código a ejecutar en cada iteración
}
```

**Ejemplo:**

```javascript
// Imprimir números del 0 al 4
for (let i = 0; i < 5; i++) {
    console.log("Iteración: " + i);
}

// Recorrer un array
let frutas = ["Manzana", "Banana", "Uva"];
for (let j = 0; j < frutas.length; j++) {
    console.log(frutas[j]);
}
```

---

### Do While

Ejecuta el bloque al menos una vez y luego verifica la condición (verificación al final).

```javascript
do {
    // Código a ejecutar
} while (condición); // ¡No olvides el punto y coma!
```

**Ejemplo:**

```javascript
let numero;

do {
    numero = parseInt(prompt("Ingresa un número mayor a 10:"));
} while (numero <= 10);

console.log("Número válido: " + numero);
```

---


(Due to technical issues, the search service is temporarily unavailable.)

Aquí tienes un resumen de los tipos de funciones en JavaScript, su sintaxis, ejemplos y casos de uso:

---

## Funciones

### 1. **Declaración de Función (Function Declaration)**

**Sintaxis:**

```javascript
function nombreFuncion(param1, param2) {
  // código
}
```
**Ejemplo:**

```javascript
function sumar(a, b) {
  return a + b;
}
```
**Características:**

- Se puede llamar antes de su declaración (hoisting).
- Ideal para funciones reutilizables o de propósito general.

---

### 2. **Expresión de Función (Function Expression)**

**Sintaxis:**

```javascript
const nombreFuncion = function(param1, param2) {
  // código
};
```

**Ejemplo:**

```javascript
const sumar = function(a, b) {
  return a + b;
};
```

**Características:**

- Asignada a una variable (no tiene hoisting).
- Útil para callbacks o funciones anónimas.

---

### 3. **Arrow Function (ES6+)**

**Sintaxis:**

```javascript
const nombreFuncion = (param1, param2) => {
  // código
};
// Si es una sola línea, puede omitir {} y el return:
const nombreFuncion = (param1, param2) => expresión;
```

**Ejemplo:**

```javascript
const sumar = (a, b) => a + b;
```

**Características:**

- No tiene su propio `this` (usa el contexto léxico).
- Ideal para funciones cortas o callbacks.
- **La más utilizada en código moderno** por su brevedad.

---

### 4. **Método en Objetos (Shorthand Method)**

**Sintaxis (ES6+):**

```javascript
const objeto = {
  metodo(param1, param2) {
    // código
  }
};
```

**Ejemplo:**

```javascript
const calculadora = {
  sumar(a, b) {
    return a + b;
  }
};
```

**Características:**

- Sintaxis simplificada para métodos en objetos.

---

### 5. **Función Generadora (Generator Function)**

**Sintaxis:**

```javascript
function* nombreFuncion() {
  yield valor;
}
```

**Ejemplo:**

```javascript
function* generarId() {
  let id = 0;
  while (true) {
    yield id++;
  }
}
```

**Características:**

- Útil para funciones que generan secuencias de valores.

---

### 6. **Función Asíncrona (Async Function)**

**Sintaxis:**

```javascript
async function nombreFuncion() {
  await promesa;
}
```

**Ejemplo:**

```javascript
async function fetchData() {
  const data = await fetch('https://api.com');
  return data.json();
}
```

**Características:**

- Simplifica el trabajo con promesas usando `await`.

---

### 7. **Constructor Function (No recomendado)**

**Sintaxis:**

```javascript
const funcion = new Function('param1', 'param2', 'return param1 + param2');
```

**Ejemplo:**

```javascript
const sumar = new Function('a', 'b', 'return a + b');
```

**Características:**

- Crea funciones dinámicamente, pero es inseguro y lento. Evitar su uso.

---

### ¿Cuál es la más utilizada?

- **Arrow functions** y **function expressions/declarations** son las más comunes.
- Las arrow functions son preferidas en código moderno por su brevedad y manejo de `this`.

---

### ¿Cuándo usar cada una?

1. **Arrow Functions:**

   - Callbacks (ej: `array.map(x => x*2)`).
   - Funciones cortas y concisas.
   - Cuando necesitas preservar el contexto de `this` (ej: en eventos o métodos de clase).

2. **Function Declarations:**

   - Funciones reutilizables en cualquier parte del código (gracias al hoisting).
   - Funciones con nombre para mejor legibilidad.

3. **Function Expressions:**

   - Cuando necesitas asignar una función a una variable o pasar como argumento.
   - Funciones condicionales (ej: `const func = condition ? () => {} : () => {}`).

4. **Async Functions:**

   - Manejo de operaciones asíncronas con promesas.

5. **Métodos en Objetos:**

   - Definir métodos en objetos de forma más limpia.

---

### Diferencias Clave
| Tipo                | Hoisting | `this` propio | Sintaxis Breve |
|---------------------|----------|---------------|----------------|
| Function Declaration| Sí       | Sí            | No             |
| Function Expression | No       | Sí            | No             |
| Arrow Function      | No       | No (léxico)   | Sí             |


### Retornado multiples valores con return 

En JavaScript, el **`return`** solo puede devolver **un único valor**, pero hay un truco que puede causar confusión. En tu ejemplo, parece que estás retornando múltiples valores, pero en realidad **solo se devolverá el último** debido al uso de la coma (`,`), que actúa como operador. Aquí está el detalle:

---

### Análisis de tu código:

```javascript
function ejem2(dinero, bolsa) {
    console.log("La compra fue exitosa 2");
    let compra = "leche";
    return compra, dinero, bolsa; // ¡Solo retorna el último valor (bolsa)!
}

let prue = ejem2("agua", "aceite");
console.log(prue); // Salida: "aceite" (solo se retorna `bolsa`)
```

- **¿Qué está pasando?**  

  La coma (`,`) en el `return` se comporta como **operador de evaluación secuencial**, no como separador de valores.  
  - Se evalúan `compra`, luego `dinero`, y finalmente `bolsa`, pero **solo se retorna el último valor** (`bolsa` en este caso).

---

### Soluciones para retornar múltiples valores:

#### 1. Retornar un array (y desestructurar):

```javascript
function ejem2(dinero, bolsa) {
    console.log("La compra fue exitosa 2");
    let compra = "leche";
    return [compra, dinero, bolsa]; // Retorna un array
}

let prue = ejem2("agua", "aceite");
console.log(prue); // Salida: ["leche", "agua", "aceite"]

// Desestructuración:
const [producto, monto, contenedor] = ejem2("agua", "aceite");
console.log(producto); // "leche"
```

#### 2. Retornar un objeto (mejor legibilidad):

```javascript
function ejem2(dinero, bolsa) {
    console.log("La compra fue exitosa 2");
    let compra = "leche";
    return { compra, dinero, bolsa }; // Retorna un objeto
}

let prue = ejem2("agua", "aceite");
console.log(prue); // { compra: "leche", dinero: "agua", bolsa: "aceite" }

// Acceso a propiedades:
console.log(prue.compra); // "leche"
```

---

### Comparación con Python:

En **Python** sí puedes retornar múltiples valores (se devuelven como una tupla):

```python
def ejem2(dinero, bolsa):
    print("La compra fue exitosa 2")
    compra = "leche"
    return compra, dinero, bolsa  # Retorna una tupla: ("leche", "agua", "aceite")

prue = ejem2("agua", "aceite")
print(prue)  # ("leche", "agua", "aceite")
```

---


- **JavaScript:** Solo retorna un valor, pero puedes empaquetar múltiples valores en un array/objeto.  
- **Python:** Retorna múltiples valores como tupla (aunque técnicamente es un solo objeto de tipo tupla).






