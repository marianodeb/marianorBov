
## ⚡ Topologías de Fuentes Conmutadas (SMPS)

En una TV, no siempre alcanza con una sola fuente. A medida que la pantalla es más grande, se necesita más potencia y eficiencia.

### 1. Flyback (La "Todoterreno" de baja potencia)
Es la más común en fuentes pequeñas o para el modo **Stand-by**.
* **Cómo funciona:** El transformador (chopper) funciona como una "represa". Almacena energía en su campo magnético cuando el transistor está encendido y la suelta ("vuela de regreso" o *fly back*) hacia el secundario cuando el transistor se apaga.
* **Función:** Alimentar el microprocesador (Stand-by) y circuitos de baja potencia (5V, 3.3V).
* **Cómo identificarla:** * Usa **un solo transistor** (o un integrado de 7-8 patas como el Viper o STR).
    * El transformador es pequeño.
    * Es la que siempre está encendida apenas enchufas la TV.



[Image of a flyback converter circuit diagram]


### 2. Forward (La "Transmisión Directa")
A diferencia de la Flyback, esta transfiere la energía **mientras** el transistor está encendido. No la almacena, la pasa directamente.
* **Función:** Se usa para potencias medias (fuentes de 100W a 200W). Era muy común en fuentes de PC y TVs LCD de primera generación.
* **Cómo identificarla:** * Suele tener **dos transistores** (Two-Switch Forward).
    * Verás un **inductor de choque extra** (una bobina grande con núcleo de ferrita) justo después de los diodos rectificadores de salida. Si ves transformador + bobina a la salida, es casi seguro Forward.

### 3. LLC / Resonante (La "Super Eficiente")
Esta es la que ves en las TVs LED modernas de muchas pulgadas. Se llama LLC por los componentes que usa: **L** (Inductor), **L** (Inductancia del transformador) y **C** (Capacitor).
* **Función:** Alimentar la etapa de potencia principal y los LEDs del Backlight. Es extremadamente eficiente y genera muy poco calor.
* **Cómo identificarla:** * Busca **dos transistores MOSFET** idénticos pegados al mismo disipador.
    * Lo más obvio: Un **capacitor de poliester rojo o azul** (generalmente de 630V o 1KV) conectado en serie con el primario del transformador chopper. Ese capacitor es el que hace que el circuito "resuene".

## 🔍 ¿Cómo conviven en una misma placa?

Es muy común ver las tres juntas en TVs de alta gama:

| Conversor | Ubicación en la placa | ¿Cuándo trabaja? |
| :--- | :--- | :--- |
| **Flyback** | Cerca de donde entra el cable de red. | Siempre (mantiene el control remoto activo). |
| **PFC (Boost)** | Una bobina grande sola antes del capacitor gordo. | Solo cuando enciendes la TV (sube el voltaje a 400V). |
| **LLC / Forward** | En el centro, conectada a los diodos de salida grandes. | Solo cuando la TV está encendida (potencia principal). |

### Tip para identificarlas rápido:
Mira el **capacitor principal** (el más grande). 
1. Si al encender la TV el voltaje en ese capacitor sube de 310V a **390V/400V**, tienes un conversor **PFC** (Boost).
2. Si después de ese capacitor ves un transformador con un capacitor de poliester en serie en el primario, tienes una **LLC**.
3. Si hay un integrado chiquito con un transformador minúsculo aparte, esa es la **Flyback** de Stand-by.



| Topología | Componente "Delator" | Dónde mirar |
| :--- | :--- | :--- |
| **Flyback** | El Entrehierro (Gap) | Si desarmas el chopper, los núcleos de ferrita no se tocan en el centro (tienen un hueco de aire). |
| **Forward** | El Inductor de Salida | Siempre hay una bobina toroidal (redonda) o cuadrada después de los diodos rectificadores. |
| **LLC** | El Capacitor de Resonancia | Un capacitor de poliester (tipo "caramelo") en serie con el bobinado primario del chopper. |



La razón de "las tres juntas" es por la **eficiencia**. En una TV moderna de 65":

1.  Una **Flyback** chiquita mantiene el stand-by (gasta casi nada de luz).
2.  Una **PFC (Boost)** corrige la corriente de la red.
3.  Una **LLC** grandota le da potencia a los LEDs y al sonido cuando la prendes.

´´´Marckdown
# Topología de Fuentes Conmutadas (SMPS)

## 1. Flyback
- **Uso:** Stand-by y potencias bajas (<150W).
- **Identificación:** Un solo transistor, transformador con entrehierro.
- **Tip:** [Pega aquí la captura del diagrama Flyback]

## 2. Forward
- **Uso:** Fuentes de PC viejas, potencias medias.
- **Identificación:** Inductor de salida toroidal después de los diodos.
- **Tip:** [Pega aquí la captura del inductor toroidal]

## 3. LLC (Resonante)
- **Uso:** Smart TVs modernas, alta eficiencia.
- **Identificación:** Dos MOSFETS y el capacitor de poliester en serie.
- **Tip:** [Pega aquí la captura del capacitor de poliester]

---
## ⚠️ Notas de Seguridad (IMPORTANTE)
- No medir en Colector/Drenador con multímetro.
- Usar tierra fría para el secundario y tierra caliente para el primario.
´´´ 

