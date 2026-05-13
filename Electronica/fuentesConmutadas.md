
Estructura de **Fuente Conmutada (SMPS)** de TV:


## 1. Módulo de Entrada y Filtro EMI
Es la "aduana" de la energía. Su función es dejar pasar la corriente alterna (AC) de la red y bloquear las interferencias (ruido electromagnético) que la propia fuente genera para que no regresen a tu red eléctrica.

*   **Componentes clave:** Fusible, Varistor (protección), Termistor NTC, Condensadores tipo X e Y, y Bobinas de choque (filtros de línea).
*   **Voltaje:** El de tu toma de corriente (110V o 220V AC).
*   **Cómo identificarlo:** Está justo donde entra el cable de alimentación. Verás bobinas con núcleo de ferrita cuadradas o redondas.


## 2. Etapa Rectificadora y de Filtrado Primario
Convierte la alterna en continua (DC) pulsante y luego la "aplana".

*   **Componentes clave:** Puente de diodos y el condensador electrolítico más grande de toda la placa (el "tanque").
*   **Voltaje esperado:** 
    *   En red de 110V: **~160V DC**.
    *   En red de 220V: **~310V DC**.
*   **Cómo identificarlo:** Busca el puente de cuatro diodos y el capacitor gigante de 400V o 450V.


## 3. Módulo PFC (Power Factor Correction) - El "Boost"
Este es el que mencionabas. Las TVs de más de 32-40 pulgadas lo suelen traer por norma. Eleva el voltaje del condensador principal para que la fuente sea más eficiente.

*   **Tipo de circuito:** Es un convertidor **Boost** (Elevador).
*   **Voltaje esperado:** Con la TV encendida, el voltaje en el condensador principal sube a **380V - 400V DC** constantes.
*   **Cómo identificarlo:** Verás una bobina (inductor) grande cerca del condensador principal y un MOSFET de potencia dedicado solo a esta etapa.


## 4. Módulo de Stand-by
Es una fuente pequeña dentro de la grande. Siempre está encendida para que el procesador reciba la señal del control remoto.

*   **Tipo de circuito:** Generalmente tipo **Flyback**.
*   **Voltaje común:** **5V DC** (o 3.3V en algunos modelos).
*   **Cómo identificarlo:** Busca el transformador chopper más pequeño de la placa.


## 5. Módulo Main/Power (Fuente Principal)
Esta es la que entrega la potencia para el sonido, el procesador y el resto de la placa main cuando sacas la TV de stand-by.

*   **Tipo de circuito:** **Flyback** (en TVs chicas) o **Resonante LLC** (en TVs grandes de alta eficiencia).
*   **Voltajes comunes:** **12V DC** y **24V DC**.
*   **Cómo identificarlo:** Es el transformador chopper mediano o grande.


## 6. Módulo LED Driver (Inverter)
Se encarga de alimentar las tiras de LEDs del backlight.

*   **Tipo de circuito:** Convertidor **Boost** (eleva el voltaje de 12V/24V a lo que necesiten los LEDs).
*   **Voltaje:** Varía mucho según el modelo (**40V hasta 200V+ DC**).
*   **Cómo identificarlo:** Está cerca de los conectores que van hacia la pantalla. Suele tener varios condensadores electrolíticos medianos en fila.


## Tabla de Resumen para Obsidian

| Módulo | Función Principal | Voltaje de Salida (Aprox) | Componente Distintivo |
| :--- | :--- | :--- | :--- |
| **EMI / Filtro** | Filtrar ruido y proteger | 110V / 220V AC | Bobinas de choque y varistor |
| **PFC (Boost)** | Corrección de potencia | 380V - 400V DC | Inductor grande + MOSFET |
| **Stand-by** | Alimentar microprocesador | 5V / 3.3V DC | Transformador Chopper pequeño |
| **Fuente Main** | Audio, Tuner, Mainboard | 12V / 24V DC | Transformador Chopper grande |
| **LED Driver** | Iluminar la pantalla | 40V - 250V DC | Conectores hacia el panel |


### Tips de Diagnóstico Rápido:
1.  **¿No prende ni el foco de stand-by?** Revisa el fusible y los 160V/310V en el filtro gordo.
2.  **¿Prende el foco pero no la TV?** Revisa si están los 5V de stand-by. Si están, verifica si llega la orden "Power-On" desde la main.
3.  **¿Tienes sonido pero no imagen (pantalla negra)?** Lo más probable es que el módulo **LED Driver** o las tiras LED estén fallando. El voltaje de salida del driver debería subir momentáneamente al encender.