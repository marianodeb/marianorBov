
## **`apt-get`**

###  **Definición y Significado**

- **`apt-get`**: Herramienta de **gestión de paquetes** en sistemas basados en Debian/Ubuntu. Es parte del sistema **APT** (*Advanced Package Tool*) y se usa para instalar, actualizar, eliminar paquetes y gestionar repositorios.  
  - **Funcionalidades clave**: Instalación, actualización de paquetes, limpieza de caché, resolución de dependencias.  
  - **Nivel técnico**: Es de **bajo nivel**, ideal para scripts y automatización.  

- **`apt`**: Versión más **moderna y amigable** de APT (introducida en 2014). Combina funciones de `apt-get`, `apt-cache`, y otras herramientas.  
  - **Ventajas**: Interfaz más limpia, barras de progreso, colores, y comandos simplificados.  
  - **Recomendado** para uso diario por usuarios finales.

---

### **Sintaxis**

#### Para `apt-get`:

```bash
sudo apt-get [opciones] <comando> [paquete(s)]
```
#### Para `apt`:

```bash
sudo apt [opciones] <comando> [paquete(s)]
```

---

###  **Opciones y Comandos Principales**

#### **Comandos Comunes (apt-get y apt):**

| Comando           | `apt-get`                          | `apt`                              | Descripción                                  |
|-------------------|------------------------------------|------------------------------------|---------------------------------------------|
| Actualizar lista  | `sudo apt-get update`              | `sudo apt update`                 | Actualiza la lista de paquetes disponibles. |
| Instalar          | `sudo apt-get install <paquete>`   | `sudo apt install <paquete>`      | Instala un paquete.                         |
| Eliminar          | `sudo apt-get remove <paquete>`    | `sudo apt remove <paquete>`       | Elimina un paquete (deja configuraciones).  |
| Eliminar + Config | `sudo apt-get purge <paquete>`     | `sudo apt purge <paquete>`        | Elimina un paquete y sus configuraciones.   |
| Actualizar Sistema| `sudo apt-get upgrade`             | `sudo apt upgrade`                | Actualiza todos los paquetes instalados.    |
| Actualización Full| `sudo apt-get dist-upgrade`        | `sudo apt full-upgrade`           | Actualiza el sistema (maneja dependencias). |
| Limpiar Caché     | `sudo apt-get clean`               | `sudo apt clean`                  | Borra archivos descargados en caché.        |
| Autolimpieza      | `sudo apt-get autoremove`          | `sudo apt autoremove`             | Elimina paquetes huérfanos.                 |

#### **Opciones Adicionales:**

| Opción      | Descripción                                 |
|-------------|---------------------------------------------|
| `-y`        | Confirma automáticamente (yes).             |
| `-q`        | Modo silencioso (quiet).                    |
| `-s`        | Simular acciones sin ejecutarlas (dry-run). |
| `--fix-broken` | Corrige dependencias rotas.               |

---

###  **Ejemplos Simples y Complejos**
#### **1. Actualizar e Instalar un Paquete:**

```bash
# Con apt-get:
sudo apt-get update && sudo apt-get install nginx

# Con apt:
sudo apt update && sudo apt install nginx
```

#### **2. Eliminar Paquete + Configuraciones:**

```bash
# Con apt-get:
sudo apt-get purge firefox

# Con apt:
sudo apt purge firefox
```

#### **3. Actualizar Todo el Sistema:**

```bash
# Con apt-get:
sudo apt-get update && sudo apt-get dist-upgrade -y

# Con apt:
sudo apt update && sudo apt full-upgrade -y
```

#### **4. Limpiar Caché y Paquetes Huérfanos:**

```bash
# Con apt-get:
sudo apt-get autoremove -y && sudo apt-get clean

# Con apt:
sudo apt autoremove -y && sudo apt clean
```

#### **5. Simular Instalación (Dry Run):**

```bash
sudo apt-get install -s python3   # apt-get
sudo apt install -s python3       # apt
```

#### **6. Buscar Paquetes (apt vs apt-cache):**

```bash
# Con apt (moderno):
apt search python

# Con apt-get (usando apt-cache):
apt-cache search python
```

---

### **Consejos Prácticos**

1. **`apt` vs `apt-get`:**  
   - Usa **`apt`** para tareas diarias (es más intuitivo y muestra mejor información).  
   - Usa **`apt-get`** en scripts (por su salida estable y predecible).  

2. **Siempre Actualiza Antes:**  

   Ejecuta `sudo apt update` antes de instalar o actualizar paquetes.  

3. **Manejo de Dependencias:**  

Si hay errores de dependencias, usa:
   
