


### **`systemd`: Explicación y Funcionamiento**

**Definición:**

`systemd` es un sistema de inicialización y gestor de servicios para sistemas operativos basados en Linux. Reemplaza a los antiguos sistemas de inicio como SysVinit y Upstart, y proporciona una manera estandarizada y eficiente de gestionar el arranque del sistema, servicios, y procesos.

**Funcionamiento:**

`systemd` gestiona el arranque y la ejecución de servicios del sistema y procesos en un entorno de Linux. Utiliza archivos de unidad para definir cómo se deben iniciar, detener y gestionar estos servicios. También proporciona mecanismos para gestionar dependencias entre servicios, ordenar el arranque, y manejar el registro de eventos del sistema.

**Componentes Clave:**

- **Unidad:** Es un archivo de configuración que describe un servicio, socket, dispositivo, montaje, etc. Existen varios tipos de unidades, como `.service` para servicios, `.socket` para sockets, `.target` para objetivos, entre otros.
- **Journal:** Un sistema de registro que captura los logs del sistema y servicios, accesible mediante `journalctl`.
- **Manager:** El proceso principal (`systemd`) que coordina la inicialización del sistema y la gestión de servicios.

## **Comandos Básicos de `systemd`:**

`systemd` no se usa directamente en la línea de comandos; en su lugar, se interactúa con él a través de herramientas como `systemctl`. Sin embargo, a continuación te presento algunos comandos relacionados que son útiles para la administración de `systemd` y sus componentes:

1. **Mostrar el estado de `systemd`:**

```bash
systemctl status
```
   Muestra el estado del sistema, indicando si `systemd` está activo y funcionando.

2. **Mostrar las unidades de `systemd` en ejecución:**

```bash
systemctl list-units
```
   Muestra una lista de todas las unidades que están actualmente activas.

3. **Mostrar todas las unidades conocidas por `systemd`:**

```bash
systemctl list-unit-files
```
   Muestra una lista de todos los archivos de unidades y su estado (habilitado, deshabilitado, etc.).
   
   **Buscar servicios por palabras clave:**
   
    systemctl list-units --type=service | grep nombre_o_palabra_clave: Si tienes una idea del nombre del servicio o alguna palabra
    clave relacionada, puedes filtrar la lista utilizando el comando grep. Por ejemplo, para buscar servicios relacionados con la red:

```bash
systemctl list-units --type=service | grep network.
```
4. **Recargar la configuración de `systemd`:**

```bash
sudo systemctl daemon-reload
```
Recarga los archivos de configuración de `systemd` después de realizar cambios.

5. **Mostrar la versión de `systemd`:**

```bash
systemctl --version
```
Muestra la versión instalada de `systemd`.

6. **Iniciar o detener unidades específicas:**

```bash
sudo systemctl start nombre_de_la_unidad
sudo systemctl stop nombre_de_la_unidad
```

Inicia o detiene una unidad específica.

7. **Reiniciar o recargar unidades específicas:**

```bash
sudo systemctl restart nombre_de_la_unidad
sudo systemctl reload nombre_de_la_unidad
```

Reinicia o recarga la configuración de una unidad específica.

8. **Habilitar o deshabilitar unidades para el inicio automático:**

```bash
sudo systemctl enable nombre_de_la_unidad
sudo systemctl disable nombre_de_la_unidad
```

Configura una unidad para que se inicie automáticamente al arrancar el sistema, o evita que lo haga.

9. **Verificar el estado de las unidades y dependencias:**

```bash
systemctl list-dependencies nombre_de_la_unidad
```

Muestra las unidades dependientes de una unidad específica.

10. **Mostrar los logs del sistema y servicios:**

```bash
journalctl
```

Muestra los registros del sistema almacenados en el Journal.

### **Diferencia entre `systemd` y `systemctl`**

- **`systemd`:**
  - **Propósito:** `systemd` es el sistema de inicialización y gestor de servicios en Linux. Es responsable de arrancar el sistema, gestionar servicios, y mantener el estado del sistema.
  - **Función Principal:** Coordina la inicialización del sistema, la gestión de servicios, la supervisión de procesos y el registro de eventos.
  - **Comandos Directos:** Los comandos directos como `systemd-analyze` y `systemd-cgtop` están más orientados a la administración de `systemd` en sí.

