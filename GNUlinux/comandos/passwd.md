## 1. Definición y significado
El nombre **`passwd`** es una abreviatura de **"password"**. Su función principal es permitir a los usuarios cambiar su propia contraseña y, para el superusuario (root), administrar las contraseñas de cualquier usuario del sistema.

Técnicamente, este comando actualiza los archivos donde se almacena la información de autenticación, principalmente `/etc/shadow` (donde viven las contraseñas encriptadas).

## 2. Instalación
En el **99.9%** de las distribuciones Linux (incluyendo Debian, Ubuntu, CentOS, Arch, etc.), `passwd` viene instalado por defecto como parte de los paquetes esenciales del sistema (`passwd` o `shadow-utils`).

Si por alguna razón extraña no estuviera (por ejemplo, en un contenedor Docker muy minimalista), puedes instalarlo así:
* **Debian/Ubuntu:** `sudo apt update && sudo apt install passwd`
* **RHEL/Fedora:** `sudo dnf install shadow-utils`

## 3. Sintaxis
La sintaxis básica es:
`passwd [opciones] [usuario]`

* Si escribís solo `passwd`, cambiás tu propia clave.
* Si sos root o tenés `sudo`, podés poner `passwd nombre_usuario`.


## 4. Opciones del comando
Aquí tenés las más importantes para administrar cuentas:

| Opción | Descripción |
| :--- | :--- |
| `-a, --all` | Se usa con `-S` para ver el estado de todos los usuarios. |
| `-d, --delete` | **Elimina la contraseña** del usuario (lo deja sin clave, ¡ojo!). |
| `-e, --expire` | **Expiración inmediata**. Fuerza al usuario a cambiar su clave al próximo login. |
| `-h, --help` | Muestra la ayuda. |
| `-l, --lock` | **Bloquea** la cuenta del usuario (le agrega un "!" al hash en `/etc/shadow`). |
| `-u, --unlock` | **Desbloquea** la cuenta. |
| `-S, --status` | Muestra el **estado** de la contraseña (si está bloqueada, fecha de cambio, etc.). |
| `-n, --mindays` | Días mínimos antes de poder volver a cambiar la clave. |
| `-x, --maxdays` | Días máximos de validez de la clave. |
| `-w, --warndays` | Días de aviso antes de que la clave expire. |


## 5. Ejemplos (Simples y Complejos)

### Ejemplos Simples
1.  **Cambiar tu propia clave:**
    `passwd`
2.  **Cambiar la clave de otro usuario (requiere sudo):**
    `sudo passwd juan`
3.  **Ver el estado de tu cuenta:**
    `passwd -S`

### Ejemplos Complejos (Administración)
1.  **Forzar a un empleado a cambiar su clave mañana:**
    `sudo passwd -e usuario_nuevo`
    *(Útil cuando creas una cuenta con una clave temporal "1234")*.
2.  **Bloquear a un usuario que se fue de vacaciones (o fue despedido):**
    `sudo passwd -l usuario_sospechoso`
3.  **Configurar una política de seguridad:**
    `sudo passwd -n 7 -x 90 -w 10 usuario1`
    *(El usuario debe esperar 7 días para cambiarla, le dura 90 días máximo y le avisa 10 días antes del vencimiento)*.

---

## 6. Consejos
* **Longitud y Complejidad:** Aunque el comando te deje poner "123", Linux te dará una advertencia. Intentá usar frases de contraseña (ej: `MiGatoUsaDebian2026!`).
* **No uses -d a la ligera:** Dejar una cuenta sin contraseña (`-d`) puede ser un agujero de seguridad crítico si el servicio permite login remoto.
* **Usa `sudo`:** Siempre que administres otros usuarios, anteponé `sudo`.


## 7. Información Adicional y Comandos Relacionados

### **¿Cómo cambiar la clave de root si la olvidaste?** (Teniendo sudo)
Como te mencioné antes, es muy sencillo. Si tenés permisos de `sudo`, simplemente ejecutá:

```bash
sudo passwd root
```
Ingresás **tu** clave de usuario y luego definís la **nueva** clave para root dos veces.

### Comandos Relacionados
* **`chage`**: Es mucho más potente para gestionar la **expiración** de cuentas (ver cuándo vence, forzar cambios, etc.).
* **`useradd` / `usermod`**: Para crear y modificar usuarios.
* **`gpasswd`**: Específico para administrar grupos.

### ¿Hay algo más nuevo o mejor?
No realmente. `passwd` es el estándar de la industria y sigue siendo la herramienta oficial. Sin embargo, en entornos empresariales grandes (servidores en la nube, empresas con miles de empleados), no se usa `passwd` manualmente. Se usan sistemas de **Gestión de Identidad** como:
* **FreeIPA** o **Active Directory**.
* **LDAP**.
* **PAM (Pluggable Authentication Modules)**: Que es el sistema que está "atrás" de `passwd` controlando las reglas de seguridad.