```bash
sudo apt --fix-broken install
```

4. **Evita `-y` en Scripts Críticos:**  

No uses `-y` en entornos donde necesites confirmar acciones manualmente.  

5. **Listar Paquetes Instalados:**  

```bash
apt list --installed    # Con apt
dpkg -l                 # Con dpkg (más detalle)
```

---

###  **Información Adicional**

#### **Diferencias Clave Entre `apt` y `apt-get`:**

| Característica            | `apt-get`                      | `apt`                          |
|---------------------------|--------------------------------|--------------------------------|
| Interfaz                  | Más técnica, sin colores.      | Amigable, con colores y progreso. |
| Comando `search`          | No existe (usa `apt-cache`).   | `apt search <paquete>`.        |
| Comando `show`            | No existe (usa `apt-cache`).   | `apt show <paquete>`.          |
| Comando `list`            | No existe.                     | `apt list --upgradable`.       |
| Manejo de `dist-upgrade`  | `apt-get dist-upgrade`.        | `apt full-upgrade`.            |

#### **Archivos Importantes:**

- **Repositorios:** `/etc/apt/sources.list` y `/etc/apt/sources.list.d/`.  
- **Configuración de APT:** `/etc/apt/apt.conf`.  
- **Caché de Paquetes:** `/var/cache/apt/archives/`.  

#### **Seguridad:**

- **Verificar Firmas:** Los paquetes se firman con GPG. Las claves se gestionan con `apt-key` (aunque está en desuso; ahora se usan archivos en `/etc/apt/trusted.gpg.d/`).  
- **Repositorios Oficiales:** Evita añadir repositorios no verificados.

#### **Historia y Curiosidades:**

- APT fue creado en 1998 para resolver el "infierno de las dependencias" en Debian.  
- `apt` nació para unificar herramientas fragmentadas (`apt-get`, `apt-cache`, etc.).  

---

###  **Notas Finales**

- **Nunca Ejecutes:**  

```bash
sudo apt-get upgrade --force   # Podría romper tu sistema.
```
- **Para Deshacer Cambios:**

Si instalaste algo por error, usa `apt-get remove` o `apt remove`.  

---

## NALA

**`nala`**, un envoltorio moderno y elegante para `apt`/`apt-get` en sistemas basados en **Debian/Ubuntu**. Es ideal para quienes buscan una experiencia más fluida y visual en la gestión de paquetes. ¡Vamos con los detalles!

### 📌 **Definición y Significado**

**`nala`** es un **front-end para APT** diseñado para ser más rápido, intuitivo y visual que `apt` o `apt-get`.  
- **Características destacadas**:  
  - Descargas en **paralelo** (acelera la instalación).  
  - Interfaz **colorida** y formateada.  
  - **Historial de transacciones** detallado.  
  - **Resolución inteligente de dependencias**.  
  - Soporte para **rollback** (deshacer operaciones).  
- **Origen**: Creado por **Volian** (equipo detrás de Ubuntu Nala), inspirado en `dnf` (Fedora) y `pacman` (Arch).  

---

### **Sintaxis**

```bash
sudo nala [comando] [opciones] [paquetes]
```

---

### **Comandos y Opciones Principales**

#### **Comandos Esenciales:**

| Comando              | Descripción                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| `nala update`        | Actualiza la lista de paquetes (como `apt update`).                         |
| `nala upgrade`       | Actualiza todos los paquetes instalados.                                    |
| `nala install`       | Instala uno o más paquetes.                                                 |
| `nala remove`        | Elimina paquetes (similar a `apt remove`).                                  |
| `nala purge`         | Elimina paquetes y sus configuraciones.                                     |
| `nala autoremove`    | Elimina paquetes huérfanos.                                                 |
| `nala clean`         | Limpia la caché de paquetes descargados.                                    |
| `nala fetch`         | Configura repositorios y espejos (mirrors) automáticamente.                 |
| `nala history`       | Muestra el historial de operaciones y permite **rollback**.                 |
| `nala list`          | Lista paquetes instalados o disponibles.                                    |
| `nala search`        | Busca paquetes en los repositorios.                                         |
| `nala show`          | Muestra información detallada de un paquete.                                |

#### **Opciones Útiles:**

| Opción                  | Descripción                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| `-y`, `--assume-yes`    | Confirma automáticamente todas las preguntas.                               |
| `-v`, `--verbose`       | Modo detallado (muestra más información).                                   |
| `--no-update`           | No actualiza la lista de paquetes antes de operar.                          |
| `--remove-essential`    | Permite eliminar paquetes esenciales (¡usar con cuidado!).                   |
| `--raw-dpkg`            | Ejecuta `dpkg` sin modificar la salida.                                     |
| `--download-only`       | Descarga paquetes sin instalarlos.                                          |
| `--format <formato>`    | Personaliza el formato de salida (ej: `json`, `plain`, `pretty`).           |

