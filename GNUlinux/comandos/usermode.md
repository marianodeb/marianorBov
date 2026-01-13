
---

### **Definición**  
`usermod` es un comando para **modificar cuentas de usuario existentes** en sistemas Linux/Unix. Permite cambiar atributos como:  
- Nombre de usuario.  
- Directorio home.  
- Grupo primario o secundarios.  
- Shell por defecto.  
- Fecha de expiración de la cuenta.  
- Entre otros.

---

### **Sintaxis Básica**  
```bash
usermod [OPCIONES] <nombre_de_usuario>
```

---

### **Opciones Principales**  
| Opción | Descripción |  
|--------|-------------|  
| `-c "comentario"` | Agrega un comentario (ej: nombre completo). |  
| `-d <nuevo_home>` | Cambia el directorio home del usuario. |  
| `-m` | Mueve el contenido del home antiguo al nuevo (se usa con `-d`). |  
| `-e <YYYY-MM-DD>` | Establece fecha de expiración de la cuenta. |  
| `-g <grupo_primario>` | Cambia el grupo primario (GID o nombre). |  
| `-G <grupos>` | Define grupos secundarios (separados por comas). |  
| `-a` | Añade grupos secundarios sin borrar los existentes (se usa con `-G`). |  
| `-l <nuevo_nombre>` | Cambia el nombre de usuario. |  
| `-L` | Bloquea la cuenta (la deshabilita). |  
| `-U` | Desbloquea la cuenta. |  
| `-s <ruta_shell>` | Define el shell por defecto (ej: `/bin/bash`). |  
| `-u <nuevo_UID>` | Cambia el UID (identificador numérico). |  
| `-o` | Permite UID duplicados (se usa con `-u`). |  
| `-Z <contexto_SElinux>` | Modifica el usuario SELinux asociado. |  

---

### **Ejemplos Simples**  

1. **Cambiar el nombre completo de un usuario**:  
   ```bash
   sudo usermod -c "Juan Pérez" juan
   ```

2. **Agregar un usuario al grupo `sudo` (sin borrar grupos actuales)**:  
   ```bash
   sudo usermod -aG sudo maria
   ```

3. **Cambiar el shell por defecto a `/bin/zsh`**:  
   ```bash
   sudo usermod -s /bin/zsh pedro
   ```

---

### **Ejemplos Complejos**  

1. **Cambiar nombre de usuario y directorio home (moviendo archivos)**:  
   ```bash
   sudo usermod -l nuevo_usuario -d /home/nuevo_usuario -m usuario_viejo
   ```

2. **Establecer fecha de expiración y bloquear la cuenta**:  
   ```bash
   sudo usermod -e 2024-12-31 -L ana
   ```

3. **Cambiar el UID y grupo primario, añadiendo grupos secundarios**:  
   ```bash
   sudo usermod -u 2000 -g developers -aG docker,www-data luis
   ```

---

### **Información Adicional**  

- **Requiere permisos de root**: Siempre usa `sudo` antes del comando.  
- **Precaución con usuarios activos**: Evita modificar usuarios que están logueados (podría causar errores).  
- **Actualizar archivos de sistema**: Los cambios se reflejan en `/etc/passwd`, `/etc/shadow`, y `/etc/group`.  
- **SELinux**: Si usas `-d` para mover el home, ejecuta `restorecon -Rv /nuevo/home` para actualizar contextos.  
- **Contraseñas**: No uses `-p` (es inseguro). Mejor emplea `passwd <usuario>`.  

---

