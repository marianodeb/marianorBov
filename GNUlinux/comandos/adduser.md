## `adduser` 


### **1. Significado**

`adduser` es un comando utilizado para **crear nuevos usuarios** o **agregar usuarios existentes a grupos** en sistemas basados en Linux/Unix. Es una herramienta más amigable que `useradd` (su equivalente de bajo nivel), ya que automatiza tareas como crear el directorio home o configurar contraseñas de forma interactiva.

---

### **2. Uso**

- Crear un nuevo usuario con configuración básica.  
- Asignar un usuario a un grupo existente.  
- Personalizar parámetros como directorio home, shell, UID, etc.  
- Crear usuarios del sistema (sin permisos de login).  

---

### **3. Sintaxis básica**

```bash
adduser [opciones] <nombre_de_usuario>  
adduser <nombre_de_usuario> <grupo>  # Agregar usuario a un grupo
```

---

### **4. Opciones principales**

| Opción               | Descripción                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| `--system`           | Crea un usuario del sistema (sin directorio home por defecto).             |
| `--home <ruta>`      | Define una ruta personalizada para el directorio home.                      |
| `--shell <ruta>`     | Especifica el shell del usuario (ej: `/usr/sbin/nologin`).                  |
| `--gecos "<texto>"`  | Agrega información del usuario (nombre completo, teléfono, etc.).          |
| `--disabled-login`   | Crea el usuario sin contraseña (no puede iniciar sesión).                  |
| `--group`            | Crea un grupo con el mismo nombre que el usuario.                           |
| `--uid <ID>`         | Define un UID específico para el usuario.                                   |
| `--ingroup <grupo>`  | Asigna el usuario a un grupo existente (en lugar de crear uno nuevo).       |
| `--quiet`            | Ejecuta el comando sin mostrar mensajes.                                    |

---

### **5. Ejemplos**  

#### **Ejemplo simple**:

Crear un usuario llamado **miusuario**:

```bash
sudo adduser miusuario  
```
El comando pedirá contraseña y datos opcionales (GECOS).

---

#### **Ejemplo complejo**:

Crear un usuario del sistema con:  
- UID 1500  
- Shell `/sbin/nologin`  
- Directorio home en `/var/miusuario`  
- Sin contraseña habilitada:

```bash
sudo adduser --system --uid 1500 --shell /sbin/nologin --home /var/miusuario --disabled-login miusuario
```

---

#### **Agregar usuario a un grupo**:

Agregar **miusuario** al grupo **sudo**:

```bash
sudo adduser miusuario sudo  
```

---

#### **Ejemplo con GECOS**:

Crear un usuario con nombre completo y comentario:

```bash
sudo adduser --gecos "Juan Pérez, Desarrollador, 555-1234, Sala 5" juan  
```

---

### **6. Información adicional**

- **Configuración predeterminada**:

  El archivo `/etc/adduser.conf` define opciones por defecto (ej: directorio home, shell, etc.).

- **Diferencia entre `adduser` y `useradd`**:

  - `adduser` es interactivo y más intuitivo.  
  - `useradd` requiere opciones explícitas (ej: `useradd -m -s /bin/bash usuario`).

- **Comandos relacionados**:

  - `deluser`: Elimina usuarios.  
  - `usermod`: Modifica propiedades de usuarios existentes.  
  - `passwd`: Cambia contraseñas.  

- **Permisos**:

  Necesitas permisos de superusuario (`sudo`) para ejecutar `adduser`.

---

### **7. Notas importantes**

- En distribuciones como **Debian/Ubuntu**, `adduser` es el recomendado. En otras (ej: Fedora), se usa `useradd`.  
- Para ver todas las opciones, ejecuta:

```bash
man adduser  
```