---

### **Ejemplos Simples y Complejos**

#### **1. Instalar Paquetes con Descargas en Paralelo:**

```bash
sudo nala install neofetch htop -y
```

#### **2. Actualizar el Sistema con Interfaz Visual:**

```bash
sudo nala update && sudo nala upgrade -y
```

#### **3. Buscar y Mostrar Información de un Paquete:**

```bash
nala search "python3*"    # Busca paquetes que coincidan
nala show python3         # Detalles del paquete
```

#### **4. Eliminar Paquetes y Limpiar Caché:**

```bash
sudo nala remove firefox --purge && sudo nala autoremove -y
```

#### **5. Rollback (Deshacer una Operación):**

```bash
sudo nala history          # Muestra el historial con IDs
sudo nala history undo 5   # Deshace la transacción con ID 5
```

#### **6. Configurar Espejos Rápidos (Mirrors):**

```bash
sudo nala fetch --auto     # Selecciona automáticamente el mirror más rápido
```

#### **7. Descargar Paquetes sin Instalar:**

```bash
sudo nala install docker.io --download-only
```

---

### 💼 **Consejos Prácticos**

1. **Instalar Nala**:

   Si no lo tienes, usa:
     
```bash
sudo apt install nala  # En Debian/Ubuntu
```

2. **Rollback Seguro**:

Usa `nala history` para ver IDs de transacciones antes de deshacer cambios.  

3. **Espejos Rápidos**:

Ejecuta `nala fetch` periódicamente para optimizar la velocidad de descarga.  

4. **Formato JSON**:

   Ideal para integrar con scripts:
   
```bash
nala search python3 --format json
```

5. **Alias para Nala**:

   Agrega esto a tu `.bashrc` para reemplazar `apt`:
   
```bash
alias apt='nala'
```

6. **Evita `--remove-essential`**:

Podría dejar tu sistema inutilizable si eliminas paquetes críticos.

---

### **Información Adicional**

#### **Diferencias Clave con `apt`/`apt-get`:**

| Característica          | `nala`                                  | `apt`/`apt-get`                     |
|-------------------------|-----------------------------------------|--------------------------------------|
| **Interfaz**            | Colorida, con resumen post-operación.   | Más básica, sin colores (en `apt-get`). |
| **Descargas**           | Paralelas (más rápidas).                | Secuenciales.                        |
| **Historial**           | Detallado con opción de rollback.       | No tiene historial integrado.        |
| **Resolución de Dependencias** | Más clara y visual.              | Técnica, sin formato amigable.       |
| **Configuración de Mirrors** | Comando `fetch` integrado.       | Requiere herramientas externas.      |

#### **Archivos de Configuración:**

- **Configuración Global**: `/etc/nala/nala.conf`.  
- **Historial de Transacciones**: `/var/lib/nala/history.json`.  
- **Espejos (Mirrors)**: `/etc/apt/sources.list.d/nala-sources.list`.  

#### **Ventajas de Nala:**

- Muestra un **resumen post-instalación** (tiempo, tamaño de descarga).  
- Soporta **autocompletado** en Bash/Zsh.  
- **Menos propenso a errores** en dependencias complejas.  

#### **Limitaciones:**

- No es compatible con **todas las opciones de `apt`** (ej: `apt-add-repository`).  
- Menos recomendado para **scripts antiguos** (mejor usar `apt-get`).  

---

### ⚡ **Curiosidades**

- **Nombre**: "Nala" viene del personaje de *El Rey León*, simbolizando elegancia y eficacia.  
- **Inspiración**: Combina lo mejor de `apt`, `dnf`, y `pacman`.  

---

## **`apt-key`**, **`apt-mark`**, y **`apt-cache`**


### **1. `apt-key` (Gestión de claves GPG)**  

#### **Definición y Significado**  
- **`apt-key`**: Herramienta para gestionar claves GPG que verifican la autenticidad de repositorios APT.  
  - **Importante**: Está **obsoleto** en sistemas modernos (Debian 11+/Ubuntu 22.04+). Ahora se usan archivos en `/etc/apt/trusted.gpg.d/`.  
  - **Uso histórico**: Añadía/eliminaba claves para confiar en repositorios externos.  

#### **Sintaxis (Obsoleta)**

```bash
sudo apt-key [opción] [archivo_clave.asc]  
```

#### **Opciones Principales**