- **`systemctl`:**
  - **Propósito:** `systemctl` es una herramienta de la línea de comandos utilizada para interactuar con `systemd`. Permite gestionar y controlar los servicios y unidades que `systemd` maneja.
  - **Función Principal:** Ejecuta comandos para iniciar, detener, reiniciar y consultar el estado de servicios y unidades bajo la gestión de `systemd`.
  - **Comandos Típicos:** `start`, `stop`, `restart`, `status`, `enable`, `disable`.

En resumen, **`systemd`** es el sistema que gestiona el arranque del sistema y la administración de servicios, mientras que **`systemctl`** es una herramienta de interfaz de línea de comandos que permite a los usuarios interactuar con `systemd` para controlar y consultar el estado de servicios y unidades.


## SYSTEMCTL


**`systemctl`:**

`systemctl` es una herramienta de la línea de comandos que se utiliza en sistemas operativos basados en Linux que utilizan el sistema de inicialización `systemd`. `systemd` es el sistema de inicio y gestión de servicios más común en muchas distribuciones modernas de Linux.

### Funcionamiento

`systemctl` se usa para controlar el estado de los servicios del sistema y gestionar el sistema en general. Permite iniciar, detener, reiniciar y verificar el estado de los servicios y unidades (unidades de servicio, montajes, dispositivos, etc.).

### Comandos básicos de `systemctl`

1. **Iniciar un servicio:**

```bash
sudo systemctl start nombre_del_servicio
```

Inicia el servicio especificado.

2. **Detener un servicio:**

```bash
sudo systemctl stop nombre_del_servicio
```

Detiene el servicio especificado.

3. **Reiniciar un servicio:**

```bash
sudo systemctl restart nombre_del_servicio
```

Reinicia el servicio especificado.

4. **Recargar la configuración de un servicio:**

```bash
sudo systemctl reload nombre_del_servicio
```

Recarga la configuración del servicio sin reiniciarlo.

5. **Verificar el estado de un servicio:**

```bash
sudo systemctl status nombre_del_servicio
```

Muestra el estado actual del servicio, incluyendo si está activo o inactivo y cualquier mensaje de error.

6. **Habilitar un servicio para que se inicie automáticamente al arrancar el sistema:**

```bash
sudo systemctl enable nombre_del_servicio
```

Configura el servicio para que se inicie automáticamente en el arranque.

7. **Deshabilitar un servicio para que no se inicie automáticamente al arrancar el sistema:**

```bash
sudo systemctl disable nombre_del_servicio
```

Evita que el servicio se inicie automáticamente en el arranque.

8. **Mostrar todos los servicios activos:**

```bash
systemctl list-units --type=service
```

Lista todos los servicios que están actualmente activos.

9. **Mostrar todos los servicios (activos e inactivos):**

```bash
systemctl list-unit-files --type=service
```

Muestra una lista de todos los archivos de unidades de servicio y sus estados.

10. **Ver los logs de un servicio:**

```bash
journalctl -u nombre_del_servicio
```

Muestra los registros del servicio especificado.

11. **Mostrar el estado del sistema:**

```bash
systemctl status
```

Proporciona una visión general del estado del sistema.
    
12. **Reinicia el servicio si falla:**

```bash
systemctl reset-failed nombre_del_servicio
```

### Ejemplos adicionales

- **Reiniciar el sistema:**

```bash
sudo systemctl reboot
```

- **Apagar el sistema:**

```bash
sudo systemctl poweroff
```

para obtener más información `man systemctl`


Journalctl

## journalctl

**Definición:**
`journalctl` es una herramienta de la línea de comandos para consultar y visualizar los registros almacenados en el Journal, que es el sistema de gestión de logs de `systemd`. Los registros pueden incluir mensajes del sistema, mensajes del kernel, y logs de servicios.

**Funcionamiento:**
`journalctl` permite consultar, filtrar y analizar los registros del sistema de una manera estructurada y eficiente. A diferencia de los logs basados en archivos tradicionales, el Journal proporciona una interfaz binaria que facilita búsquedas avanzadas y consultas en tiempo real.

**Comandos Básicos:**

1. **Ver todos los registros:**

```bash
journalctl
```

Muestra todos los registros almacenados en el Journal.

2. **Ver los registros de un servicio específico:**

```bash
journalctl -u nombre_del_servicio
```

Muestra los registros del servicio especificado por su nombre.

3. **Ver los registros más recientes:**

```bash
journalctl -e
```

Muestra los registros más recientes, desplazándose hasta el final.

4. **Ver registros desde una fecha específica:**

```bash
journalctl --since "YYYY-MM-DD HH:MM:SS"
```

Muestra los registros desde la fecha y hora especificadas.

5. **Ver registros hasta una fecha específica:**

