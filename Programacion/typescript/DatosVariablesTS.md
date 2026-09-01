
# VARIABLES Y TIPOS DE DATOS EN TYPESCRIPT


## LAS 3 PALABRAS PARA DECLARAR VARIABLES

Para crear un "cajón", usamos una de estas tres palabras. La elección es **obligatoria** y define cómo se comportará ese cajón.

### A) `let` → El cajón que puede cambiar (El más usado)
Usamos `let` cuando el valor dentro del cajón **va a variar** con el tiempo.

```typescript
let precio = 100;      // Creo el cajón "precio" con 100
precio = 150;          // ✅ Cambio el valor a 150 (está permitido)
precio = 200;          // ✅ Sigue cambiando
```

### B) `const` → El cajón que NO puede cambiar (El más seguro)
Usamos `const` cuando el valor **NUNCA va a cambiar**. Es una constante. Si intentas cambiarlo, TypeScript te dará un error.

```typescript
const IVA = 0.21;      // Creo el cajón "IVA" con 0.21
IVA = 0.22;            // ❌ ERROR: No se puede cambiar una constante
```

**Regla de oro:** Siempre que puedas, usa `const`. Si después ves que necesitas cambiarlo, lo cambias a `let`.

### C) `var` → LA FORMA ANTIGUA (NO LA USES NUNCA)
`var` es la forma en que se hacía antes en JavaScript. Tiene problemas de comportamiento y puede causar errores difíciles de encontrar. **En TypeScript moderno, está prohibido usarla.**

```typescript
var nombre = "Juan";   // ❌ Nunca hagas esto. Siempre usa let o const.
```



## ¿CÓMO SE ESCRIBE UNA VARIABLE? (SINTAXIS)

La estructura para crear una variable es siempre la misma:

```
palabra clave (let/const) + nombre + "=" + valor;
```

**Ejemplos:**

```typescript
let pais = "Argentina";     // Creo un cajón llamado "pais" con el texto "Argentina"
const DIA = 7;              // Creo un cajón llamado "DIA" con el número 7
let temperatura = 22.5;     // Creo un cajón "temperatura" con un número decimal
let encendido = true;       // Creo un cajón "encendido" con verdadero/falso
```



## ¿QUÉ SON LOS "TIPOS DE DATOS"?

TypeScript es muy ordenado. No le gusta que mezcles cosas. 
Un **tipo de dato** es simplemente la **categoría** a la que pertenece tu valor. 

- Si pones `"Hola"`, el tipo es `string` (texto).
- Si pones `10`, el tipo es `number` (número).
- Si pones `true`, el tipo es `boolean` (verdadero/falso).



## LOS 3 TIPOS DE DATOS PRIMITIVOS QUE MÁS VAS A USAR

Estos son los básicos. El 90% de tus variables serán de estos tres tipos.

### A) `string` → Para texto
Siempre va entre comillas (simples, dobles o invertidas).

```typescript
let nombre = "Carlos";         // Con comillas dobles
let apellido = 'Pérez';        // Con comillas simples
let mensaje = `Hola ${nombre}`; // Con comillas invertidas (permite meter variables dentro)
```

### B) `number` → Para números
Pueden ser enteros, decimales, negativos. Sin comillas.

```typescript
let edad = 30;                 // Entero
let altura = 1.75;             // Decimal
let temperatura = -5;          // Negativo
```

### C) `boolean` → Para verdadero o falso
Solo existen dos valores posibles: `true` (verdadero) o `false` (falso). Sin comillas.

```typescript
let esMayorDeEdad = true;      // Es verdadero
let tieneHijos = false;        // Es falso
let estaLogueado = true;       // Está logueado
```



## LA GRAN PREGUNTA: ¿TENGO QUE DECLARAR EL TIPO O NO?

Aquí está el centro de tu duda. **TypeScript es muy inteligente**. Él sabe adivinar el tipo de dato solo con mirar el valor que le pones.

### Caso 1: Cuando el valor existe → NO DECLARES EL TIPO (Está bien)