| Opción          | Descripción                                  |  
|-----------------|----------------------------------------------|  
| `add`           | Añade una clave GPG desde un archivo.        |  
| `del`           | Elimina una clave por su ID.                 |  
| `list`          | Lista todas las claves almacenadas.          |  
| `adv`           | Operaciones avanzadas (ej: actualizar claves). |  

#### **Ejemplos**  
- **Añadir clave GPG (antiguo método)**:

```bash  
sudo apt-key add archivo_clave.asc  
```
  
- **Listar claves**:

```bash  
sudo apt-key list  
```

#### **Método Moderno (Recomendado)**

```bash  
# Copiar la clave a /etc/apt/trusted.gpg.d/  
sudo cp mi_clave.gpg /etc/apt/trusted.gpg.d/  
```

#### **Consejos**

- **No uses `apt-key`**: En sistemas nuevos, usa archivos `.gpg` o `.asc` en `/etc/apt/trusted.gpg.d/`.  
- **Verificar claves**: Descarga claves desde fuentes oficiales (ej: `wget -O- URL | gpg --dearmor > clave.gpg`).  

---

## **2. `apt-mark` (Gestionar estados de paquetes)**

#### **Definición y Significado**

- **`apt-mark`**: Herramienta para marcar paquetes como **manualmente instalados**, **retenidos** (no actualizables), o **automáticos**.  

#### **Sintaxis**

```bash  
sudo apt-mark [opción] [paquete1 paquete2 ...]  
```

#### **Opciones Principales**

| Opción          | Descripción                                  |  
|-----------------|----------------------------------------------|  
| `hold`          | Bloquea un paquete para evitar actualizaciones. |  
| `unhold`        | Desbloquea un paquete retenido.              |  
| `auto`          | Marca un paquete como instalado automáticamente. |  
| `manual`        | Marca un paquete como instalado manualmente. |  
| `showhold`      | Lista todos los paquetes retenidos.          |  

#### **Ejemplos**

- **Evitar que se actualice el kernel**:

```bash  
sudo apt-mark hold linux-image-generic  
```
- **Listar paquetes retenidos**:

```bash  
sudo apt-mark showhold  
```
  
- **Marcar paquete como automático**:

```bash  
sudo apt-mark auto nginx  
```

#### **Consejos**

- **Paquetes esenciales**: No retengas paquetes críticos (ej: `systemd`).  
- **Alternativa a `hold`**: Usa `apt-mark hold` en lugar de editar `/etc/apt/preferences.d/` manualmente.  

---

##  **3. `apt-cache` (Consultar información de paquetes)**

#### **Definición y Significado**

- **`apt-cache`**: Herramienta para **buscar y mostrar información** de paquetes en repositorios (sin modificar el sistema).  

#### **Sintaxis**
 
```bash  
apt-cache [comando] [opciones] [patrón_o_paquete]  
```

#### **Comandos Principales**

| Comando          | Descripción                                  |  
|------------------|----------------------------------------------|  
| `search`         | Busca paquetes por nombre o descripción.     |  
| `show`           | Muestra detalles de un paquete (versión, dependencias, etc.). |  
| `policy`         | Muestra la prioridad de instalación y versión disponible. |  
| `depends`        | Lista las dependencias de un paquete.        |  
| `rdepends`       | Lista paquetes que dependen del especificado. |  

#### **Ejemplos**

- **Buscar paquetes de Python**:

```bash  
apt-cache search python3  
```
  
- **Ver detalles de `nginx`**:

```bash  
apt-cache show nginx  
```
  
- **Ver dependencias de `firefox`**:

```bash  
apt-cache depends firefox  
```
  
- **Ver políticas de versión**:

```bash  
apt-cache policy nginx  
```

#### **Consejos**

- **Filtrar búsquedas**: Usa `grep` para resultados específicos:

```bash  
apt-cache search "editor de texto" | grep -i "markdown"  
```
  
- **Alternativa moderna**: `apt show` y `apt search` reemplazan algunas funciones de `apt-cache`.  

---

#### **Información Adicional**

##### **Diferencias Entre `apt-cache` y `apt`**

| Función               | `apt-cache`                  | `apt`                          |  
|-----------------------|------------------------------|--------------------------------|  
| Buscar paquetes       | `apt-cache search`           | `apt search`                   |  
| Mostrar detalles      | `apt-cache show`             | `apt show`                     |  
| Políticas de versión  | `apt-cache policy`           | No tiene equivalente directo.  |  

##### **Casos de Uso Avanzados**

- **Ver conflictos de paquetes**:

```bash  
apt-cache showsrc <paquete> | grep Conflict
```
  
- **Listar todos los paquetes disponibles**:

```bash  
apt-cache pkgnames 
```






