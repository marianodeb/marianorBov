

paso 1: Base a Emisor

![[Medir-transistor-paso-1.png]]

Conecta el cable positivo del multímetro a la BASE (B) del transistor y el cable negativo del medidor al EMISOR (E) del transistor.

1. Para un transistor NPN en buenas condiciones, el medidor debe mostrar una caída de voltaje entre 0.45V y 0.9V.
2. Si está probando el transistor PNP, debería ver en la pantalla «OL» o «Over Limit» (por encima del umbral).


paso 2 Base a Colector

![[Medir-transistor-paso-2.png]]

Mantén el cable positivo del multímetro en la BASE (B) y coloca el cable negativo del medidor en el COLECTOR (C) del transistor.

1. Para un transistor NPN en buenas condiciones, el medidor debe mostrar una caída de voltaje entre 0.45V y 0.9V.
2. Si estás probando el transistor PNP, deberás ver en la pantalla las letras «OL» (por encima del umbral).


Paso 3: Emisor a Base

![[Medir-transistor-paso-3.png]]

Conecta el cable positivo del multímetro al EMISOR (E) del transistor y el cable negativo del medidor a la BASE (B) del transistor.

1. Para un transistor NPN en buenas condiciones, tendrás que ver «OL» o «Over Limit» (por encima del umbral) en la pantalla.
2. Si estás probando un transistor PNP, el medidor debe mostrar una caída de voltaje entre 0.45V y 0.9V.


Paso 4: Colector a Base

![[Medir-transistor-paso-4.png]]

Conecta el cable positivo del multímetro al COLECTOR (C) del transistor. Conecta el cable negativo del medidor a la BASE (B) del transistor.

1. Para un transistor NPN en buenas condiciones, deberás ver en la pantalla «OL» (Over Limit).
2. Si estás probando con un transistor PNP, el medidor debe de mostrar una caída de voltaje entre 0.45V y 0.9V.


Paso 4: Colector a Emisor

![[Medir-transistor-paso-5.png]]

Conecta el cable positivo del medidor al COLECTOR (C) y el cable negativo del medidor al EMISOR (E).

1. Si tienes un transistor NPN o PNP en buenas condiciones, se mostrará «OL» o «Over Limit» en el medidor.
2. Ahora cambia los cables (positivo para el emisor y negativo para el colector). Una vez más, con un transistor NPN o PNP en buen estado debería leer «OL».

Conclusiones

1. Si su transistor bipolar mide lo contrario a estos pasos, considéralo como malo o defectuoso.

2. También puedes usar la caída de voltaje para determinar qué conductor es el emisor en un transistor, porque la unión de la base-emisor generalmente tiene una caída de voltaje ligeramente mayor que la unión de la base-colector.

3. Recuerda: Esta prueba solo verifica que el transistor no esté en cortocircuito o abierto, no garantiza que el transistor esté operando dentro de los parámetros proyectados. Solo debe usarse para ayudarte a decidir si necesita «reemplazar» o «probar otro componente».

Esta prueba sólo funciona en transistores bipolares; debe usar un método diferente para probar los FET.

4. Las pruebas con un multímetro proporcionan únicamente una verificación confiable de que el transistor bipolar no ha explotado, pero sigue siendo muy útil.


---

¡Claro que sí! Aquí tienes un resumen técnico estructurado, limpio y listo para que lo copies y pegues en tu **Obsidian**. He organizado todo en tablas y bloques de texto Markdown para que sea fácil de consultar.

***

# Guía Técnica: Comprobación de Componentes Electrónicos

Esta guía resume las técnicas de medición con multímetro en modo **Prueba de Diodos ($\rightarrow|-$)** y **Resistencia ($\Omega$)**.

## 1. Diodos y Puente Rectificador

| Componente | Prueba | Punta Roja (+) | Punta Negra (-) | Valor Esperado |
| :--- | :--- | :--- | :--- | :--- |
| **Diodo (Silicio)** | Polarización Directa | Ánodo | Cátodo (Banda) | `0.5V - 0.7V` |
| **Diodo (Silicio)** | Polarización Inversa | Cátodo (Banda) | Ánodo | `OL` (Abierto) |
| **Puente Rect.** | Diodos positivos | Terminales AC (~)| Positivo (+) | `OL` |
| **Puente Rect.** | Diodos positivos | Positivo (+) | Terminales AC (~)| `0.5V - 0.7V` |
| **Puente Rect.** | Diodos negativos | Negativo (-) | Terminales AC (~)| `0.5V - 0.7V` |


