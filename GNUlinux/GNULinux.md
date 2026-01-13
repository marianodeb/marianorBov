
## **1. GNU**

### ** Origen y Etimología**  

- **Nombre**: "**GNU**" significa *"GNU's Not Unix"* (un acrónimo recursivo, como un chiste técnico).  
- **Creador**: **Richard Stallman** (1983).  
- **Filosofía**: Promover el **software libre** (libertad de uso, modificación y distribución).  
- **Objetivo**: Crear un sistema operativo **100% libre** y compatible con Unix, pero sin usar código propietario.  

### **⚙️ Componentes clave**  

- Herramientas básicas: `GCC` (compilador), `Glibc` (biblioteca C), `Bash` (shell), `Coreutils` (comandos como `ls`, `cp`).  
- **Problema**: Para 1990, GNU tenía casi todo… excepto el **kernel** (núcleo del sistema).  



## **2. Linux**  

### ** Origen y Etimología**  

- **Nombre**: Viene de **Linus Torvalds** (su creador) + **Unix** (el sistema que imitaba).  
- **Creador**: Linus Torvalds (1991), un estudiante finlandés.  
- **Filosofía**: Pragmática (eficiencia técnica > ideología). Originalmente, **no era software libre** (Torvalds lo licenció bajo GPL más tarde).  
- **Objetivo**: Crear un kernel gratuito para PCs de la época (i386).  

### **⚙️ Características**  

- **Kernel monolítico** (gestiona hardware, memoria, procesos).  
- Se combinó con herramientas GNU para formar un **sistema operativo completo**.  

## **3. GNU/Linux**  

### ** Origen**  

- **Unión** del kernel **Linux** + herramientas **GNU** = Sistema operativo funcional (años 90).  
- **Controversia**: Stallman insiste en llamarlo **"GNU/Linux"** porque Linux solo es el kernel, y el resto son herramientas GNU. Muchos lo llaman simplemente "Linux".  

### **Distribuciones**  

- Combinan GNU/Linux + software adicional: **Debian**, **Fedora**, **Ubuntu**, etc.  


## **4. Software Libre (Free Software)**  

### **Filosofía**  

- **Definición**: Software que respeta las **4 libertades** (Stallman, FSF):  
  1. **Usar** el programa para cualquier propósito.  
  2. **Estudiar y modificar** el código.  
  3. **Distribuir** copias.  
  4. **Distribuir versiones modificadas**.  
- **Licencias**: GPL (la más usada, obliga a que derivados sean libres).  

### ** Énfasis**  

- **Libertad del usuario** (no solo gratuidad). "Free as in freedom, not free beer".  



## **5. Open Source (Código Abierto)**  

### ** Origen**  

- Término acuñado en **1998** (Eric Raymond, Bruce Perens) para hacer el software libre más "atractivo" para empresas.  
- **Filosofía**: Valor práctico (calidad, colaboración, seguridad) > ideología.  

### **Licencias**  

- Pueden ser permisivas (MIT, Apache) o copyleft (GPL).  


## ** Diferencias: Software Libre vs Open Source** 

| **Aspecto**          | **Software Libre**               | **Open Source**               |  
|----------------------|----------------------------------|--------------------------------|  
| **Enfoque**          | Ético (libertades del usuario)   | Técnico (calidad del código)   |  
| **Licencias típicas**| GPL, AGPL                        | MIT, Apache, BSD               |  
| **Ejemplo**          | GNU Bash, Linux kernel (GPL)     | Kubernetes (Apache), React (MIT)|  
| **¿Puede ser privativo?** | No (derivados deben ser libres) | Sí (puede usarse en software cerrado). |  

### ** Clave**  

- **Software Libre = Siempre Open Source**, pero **Open Source ≠ siempre Software Libre** (ej.: licencias permisivas permiten su uso en software privativo).  


## ** Conclusión**  

- **GNU/Linux** es el sistema operativo libre más importante, fruto de la filosofía de Stallman y el pragmatismo de Torvalds.  
- **Software Libre** es una postura ética; **Open Source** es una metodología de desarrollo.  
- Linux domina hoy en servidores, nube y dispositivos embebidos gracias a su modelo colaborativo.  

---

## **Ecosistema GNU/Linux**  

