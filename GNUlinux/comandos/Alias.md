

## ALIAS

### **Definición y Significado**

`alias` es un comando **integrado en shells como Bash o Zsh** que permite crear **atajos personalizados** para comandos largos o complejos.
 
- **Temporal**: Los alias se borran al cerrar la terminal (a menos que se guarden en archivos de configuración como `.bashrc` o `.zshrc`).
- **Personalización**: Útil para redefinir comandos con opciones predeterminadas o crear macros.

---

### **Sintaxis Básica**

```bash
alias [nombre_alias]='comando'   # Crear un alias
alias                             # Listar todos los alias
unalias <nombre_alias>           # Eliminar un alias
```

---

### **Opciones y Funcionalidades**

| Opción/Modificador | Descripción                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| `alias` sin opciones | Lista todos los alias activos en la sesión actual.                          |
| `alias <nombre>`   | Muestra la definición de un alias específico.                               |
| `unalias -a`       | Elimina **todos** los alias de la sesión actual.                             |
| `\comando`         | Ignora el alias y ejecuta el comando original (ej: `\ls` usa el `ls` real).  |

---

### **Ejemplos Simples y Complejos**

#### **1. Ejemplo Básico:**

```bash
alias ll='ls -lha'  # Atajo para listar archivos con detalles y ocultos
```

**Uso:**

```bash
ll  # Equivale a ejecutar "ls -lha"
```

#### **2. Alias con Comandos Múltiples:**

```bash
alias update='sudo apt update && sudo apt upgrade -y'  # Actualiza el sistema
```

#### **3. Alias para Evitar Errores:**

```bash
alias rm='rm -i'  # Pregunta antes de borrar (evita borrar archivos por accidente)
```

#### **4. Alias con Argumentos (usando funciones):**

```bash
alias mkcd='_mkcd() { mkdir "$1" && cd "$1"; }; _mkcd'  # Crea un directorio y entra en él
```
**Uso:**

```bash
mkcd nuevo_proyecto  # Crea "nuevo_proyecto" y navega ahí
```

#### **5. Alias para Conexiones SSH:**

```bash
alias conectar_servidor='ssh -i ~/.ssh/mi_llave.pem usuario@192.168.1.100'
```

#### **6. Alias con Variables:**

```bash
alias hoy='echo "Fecha: $(date +%d/%m/%Y)"'  # Muestra la fecha actual
```

---

### **Consejos Prácticos**

- **Hacer Alias Permanentes:** Guárdalos en `~/.bashrc`, `~/.zshrc`, o `~/.bash_profile` y ejecuta `source ~/.bashrc` para aplicar cambios.
- **Listar Alias Existentes:** Usa `alias` o `alias -p`.
- **Eliminar un Alias:** `unalias <nombre>`.
- **Evitar Conflictos:** No uses nombres de comandos existentes (ej: `alias ls='ls -lha'` podría causar loops).
- **Alias Seguros:** Usa comillas simples (`' '`) para evitar expansión de variables no deseada.

---

###  **Información Adicional**

- **Alias vs Funciones:** Los alias son simples, pero para lógica compleja (ej: argumentos), usa **funciones en Bash**.
- **Prioridad de Comandos:** Los alias tienen mayor prioridad que comandos reales. Usa `\comando` para ignorar el alias.
- **Alias en Scripts:** Los alias **no funcionan en scripts** a menos que se definan explícitamente o se habilite su expansión con `shopt -s expand_aliases`.
- **Soporte Multi-Shell:** Configura alias en archivos específicos según tu shell:
  - **Bash:** `~/.bashrc`
  - **Zsh:** `~/.zshrc`
  - **Fish:** `~/.config/fish/config.fish`

---

###  **Ejemplo de Alias Peligroso (¡Evita esto!):**

```bash
alias ls='rm -rf'  # ¡Nunca hagas esto! Redefiniría "ls" para borrar archivos.
```

---

## Mis Alias

### Alias del Sistema

```bash
# Alias del Sistema
alias buscar='sudo apt search'
alias instalar='sudo apt install'
alias l='ls -l'
alias ld='ls -l --group-directories-first'
alias ll='ls -la'
alias lld='ls -la --group-directories-first'
alias nf='neofetch'
alias e='exit'
alias act='sudo apt update && sudo apt upgrade'
alias eliminar='sudo apt-get --purge remove'

```


```bash
alias cx='cmatrix'
alias hp='htop'
alias n='nvim'
alias c='cd'
alias a='sudo shutdown now'
alias r='sudo reboot'
alias l='lsd -l'
alias i='sudo apt-get install'
alias ll='lsd -la'
alias act='sudo apt-get update && sudo apt-get upgrade'
alias nf='neofetch'
alias mu='cmus'
alias dpkg='sudo dpkg -i'
```

---

### Alias git


```bash
alias gi='git init'
alias ga='git add'
alias gad='git add .'
alias gc='git commit'
alias gp='git push'
alias gs='git status'
alias gss='git status -s'
alias gl='git log'
alias glo='git log --oneline'
alias gb='git branch'
alias gcl='git clone'
```

---

### Alias para MariaDB

```bash
# Alias para MariaDB
alias mariadb_start='sudo systemctl start mariadb'
alias mariadb_stop='sudo systemctl stop mariadb'
alias mariadb_restart='sudo systemctl restart mariadb'
```

---

### Alias para PostgresSQL

```bash
#Alias para PostgreSQL
alias postgres_start='sudo systemctl start postgresql'
alias postgres_stop='sudo systemctl stop postgresql'
alias postgres_restart='sudo systemctl restart postgresql'
```

---

### Alias Pihole y Nginx

```bash
#Alias Pihole y Nginx
alias nginx_on='sudo systemctl stop dnsmasq && sudo systemctl start nginx'
alias nginx_off='sudo systemctl stop nginx'
alias pihole_on='sudo systemctl stop nginx && sudo systemctl start dnsmasq'
alias pihole_off='sudo systemctl stop dnsmasq'
```

---

