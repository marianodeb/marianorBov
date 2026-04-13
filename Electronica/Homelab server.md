
## OpenMediaVault (OMV)

### ¿Qué es?
OpenMediaVault (OMV) es un sistema operativo de red (NAS) de próxima generación basado en Debian Linux. Está diseñado para entornos domésticos o pequeñas empresas. Su objetivo principal es transformar una PC o placa en un servidor de archivos robusto, administrado enteramente desde una interfaz web.

### ¿Cómo funciona?
Funciona montándose sobre un sistema operativo base (Debian) y proporcionando una interfaz gráfica en el navegador para gestionar discos duros, crear carpetas compartidas, configurar usuarios y establecer permisos sin necesidad de tocar la terminal. Administra protocolos de red como SMB/CIFS, FTP y NFS para que los archivos sean accesibles desde cualquier dispositivo conectado al router.

### Instalación
Si ya tenés un sistema Debian limpio funcionando (sin entorno gráfico de escritorio), podés instalar OMV ejecutando un script oficial directamente en la terminal:

```bash
wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash
```
*(También se puede instalar desde cero descargando su imagen ISO e instalándola como un sistema operativo completo).*

### Ejemplos de uso
* **Servidor de copias de seguridad:** Podés configurar un disco duro viejo en OMV y usarlo para guardar copias de seguridad automáticas de tu PC principal.
* **Almacenamiento multimedia:** Crear una carpeta compartida en la red local donde guardás películas o música para reproducirlas desde un Smart TV o el celular.