```typescript
let nombre = "Carlos";   // Aquí TS mira y dice: "Ah, es un string". ¡No necesito escribir nada más!
let edad = 30;           // TS mira y dice: "Ah, es un number". 
let activo = true;       // TS mira y dice: "Ah, es un boolean".
```

**¿Por qué no poner el tipo?** Porque es más corto, más limpio y haces lo mismo. Esta es la forma **más común** en el día a día de un programador.

### Caso 2: Cuando el valor NO existe aún → SÍ DEBES DECLARAR EL TIPO

Imagina que quieres crear el cajón "precio", pero aún no sabes cuánto vale. Lo vas a llenar más tarde.

```typescript
let precio;              // ❌ ¡Peligro! TS no sabe qué es. Asume que es "any" (cualquier cosa).
precio = 10;             // Ahora es número
precio = "diez";         // ¡Esto también lo permite! Y aquí hay un error que no ves
```

Para evitar que pase esto, le **DECLARAMOS EL TIPO** desde el principio:

```typescript
let precio: number;      // ✅ Le digo: "Oye TS, esto será un número, aunque ahora no tenga valor".
precio = 10;             // ✅ Correcto
precio = "diez";         // ❌ ERROR: TypeScript me avisa antes de que falle mi programa. ¡Genial!
```

### Caso 3: Cuando el tipo puede ser MÁS DE UNO → SÍ DEBES DECLARAR EL TIPO

A veces, una variable puede ser, por ejemplo, un número O un texto. Por ejemplo, un ID de usuario puede ser "ABC123" (texto) o 12345 (número). 

```typescript
let idUsuario: string | number;   // ✅ Así se declara: "Esto será string O number"
idUsuario = "ABC123";             // ✅ Correcto
idUsuario = 456;                  // ✅ Correcto
idUsuario = true;                 // ❌ Error: no es string ni number
```


## OTROS TIPOS DE DATOS (Avanzados pero necesarios)

### A) `null` → Vacío intencional
Usamos `null` cuando queremos decir "este cajón está vacío a propósito". Es útil cuando esperamos un valor pero aún no lo tenemos.

```typescript
let usuario = null;   // "usuario" está vacío a propósito
usuario = "Ana";      // Después le pongo un valor
```

### B) `undefined` → No definido
Es el valor que tiene una variable cuando la creaste pero **nunca** le pusiste nada. Es un error del sistema, no algo que quieras usar a propósito.

```typescript
let cosa;              // No le puse valor
console.log(cosa);     // Salida: undefined (porque no existe)
```

### C) `any` → Cualquier cosa (EVÍTALO)
Cuando pones `any`, le dices a TypeScript: "déjame poner lo que quiera". Esto **desactiva toda la protección** de TypeScript. No lo uses a menos que sea estrictamente necesario.

```typescript
let variable: any = "texto";
variable = 42;          // ✅ Permite cambiar a número
variable = true;        // ✅ Permite cambiar a booleano
// Has perdido toda la seguridad.
```

### D) `Array` → Listas de cosas
Los arrays son como una **lista de cajones**. Guardan varios valores del **mismo tipo**.

```typescript
// Forma 1 (La más común y bonita):
let frutas: string[] = ["Manzana", "Pera", "Banana"]; // Lista de textos

// Forma 2 (menos usada):
let numeros: Array<number> = [1, 2, 3, 4]; // Lista de números

// ✅ También puedes dejar que TS lo adivine:
let colores = ["Rojo", "Azul"]; // TS ya sabe que es string[] (no hace falta poner nada)
```

### E) `object` → Para cosas más complejas
Los objetos son como **una bolsa que contiene varios cajones dentro**. Sirven para agrupar información de una misma cosa (ej. los datos de un usuario).

```typescript
// Declaración con tipo explícito (el más usado):
let usuario: { nombre: string; edad: number } = {
    nombre: "Carlos",
    edad: 30
};

// También puedes dejarlo sin tipo, TS lo adivina solo:
let producto = {
    id: 1,
    nombre: "Laptop",
    precio: 999.99
};
// TS ya sabe que producto tiene esas propiedades con esos tipos.
```