## 2. Transistores BJT: Identificación NPN/PNP

Para saber si es NPN o PNP sin datasheet, busca la **Base** (el pin que da lectura con los otros dos).

| Si la punta fija en la BASE es... | Los otros dos pines marcan valor con la punta... | El transistor es... |
| :--- | :--- | :--- |
| **ROJA (+)** | Negra (-) | **NPN** |
| **NEGRA (-)** | Roja (+) | **PNP** |


## 3. Tabla Maestra de Comprobación (BJT, MOSFET, IGBT)

Esta tabla detalla dónde colocar las puntas para determinar si el componente está **SANO** o **DEFECTUOSO**.

| Tipo de Transistor | Prueba | Punta Roja (+) | Punta Negra (-) | Lectura Correcta (SANO) | Lectura de FALLO (MALO) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **BJT (NPN)** | Base-Emisor | Base | Emisor | `0.5V - 0.7V` | `0.00V` (Corto) o `OL` (Abierto) |
| | Base-Colector | Base | Colector | `0.5V - 0.7V` | `0.00V` (Corto) o `OL` (Abierto) |
| | Colector-Emisor| Colector | Emisor | `OL` | `0.00V` o cualquier valor bajo |
| **BJT (PNP)** | Base-Emisor | Emisor | Base | `0.5V - 0.7V` | `0.00V` o `OL` |
| | Base-Colector | Colector | Base | `0.5V - 0.7V` | `0.00V` o `OL` |
| | Emisor-Colector| Emisor | Colector | `OL` | `0.00V` o valor bajo |
| **MOSFET (Canal N)**| Gate-Todo | Gate | Cualquier pin | `OL` | Si marca algo, está fugado |
| | Diodo Interno | Source | Drain | `0.4V - 0.8V` | `OL` o `0.00V` |
| | Estado Apagado | Drain | Source | `OL` | `0.00V` (Corto D-S) |
| **IGBT** | Gate-Todo | Gate | Cualquier pin | `OL` | Si marca algo, Gate dañada |
| | Diodo Interno | Emisor | Colector | `0.4V - 0.7V` | `OL` o `0.00V` |
| | Estado Apagado | Colector | Emisor | `OL` | `0.00V` (Corto C-E) |


## 4. Diferencias según Encapsulado (THT vs SMD)

### Encapsulados THT (Through-Hole)
* **TO-92 (Pequeños):** Mirando la cara plana de frente, el pinout suele ser **1:Emisor, 2:Base, 3:Colector** (EBC), pero en algunos es (CBE).
* **TO-220 (Potencia):** Mirando de frente con la pestaña metálica hacia atrás, suele ser **1:Base, 2:Colector, 3:Emisor** (BCE). El Colector suele estar unido a la pestaña metálica.

### Encapsulados SMD (Surface Mount)
* **SOT-23 (3 patas):** Es el más común.
    * **Pata sola (arriba):** Colector o Drain.
    * **Pata inferior izquierda:** Base o Gate.
    * **Pata inferior derecha:** Emisor o Source.
* **DPAK / D2PAK:** La aleta grande (tab) es el Colector/Drain. Las patas pequeñas son Base/Gate y Emisor/Source.

## 5. El caso especial: JFET
A diferencia de los demás, el JFET es **normalmente conductivo**.
* **Medición Drain-Source:** En modo Resistencia ($\Omega$), debe marcar un valor bajo (50$\Omega$ - 500$\Omega$) en **ambos sentidos**. Si marca `OL`, está abierto.
* **Gate:** Se comporta como un solo diodo hacia el canal. En un JFET Canal N, la punta Roja en Gate y Negra en Source marcará `~0.6V`.

## Notas Finales para tu Obsidian
> [!IMPORTANT]
> **Regla de Oro:** Si un transistor marca `0.00V` o pita entre cualquier par de patas, está en **cortocircuito**. Si marca `OL` en todas las combinaciones (incluyendo Base-Emisor y Base-Colector), está **abierto**.

> [!TIP]
> **Fugas:** Si un BJT marca un valor muy alto (ej. `1.8V`) donde debería marcar `OL`, tiene una **fuga** y causará fallas intermitentes o calentamiento. ¡Reemplázalo!


---

---


# Guía Rápida de Medición: Bien vs. Mal

