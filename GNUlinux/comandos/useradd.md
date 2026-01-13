
## `useradd`

### **1. Significado**

`useradd` es un comando de bajo nivel para **crear nuevos usuarios** en sistemas Linux/Unix. A diferencia de `adduser`, no es interactivo y requiere especificar todas las opciones manualmente. Es útil para scripts o automatización.

---

### **2. Uso**

- Crear usuarios con configuraciones específicas (UID, GID, directorio home, shell, etc.).  
- Definir usuarios del sistema (sin capacidad de login).  
- Configurar grupos primarios y secundarios.  
- Trabajar en entornos donde se necesita precisión y control total.

---

### **3. Sintaxis básica**

```bash
useradd [opciones] <nombre_de_usuario>
```

---

### **4. Opciones principales**  
| Opción               | Descripción                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| `-m` o `--create-home` | Crea el directorio home del usuario (ej: `/home/usuario`).                 |
| `-s <shell>`         | Especifica el shell del usuario (ej: `/bin/bash` o `/sbin/nologin`).        |
| `-u <UID>`           | Define un UID específico para el usuario.                                   |
| `-g <grupo>`         | Establece el grupo primario (GID) del usuario.                              |
| `-G <grupos>`        | Asigna grupos secundarios (separados por comas).                            |
| `-d <ruta>`          | Define una ruta personalizada para el directorio home.                      |
| `-c "<comentario>"`  | Agrega un comentario (generalmente nombre completo o descripción).         |
| `-e <YYYY-MM-DD>`    | Establece una fecha de expiración para la cuenta.                           |
| `-p <contraseña>`    | Define la contraseña (encriptada). **No recomendado por seguridad**.        |
| `-r`                 | Crea un usuario del sistema (sin directorio home a menos que se use `-m`).  |
| `-k <plantilla>`     | Usa archivos de plantilla del directorio `/etc/skel` para el home.          |

---

### **5. Ejemplos**

#### **Ejemplo simple**:

Crear un usuario llamado **juan** con directorio home y shell Bash:

```bash
sudo useradd -m -s /bin/bash juan  
```

---

#### **Ejemplo complejo**:

Crear un usuario del sistema con:

- UID 2000  
- Grupo primario `developers` (debe existir)  
- Grupos secundarios `sudo,docker`  
- Directorio home en `/opt/juan`  
- Comentario "Usuario para despliegues"  
- Fecha de expiración 2025-12-31:

```bash
sudo useradd -r -u 2000 -g developers -G sudo,docker -d /opt/juan -s /bin/bash -c "Usuario para despliegues" -e 2025-12-31 -m juan  
```

---

#### **Crear usuario sin shell de login**:

```bash
sudo useradd -s /sbin/nologin -m usuario_backup  
```

---

#### **Usar contraseña encriptada**:

Primero genera la contraseña encriptada con `openssl`:

```bash
openssl passwd -6 "mi_contraseña"  # Genera algo como: $6$trH5eF...  
```

Luego crea el usuario:

```bash
sudo useradd -m -p '$6$trH5eF...' juan  
```

---

### **6. Información adicional**

- **Archivos de configuración clave**:

  - `/etc/default/useradd`: Define valores predeterminados (shell, directorio home, etc.).  
  - `/etc/login.defs`: Configura políticas de contraseñas, UID/GID mínimos, etc.  

- **Diferencia clave con `adduser`**:

  - `useradd` no crea el directorio home ni solicita contraseña por defecto.  
  - `adduser` es un script más amigable que llama a `useradd` internamente con opciones predefinidas.  

- **Comandos relacionados**:

  - `usermod`: Modificar propiedades de un usuario existente.  
  - `userdel`: Eliminar un usuario.  
  - `passwd`: Establecer/actualizar contraseñas.  

- **Permisos**:

  Requiere permisos de superusuario (`sudo`).  

---

### **7. Notas importantes**

- **¡Cuidado con `-p`!**: La contraseña debe estar encriptada. Es más seguro usar `passwd` después de crear el usuario.  
- **Distribuciones**:  
  - En Debian/Ubuntu, `useradd` no crea el directorio home por defecto (usa `-m`).  
  - En Red Hat/CentOS, el comportamiento puede variar según `/etc/login.defs`.  
- **Verificar cambios**:  
  Para confirmar la creación, revisa `/etc/passwd`, `/etc/shadow` y `/etc/group`.  

---

### **8. Comando para ver todas las opciones**

```bash
man useradd  
```


