

## Mis prompt 

```bash
export PS1='\[\033[01;36m\] \[\033[01;33m\]\u \[\033[01;31m\]@ \h  \[\033[01;34m\] \w\[\033[1;32m\] \n$(__git_ps1 " (%s)")\[\033[1;36m\] \$\[\033[00m\]'
```

Mejora en la visulizacion de la rama en git

```bash
export PS1='\[\033[01;36m\] \[\033[01;33m\]\u \[\033[01;31m\]@ \h  \[\033[01;34m\] \w\[\033[1;32m\] \n$(__git_ps1 " %s ")\[\033[1;36m\] \$\[\033[00m\]'
```

---

```bash
export PS1='\[\033[01;36m\] \[\033[01;33m\]\u \[\033[01;31m\]@ \h \[\033[01;34m\]\w\[\033[1;32m\]\n\$\[\033[00m\] '
```



```bash
export PS1='\[\033[01;32m\]\u@\h \[\033[01;34m\]\w \[\033[01;33m\]$(__git_ps1 " %s ")\[\033[01;32m\]\[\033[00m\] '
```



```bash
export PS1='\[\033[01;36m\] \[\033[01;33m\]\u\[\033[01;31m\]@\h \[\033[01;34m\]\w\[\033[1;32m\]$(__git_ps1 "  %s")\n\[\033[1;36m\]\[\033[00m\] '
```



```bash
export PS1='\[\033[01;32m\]\u \[\033[01;34m\]\w \[\033[01;33m\]$(__git_ps1 " %s ")\n\[\033[01;36m\]❯\[\033[00m\] '
```



```bash
export PS1='\[\033[01;32m\]\u \[\033[01;34m\]\w \[\033[01;33m\]$(__git_ps1 " %s ")\[$([ $? -eq 0 ] && echo "01;32" || echo "01;31")\]❯\[\033[00m\] '
```

```bash
export PS1='\[\033[01;32m\]\u \[\033[01;34m\]\w \[\033[01;33m\]$(__git_ps1 " %s ")\[$([ $? -eq 0 ] && echo "01;32" || echo "01;31")\]\$\[\033[00m\] '
```

Promp con seguimiento de estado

```bash
export PS1='\[\033[01;32m\]\u \[\033[01;34m\]\w \[\033[01;33m\]$(__git_ps1 "  %s \[\033[0;91m\]✗\[\033[0;93m\]✓\[\033[0;96m\]✚")\[\033[01;36m\]\$\[\033[00m\] '
```

```bash
export PS1='PS1_CMD1=$(ip route get 1.1.1.1 | awk -F"src " '"'"'NR == 1{ split($2, a," ");print a[1]}'"'"'); PS1_CMD2=$(git branch --show-current 2>/dev/null); PS1_CMD3=$(__git_ps1 " (%s)")'; PS1='\u@:\h\w${PS1_CMD1}\n${PS1_CMD2}${PS1_CMD3}\n\\$'
```

```bash

```


```bash

```

Con `__git_ps1` (que viene con Git) y unas variables especiales, puedes mostrar el estado de los archivos (modificados, añadidos, eliminados, etc.) de forma sencilla.  

### 🔧 **Solución rápida (sin scripts externos)**  

Agrega esto **antes** de tu `PS1` en tu `.bashrc` o `.zshrc`:  


```bash
# Configuración para __git_ps1 (muestra cambios en el repositorio)
export GIT_PS1_SHOWDIRTYSTATE=1        # * para modificados, + para staged
export GIT_PS1_SHOWSTASHSTATE=1        # $ si hay stashes
export GIT_PS1_SHOWUNTRACKEDFILES=1    # % si hay archivos nuevos
export GIT_PS1_SHOWUPSTREAM="auto"     # Muestra diferencias con upstream (>< adelanto/atraso)

# Luego define tu PS1 (ejemplo compacto):
export PS1='\[\033[01;32m\]\u \[\033[01;34m\]\w \[\033[01;33m\]$(__git_ps1 "  %s")\[\033[01;36m\]\$\[\033[00m\] '
```

### 🌟 **Resultado**  

- ` main *` → Archivos modificados (no staged).  
- ` main +` → Archivos staged (listos para commit).  
- ` main %` → Archivos nuevos (untracked).  
- ` main $` → Hay stashes guardados.  
- ` main >` → Tu rama está adelantada al upstream.  

---

### 🛠 **Versión mejorada (con colores y símbolos personalizados)**  

Si quieres más detalle (como diferenciar modificados de staged), usa este formato:  

```bash
export PS1='\[\033[01;32m\]\u \[\033[01;34m\]\w \[\033[01;33m\]$(__git_ps1 "  %s\[\033[0;33m\]%s%s%s%s\[\033[01;33m\]")\[\033[01;36m\]\$\[\033[00m\] '
```

#### Simbología:  

- `✚` → Modificados (no staged).  
- `●` → Staged (listos para commit).  
- `✖` → Eliminados.  
- `…` → Archivos nuevos (untracked).  

*(Nota: Para esto necesitarías modificar `__git_ps1` o usar una función personalizada, pero es el siguiente nivel)*.  

---

### 📌 **Pasos para implementarlo**  

1. **Abre tu `.bashrc` o `.zshrc`**:  

```bash
nano ~/.bashrc  # o ~/.zshrc
```
2. **Pega la configuración de arriba**.  
3. **Recarga el terminal**:  

