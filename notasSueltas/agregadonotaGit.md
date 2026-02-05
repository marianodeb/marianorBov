



**índice exacto de todos los títulos y secciones que me pasaste en los 7 bloques**

### **Índice de Secciones (Tus notas originales)**

**1. Fundamentos y Configuración Inicial**

* Tipos de configuraciones de GIT (Global, Local, Sistema).
* Jerarquía de configuraciones y funcionamiento en USB.
* Configuración Global (Usuario, Correo, Editor `code --wait`, Rama `main`).
* Edición manual de archivos de configuración (`git config -e`).
* Configuración de `core.autocrlf` (Windows vs Linux/Mac).

**2. Flujo de Trabajo Local**

* Iniciar un Repositorio Local (`git init`).
* Agregar Archivos (`git add .`) y Crear Commits.

**3. Conectividad Remota**

* Conectar a Remoto (SSH vs HTTPS).
* Cambiar el Remoto de HTTPS a SSH (`git remote set-url`).
* Clonar Repositorios.

**4. Configuración SSH Avanzada**

* Generación de llaves: Algoritmos `ed25519`, `RSA` (4096 bits), `ECDSA`.
* Significado del parámetro `-C` (comentarios).
* **Gestión del Agente SSH:** `eval $(ssh-agent -s)`, `ssh-add -D`, `ssh-add ~/.ssh/...`.
* Prueba de conexión (`ssh -T git@github.com`).
* **Archivo de Configuración SSH (`~/.ssh/config`):** Estructura para múltiples cuentas (Personal, Notas, Trabajo) y uso de Alias.

**5. Sincronización y Recuperación**

* Conexión de repositorio local modificado a remoto desactualizado.
* Resolución de conflictos durante `git pull`.
* Descartar cambios locales forzando la rama (`git reset --hard`).

**6. Gestión Completa de Ramas (Branch)**

* Crear, Eliminar (local/remota), Moverse (`switch`/`checkout`).
* Listar (`-a`, `-r`), Renombrar y Fusionar (`merge`).
* Rebasar (`rebase`) y Sincronizar (`fetch`, `pull`).
* Crear rama desde commit específico o desde un tag.
* Limpieza de ramas huérfanas (`fetch --prune`).
* Seguimiento de ramas remotas (`--track`).

**7. Referencias y Herramientas**

* Visores de historial: **Tig** y **Lazygit**.
* Historial gráfico (`git log --graph --oneline --decorate --all`).

**8. Comandos de Inspección y Estado**

* Significado de los códigos de `git status -s` (M, D, A, ??, R, C, U).
* Uso de `git log` y la lista de sus **92 opciones** (desde `--abbrev` hasta `--simplify-merges`).

**9. Automatización (Scripts)**

* Script para Configuración Automática de SSH y Git (Carga de llaves desde pendrive `/media/user/bodzzy/...`).

---
---
---

## Configuracion de Git - SSH y su archivo de configuracion.


### 1. El Archivo de Configuración (`~/.ssh/config`)

Este archivo es el "traductor". Cuando Git ve una dirección, busca aquí para saber qué llave física debe sacar de tu bolsillo.

#### Cómo crear/editar el archivo:

`nano ~/.ssh/config`

#### Contenido de ejemplo con 3 cuentas:

```text
# CUENTA 1: Personal (Usa el nombre estándar)
# Comando: git remote add origin git@github.com:usuario/repo-personal.git
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_github_mariano
    IdentitiesOnly yes

# CUENTA 2: Notas (Usa el alias 'github-notas')
# Comando: git remote add origin git@github-notas:usuario/repo-notas.git
Host github-notas
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_github_notas
    IdentitiesOnly yes

# CUENTA 3: Trabajo (Usa el alias 'github-trabajo')
# Comando: git remote add origin git@github-trabajo:usuario/repo-trabajo.git
Host github-trabajo
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_github_trabajo
    IdentitiesOnly yes

```

### 2. Cómo agregar una cuenta nueva (Paso a Paso)

Si mañana quieres agregar la cuenta de "Trabajo":

1. **Generar la llave:**

`ssh-keygen -t ed25519 -C "trabajo@mail.com" -f ~/.ssh/id_github_trabajo`

2. **Subir la pública a GitHub:**

`cat ~/.ssh/id_github_trabajo.pub` (Copias el texto y lo pegas en la web de la cuenta de trabajo).

3. **Actualizar el archivo `config`:**

Añades el bloque de "CUENTA 3" que vimos arriba.

4. **Refrescar el sistema (Activar):**

Cada vez que agregas una llave o reinicias la PC, es bueno hacer esto para que la terminal "recuerde":

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_github_trabajo

```

### 3. La Magia: Iniciar un Repo y Vincularlo

Aquí es donde usas los alias para que Git sepa qué cuenta usar.

1. **Entrar a tu proyecto:** `cd ~/mi-proyecto`
2. **Iniciar Git:** `git init`
3. **Guardar archivos:**

```bash
git add .
git commit -m "Primer commit"

```


4. **Vincular usando el ALIAS (Paso Crítico):**
Si este proyecto es del **trabajo**, NO copies la URL de GitHub tal cual. Modifícala así:
* *URL Original:* `git@github.com:marianodeb/proyecto.git`
* *URL con Alias:* `git remote add origin git@github-trabajo:marianodeb/proyecto.git`


5. **Subir:**
`git push -u origin main`

### 4. Resumen de Funcionamiento

* **¿Qué hace Git?** Mira lo que hay después del `@` en la URL (ej: `github-trabajo`).
* **¿Qué hace SSH?** Busca ese nombre en el archivo `config`.
* **¿Cuál es el resultado?** SSH ve que `github-trabajo` en realidad debe ir a `github.com` pero usando la llave de la oficina.

### Comandos de auxilio:

* **Ver si funciona la conexión de un alias:** `ssh -T git@github-trabajo`
* **Ver qué URL tiene mi carpeta actual:** `git remote -v`
* **Si te equivocaste de URL al vincular:** `git remote set-url origin git@alias-correcto:usuario/repo.git`