```bash
journalctl --until "YYYY-MM-DD HH:MM:SS"
```

Muestra los registros hasta la fecha y hora especificadas.

6. **Ver registros dentro de un rango de fechas:**

```bash
journalctl --since "YYYY-MM-DD HH:MM:SS" --until "YYYY-MM-DD HH:MM:SS"
```

Muestra los registros dentro del rango de fechas y horas especificado.

7. **Mostrar los registros en tiempo real:**

```bash
journalctl -f
```

Muestra los registros en tiempo real, similar a `tail -f` en archivos de log.

8. **Mostrar los registros del arranque actual:**

```bash
journalctl -b
```

Muestra los registros desde el último arranque del sistema.

9. **Mostrar los registros del arranque anterior:**

```bash
journalctl -b -1
```

Muestra los registros del arranque anterior.

10. **Mostrar registros de una prioridad específica:**

```bash
journalctl -p prioridad
```

Donde `prioridad` puede ser `emerg`, `alert`, `crit`, `err`, `warning`, `notice`, `info`, `debug`.

11. **Mostrar el ID del boot (arranque) actual:**

```bash
journalctl --list-boots
```

Muestra una lista de arranques anteriores junto con su ID.

12. **Mostrar logs de un usuario específico:**

```bash
journalctl _UID=numero_de_usuario
```

Muestra los registros asociados con un UID específico.

13. **Mostrar logs relacionados con una unidad específica por PID:**

```bash
journalctl _PID=numero_de_pid
```

Muestra los registros relacionados con un PID específico.

14. **Mostrar logs relacionados con una unidad específica por nombre de unidad:**

```bash
journalctl -u nombre_del_servicio
```

Muestra los registros de una unidad específica.

15. **Mostrar logs con un filtro de campo específico:**

```bash
journalctl _FIELD=valor
```

Muestra los registros que contienen un campo específico con un valor dado.

### **Diferencia entre `systemctl` y `journalctl`**

- **`systemctl`:**
  - **Propósito:** Gestión de servicios y del sistema bajo `systemd`.
  - **Función Principal:** Controlar el estado de los servicios (iniciar, detener, reiniciar), habilitar o deshabilitar servicios, y mostrar el estado del sistema.
  - **Comandos Típicos:** `start`, `stop`, `restart`, `status`, `enable`, `disable`, `list-units`, `list-unit-files`.

- **`journalctl`:**
  - **Propósito:** Consultar y visualizar registros de logs del sistema y servicios.
  - **Función Principal:** Consultar y analizar registros generados por el sistema y los servicios, filtrando por fecha, servicio, prioridad, entre otros.
  - **Comandos Típicos:** `-u`, `--since`, `--until`, `-f`, `-b`, `--list-boots`, `-p`, `_UID`, `_PID`.


---

## **Guía de Gestión de Servicios con `systemctl`**

### **1. ¿Qué es `systemctl`?**

- **Herramienta principal** para administrar servicios en sistemas Linux basados en `systemd` (la mayoría de distribuciones modernas, incluida Raspberry Pi OS).
- Controla el **ciclo de vida** de servicios: inicio, detención, reinicio, habilitación al arranque, etc.

---

### **2. Comandos Básicos Universales (aplican a *cualquier* servicio)**

| **Comando**                          | **Descripción**                                                                 |
|--------------------------------------|---------------------------------------------------------------------------------|
| `sudo systemctl start <servicio>`    | Inicia el servicio *ahora mismo*.                                               |
| `sudo systemctl stop <servicio>`     | Detiene el servicio *ahora mismo*.                                              |
| `sudo systemctl restart <servicio>`  | Reinicia el servicio (ideal tras cambios de configuración).                     |
| `sudo systemctl reload <servicio>`   | Recarga la configuración *sin reiniciar* (si el servicio lo permite).           |
| `sudo systemctl enable <servicio>`   | Habilita el inicio automático **al reiniciar el sistema**.                      |
| `sudo systemctl disable <servicio>`  | Deshabilita el inicio automático.                                               |
| `sudo systemctl status <servicio>`   | Muestra el estado actual (activo/inactivo, habilitado, logs recientes, etc.).   |
| `sudo systemctl is-enabled <servicio>` | Verifica si el servicio está habilitado para iniciar al arranque.             |

---

### **3. Estados Clave en `systemctl status`**

Al ejecutar `systemctl status <servicio>`, fíjate en:

#### **A. `Loaded`**