Poné el multímetro en **Diodo ($\rightarrow|-$)**.

### 1. Transistores BJT (NPN y PNP)
*La Base es la clave para identificar el tipo.*

| Tipo | Roja (+) en | Negra (-) en | Lectura CORRECTA | Si marca esto está MAL |
| :--- | :--- | :--- | :--- | :--- |
| **NPN** | **Base** | Emisor | `0.500 a 0.700` | `0.000` (Corto) / `OL` (Abierto) |
| **NPN** | **Base** | Colector | `0.500 a 0.700` | `0.000` (Corto) / `OL` (Abierto) |
| **PNP** | Emisor | **Base** | `0.500 a 0.700` | `0.000` (Corto) / `OL` (Abierto) |
| **PNP** | Colector | **Base** | `0.500 a 0.700` | `0.000` (Corto) / `OL` (Abierto) |
| **Cualquiera** | Colector | Emisor | `OL` | `0.000` o cualquier número |


### 2. MOSFET (Canal N)
*El más común en fuentes y notebooks.*

| Roja (+) en | Negra (-) en | Lectura CORRECTA | Si marca esto está MAL |
| :--- | :--- | :--- | :--- |
| **Gate** | Cualquier pin | `OL` | Cualquier número o pitido (Gate rota) |
| **Source** | **Drain** | `0.400 a 0.600` | `OL` (Diodo interno abierto) |
| **Drain** | **Source** | `OL` | `0.000` (Transistor en corto) |


### 3. IGBT
*Muy usado en Inverters y Soldadoras.*

| Roja (+) en | Negra (-) en | Lectura CORRECTA | Si marca esto está MAL |
| :--- | :--- | :--- | :--- |
| **Gate** | Cualquier pin | `OL` | Si marca algo está quemado |
| **Emisor** | **Colector** | `0.400 a 0.600` | `OL` (Diodo abierto) |
| **Colector** | **Emisor** | `OL` | `0.000` (Corto total) |


### 4. Resumen Visual (SMD y Encapsulados)

* **SMD (SOT-23):** Con la pata sola arriba, esa es **Colector/Drain**. Abajo izquierda es **Base/Gate** y abajo derecha es **Emisor/Source**.
* **TO-220 (Grande con chapa):** De izquierda a derecha: **1.Base/Gate | 2.Colector/Drain | 3.Emisor/Source**.

**Resumen de Fallas:**
1.  **Pita o marca 0.000:** Está en **CORTO**.
2.  **Marca OL donde debería dar número:** Está **ABIERTO**.
3.  **Marca número donde debería dar OL:** Tiene **FUGA** (está "pinchado").



---

---


Tenés razón, me fui por las ramas con la explicación y te faltó el dato clave en la tabla. Acá tenés la posta, directo al grano, sin vueltas y con los valores exactos que tenés que ver en el tester para saber si el componente sirve o va a la basura.

Copiá esto en tu Obsidian:

# Guía Rápida de Medición: Bien vs. Mal

Poné el multímetro en **Diodo ($\rightarrow|-$)**.

### 1. Transistores BJT (NPN y PNP)
*La Base es la clave para identificar el tipo.*

| Tipo | Roja (+) en | Negra (-) en | Lectura CORRECTA | Si marca esto está MAL |
| :--- | :--- | :--- | :--- | :--- |
| **NPN** | **Base** | Emisor | `0.500 a 0.700` | `0.000` (Corto) / `OL` (Abierto) |
| **NPN** | **Base** | Colector | `0.500 a 0.700` | `0.000` (Corto) / `OL` (Abierto) |
| **PNP** | Emisor | **Base** | `0.500 a 0.700` | `0.000` (Corto) / `OL` (Abierto) |
| **PNP** | Colector | **Base** | `0.500 a 0.700` | `0.000` (Corto) / `OL` (Abierto) |
| **Cualquiera** | Colector | Emisor | `OL` | `0.000` o cualquier número |


### 2. MOSFET (Canal N)
*El más común en fuentes y notebooks.*

| Roja (+) en | Negra (-) en | Lectura CORRECTA | Si marca esto está MAL |
| :--- | :--- | :--- | :--- |
| **Gate** | Cualquier pin | `OL` | Cualquier número o pitido (Gate rota) |
| **Source** | **Drain** | `0.400 a 0.600` | `OL` (Diodo interno abierto) |
| **Drain** | **Source** | `OL` | `0.000` (Transistor en corto) |


