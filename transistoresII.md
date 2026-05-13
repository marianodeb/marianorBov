Es fundamental entender que para probar la mayoría de los transistores con un multímetro, lo haremos utilizando la función de **Prueba de Diodos (▲|)**.

El multímetro, en este modo, aplica un voltaje pequeño entre las puntas. Dependiendo de si la punta Roja (+) o Negra (-) está en un terminal u otro, "activará" o "bloqueará" el flujo de corriente dentro del transistor, permitiéndonos leer la caída de tensión de las uniones internas de silicio.

---

### Lo que debes saber antes de empezar

1.  **Puntas del Tester:** Roja es Positiva (+), Negra es Común/Negativa (-).
2.  **Modo de Medición:** Gira la perilla a **Diodos (▲|)**.
3.  **Fuera del circuito:** Las pruebas son 100% confiables solo si el transistor está desoldado de la placa.
4.  **Cuando un transistor está MAL:**
    * **Cortocircuito:** El multímetro pita continuamente o marca `0.000`.
    * **Abierto:** Marca `OL` (Open Loop) en todas las combinaciones, incluso donde debería marcar valor.

---

### 1. Transistores Bipolar (BJT) - NPN y PNP

Los BJT se comportan como si fueran **dos diodos unidos por su Base**.

#### Encapsulados Tradicionales (THT - ej. TO-92, TO-220) y SMD (ej. SOT-23)

| Tipo | Punta ROJA (+) en: | Punta NEGRA (-) en: | Lectura Esperada (Modo Diodo) | Interpretación |
| :--- | :--- | :--- | :--- | :--- |
| **NPN** | **Base** | Emisor | **0.500V - 0.700V** | Unión Base-Emisor BIEN |
| | **Base** | Colector | **0.500V - 0.700V** | Unión Base-Colector BIEN |
| | Colector | **Base** | **OL** (Abierto) | Polarización inversa BIEN |
| | Emisor | **Base** | **OL** (Abierto) | Polarización inversa BIEN |
| | Colector | Emisor | **OL** (Abierto) | No hay corto C-E |
| | | | | |
| **PNP** | Emisor | **Base** | **0.500V - 0.700V** | Unión Emisor-Base BIEN |
| | Colector | **Base** | **0.500V - 0.700V** | Unión Colector-Base BIEN |
| | **Base** | Emisor | **OL** (Abierto) | Polarización inversa BIEN |
| | **Base** | Colector | **OL** (Abierto) | Polarización inversa BIEN |
| | Emisor | Colector | **OL** (Abierto) | No hay corto E-C |

* *Tip:* La lectura Base-Emisor suele ser unos milivoltios *más alta* que Base-Colector.
* *Identificación de pines:* En TO-92 (pequeños de plástico), de frente es común E-B-C. En TO-220 (potencia), es B-C-E. **En SMD SOT-23**, de frente con una pata arriba, la de arriba es Colector, abajo-izquierda es Base, abajo-derecha es Emisor (confirma siempre con el código).

---

### 2. Transistores de Efecto de Campo (MOSFET) - Canal N y P

Los MOSFET tienen una estructura distinta. Lo principal a probar es el aislamiento del pin Gate (Puerta) y el diodo interno de protección entre Drain (Drenador) y Source (Surtidor).

#### Encapsulados Tradicionales y SMD

* **Paso 1: Verificar aislamiento de Gate.**
    * Toca con la punta Roja Gate y con la Negra Source. Lectura: **OL**.
    * Toca con la punta Roja Gate y con la Negra Drain. Lectura: **OL**.
    * *Si marca algún valor o pita entre Gate y cualquier otro pin, el MOSFET está destruido.*

* **Paso 2: Probar el Diodo Interno Drain-Source.**

| Tipo | Punta ROJA (+) en: | Punta NEGRA (-) en: | Lectura Esperada (Modo Diodo) | Interpretación |
| :--- | :--- | :--- | :--- | :--- |
| **MOSFET Canal N**| Source | Drain | **0.500V - 0.800V** | Diodo interno BIEN |
| | Drain | Source | **OL** (Abierto) | El MOSFET está apagado (Normal) |
| | | | | |
| **MOSFET Canal P**| Drain | Source | **0.500V - 0.800V** | Diodo interno BIEN |
| | Source | Drain | **OL** (Abierto) | El MOSFET está apagado (Normal) |

---

### 3. Otros Tipos: IGBT y JFET

#### IGBT (Insulated Gate Bipolar Transistor)

El IGBT es híbrido. Se prueba casi igual que un MOSFET de potencia.

* **Paso 1: Aislamiento de Gate.** Igualmente, Gate (G) debe dar **OL** con Colector (C) y con Emisor (E).
* **Paso 2: Diodo Interno Colector-Emisor.** La mayoría de IGBTs de potencia modernos incluyen un diodo de protección.

| Punta ROJA (+) en: | Punta NEGRA (-) en: | Lectura Esperada (Modo Diodo) | Interpretación |
| :--- | :--- | :--- | :--- |
| Emisor | Colector | **0.500V - 0.700V** | Diodo interno BIEN |
| Colector | Emisor | **OL** (Abierto) | IGBT está apagado (Normal) |

#### JFET (Junction Field Effect Transistor)

El JFET es el más diferente. **En su estado normal (sin voltaje en Gate), el canal entre Drain (D) y Source (S) es conductivo.**

* **Paso 1: Canal Drain-Source.**
    * Pon el tester en **Resistencia (Ω)**. Mide entre D y S en ambos sentidos. Debería marcar una resistencia baja y fija (ej. entre 50Ω y 500Ω). No marca OL ni corto total.
* **Paso 2: Gate.**
    * Pon el tester en **Diodos (▲|)**.
    * **JFET Canal N:** Roja en Gate, Negra en Source → Marca como un diodo (~0.6V). Al revés → OL.
    * **JFET Canal P:** Negra en Gate, Roja en Source → Marca como un diodo (~0.6V). Al revés → OL.