## LOS "TYPE ALIAS" (APODOS PARA TIPOS)

Cuando tienes un tipo muy largo o complicado (como un objeto con muchas propiedades), puedes darle un **nombre** (alias) para no tener que escribirlo todo el tiempo.

Es como ponerle una etiqueta a un tipo complejo para reutilizarlo.

```typescript
// 1. Creo el alias (como una plantilla)
type Usuario = {
    nombre: string;
    edad: number;
    email: string;
};

// 2. Ahora uso el alias como si fuera un tipo normal
let cliente1: Usuario = {
    nombre: "Ana",
    edad: 25,
    email: "ana@mail.com"
};

let cliente2: Usuario = {
    nombre: "Luis",
    edad: 32,
    email: "luis@mail.com"
};
// ¡Mucho más limpio y fácil de mantener!
```


## ¿QUÉ SIGNIFICA `: string`, `: number`, ETC.?

Cuando ves `let nombre: string = "Carlos"`, el `: string` es una **anotación de tipo**. Es una forma de decirle a TypeScript: "**Oye, asegúrate de que aquí solo vayan textos**".

Pero como ya vimos, si pones `let nombre = "Carlos"`, TS ya sabe que es string. 

**Regla práctica:** 
- Si pones `= valor` → No pongas `: tipo` (deja que TS lo adivine).
- Si **NO** pones `= valor` → Pon `: tipo` (porque TS no puede adivinar).


## ¿QUÉ PASA SI ME EQUIVOCO DE TIPO? (EL PODER DE TS)

Aquí está la magia de TypeScript. Si intentas meter un texto donde debería ir un número, TypeScript te va a mostrar un **error en rojo** en tu editor de código **ANTES** de que ejecutes el programa.

**Ejemplo de error:**
```typescript
let edad: number = 25;
edad = "veinticinco"; // ❌ ERROR: Type 'string' is not assignable to type 'number'.
```

**Ejemplo con inferencia:**
```typescript
let precio = 100;   // TS sabe que es number
precio = "caro";    // ❌ ERROR: No puedes poner un texto donde TS espera un número.
```

**¿Por qué es genial esto?** Porque en JavaScript normal, este error solo aparecería cuando el programa está corriendo y tu web se rompería. En TypeScript, el error aparece mientras escribes, ahorrándote horas de buscar fallos.


## EJEMPLO PRÁCTICO COMPLETO (SIN FUNCIONES COMPLEJAS)

Vamos a hacer un programa pequeño que usa todo lo que hemos visto. Solo declara variables y las usa.

```typescript
// 1. Variables simples con inferencia (más común)
const NOMBRE_EMPRESA = "Mi Tienda";   // const porque no cambia
let producto = "Laptop";              // let porque puede cambiar
let precio = 1000;                    // number
let descuento = 0.15;                 // number (15%)
let disponible = true;                // boolean

// 2. Variables con tipo explícito (por si cambian)
let categoria: string;                // Declaro que será string
categoria = "Electrónica";            // Le pongo el valor después

// 3. Union Type (puede ser número o texto)
let codigo: number | string;
codigo = 12345;                       // ✅ Número
codigo = "ABC123";                    // ✅ Texto

// 4. Listas (arrays)
let categorias: string[] = ["Electrónica", "Ropa", "Hogar"];

// 5. Objeto con alias (type)
type Producto = {
    id: number;
    nombre: string;
    precio: number;
};

// Creamos un producto usando el alias
let miProducto: Producto = {
    id: 1,
    nombre: "Teclado",
    precio: 50
};

// 6. Modifico algunas variables para ver que funcionan
producto = "Mouse";                   // ✅ Cambio producto
precio = 25;                          // ✅ Cambio precio
disponible = false;                   // ✅ Cambio disponibilidad
// categoria = 123;                   // ❌ ERROR: No puedo poner número porque es string
// precio = "gratis";                // ❌ ERROR: No puedo poner texto donde va número
```