### 3. IGBT
*Muy usado en Inverters y Soldadoras.*

| Roja (+) en | Negra (-) en | Lectura CORRECTA | Si marca esto está MAL |
| :--- | :--- | :--- | :--- |
| **Gate** | Cualquier pin | `OL` | Si marca algo está quemado |
| **Emisor** | **Colector** | `0.400 a 0.600` | `OL` (Diodo abierto) |
| **Colector** | **Emisor** | `OL` | `0.000` (Corto total) |


### 4. Resumen Visual (SMD y Encapsulados)

* **SMD (SOT-23):** Con la pata sola arriba, esa es **Colector/Drain**. Abajo izquierda es **Base/Gate** y abajo derecha es **Emisor/Source**.
* **TO-220 (Grande con chapa):** De izquierda a derecha: **1.Base/Gate | 2.Colector/Drain | 3.Emisor/Source**.

**Resumen de Fallas:**
1.  **Pita o marca 0.000:** Está en **CORTO**.
2.  **Marca OL donde debería dar número:** Está **ABIERTO**.
3.  **Marca número donde debería dar OL:** Tiene **FUGA** (está "pinchado").


---


---


Tenés razón, te la hago corta y al pie para que la pegues en tu Obsidian. El problema con los **MOSFET SMD** (como los de las placas madre) es que suelen ser de **Canal N** y se miden distinto si querés saber si están en corto o si el diodo interno está sano.

Acá tenés la tabla definitiva para medir los MOSFET SMD (encapsulados SOT-23, DPAK, SO-8) directamente para reparación de placas:

### Medición de MOSFET SMD (Canal N)



| Punta Roja (+) | Punta Negra (-) | Lectura Correcta (SANO) | Interpretación |
| :--- | :--- | :--- | :--- |
| **Gate (G)** | **Cualquiera** | `OL` | **Gate Aislada:** Si marca algo o pita, el MOSFET no sirve. |
| **Source (S)** | **Drain (D)** | `0.400V - 0.600V` | **Diodo Interno:** Estás midiendo el diodo de protección. |
| **Drain (D)** | **Source (S)** | `OL` | **Estado Apagado:** No debe dejar pasar nada en este sentido. |


### Cómo detectar el fallo rápido en Placa Madre:

1.  **El Corto Total (Lo más común):** Ponés el tester en continuidad (el que hace *pip*). Tocás **Drain y Source**. Si pita y marca `0.000`, ese MOSFET está muerto y es el que te está bloqueando el arranque de la placa o haciendo que la fuente se proteja.
2.  **Gate "Pinchada":** Si medís entre la pata de **Gate** y **Source** y te da un valor bajo (ej. `0.020V` o pita), el transistor está dañado internamente y no va a conmutar.
3.  **Identificación de patas en SMD:**
    *   **SOT-23 (3 patas):** Una arriba (Drain), dos abajo (Izquierda: Gate, Derecha: Source).
    *   **DPAK / D2PAK (Esa que tiene una aleta soldada):** La aleta grande es **Drain**, la pata izquierda es **Gate** y la derecha es **Source**.
    *   **SO-8 (8 patas, integrados):** Generalmente, las patas 1, 2, 3 son **Source**, la 4 es **Gate** y las 5, 6, 7, 8 son **Drain**.



**Resumen para tu nota:**
*   **Si pita entre Drain y Source:** CAMBIAR (Corto).
*   **Si marca valor entre Gate y los demás:** CAMBIAR (Fuga).
*   **Si no marca el diodo entre S y D (da OL en ambos sentidos):** CAMBIAR (Abierto).


---

---


Tenés razón, te la hago corta y al pie para que la pegues en tu Obsidian. El problema con los **MOSFET SMD** (como los de las placas madre) es que suelen ser de **Canal N** y se miden distinto si querés saber si están en corto o si el diodo interno está sano.

Acá tenés la tabla definitiva para medir los MOSFET SMD (encapsulados SOT-23, DPAK, SO-8) directamente para reparación de placas:

### Medición de MOSFET SMD (Canal N)