- **`enabled`**: El servicio se iniciará **automáticamente al arrancar el sistema**.
- **`disabled`**: No se inicia automáticamente.
- **`preset: enabled`**: El paquete trae por defecto la habilitación, pero puede estar anulada.

#### **B. `Active`**

- **`active (running)`**: El servicio está funcionando.
- **`inactive (dead)`**: El servicio está detenido.
- **`failed`**: Falló al iniciar (revisa logs con `journalctl -u <servicio>`).

---

### **4. Ejemplos Prácticos para Distintos Servicios**

#### **A. Servicio Web (Nginx/Apache)**

```bash
# Iniciar y habilitar Nginx al arranque:
sudo systemctl enable --now nginx

# Verificar estado:
systemctl status nginx

# Si hay un error, ver logs:
journalctl -u nginx -xe
```

#### **B. Base de Datos (MySQL/MariaDB)**

```bash
# Iniciar MySQL:
sudo systemctl start mysql

# Habilitar para que inicie automáticamente:
sudo systemctl enable mysql

# Ver puertos en uso (para confirmar que está escuchando):
sudo ss -tulnp | grep mysql
```

#### **C. Docker**

```bash
# Habilitar Docker al arranque:
sudo systemctl enable docker

# Iniciar Docker ahora:
sudo systemctl start docker

# Ver contenedores en ejecución:
docker ps
```

#### **D. Servicio Personalizado (ej: un script Python)**

1. Crea un archivo de servicio en `/etc/systemd/system/mi-script.service`:

```ini
   [Unit]
   Description=Mi Script Python

   [Service]
   ExecStart=/usr/bin/python3 /ruta/al/script.py
   Restart=on-failure

   [Install]
   WantedBy=multi-user.target
```

2. Recarga systemd y gestiona el servicio:

```bash
sudo systemctl daemon-reload
sudo systemctl start mi-script
sudo systemctl enable mi-script
```

---

### **5. Recomendaciones y Buenas Prácticas**

1. **Siempre verifica el estado tras modificar un servicio**:

```bash
systemctl status <servicio>
```
   
2. **Usa `journalctl` para depurar errores**:

```bash
journalctl -u <servicio> -xe  # Muestra logs detallados del servicio.
```

3. **No habilites servicios innecesarios** por seguridad y rendimiento.
4. **Haz copias de seguridad de archivos de configuración** antes de editarlos:

```bash
sudo cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.backup
```

5. **Conoce los puertos** que usan tus servicios:

```bash
sudo ss -tulnp  # Lista todos los puertos en uso y sus servicios.
```

---

### **6. Flujo de Trabajo Típico al Instalar un Servicio**

1. **Instala el paquete**:

```bash
sudo apt install <paquete>
```

2. **Inicia el servicio**:

```bash
sudo systemctl start <servicio>
```

3. **Habilita el inicio automático**:

```bash
sudo systemctl enable <servicio>
```

4. **Configura el firewall** (si es necesario):

```bash
sudo ufw allow 80/tcp  # Ejemplo: permite tráfico HTTP en Nginx.
```

---

### **7. Comandos Adicionales Útiles**

- **Listar todos los servicios**:

```bash
systemctl list-unit-files --type=service
```

- **Ver servicios activos**:

```bash
systemctl list-units --type=service --state=running
```

- **Mascarar un servicio** (evitar que se inicie manual o automáticamente):

```bash
sudo systemctl mask <servicio>
```

---

### **8. Ejemplo de Notas para Obsidian**

```markdown
## Gestión de Servicios en Linux (`systemctl`)

### Comandos Clave
- Iniciar: `sudo systemctl start <servicio>`
- Habilitar al arranque: `sudo systemctl enable <servicio>`
- Estado: `systemctl status <servicio>`

### Casos de Uso
- **Nginx**: 
  - `sudo systemctl enable --now nginx`
  - Puerto: 80/TCP
- **MySQL**: 
  - Logs: `journalctl -u mysql`
  - Reiniciar tras cambios: `sudo systemctl restart mysql`

### Enlaces Relacionados
- [Documentación Oficial de systemd](https://www.freedesktop.org/wiki/Software/systemd/)
```

---

### **9. Recursos Extra**

- **Libro recomendado**: *"The Linux Command Line"* de William Shotts (capítulo sobre systemd).
- **Curso gratuito**: [Linux Administration en freeCodeCamp](https://www.freecodecamp.org/learn/).
- **Cheat Sheet**: [Descargar PDF de comandos systemctl](https://cheatography.com/tme520/cheat-sheets/systemd/).

---