```bash
source ~/.bashrc
```

---

### 🔥 **Bonus: Prompt con emojis (más intuitivo)**  

```bash
export PS1='\[\033[01;32m\]\u \[\033[01;34m\]\w \[\033[01;33m\]$(__git_ps1 "  %s \[\033[0;91m\]✗\[\033[0;93m\]✓\[\033[0;96m\]✚")\[\033[01;36m\]\$\[\033[00m\] '
```

*(Aquí usé colores y símbolos para representar cambios, pero requiere ajustes en `__git_ps1`)*.  

---




## 1️⃣ **Mostrar el número de archivos modificados (ej: `+2`)**  

Para esto necesitamos reemplazar `__git_ps1` con una función personalizada que cuente archivos.  

### 🔧 **Código (añádelo a tu `.bashrc` o `.zshrc`)**:

```bash
# Función para contar archivos en Git
git_status_counts() {
    local staged=$(git diff --cached --numstat | wc -l | tr -d ' ')
    local modified=$(git diff --name-only | wc -l | tr -d ' ')
    local untracked=$(git ls-files --others --exclude-standard | wc -l | tr -d ' ')
    
    local status=""
    [[ $staged -gt 0 ]] && status+=" ●$staged"
    [[ $modified -gt 0 ]] && status+=" ✚$modified"
    [[ $untracked -gt 0 ]] && status+=" …$untracked"
    
    echo "$status"
}

# Prompt con Git mejorado
export PS1='\[\033[01;32m\]\u \[\033[01;34m\]\w \[\033[01;33m\]$(if git rev-parse --git-dir > /dev/null 2>&1; then echo "  $(git branch --show-current)$(git_status_counts)"; fi)\[\033[01;36m\]\$\[\033[00m\] '
```

### 🌟 **Resultado**:  

- ` main ●2 ✚3 …1` → 2 staged, 3 modificados, 1 nuevo.  
- ` feat/login ✚5` → 5 archivos modificados (sin staged).  

---

## 2️⃣ **Añadir el tiempo de ejecución del último comando**  

Para mostrar cuánto tardó el último comando (ej: `[3.5s]`).  

### 🔧 **Código**:

```bash
# Añade esto ANTES de tu PS1
function timer_start() {
    timer=${timer:-$SECONDS}
}
function timer_stop() {
    elapsed=$((SECONDS - timer))
    unset timer
}
trap 'timer_start' DEBUG
PROMPT_COMMAND=timer_stop

# Luego, en tu PS1, añade esto donde quieras mostrar el tiempo:
\[\033[01;35m\]$([ $elapsed -gt 0 ] && echo "[${elapsed}s] ")\[\033[00m\]
```

### 🌟 **Ejemplo**:  

```bash
export PS1='\[\033[01;35m\]$([ $elapsed -gt 0 ] && echo "[${elapsed}s] ")\[\033[01;32m\]\u \[\033[01;34m\]\w \[\033[01;33m\]$(__git_ps1 "  %s")\[\033[01;36m\]\$\[\033[00m\] '
```
- Si un comando tarda 2 segundos, mostrará: `[2s] usuario ~/proyecto  main $`.  

---

## 3️⃣ **Usar Powerline para un efecto visual profesional**  

Powerline usa símbolos triangulares (▲) y colores degradados para un prompt elegante.  

### 🔧 **Instalación (requiere fuentes Powerline)**:

1. Instala una fuente Powerline (ej: `Fira Code`, `Meslo LG M`).  
2. Usa símbolos Unicode como ``, ``, ``.  

### 🌈 **Código para un prompt tipo Powerline**:

```bash
export PS1='\[\033[1;32m\]\u \[\033[1;34m\] \[\033[1;37m\]\w \[\033[1;34m\]\[\033[1;33m\]$(__git_ps1 "  %s")\[\033[0;33m\] \[\033[01;36m\]\$\[\033[00m\] '
```

### 🎨 **Personalización avanzada**:

- **Colores por sección**: Usa `\[\033[48;5;Xm\]` para fondo y `\[\033[38;5;Xm\]` para texto.  
- **Símbolos**:  
  - `` = Triángulo hacia la derecha.  
  - `` = Separador delgado.  
  - `` = Triángulo hacia la izquierda.  

### 🌟 **Resultado**:  

![Prompt Powerline](https://i.imgur.com/VnU5l4l.png) *(Usuario y ruta con fondos segmentados)*.  

---

## 🔥 **Combinación FINAL (Git + Tiempo + Powerline)**  

```bash
export PS1='\[\033[1;35m\]$([ $elapsed -gt 0 ] && echo "[${elapsed}s] ")\[\033[1;32m\]\u \[\033[1;34m\] \[\033[1;37m\]\w \[\033[1;34m\]\[\033[1;33m\]$(if git rev-parse --git-dir > /dev/null 2>&1; then echo "  $(git branch --show-current)$(git_status_counts)"; fi)\[\033[0;33m\] \[\033[01;36m\]\$\[\033[00m\] '
```

---

### 📌 **Recomendaciones finales**:  
1. **Fuentes**: Usa terminales con soporte para símbolos (Kitty, iTerm2, Alacritty).  
2. **Plugin para Git rápido**: Si usas Zsh, considera `zsh-git-prompt`.  
3. **Temas prehechos**: Mira `starship`, `spaceship-prompt` o `powerlevel10k`.  