| Punta Roja (+) | Punta Negra (-) | Lectura Correcta (SANO) | Interpretación |
| :--- | :--- | :--- | :--- |
| **Gate (G)** | **Cualquiera** | `OL` | **Gate Aislada:** Si marca algo o pita, el MOSFET no sirve. |
| **Source (S)** | **Drain (D)** | `0.400V - 0.600V` | **Diodo Interno:** Estás midiendo el diodo de protección. |
| **Drain (D)** | **Source (S)** | `OL` | **Estado Apagado:** No debe dejar pasar nada en este sentido. |


### Cómo detectar el fallo rápido en Placa Madre:

1.  **El Corto Total (Lo más común):** Ponés el tester en continuidad (el que hace *pip*). Tocás **Drain y Source**. Si pita y marca `0.000`, ese MOSFET está muerto y es el que te está bloqueando el arranque de la placa o haciendo que la fuente se proteja.
2.  **Gate "Pinchada":** Si medís entre la pata de **Gate** y **Source** y te da un valor bajo (ej. `0.020V` o pita), el transistor está dañado internamente y no va a conmutar.
3.  **Identificación de patas en SMD:**
    *   **SOT-23 (3 patas):** Una arriba (Drain), dos abajo (Izquierda: Gate, Derecha: Source).
    *   **DPAK / D2PAK (Esa que tiene una aleta soldada):** La aleta grande es **Drain**, la pata izquierda es **Gate** y la derecha es **Source**.
    *   **SO-8 (8 patas, integrados):** Generalmente, las patas 1, 2, 3 son **Source**, la 4 es **Gate** y las 5, 6, 7, 8 son **Drain**.



**Resumen para tu nota:**
*   **Si pita entre Drain y Source:** CAMBIAR (Corto).
*   **Si marca valor entre Gate y los demás:** CAMBIAR (Fuga).
*   **Si no marca el diodo entre S y D (da OL en ambos sentidos):** CAMBIAR (Abierto).


---

---

No, también existen de **Canal P**, aunque en placas madre de PC y notebooks el **90% son Canal N** porque son más eficientes para manejar potencia.

Si te cruzás con uno de **Canal P**, la medición es exactamente al revés. Acá tenés la comparativa corta para tu Obsidian, así no te confundís cuando midas:

### Comparativa: MOSFET Canal N vs. Canal P
*(Multímetro en modo Diodo $\rightarrow|-$)*

| Tipo de MOSFET | Punta Roja (+) en | Punta Negra (-) en | Lectura CORRECTA |
| :--- | :--- | :--- | :--- |
| **Canal N** (Normal) | **Source (S)** | **Drain (D)** | `0.400V a 0.600V` |
| **Canal N** (Normal) | Drain (D) | Source (S) | `OL` |
| | | | |
| **Canal P** (Raro) | **Drain (D)** | **Source (S)** | `0.400V a 0.600V` |
| **Canal P** (Raro) | Source (S) | Drain (D) | `OL` |



### ¿Cómo los distinguís rápido en la placa?

1.  **Por el código:** Si el código del componente termina en número **par**, suele ser **Canal N**. Si termina en **impar**, suele ser **Canal P**. (Ejemplo: AO4406 es N, AO4407 es P).
2.  **Por la medición:** Si al medir entre **Source (Roja)** y **Drain (Negra)** te da el valor del diodo, es **Canal N**. Si te da `OL` y tenés que invertir las puntas para que marque, es **Canal P**.

### Resumen de seguridad:
*   **Gate (G):** No importa si es N o P, **SIEMPRE** debe dar `OL` contra las otras patas. Si marca algo, está pinchado.
*   **En Placas Madre:** Los MOSFETs que alimentan al procesador (VRM) son **siempre Canal N**. Los Canal P a veces aparecen en la entrada de voltaje o en el circuito de carga de batería.

¿Te sirve así o necesitás que te aclare algo más de los integrados de 8 patas (SO-8)?


---

---


Esos que decís, con dos patitas arriba y una abajo (o viceversa), son los **SOT-23**. Son los transistores SMD más comunes en electrónica de señal.

A diferencia de los MOSFET de potencia (donde la aleta larga es el Drain), en estos las 3 patitas son iguales. Lo más probable es que sean **Transistores BJT (NPN o PNP)** o **MOSFET de pequeña señal**.



### 1. ¿Cómo saber qué son?
La mayoría de las veces, si son de 3 patas iguales en placa madre, son **BJT**. Se miden igual que los grandes, pero el pinout (la posición de las patas) suele ser estándar:

