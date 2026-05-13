
## **T-CON** (Timing Controller). 
Es una de las piezas más críticas porque es el "cerebro" que decide qué píxel se enciende y con qué color.


### 1. ¿Es lo mismo en TV que en Monitores?
**Sí y no.** * **Función:** Es exactamente la misma. Ambas convierten la señal de video que viene de la placa Main (principal) en señales que el panel LCD/LED pueda entender.
* **Forma física:** En monitores y TVs pequeñas, la T-CON suele estar integrada en la placa "Source" (la regleta larga que va pegada al vidrio del panel). En TVs grandes, suele ser una placa independiente conectada por cables flex.


### 2. Nombres y Siglas Variantes
Dependiendo del fabricante (Samsung, LG, Sony, etc.), podés encontrarla mencionada como:
1.  **T-CON:** Timing Controller (El más común).
2.  **Logic Board:** Usado mucho en diagramas de bloque.
3.  **Control Board:** Referencia genérica al control del panel.
4.  **X-Board / S-Board:** A veces se refieren así cuando está integrada en los flex del panel.


### 3. Funcionamiento General
La T-CON recibe datos en formato **LVDS** (Low Voltage Differential Signaling) o **V-by-One** (en 4K) desde la Main. Su trabajo es procesar esos datos y enviarlos a los **Drivers de Columna** (Source Drivers) y **Drivers de Fila** (Gate Drivers) del panel para formar la imagen.


### 4. Voltajes Críticos (La "Fórmula Mágica")
Si falta uno de estos, la pantalla se queda negra, blanca, con rayas o con efecto "fantasma".

| Sigla | Nombre | Voltaje Aprox. | Origen | Destino / Función |
| :--- | :--- | :--- | :--- | :--- |
| **VIN / VCC** | Voltaje de Entrada | **12V** (TVs) o **5V** (Monitores) | Viene de la Placa Main | Alimenta el fusible de la T-CON y al conversor DC-DC. |
| **VDD / VLOGIC** | Voltaje Digital | **3.3V** | Conversor DC-DC | Alimenta el procesador (Escalador) y la memoria EEPROM. |
| **AVDD / VDA** | Voltaje Analógico | **13V a 17V** | Conversor DC-DC | Alimenta el circuito de corrección Gamma y los Drivers del panel. |
| **VGH / VON** | Gate High | **20V a 32V** | Conversor DC-DC | Es el voltaje para "encender" los transistores del panel. |
| **VGL / VOFF** | Gate Low | **-5V a -10V** (Negativo) | Conversor DC-DC | Es el voltaje para "apagar" los transistores del panel. |
| **VCOM** | Voltaje Común | **5V a 7V** | Circuito VCOM | Voltaje de referencia para los cristales líquidos. Si falla, hay poco contraste o parpadeo. |


### 5. Test Points (Puntos de Prueba)
Para diagnosticar, buscá estos nombres serigrafiados en la placa cerca del integrado conversor DC-DC:

#### **Paso a paso para medir:**
1.  **Fusible de entrada (F1):** Poné el tester en escala de Voltaje DC. Deberías tener 12V (o 5V) en ambos lados del fusible. Si solo hay de un lado, el fusible está volado por un corto.
2.  **Punto VDD / 3.3V:** Verificá que el procesador esté alimentado. Si no está, la placa está "muerta".
3.  **Puntos VGH y VGL:** Son fundamentales. Si VGH no está presente, la imagen puede verse lenta o quedar congelada. Si VGL falta, la pantalla suele verse blanca o con rayas verticales de colores.
4.  **Punto VCOM:** Si tenés imagen pero se ve muy lavada (blanquecina) o con efecto negativo, medí este punto. Suele ser un valor estable cercano a la mitad de AVDD.