#### **1. Distribuciones GNU/Linux: [[Debian]], [[Fedora]], [[Arch]]**  

GNU/Linux no es un sistema operativo único, sino un **ecosistema de distribuciones** (distros), cada una con su filosofía y enfoque. Las más relevantes y sus derivadas principales son:  

| **Distro Base** | **Filosofía**              | **Derivadas Importantes**              |  
|-----------------|----------------------------|----------------------------------------|  
| **Debian**      | Estabilidad, software libre puro | Ubuntu, Linux Mint, Kali Linux       |  
| **Fedora**      | Innovación, respaldada por Red Hat | RHEL (Red Hat Enterprise Linux), CentOS Stream |  
| **Arch**        | Minimalismo, rolling release | Manjaro, EndeavourOS, ArcoLinux      |  

- **Debian**: Usada como base para muchas distros por su solidez.  
- **Fedora**: Es el "banco de pruebas" de Red Hat, con tecnologías nuevas.  
- **Arch**: Para usuarios avanzados; rolling release (actualizaciones continuas).  

#### **2. [[Arbol de directorios y Archivos de configuracion]] **

En GNU/Linux, todo parte del **directorio raíz (`/`)**, siguiendo el **Filesystem Hierarchy Standard (FHS)**:  
- **`/bin`**: Comandos esenciales (ej. `ls`, `bash`).  
- **`/etc`**: Configuraciones globales (ej. `/etc/bashrc`).  
- **`/home`**: Directorios de usuarios (ej. `/home/usuario`).  
- **`/usr`**: Software instalado (ej. `/usr/bin`, `/usr/lib`).  

*Relación con GNU*: Muchas de estas rutas y estándares fueron definidos por herramientas GNU (`coreutils`).  


#### **3.[[Bash born again shell]] **  

- **Origen**: Creado por **Brian Fox** para el proyecto GNU (1989), como reemplazo libre de la Bourne Shell (`sh`).  
- **Uso**: Intérprete de comandos predeterminado en la mayoría de distros (Debian, Fedora, Arch).  
- **Relación con GNU/Linux**:  
  - Sin Bash, la administración de GNU/Linux sería mucho más limitada.  
  - Ejemplo: Los scripts de inicio (`/etc/profile`) usan sintaxis Bash.  

#### **4. [[Comandos]]**  

GNU/Linux se maneja mediante **comandos**, muchos provistos por GNU:  
- **`ls`** (listar archivos) → Parte de GNU `coreutils`.  
- **`grep`** (búsqueda) → Herramienta GNU.  
- **`apt`** (Debian) / **`dnf`** (Fedora) / **`pacman`** (Arch): Gestores de paquetes, dependientes del sistema base.  

*Filosofía*: La libertad de GNU permite modificar y redistribuir estos comandos.  

#### **5. Terminal**  

- **Concepto**: Interfaz de texto para interactuar con el sistema (usando Bash u otras shells como `zsh`).  
- **Relación con GNU/Linux**:  
  - Sin terminal, no se aprovecharían herramientas GNU como `gcc` o `make`.  
  - Distros como Arch y Fedora asumen que el usuario usará la terminal para administración avanzada.  

#### Ejemplo de terminal:

**[[kitty_confi]]**

### **Resumen de Relaciones** 
 
| **Título**               | **Conexión con GNU/Linux**                                             |     |
| ------------------------ | ---------------------------------------------------------------------- | --- |
| **Debian/Fedora/Arch**   | Distros que combinan kernel Linux + herramientas GNU.                  |     |
| **Árbol de directorios** | Estructura estándar gestionada por comandos GNU (`ls`, `cd`, `mkdir`). |     |
| **Bash**                 | Shell creada por GNU, usada en casi todas las distros.                 |     |
| **Comandos**             | Herramientas GNU (`coreutils`) son la base de la administración.       |     |
| **Terminal**             | Interfaz donde se ejecutan comandos GNU y se gestiona el sistema.      |     |

### **Conclusión**  

GNU/Linux es un **rompecabezas** donde:  

- **GNU** aporta las herramientas básicas (Bash, comandos).  
- **Linux** es el núcleo que gestiona el hardware.  
- **Distros** como Debian, Fedora o Arch personalizan el sistema para distintos usos.  

---

## Aplicaciones

[[mpd]] Reproductor de musica