*   **Pata sola (la que está sola de un lado):** **COLECTOR** (en BJT) o **DRAIN** (en MOSFET).
*   **Patas de abajo (izquierda):** **BASE** (en BJT) o **GATE** (en MOSFET).
*   **Patas de abajo (derecha):** **EMISOR** (en BJT) o **SOURCE** (en MOSFET).


### 2. ¿Cómo se miden? (La técnica rápida)

Poné el multímetro en **Diodo ($\rightarrow|-$)**.

#### Si sospechás que es un BJT (NPN/PNP):
Buscamos las dos uniones de diodo.

| Prueba | Punta Roja (+) | Punta Negra (-) | Lectura SANA |
| :--- | :--- | :--- | :--- |
| **Si es NPN** | **Base** (abajo izq.) | Colector (arriba) | `0.500 - 0.700` |
| | **Base** (abajo izq.) | Emisor (abajo der.) | `0.500 - 0.700` |
| **Si es PNP** | Colector (arriba) | **Base** (abajo izq.) | `0.500 - 0.700` |
| | Emisor (abajo der.) | **Base** (abajo izq.) | `0.500 - 0.700` |

*Si marca `0.000` o pita entre cualquier pata: **A la basura, está en corto.***


#### Si sospechás que es un MOSFET (Canal N):
A veces se usan para activar ventiladores o luces (pequeña carga).

| Punta Roja (+) | Punta Negra (-) | Lectura SANA |
| :--- | :--- | :--- |
| **Gate** (abajo izq.) | Cualquiera | `OL` (Si marca algo, está roto) |
| **Source** (abajo der.) | **Drain** (arriba) | `0.500 - 0.800` (Diodo interno) |
| **Drain** (arriba) | **Source** (abajo der.) | `OL` |


### Resumen para tu Obsidian:
*   **SOT-23:** Transistor miniatura. 3 patas iguales.
*   **Falla típica:** Corto entre la pata de arriba (Colector/Drain) y la pata derecha de abajo (Emisor/Source).
*   **Pinout estándar:**
    1.  Abajo Izquierda: **Base / Gate**
    2.  Abajo Derecha: **Emisor / Source**
    3.  Arriba (sola): **Colector / Drain**

**Ojo:** Como son tan chiquitos, a veces se queman y se les hace un "pocito" o punto negro en el plástico. Si ves eso, ni midas, cambialo de una.

---

### Tabla Maestra de Transistores (BJT vs. MOSFET)

| Característica | **BJT (NPN)** | **BJT (PNP)** | **MOSFET (Canal N)** | **MOSFET (Canal P)** |
| --- | --- | --- | --- | --- |
| **Terminal de Control** | **Base (B)** | **Base (B)** | **Gate (G)** / Compuerta | **Gate (G)** / Compuerta |
| **Entrada de Flujo** | **Colector (C)** | **Emisor (E)** | **Drain (D)** / Drenador | **Source (S)** / Fuente |
| **Salida de Flujo** | **Emisor (E)** | **Colector (C)** | **Source (S)** / Fuente | **Drain (D)** / Drenador |
| **Sentido del Flujo** | De **C** hacia **E** | De **E** hacia **C** | De **D** hacia **S** | De **S** hacia **D** |
| **¿Cómo se activa?** | Voltaje **(+)** en Base | Voltaje **(-)** en Base | Voltaje **(+)** en Gate | Voltaje **(-)** en Gate |
| **Analogía** | Canilla estándar | Canilla invertida | Interruptor táctil N | Interruptor táctil P |


### Tabla Maestra: BJT, MOSFET e IGBT

| Característica | **BJT (NPN)** | **BJT (PNP)** | **MOSFET (Canal N)** | **MOSFET (Canal P)** | **IGBT (N)** |
| --- | --- | --- | --- | --- | --- |
| **Terminal de Control** | **Base (B)** | **Base (B)** | **Gate (G)** | **Gate (G)** | **Gate (G)** |
| **Entrada de Flujo** | **Colector (C)** | **Emisor (E)** | **Drain (D)** | **Source (S)** | **Colector (C)** |
| **Salida de Flujo** | **Emisor (E)** | **Colector (C)** | **Source (S)** | **Drain (D)** | **Emisor (E)** |
| **Sentido del Flujo** | De **C** a **E** | De **E** a **C** | De **D** a **S** | De **S** a **D** | De **C** a **E** |
| **¿Cómo se activa?** | Voltaje **(+)** | Voltaje **(-)** | Voltaje **(+)** | Voltaje **(-)** | Voltaje **(+)** |
| **Naturaleza** | Corriente | Corriente | Voltaje | Voltaje | Voltaje |


