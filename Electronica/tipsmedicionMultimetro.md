
## ⚠️ Zonas Críticas y Seguridad con el Multímetro

| Zona / Componente | Riesgo | ¿Por qué? | Tip de Seguridad |
| :--- | :--- | :--- | :--- |
| **Colector / Drenador (MOSFET)** | **Extremo** | Picos de "Flyback" de **600V a 1000V** a alta frecuencia. | **NUNCA** midas aquí con la fuente encendida y un multímetro común. |
| **Primario del Chopper** | **Muy Alto** | Ruido de conmutación y alta tensión. | Si necesitas ver si oscila, se usa un osciloscopio con sonda 10x (o más). |
| **Capacitor Principal (Hot)** | **Alto** | Almacena mucha energía incluso desenchufada la fuente. | **Descargalo siempre** con una resistencia o lámpara antes de medir continuidad. |
| **Salida del Chopper (Ánodo)** | **Medio** | Voltaje de alta frecuencia (AC rápida). | El multímetro no llegará a leer la frecuencia real y dará valores erróneos. |
| **Inverters de Backlight (CCFL)** | **Extremo** | Salidas de hasta **1500V AC** en pantallas viejas. | No acerques las puntas; el arco eléctrico puede saltar al tester. |
| **Líneas de Datos (SDA/SCL)** | **Bajo** | Puedes resetear el microprocesador sin querer. | Usa puntas muy finas ("agujas") para no puentear pines accidentalmente. |


### 💡 Tips Extra para tus Notas de Hardware Hacking

* **La Regla de la Mano en el Bolsillo:** Cuando midas en el lado "Caliente" (Hot) con la fuente encendida, mantén una mano en el bolsillo. Esto evita que, en caso de una descarga, la corriente pase por tu pecho (corazón) de un brazo al otro.
* **Diferencia de Tierras:** * Para medir el **Primario**: Punta negra al negativo del capacitor grande.
    * Para medir el **Secundario**: Punta negra al chasis, sintonizador o negativo de capacitores de salida.
    * *Nota: Nunca unas ambas tierras con el multímetro o podrías causar un corto.*
* **Puntas de Prueba:** Si vas a medir componentes SMD (esos chiquititos), ponele una aguja de coser a la punta roja del multímetro con un poco de termocontraíble. Te va a salvar de hacer un corto entre patas de integrados.
* **Modo Continuidad:** Nunca, jamás, uses el modo "pito" (continuidad) o medir Ohms en un circuito que sospeches que tiene capacitores cargados. Es la forma más rápida de quemar el fusible interno o el procesador del tester.