## ERRORES COMUNES Y CÓMO EVITARLOS

| **Error común** | **Código malo** | **Código bueno** |
|-----------------|-----------------|------------------|
| Usar `var` | `var nombre = "Juan"` | `let nombre = "Juan"` |
| Usar `any` | `let dato: any = "texto"` | `let dato: string = "texto"` |
| No declarar tipo en variable vacía | `let total;` | `let total: number;` |
| Mezclar tipos en un array | `let mezcla = [1, "dos"]` | `let mezcla: (number \| string)[] = [1, "dos"]` |
| Asignar tipo incorrecto | `let edad = 25; edad = "25";` | `let edad = 25; edad = 25;` |


## PREGUNTAS FRECUENTES (FAQ)

**P: ¿Siempre que creo una variable debo ponerle tipo?**  
R: No. Si le das un valor al crearla, TypeScript lo adivina automáticamente. Solo pon el tipo si no tiene valor o si puede ser de varios tipos.

**P: ¿Por qué no usamos `var`?**  
R: Porque `var` tiene comportamientos raros con el ámbito (dónde vive la variable) y puede causar bugs. `let` y `const` son modernos y seguros.

**P: ¿Cuál es la diferencia entre `null` y `undefined`?**  
R: `undefined` significa "nunca se le asignó un valor". `null` significa "se le asignó intencionalmente el valor vacío".

**P: ¿Qué hago si quiero que una variable pueda ser "número o nada"?**  
R: Usas unión: `let edad: number | null = null;` o `number | undefined`.

**P: ¿Puedo cambiar el tipo de una variable después de crearla?**  
R: No. Si creas `let nombre = "Carlos"` (string), siempre será string. Si necesitas que pueda cambiar, usa unión desde el principio.


## RECOMENDACIONES FINALES (PARA QUE NO TENGAS DUDAS)

1. **Siempre usa `const`**, a menos que sepas que la variable cambiará (ahí usa `let`).
2. **Nunca uses `var`**. Olvídate de que existe.
3. **Deja que TypeScript adivine el tipo** siempre que puedas. Es código más limpio.
4. **Pon el tipo manualmente** solo cuando: la variable no tenga valor inicial, o pueda ser de varios tipos.
5. **Usa `type`** para dar nombres a tipos complejos (objetos o uniones).
6. **Nunca uses `any`** a menos que sea tu última opción. Te quita toda la seguridad.
7. **Prueba tu código**: Si ves un error rojo en tu editor, no lo ignores. TypeScript te está salvando de un bug futuro.


## ¡NO OLVIDES ESTO! (RESUMEN EN UNA TABLA)

| **Concepto** | **Qué es** | **Ejemplo** |
|--------------|------------|-------------|
| Variable | Cajón para guardar datos | `let nombre = "Ana"` |
| `let` | Para datos que cambian | `let precio = 10` |
| `const` | Para datos fijos | `const IVA = 0.21` |
| `string` | Texto | `"Hola mundo"` |
| `number` | Números | `25`, `3.14`, `-10` |
| `boolean` | Verdadero/Falso | `true`, `false` |
| `null` | Vacío intencional | `let usuario = null` |
| `undefined` | Sin valor asignado | `let cosa;` |
| `Array` | Lista de cosas | `["a", "b"]` |
| `Object` | Grupo de datos | `{ nombre: "Juan" }` |
| `type` | Alias para tipos | `type Usuario = { ... }` |
| `|` (union) | Más de un tipo | `string \| number` |
| `: tipo` | Anotación de tipo | `let nombre: string` |


## CONCLUSIÓN FINAL

**TypeScript** te da **poder y seguridad** sin complicarte la vida. La mayoría del tiempo escribirás:

```typescript
let nombre = "Carlos";   // Sin tipos, es más rápido
const EDAD = 30;         // Constantes siempre
```

Y solo en casos específicos escribirás:

```typescript
let precio: number;      // Cuando no tiene valor aún
let id: string | number; // Cuando puede ser dos cosas
```