### 6. Señales de Datos (LVDS)
No todo es voltaje. Entre la Main y la T-CON viajan pares de cables trenzados. 
* **RX0, RX1, RX2, CLK, RX3:** Son señales de baja amplitud (aprox. 1.2V).
* Si tenés osciloscopio, deberías ver ráfagas de datos. Si no tenés, con el tester en DC deberías medir valores muy similares entre cada par (ej. 1.1V y 1.3V). Si un par mide 0V o 3.3V fijos, la Main está tirando fruta o el cable flex está dañado.


### Resumen para tu cuaderno:
> **Falla típica:** "Prende el backlight (hay luz) pero no hay imagen". 
> **Acción:** Ir directo a la T-CON. Medir fusible -> Medir VDD (3.3V) -> Medir VGH/VGL. Si los voltajes están, el problema puede ser el procesador de la T-CON o el panel mismo en corto.


---


### Tabla Maestra de Equivalencias T-CON

| Función Principal | Sigla Universal / Estándar | Siglas según Fabricante (Samsung, LG, Sony, AUO) | Rango de Voltaje Típico | Notas de Diagnóstico |
| :--- | :--- | :--- | :--- | :--- |
| **Entrada Principal** | **VIN** | **VCC, BIN, V-IN, UVIN** | 12V (TV) / 5V (Monit.) | Si no llega aquí, el fusible (F1) está abierto o la Main no envía señal. |
| **Lógica Digital** | **VDD** | **VCC, VCORE, D-VDD, 3.3V** | 3.3V (a veces 1.2V o 1.8V) | Alimenta el procesador y la EEPROM. Sin esto, la placa no "arranca". |
| **Analógico (Alto)** | **AVDD** | **VDA, V-SOURCE, BDD, VAMP** | 13V a 18V | Si falta, la pantalla suele quedar negra o con líneas grises. |
| **Analógico (Medio)** | **HAVDD** | **HBDD, HABDD, VG-REF** | 7V a 9V (Mitad de AVDD) | Usado para la escala de grises (Gamma). |
| **Gate ON (Encendido)**| **VGH** | **VON, V-GATE, VDDG, VGH_P** | 20V a 32V | Activa los píxeles. Si falta: imagen lenta, congelada o "ghosting". |
| **Gate OFF (Apagado)**| **VGL** | **VOFF, V-OFF, VEEG, VSS** | -5V a -10V (Negativo) | Apaga los píxeles. Si falta: pantalla blanca o con neblina. |
| **Voltaje Común** | **VCOM** | **V-COM, VCM, V-REF** | 5V a 7.5V | Es la referencia del cristal líquido. Si falla: imagen negativa o parpadeo. |



### ¿Quién llama cómo a qué? (Por marcas)

* **Samsung:** Es muy fan de usar **AVDD** y **VON / VOFF**. En sus diagramas más viejos podés encontrar **VADD** (con doble D) para el analógico.
* **LG (Display):** Les encanta usar **VGH** y **VGL**. Para el voltaje analógico suelen usar **VDA**.
* **AUO (AU Optronics):** Estos son los que usan **BDD** y **HBDD** (como viste en el video). También usan mucho la sigla **VCOM** de forma muy clara.
* **Chimei Innolux (CMO):** Suelen usar **VCC** para los 3.3V y **VGH/VGL** para los voltajes de gate.



### Tip de Oro para tus notas: El "Punto de Reposo"
Cuando estés frente a una placa que no tiene ninguna serigrafía (pasa mucho en las chinas genéricas), buscá los **capacitores electrolíticos o cerámicos más grandes** cerca del integrado conversor DC-DC:
1.  El capacitor cerca de la entrada es **VIN**.
2.  El que mide negativo es **VGL**.
3.  El que mide más de 20V es **VGH**.
4.  El que mide entre 13V y 17V es **AVDD**.



### Señales de Control (Bonus)
No olvides que además de los voltajes, hay señales de pulso que podés encontrar como test points:
* **STV:** Inicio de frame (Start Vertical).
* **CPV / CLK:** Señal de reloj para las filas.
* **OE (Output Enable):** Habilita la salida de imagen.