![[transistoresbjtmosfetigbt1.png]]


![[transistoresbjtmosfetigbt2.png]]



### Puntos clave para tu razonamiento

Para que no tengas que memorizar la tabla y solo la **razones**:

1. **La relación entre ellos:**
* El **NPN** es el "hermano" del **Canal N**. Ambos quieren que la corriente salga por el terminal que suena a "origen o salida" (**Emisor / Source**).
* El **PNP** es el "hermano" del **Canal P**. En ambos, la energía entra por donde normalmente saldría en los otros.


2. **El "Gatillo" (Control):**
* Los tipos **N** (NPN y Canal N) son "felices" con el positivo. Les das un empujón positivo y abren la canilla.
* Los tipos **P** (PNP y Canal P) son "rebeldes". Necesitan que el voltaje de control caiga o sea negativo respecto a la entrada para poder conducir.


3. **Identificación por la Flecha (Símbolo):**
* Si la flecha **sale** del transistor (hacia afuera), es un **N** (NPN o Canal N). La corriente busca la salida/tierra.
* Si la flecha **entra** al transistor, es un **P** (PNP o Canal P). La corriente viene desde la fuente de alimentación.



### ¿Cómo usar esto con el multímetro?

* **En BJT:** Si es NPN, la punta **Roja** (positiva) va en la Base para "activar" los diodos internos hacia Colector y Emisor.
* **En MOSFET:** Si es Canal N, la punta **Roja** en la Gate es la que "carga" la compuerta para que el multímetro luego detecte paso entre Drenador y Fuente.




---


![[transistoresbjtmosfetigbt3.png]]


Resumen para el diagnóstico con multímetro (en modo **Diodo**):

### Tabla Maestra de Medición de Transistores de Potencia

| Tipo de Transistor | Terminal (+) Rojo | Terminal (-) Negro | Lectura Típica | Explicación |
| --- | --- | --- | --- | --- |
| **BJT NPN** | **Base** | **Emisor o Colector** | **0.45V - 0.9V** | La Base es el ánodo (+) de los dos diodos internos. |
| **BJT PNP** | **Emisor o Colector** | **Base** | **0.45V - 0.9V** | La Base es el cátodo (-) de los dos diodos internos. |
| **MOSFET Canal N** | **Fuente (S)** | **Drenador (D)** | **0.40V - 0.7V** | Mides el **diodo de cuerpo** interno. |
| **MOSFET Canal P** | **Drenador (D)** | **Fuente (S)** | **0.40V - 0.7V** | Mides el diodo de cuerpo en sentido inverso. |
| **IGBT Canal N** | **Emisor (E)** | **Colector (C)** | **0.40V - 0.8V** | Mides el **diodo de protección** (muy común en soldadoras). |
| **IGBT Canal P** | **Colector (C)** | **Emisor (E)** | **0.40V - 0.8V** | Mides el diodo de protección en sentido opuesto. |


### Notas Cruciales para tu Diagnóstico:

1. **La "Regla del Infinito" (OL):**
* En los **BJT**, si mides entre Colector y Emisor en cualquier sentido, debe dar **OL**.
* En **MOSFET e IGBT**, cualquier medición que involucre la **Comuerta (Gate)** debe dar **OL** (Circuito Abierto). Si el Gate marca algún voltaje con otro pin, el componente está perforado y debes cambiarlo.


2. **El Diodo de Cuerpo:**
* A diferencia de los BJT, los MOSFET e IGBT casi siempre incluyen un diodo entre sus terminales de salida (D-S o C-E). Por eso verás una lectura similar a la de un diodo común en un solo sentido.


3. **Estado de Reposo:**
* Asegúrate de tocar todos los pines con tus dedos o con las puntas del multímetro (unidas) antes de medir, para descargar cualquier carga estática en el Gate que pueda "activar" el transistor accidentalmente durante la prueba.



Nota:
Los transistores BJT: la base entre colector y emisor dependiendo si es pnp o npn debe medir como un diodo
Los transistores MOSFET: el GATE (compuerta que seria como la base de los BJT) no mide con DRAIN y SOURCE pero entre DRAIN (Drenador) Y SOURCE (Fuente) debe medir en un sentido dependiendo si es canal N o P