### Enlaces Oficiales
* **Sitio Web:** [openmediavault.org](https://www.openmediavault.org/)
* **Documentación:** [docs.openmediavault.org](https://docs.openmediavault.org/)
---

## CasaOS

### ¿Qué es?
CasaOS es un sistema de nube personal simple, fácil de usar y elegante, construido alrededor del ecosistema de Docker. A diferencia de OMV o TrueNAS, no es un sistema operativo completo en sí mismo, sino una interfaz web muy pulida que se instala "por encima" de tu distribución de Linux actual.

### ¿Cómo funciona?
CasaOS actúa como un panel de control amigable que simplifica al máximo el uso de Docker. En lugar de escribir comandos complejos en la terminal o armar archivos `docker-compose.yml`, te ofrece una "App Store" donde instalás servicios (como WordPress, Pi-hole, o servidores multimedia) con un solo clic. CasaOS se encarga de descargar la imagen de Docker, configurar los puertos y crear los volúmenes de almacenamiento en segundo plano.

### Instalación
Se instala súper rápido sobre casi cualquier distribución de Linux (Ubuntu, Debian, Raspberry Pi OS) ejecutando un solo comando en la terminal:

```bash
curl -fsSL https://get.casaos.io | sudo bash
```

### Ejemplos de uso
* **Nube personal:** Instalar la aplicación "Nextcloud" desde la tienda de CasaOS con un clic, creando tu propio Google Drive privado.
* **Centro de domótica:** Instalar "Home Assistant" para concentrar y controlar desde un solo lugar todos los sensores de temperatura o relés inteligentes de la casa.
* **Gestor de descargas:** Correr un contenedor de qBittorrent para gestionar descargas 24/7 sin dejar tu computadora de escritorio encendida.

### Enlaces Oficiales
* **Sitio Web:** [casaos.io](https://casaos.io/)
* **GitHub:** [github.com/IceWhaleTech/CasaOS](https://github.com/IceWhaleTech/CasaOS)
---

## TrueNAS (Core / Scale)

### ¿Qué es?
TrueNAS es un sistema operativo de almacenamiento (NAS) de nivel empresarial. A diferencia de CasaOS y OMV, que son más amigables para el usuario de a pie, TrueNAS está fuertemente centrado en el sistema de archivos **ZFS**. Viene en dos sabores principales: *Core* (basado en FreeBSD) y *Scale* (basado en Linux/Debian).

### ¿Cómo funciona?
TrueNAS se instala directamente en el hardware ("bare metal") o en una máquina virtual dedicada con acceso directo a los discos. Utiliza las características avanzadas de ZFS para garantizar la integridad de los datos (evitar que los archivos se corrompan con el tiempo), manejar agrupaciones (pools) de discos duros en diferentes configuraciones de RAID, y crear "snapshots" (fotografías del sistema en un momento dado que permiten recuperar archivos borrados por error al instante).

### Instalación
No se instala a través de un comando sobre otro sistema. Requiere descargar la imagen ISO oficial, "quemarla" en un pendrive y bootear la máquina (o la máquina virtual) desde ahí para formatear el disco principal e instalar el sistema operativo completo.

### Ejemplos de uso
* **Bóveda de datos a prueba de fallos:** Usar TrueNAS con múltiples discos para asegurar que, si un disco duro se rompe físicamente, el sistema siga funcionando sin perder un solo byte de información de tus proyectos o bases de datos importantes.
* **Virtualización y contenedores (TrueNAS Scale):** Levantar máquinas virtuales completas o instalar aplicaciones web alojadas en la misma máquina que maneja los discos, aprovechando la base de Linux.

### Enlaces Oficiales
* **Sitio Web:** [truenas.com](https://www.truenas.com/)
* **Documentación:** [truenas.com/docs/](https://www.truenas.com/docs/)
---

## Home Assistant

### ¿Qué es?
Home Assistant es una plataforma de domótica de código abierto diseñada para ser el cerebro central de un hogar inteligente. Su enfoque principal es la **privacidad** y el **control local**, permitiendo que todos tus dispositivos inteligentes se comuniquen entre sí sin depender obligatoriamente de la nube de los fabricantes.

### ¿Cómo funciona?
Funciona como un traductor universal. Integra miles de dispositivos de distintas marcas (Xiaomi, Philips Hue, Sonoff, Tuya, etc.) bajo una misma interfaz. Utiliza "integraciones" para conectarse a dispositivos vía Wi-Fi, Zigbee o Bluetooth. Te permite crear automatizaciones complejas (ej: "si el sensor de movimiento detecta a alguien y es de noche, encender la luz al 20%") y paneles de control personalizados para ver el estado de tu casa en tiempo real.

### Instalación
Existen varias formas de instalarlo, pero las dos más comunes son:

1. **Home Assistant OS (HAOS):** Es un sistema operativo completo. Ideal para instalar en una Raspberry Pi o una Mini PC dedicada.
2. **Docker:** Ideal si ya usás CasaOS o OMV. Se instala como un contenedor con un solo comando o desde la tienda de aplicaciones:

```bash
docker run -d --name homeassistant --privileged --restart=unless-stopped -v /PATH_TO_YOUR_CONFIG:/config --network=host ghcr.io/home-assistant/home-assistant:stable
```

### Ejemplos de uso
* **Automatización de iluminación:** Configurar que las luces exteriores se enciendan automáticamente al ponerse el sol y se apaguen al amanecer.
* **Monitorización de energía:** Si tenés enchufes inteligentes, podés ver gráficos de consumo eléctrico y recibir alertas si un electrodoméstico consume más de lo debido.
* **Seguridad integrada:** Hacer que, si la cámara detecta un desconocido cuando no hay nadie en casa, te llegue una notificación al celular con la foto del evento.

### Enlaces Oficiales
* **Sitio Web:** [home-assistant.io](https://www.home-assistant.io/)
* **Comunidad (Foro):** [community.home-assistant.io](https://community.home-assistant.io/)

---
Es una de las dudas más comunes al empezar. La elección depende totalmente de cuánto control quieras tener sobre el sistema y qué hardware estés usando. Aquí tenés la comparativa para sumar a tus notas:

---

## Comparativa: Home Assistant OS (HAOS) vs. Home Assistant en Docker

### 1. Home Assistant OS (Sistema Independiente)
Es la forma "oficial" y recomendada para la mayoría. El sistema operativo está diseñado exclusivamente para correr Home Assistant.

* **Ventajas:**
    * **Add-ons:** Tenés una tienda de complementos (Mosquitto MQTT, Zigbee2MQTT, Google Drive Backup) que se instalan y configuran con un clic.
    * **Snapshots Completos:** Podés hacer una copia de seguridad de TODO el sistema (configuración, complementos y datos) y restaurarlo fácilmente.
    * **Gestión de Hardware:** Maneja automáticamente los drivers para antenas Zigbee, Bluetooth o discos externos.
* **Cuándo elegirlo:** Si tenés una **Raspberry Pi** o una **Mini PC dedicada** solo para domótica y querés que sea lo más estable y simple posible.



### 2. Home Assistant en Docker (CasaOS / OMV)
Aquí, Home Assistant es solo una "aplicación" más dentro de tu servidor, compartiendo recursos con otros servicios como Plex o Nextcloud.

* **Ventajas:**
    * **Eficiencia:** Aprovechás un solo hardware para muchas funciones (NAS + Domótica + Nube).
    * **Portabilidad:** Podés mover tu contenedor de un servidor a otro fácilmente si tenés bien organizados los volúmenes de datos.
    * **Control total del host:** Podés seguir usando la terminal de Debian para otras tareas sin las restricciones que impone HAOS.
* **Desventajas:**
    * **Sin Add-ons:** No existe la pestaña de "Add-ons". Si querés usar algo como *Zigbee2MQTT*, tenés que instalarlo como otro contenedor aparte en Docker y conectarlos manualmente.
    * **Curva de aprendizaje:** Requiere entender cómo mapear puertos y dispositivos USB dentro de Docker.
* **Cuándo elegirlo:** Si ya tenés un servidor con **CasaOS o Debian** funcionando 24/7 y no querés comprar otra computadora, o si preferís gestionar vos mismo cada servicio por separado.



### Resumen rápido
| Característica | HAOS (Independiente) | Docker (CasaOS/OMV) |
| :--- | :--- | :--- |
| **Dificultad** | Muy baja | Media |
| **Tienda de Add-ons** | Sí | No (se hace manual) |
| **Copias de seguridad** | Nativas y completas | Manuales (carpetas de config) |
| **Uso de hardware** | Dedicado | Compartido |

---

## Diferencia entre OMV y casaOS

Aunque ambos pueden convivir en el mismo servidor (de hecho, CasaOS se instala muy bien sobre la base Debian de OMV), sus enfoques son muy distintos. Podríamos decir que **OpenMediaVault es el "ingeniero de infraestructura"** y **CasaOS es el "diseñador de experiencia de usuario"**.


### 1. El objetivo principal
* **OpenMediaVault (OMV):** Su prioridad es la **gestión de discos y archivos**. Se enfoca en que tus discos duros estén sanos, en RAID, con permisos de usuario estrictos y compartidos por red de forma profesional (SMB, NFS, FTP).
* **CasaOS:** Su prioridad es la **gestión de aplicaciones**. Se enfoca en que instalar un Plex, un Home Assistant o un Nextcloud sea tan fácil como instalar una app en el celular, sin tocar la terminal.

### 2. Gestión de Almacenamiento
| Característica | OpenMediaVault | CasaOS |
| :--- | :--- | :--- |
| **RAID / Unión de discos** | Nativo y muy potente (puedes combinar varios discos en uno solo). | Muy básico. Solo permite ver carpetas y montar discos individuales. |
| **Permisos de Usuario** | Granulares (quién puede leer, quién puede escribir en cada carpeta). | Simplificados (acceso general para el dueño de la nube). |
| **Sistemas de Archivos** | Soporta EXT4, XFS, JFS y BTRFS con herramientas de chequeo. | Usa lo que ya tenga el disco, no tiene herramientas de reparación. |

### 3. Facilidad de Uso (Docker)
* **OMV:** Para usar Docker, necesitas instalar un plugin (omv-extras) y luego usar una interfaz llamada *Portainer* o escribir archivos `docker-compose.yml`. Es potente pero requiere aprender un poco.
* **CasaOS:** Es el "rey" de Docker para principiantes. Tiene una tienda visual donde hacés clic en "Instalar" y la aplicación aparece en tu pantalla de inicio lista para usar.

### 4. Interfaz Visual
* **OMV:** Es una interfaz de administración clásica: menús laterales, muchas opciones técnicas, tablas de datos y estados del sistema.
* **CasaOS:** Es un "Dashboard" moderno. Te muestra el clima, el estado de la CPU/RAM de forma gráfica y los íconos de tus aplicaciones. Es mucho más amigable para el día a día.

### ¿Cuál elegir?

* **Elegí OpenMediaVault si:** Tenés varios discos duros viejos y querés armar un NAS seguro para guardar fotos familiares o archivos importantes de trabajo, priorizando la integridad de los datos.
* **Elegí CasaOS si:** Querés un centro multimedia o de domótica rápido, donde lo importante es correr aplicaciones y no te preocupa tanto la configuración avanzada de los discos.

**💡 Pro Tip:** Mucha gente (especialmente en Debian) instala primero **OpenMediaVault** para configurar los discos y las carpetas compartidas, y luego instala **CasaOS** encima para tener lo mejor de los dos mundos: la robustez de OMV en el fondo y la facilidad de CasaOS en el frente.

---

## Resume 


## Guía Maestra: Servidor Doméstico y Domótica (Debian Stack)

Esta guía detalla la arquitectura de un servidor basado en **Debian**, gestionado por **OpenMediaVault** para el almacenamiento y **CasaOS** para las aplicaciones, integrando **Home Assistant** como cerebro domótico.



### 1. Arquitectura del Sistema (El Modelo de Capas)
Para un servidor robusto y flexible, no se instala un sistema "dentro" de otro, sino que se construyen capas de software en paralelo sobre una misma base:

* **Capa 1: El Motor (Debian Linux):** El sistema operativo base que interactúa con el hardware. Se recomienda la versión *Netinst* (sin entorno gráfico) para máxima eficiencia.
* **Capa 2: El Chasis (OpenMediaVault):** Se encarga de la infraestructura. Gestiona discos duros, arreglos RAID, salud de las unidades y protocolos de red (SMB/NFS).
* **Capa 3: La Interfaz (CasaOS):** Actúa como un panel de control amigable (Dashboard) para gestionar contenedores Docker y aplicaciones con un solo clic.


### 2. Componentes del Servidor (Notas Técnicas)

### ## OpenMediaVault (OMV)
* **¿Qué es?** Sistema NAS de próxima generación basado en Debian.
* **Función principal:** Transformar hardware en un servidor de archivos profesional administrado vía web.
* **Instalación:** 

```bash
wget -O - https://github.com/OpenMediaVault-Plugin Developers/installScript/raw/master/install | sudo bash
```

* **Uso ideal:** Servidor de copias de seguridad y almacenamiento multimedia masivo.

### ## CasaOS
* **¿Qué es?** Interfaz de "nube personal" centrada en el ecosistema Docker.
* **Función principal:** Simplificar la instalación de servicios (Plex, Nextcloud, AdGuard) mediante una App Store visual.
* **Instalación:**
    ```bash
    curl -fsSL https://get.casaos.io | sudo bash
    ```
* **Uso ideal:** Gestión rápida de contenedores y visualización del estado del servidor (CPU/RAM).

### ## TrueNAS (Alternativa Empresarial)
* **Nota:** A diferencia de OMV/CasaOS, TrueNAS se instala como un sistema operativo completo ("Bare Metal") y se centra en el sistema de archivos **ZFS**. Es ideal para redundancia de datos crítica pero requiere hardware más potente.


### 3. El Cerebro: Home Assistant (HA)

#### ¿Qué es?
Plataforma de domótica de código abierto centrada en la privacidad y el control local. Permite unificar dispositivos de diferentes marcas (Zigbee, Wi-Fi, Bluetooth).

#### Comparativa de Instalación:
| Característica | HAOS (Sistema Independiente) | HA en Docker (CasaOS/OMV) |
| :--- | :--- | :--- |
| **Dificultad** | Muy baja | Media |
| **Add-ons** | Sí (Tienda nativa) | No (Se instalan manual como contenedores) |
| **Backups** | Snapshots totales de un clic | Manuales (Carpetas de configuración) |
| **Uso ideal** | Hardware dedicado (Raspberry Pi) | Servidor compartido (Debian + OMV) |


### 4. Hoja de Ruta: Instalación y Configuración

Para evitar conflictos y asegurar que los datos se guarden en el lugar correcto, seguí este orden:

1.  **Instalar Debian 12:** Configurar el sistema base sin entorno gráfico.
2.  **Instalar OMV:** Ejecutar el script y configurar los discos duros físicos (formateo y montaje).
3.  **Configurar Carpetas Compartidas:** Crear las carpetas en OMV para que la red local las vea.
4.  **Instalar CasaOS:** Ejecutar el script. Al detectar a OMV, CasaOS suele moverse al puerto **81** o **8080**.
5.  **Desplegar Apps:** Instalar Home Assistant o Plex desde CasaOS, apuntando sus rutas de datos a los discos que ya configuraste en OMV.


### 5. Enlaces de Referencia
* **OMV:** [openmediavault.org](https://www.openmediavault.org/)
* **CasaOS:** [casaos.io](https://casaos.io/)
* **Home Assistant:** [home-assistant.io](https://www.home-assistant.io/)
* **TrueNAS:** [truenas.com](https://www.truenas.com/)

---

## **ESPHome** 

Es básicamente el "santo grial" para cualquiera que quiera dominar la domótica sin volverse loco escribiendo miles de líneas de código en C++. Es la herramienta perfecta para darle vida a esos ESP32 y ESP8266 que tienes por ahí.

## ¿Qué es ESPHome?

Es un sistema que te permite crear firmwares personalizados para placas **ESP8266** y **ESP32** de una manera absurdamente sencilla. En lugar de programar, escribes un archivo de configuración **YAML** (muy parecido a lo que se usa en Home Assistant o Docker).

**¿Cómo funciona?**

Tú describes qué sensores o actuadores tienes conectados en ese archivo `.yaml`, y ESPHome se encarga de compilar el código y "flashearlo" (instalarlo) en la placa de forma inalámbrica (OTA) o por USB.

---

## Requerimientos Principales

- **Hardware:** Placas ESP32 o ESP8266 (NodeMCU, Wemos D1 Mini, etc.).
    
- **Software:** Python instalado en tu sistema (si lo usas por línea de comandos).
    
- **Navegador:** Recomendado usar **Google Chrome** o **Microsoft Edge** si planeas usar la interfaz web para el primer flasheo (por el soporte de WebSerial).
    
- **Red:** Conexión Wi-Fi de 2.4 GHz (los ESP no suelen llevarse bien con las de 5 GHz).
    

---

## Instalación en Debian (XFCE)

Como usas **Debian**, tienes varias formas de instalarlo. La más limpia para tu flujo de trabajo es mediante Python o Docker.

### Opción A: Mediante Python (Línea de comandos)

1. Asegúrate de tener Python y el gestor de paquetes:

`sudo apt update && sudo apt install python3-pip python3-venv`

2. Crea un entorno virtual para no ensuciar el sistema:

`python3 -m venv esphome_venv`

3. Actívalo: 

`source esphome_venv/bin/activate`

4. Instala ESPHome: 
 
`pip3 install esphome`


### Opción B: Interfaz Gráfica (Dashboard)

Si prefieres ver todo en el navegador, una vez instalado con el método anterior, solo corre:

`esphome dashboard config/`

Luego entras a `http://localhost:6052` y verás una interfaz muy intuitiva para gestionar tus nodos.

---

## Conexionado y Primeros Pasos

Para conectar tu placa por primera vez:

1. Conecta el ESP32/ESP8266 a un puerto USB de tu PC.
    
2. En el Dashboard de ESPHome, dale a **"New Device"**.
    
3. Configura el nombre y tus credenciales de Wi-Fi.
    
4. Selecciona el tipo de placa.
    
5. Dale a **"Install"** y elige **"Plug into this computer"**.
    

---

## Información Oficial y Recursos

- **Sitio Web Oficial:** [esphome.io](https://esphome.io) (La documentación es excelente y tiene ejemplos para casi cualquier sensor).
    
- **Dispositivos compatibles:** [esphome-configs.io](https://www.google.com/search?q=https://www.esphome-configs.io) (Recetas listas para copiar y pegar).
    

---

## Tips para tu flujo de trabajo (Markdown y Proyectos)

- **Integración con Home Assistant:** Si ya usas Home Assistant, ESPHome aparece mágicamente como una integración una vez que el dispositivo está en la red.
    
- **Documentación en Obsidian:** Te recomiendo crear una nota "Template" en tu **Obsidian** para tus archivos YAML. ESPHome usa una estructura muy lógica que se ve genial en bloques de código de Markdown.
    
- **Uso en el Huerto:** Para tu proyecto de riego, ESPHome tiene un componente llamado `deep_sleep`. Es vital si piensas usar baterías, ya que permite que el ESP32 "duerma" y solo despierte cada 30 minutos para medir la humedad y regar, ahorrando muchísima energía.
    

¿Te gustaría que te ayude a armar el primer archivo YAML para los sensores de humedad de tus bancales?


