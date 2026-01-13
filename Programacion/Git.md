

## **Guía Completa para Configurar y Usar Git**

### **Introducción**

Git es una herramienta esencial para el control de versiones en el desarrollo de software. 

1. **Configurar Git localmente** (usuario, correo, y otros ajustes).
2. **Iniciar un repositorio local** y conectarlo a un repositorio remoto en GitHub.
3. **Clonar un repositorio remoto** usando HTTPS o SSH.
4. **Trabajar con Git** de manera eficiente, incluyendo comandos básicos y solución de problemas comunes.

---

### Tipos de configuraciones de GIT

1. **Configuración global (git config --global)**

Esta configuración se aplica a todos los repositorios en tu sistema.

Los datos (como el nombre de usuario y el correo) se guardan en un archivo de configuración en tu carpeta de usuario (por ejemplo, ~/.gitconfig en Linux/Mac o C:\Users\TuUsuario\.gitconfig en Windows).

Es útil si trabajas en varios repositorios y quieres usar la misma información de usuario en todos ellos.

Ejemplo:


```bash
git config --global user.name "Tu nombre"
git config --global user.email "tu@email.com"
```

2. **Configuración local (git config)**

Esta configuración se aplica solo al repositorio actual.

Los datos se guardan en el archivo .git/config dentro de la carpeta del repositorio.

Es útil cuando quieres usar una configuración específica para un repositorio en particular.

Ejemplo:


```bash
git config user.name "Tu nombre"
git config user.email "tu@email.com"
```

Para conocer el nombre o email del repositori ultilizaremos el siguiente comando:


```bash
git config user.name 
git config user.email 
```

3. Cómo funciona en tu caso

Como no tienes una configuración global (porque no puedes guardarla en tu sistema), usas la configuración local.

Cuando ejecutas git config user.name "Tu nombre" y git config user.email "tu@email.com", estos datos se guardan en el archivo .git/config de tu repositorio en la memoria USB.

Esto te permite hacer git add y git commit sin problemas, ya que Git tiene la información necesaria para asociar los commits con tu usuario y correo.

4. Jerarquía de configuraciones

Git sigue un orden de prioridad al buscar configuraciones:

  1. Local (repositorio actual): Si existe, Git usa esta configuración.

  2. Global (usuario): Si no hay configuración local, Git usa la global.

  3. Del sistema (toda la máquina): Si no hay configuración global, Git usa la del sistema.

En tu caso, como no tienes configuración global, Git usa la local que defines en tu repositorio.


---
### **1. Configuración Global de Git**

Antes de empezar a trabajar con Git, es importante configurar tu entorno local. Esto incluye definir tu nombre de usuario, correo electrónico y otras preferencias.

#### **1.1. Configurar Usuario y Correo**
1. Configura tu nombre de usuario:

```bash
git config --global user.name "Tu Nombre"
```
   - **Nota**: Usa tu nombre real o un nombre de usuario reconocible.

2. Configura tu correo electrónico:

```bash
git config --global user.email "tu_correo@ejemplo.com"
```
   - **Nota**: Usa el correo asociado a tu cuenta de GitHub.

3. Verifica la configuración:

```bash
git config --list
```

#### **1.2. Configurar el Editor de Texto (Opcional)**

Si prefieres usar un editor de texto específico para los mensajes de commit (por ejemplo, VS Code), puedes configurarlo:

```bash
git config --global core.editor "code --wait"
```

#### **1.3. Configurar el Nombre de la Rama Principal (Opcional)**

Por defecto, Git usa `master` como nombre de la rama principal. Sin embargo, puedes cambiarlo a `main` (recomendado):

```bash
git config --global init.defaultBranch main
```

#### Editar manualmente el archivo de configuración

Ámbito local (dentro de un repositorio Git):

```bash
git config -e
```

Ámbito global (configuraciones para tu usuario):

```bash
git config --global -e
```

Ámbito del sistema (configuraciones para todo el sistema):

```bash
git config --system -e
```


#### Configuración de core.autocrlf en Git

¿Para qué sirve?
El comando git config --global core.autocrlf se usa para configurar cómo Git maneja los fines de línea (line endings) en archivos de texto, lo cual es importante al trabajar en diferentes sistemas operativos (Windows, macOS, Linux).

Valores comunes:

**- true (recomendado para Windows):**

Convierte LF a CRLF al hacer checkout.
Convierte CRLF a LF al hacer commit.

**- input (recomendado para macOS/Linux):**

Convierte CRLF a LF al hacer commit, pero no hace conversiones al hacer checkout.

**- false**

Desactiva cualquier conversión de fines de línea (no recomendado para colaboración).

Ejemplos de uso:

Configuración para Windows:

```bash
git config --global core.autocrlf true
```

Configuración para macOS/Linux:

```bash
git config --global core.autocrlf input
```

Desactivar conversión (no recomendado):

```bash
git config --global core.autocrlf false
```

Es recomendable configurar core.autocrlf al inicio de un proyecto para evitar problemas de fines de línea, especialmente en entornos colaborativos. Si ya existe un repositorio con problemas de fines de línea, se puede usar un archivo .gitattributes para normalizarlos.


Si no configuras core.autocrlf, podrías enfrentarte a problemas como:

- Archivos marcados como modificados sin razón aparente (debido a cambios en los fines de línea).

- Conflictos al fusionar código con otros desarrolladores.

- Inconsistencias en el repositorio.

---

### **2. Iniciar un Repositorio Local**

#### **2.1. Crear un Repositorio Local**

1. Abre una terminal y navega a la carpeta donde quieres crear tu proyecto:

```bash
cd Documentos/Proyectos
mkdir mi-proyecto
cd mi-proyecto
```

2. Inicializa un repositorio Git:

```bash
git init
```

#### **2.2. Agregar Archivos al Repositorio**

1. Crea un archivo de ejemplo (ejemplo: `README.md`):

```bash
echo "# Mi Proyecto" > README.md
```

2. Agrega los archivos al "stage":


```bash
git add .
```

3. Crea un commit:

```bash
git commit -m "Commit inicial"
```

---

### **3. Conectar el Repositorio Local a un Remoto**

#### **3.1. Crear un Repositorio Remoto en GitHub**

1. Inicia sesión en [GitHub](https://github.com).
2. Haz clic en el botón "+" en la esquina superior derecha y selecciona "New repository".
3. Elige un nombre para tu repositorio (ejemplo: "mi-proyecto").
4. Decide si el repositorio será público o privado.
5. Haz clic en "Create repository".
6. Copia la URL de clonación (puedes elegir entre HTTPS o SSH).

#### **3.2. Conectar el Repositorio Local al Remoto**

1. Conecta el repositorio local al remoto usando la URL que copiaste de GitHub:

   - **SSH**:
   
```bash
git remote add origin git@github.com:tu_usuario/mi-proyecto.git
```

   - **HTTPS**:
   
```bash
git remote add origin https://github.com/tu_usuario/mi-proyecto.git
```

2. Envía los cambios al repositorio remoto:
  
```bash
git push -u origin main
```

#### Resumen en codigo.

```bash
# Crear repositorio local y conectar al remoto
cd Documentos/Proyectos
mkdir mi-proyecto
cd mi-proyecto
git init
git remote add origin git@github.com:tu_usuario/mi-proyecto.git  # O HTTPS
echo "# Mi Proyecto" > README.md
git add .
git commit -m "Commit inicial"
git push -u origin main
```

Recuerda reemplazar tu_usuario con tu nombre de usuario de GitHub y mi-proyecto con el nombre de tu proyecto.


---

### **4. Clonar un Repositorio Remoto**

#### **4.1. Clonar con HTTPS**

Si no has configurado SSH o prefieres usar HTTPS, puedes clonar un repositorio de la siguiente manera:

1. Copia la URL HTTPS del repositorio en GitHub.
2. Abre una terminal y navega a la carpeta donde quieres clonar el repositorio.
3. Ejecuta el siguiente comando:

```bash
git clone https://github.com/tu_usuario/mi-proyecto.git
```

#### **4.2. Clonar con SSH**

Si has configurado SSH en GitHub, puedes clonar el repositorio de manera más segura:

1. Copia la URL SSH del repositorio en GitHub.
2. Abre una terminal y navega a la carpeta donde quieres clonar el repositorio.
3. Ejecuta el siguiente comando:

```bash
git clone git@github.com:tu_usuario/mi-proyecto.git
```

---

### **5. Configurar SSH para Git**

#### **5.1. Generar una Clave SSH**

1. Ejecuta el siguiente comando para generar una clave SSH:

```bash
ssh-keygen -t ed25519 -C "tu_correo@ejemplo.com"
```

   - `-t ed25519`: Especifica el tipo de clave (ed25519 es más seguro).
   - `-C "tu_correo@ejemplo.com"`: Agrega un comentario con tu correo.
   
Otro ejemplo con otro algoritmo:

```bash
ssh-keygen -t rsa -b 4096 -C "tu_correo@ejemplo.com"
```

   - `-t rsa`: Especifica el tipo de clave (RSA).
   - `-b 4096`: Longitud de la clave (4096 bits).
   - `-C "tu_correo@ejemplo.com"`: Agrega un comentario con tu correo.


2. Guarda la clave en la ubicación predeterminada o elige otra.
3. Opcional: Ingresa una frase de contraseña.


Se te pedirá que elijas una ubicación para guardar las claves. Puedes aceptar la ubicación predeterminada (generalmente ~/.ssh/id_rsa) o elegir otra. También se te pedirá que ingreses una frase de contraseña (opcional). ejemplo: "rogelin2"

#### **5.2. Agregar la Clave SSH a GitHub**

1. Copia el contenido de la clave pública:

```bash
cat ~/.ssh/id_ed25519.pub
```

   1. Copia el contenido del archivo de clave pública (~/.ssh/id_rsa.pub). Puedes abrirlo con un editor de texto o usar el comando cat ~/.ssh/id_rsa.pub.
   2. Inicia sesión en GitHub.
   3. Ve a la configuración de tu cuenta (haz clic en tu foto de perfil y luego en "Settings").
   4. En la barra lateral, haz clic en "SSH and GPG keys".
   5. Haz clic en "New SSH key" o "Add SSH key".
   6. Pega el contenido de la clave pública en el campo "Key".
   7. Asigna un título a la clave (por ejemplo, "Mi computadora").
   8. Haz clic en "Add SSH key".

#### **5.3. Verificar la Conexión SSH**

Prueba la conexión con GitHub:

```bash
ssh -T git@github.com
```

Si todo está configurado correctamente, verás un mensaje como:

```
Hi tu_usuario! You've successfully authenticated...
```
---

#### Cambiar el Remoto a SSH**

Si ya tienes un repositorio configurado con HTTPS, puedes cambiarlo a SSH:

```bash
git remote set-url origin git@github.com:tu_usuario/tu_repositorio.git

```
---

#### Algoritmos para Generar Claves SSH**

El comando ssh-keygen te permite generar claves SSH utilizando diferentes algoritmos criptográficos

ed25519: Este es el algoritmo más moderno y seguro. Se recomienda su uso por su alta seguridad y eficiencia.

- **ed25519** (recomendado):

```bash
ssh-keygen -t ed25519 -C "tu_correo@ejemplo.com"
```

- **RSA** (ampliamente compatible):

rsa: Es un algoritmo más antiguo pero que aún se considera seguro. Es ampliamente utilizado y compatible con muchos sistemas.

```bash
ssh-keygen -t rsa -b 4096 -C "tu_correo@ejemplo.com"
```

(El parámetro -b 4096 especifica la longitud de la clave en bits. Se recomienda usar al menos 4096 bits para mayor seguridad).

**ECDSA**: Otro algoritmo moderno basado en curvas elípticas. Ofrece buena seguridad y eficiencia.
  
- **ECDSA** (basado en curvas elípticas):

```bash
ssh-keygen -t ecdsa -b 521 -C "tu_correo@ejemplo.com"
```

(El parámetro -b 521 especifica la longitud de la clave. Es un valor común para claves ECDSA).


El parámetro -C "" en el comando ssh-keygen se utiliza para agregar un comentario a la clave pública. Este comentario puede ser cualquier texto que desees, como tu dirección de correo electrónico, tu nombre o una descripción de la clave

---

## Conexión de repositorio local modificado a remoto desactualizado desde cero

### Preparación inicial en tu nueva PC

### 1\. Activar el agente SSH y gestionar tus claves

Este paso es crucial para que tu computadora se comunique de forma segura con GitHub.

```bash
eval "$(ssh-agent -s)"          # Inicia el agente SSH

ssh-add -D                      # Elimina cualquier clave SSH previamente cargada

ssh-add ~/.ssh/ssh01/id_ed25519 # Agrega tu nueva clave SSH. ¡Importante! Asegúrate que la ruta sea correcta.

ssh-add -l                      # Verifica que la clave SSH se haya agregado correctamente
```

**Nota:** Si aún no tienes una clave SSH generada, deberás crearla antes de agregarla. La ruta `~/.ssh/ssh01/id_ed25519` es un ejemplo.

### 2\. Probar la conexión SSH

Después de agregar tu clave, es buena práctica verificar la conexión.

```bash
ssh -T git@github.com # Prueba la conexión con GitHub
```

Si la conexión es exitosa, verás un mensaje de autenticación correcta.

### 3\. Clonar el repositorio remoto

Ahora, clona el repositorio remoto desactualizado en tu nueva PC.

```bash
git clone <URL_DEL_REPOSITORIO_REMOTO>
```

Reemplaza `<URL_DEL_REPOSITORIO_REMOTO>` con la URL de tu repositorio de GitHub (la encuentras en la página de tu repositorio).


### 4\. Resolver conflictos y subir tus cambios

Una vez que hayas copiado los archivos, Git detectará las diferencias. Es muy probable que existan conflictos debido a que el repositorio remoto está desactualizado.

```bash
cd <NOMBRE_DE_TU_REPOSITORIO> # Navega a la carpeta de tu repositorio clonado
git status                   # Verifica el estado de los archivos (mostrará los cambios)
git add .                    # Agrega todos los archivos modificados y nuevos al área de staging
git commit -m "Sincronizando bóveda de Obsidian desde nueva PC" # Crea un commit con tus cambios
git pull origin main         # Descarga los cambios del remoto y los fusiona con tu rama local (usa 'master' si es la rama principal de tu repositorio)
```

Durante el `git pull`, es muy probable que Git te notifique sobre **conflictos de fusión**. Deberás **resolver estos conflictos manualmente** editando los archivos afectados para elegir qué versión quieres conservar.

Después de resolver todos los conflictos, haz un nuevo commit para confirmar la resolución:

```bash
git add .
git commit -m "Resolución de conflictos y actualización de bóveda"
```

### 5\. Subir tus cambios al repositorio remoto

Finalmente, envía tus cambios locales (incluidas las modificaciones de tu bóveda de Obsidian y las resoluciones de conflictos) al repositorio remoto.

```bash
git push origin main # O 'master'
```



---


### Rama - Branch

### 1. **Crear una rama**

Para crear una nueva rama en Git, puedes usar el siguiente comando:

```bash
git branch nombre_de_la_rama
```

Este comando crea una nueva rama, pero no cambia automáticamente a ella. Para crear una rama y cambiarte a ella inmediatamente, puedes usar:

```bash
git checkout -b nombre_de_la_rama
```

O, en versiones más recientes de Git (2.23+), puedes usar:

```bash
git switch -c nombre_de_la_rama
```

### 2. **Eliminar una rama**

Para eliminar una rama local que ya no necesitas, puedes usar:

```bash
git branch -d nombre_de_la_rama
```

Si la rama tiene cambios que no han sido fusionados y estás seguro de que quieres eliminarla de todos modos, puedes forzar la eliminación con:

```bash
git branch -D nombre_de_la_rama
```

Para eliminar una rama remota, usa:

```bash
git push origin --delete nombre_de__la_rama
```

### 3. **Moverse entre ramas**

Para cambiar a una rama existente, puedes usar:

```bash
git checkout nombre_de_la_rama
```

O, en versiones más recientes de Git (2.23+), puedes usar:

```bash
git switch nombre_de_la_rama
```

### 4. **Listar o ver ramas**

Para listar todas las ramas locales en tu repositorio, usa:

```bash
git branch
```

Esto mostrará una lista de ramas locales, con un asterisco (`*`) al lado de la rama actual.

Para listar todas las ramas, incluyendo las remotas, usa:

```bash
git branch -a
```

Para listar solo las ramas remotas, usa:

```bash
git branch -r
```

### 5. **Renombrar una rama**

Para renombrar una rama local, puedes usar:

```bash
git branch -m nombre_actual nuevo_nombre
```

Si la rama ya ha sido enviada al repositorio remoto, deberás eliminar la rama antigua y enviar la nueva:

```bash
git push origin --delete nombre_actual
git push origin nuevo_nombre
```

### 6. **Fusionar ramas**

Para fusionar una rama en la rama actual, primero cambia a la rama de destino y luego usa:

```bash
git merge nombre_de_la_rama_a_fusionar
```

### 7. **Rebasar ramas**

El rebase es una alternativa a la fusión. Para rebasar la rama actual con otra rama, usa:

```bash
git rebase nombre_de_la_rama
```

Esto aplicará los cambios de la rama especificada sobre la rama actual.

### 8. **Sincronizar ramas remotas**

Para actualizar tu lista de ramas remotas y asegurarte de que estás al día con los cambios en el repositorio remoto, usa:

```bash
git fetch origin
```

Para actualizar una rama local con los cambios de su contraparte remota, puedes usar:

```bash
git pull origin nombre_de_la_rama
```

### 9. **Crear una rama a partir de un commit específico**

Si deseas crear una rama a partir de un commit específico, primero encuentra el hash del commit (puedes usar `git log` para ver los commits) y luego usa:

```bash
git branch nombre_de_la_rama hash_del_commit
```

### 10. **Comparar ramas**

Para ver las diferencias entre dos ramas, puedes usar:

```bash
git diff nombre_de_la_rama1..nombre_de_la_rama2
```

### 11. **Forzar el movimiento a una rama (descarta cambios locales)**

Si tienes cambios locales que no deseas conservar y quieres forzar el cambio a otra rama, puedes usar:

```bash
git reset --hard
git checkout nombre_de_la_rama
```

### 12. **Ver el historial de una rama**

Para ver el historial de commits de una rama específica, usa:

```bash
git log nombre_de_la_rama
```

### 13. **Crear una rama y hacer un seguimiento de la rama remota**

Si creas una rama local y quieres que haga seguimiento de una rama remota, puedes usar:

```bash
git checkout --track origin/nombre_de_la_rama
```

O, en versiones más recientes de Git:

```bash
git switch --track origin/nombre_de_la_rama
```

### 14. **Eliminar ramas locales que ya no existen en el remoto**

Si has eliminado ramas remotas y quieres limpiar las ramas locales que ya no tienen un equivalente remoto, puedes usar:

```bash
git fetch --prune
```

Esto eliminará automáticamente las ramas locales que ya no tienen un rastro en el repositorio remoto.

### 15. **Crear una rama a partir de un tag**

Si deseas crear una rama a partir de un tag, puedes usar:

```bash
git branch nombre_de_la_rama nombre_del_tag
```

### 16. **Ver la última rama en la que estabas**

Si quieres volver a la última rama en la que estabas trabajando, puedes usar:

```bash
git checkout -
```

O, en versiones más recientes de Git:

```bash
git switch -
```

### 17. **Verificar el estado de las ramas**

Para ver el estado actual de las ramas, incluyendo cuáles tienen cambios no comprometidos, puedes usar:

```bash
git status
```

### 18. **Crear una rama y enviarla al repositorio remoto**

Si creas una rama local y quieres enviarla al repositorio remoto inmediatamente, puedes usar:

```bash
git push -u origin nombre_de_la_rama
```

El flag `-u` (o `--set-upstream`) establece la rama local para hacer seguimiento de la rama remota.

### 19. **Verificar diferencias entre la rama local y la remota**

Para ver las diferencias entre tu rama local y su contraparte remota, puedes usar:

```bash
git diff origin/nombre_de_la_rama
```

### 20. **Forzar la actualización de una rama local con la remota**

Si quieres actualizar tu rama local con los cambios de la rama remota y descartar cualquier cambio local, puedes usar:

```bash
git reset --hard origin/nombre_de_la_rama
```

### En el siguiente enlace continuan los comandos desde 01 hasta el 89 con comando como:

#### LINK [[git Ramas Visores]]


- Verificar el historial de una rama en un formato gráfico

```bash
git log --graph --oneline --decorate --all
```

- visores de historial como: **Tig Lazygit**
    intalacion, comandos, etc.

- Diferencias entre `git checkout` y `git switch`



---

### **6. Comandos Básicos de Git**

#### **6.0. Configurar nombre y correo:

#### Muestra todas las propiedades que Git ha configurado

```bash
git config --list
```

```bash
  git config --global user.name "Tu nombre"
  git config --global user.email "tu_correo@ejemplo.com"
```
#### **6.1. Iniciar un Repositorio**

```bash
git init
```

#### **6.2. Agregar Archivos al Stage**

```bash
git add .
```
#### Saca el archivo del area de stage

```bash
$git rm --cached nombre_del_archivo.txt
```

#### **6.3. Crear un Commit**

```bash
git commit -m "Mensaje descriptivo"
```

#### Muestra informacion de cada version. se muestra despues de hacer commit

```bash
$git log
```

#### Muestra todos los procesos con su id en una sola linea. se muestra despues de hacer commit

```bash
git log --on line
```

#### Nos lleva a la version que uno quiere con el numero id que muestra log --online

```bash
git checkout numero_ID
```

#### Nos lleva a la ultima version 

```bash
git switch -
```


#### **6.4. Subir Cambios al Repositorio Remoto**

```bash
git push -u origin main
```

#### **6.5. Ver el Estado del Repositorio**

```bash
git status
```

Tambien se puede utilizar git status -s. Es mas resumido.

```bash
git status -s
```

**M: Modificado (Modified)**

  M en la primera columna: El archivo ha sido modificado en el working directory pero aún no ha sido añadido al staging area.

  M en la segunda columna: El archivo ha sido modificado y añadido al staging area.

**D: Eliminado (Deleted)**

  D en la primera columna: El archivo ha sido eliminado en el working directory pero aún no se ha registrado en el staging area.

  D en la segunda columna: El archivo ha sido eliminado y se ha registrado en el staging area.

**A: Añadido (Added)**

  A en la segunda columna: El archivo es nuevo y ha sido añadido al staging area.

**??: Sin seguimiento (Untracked)**

  ??: El archivo es nuevo y no está siendo rastreado por Git (no ha sido añadido al staging area).

**R: Renombrado (Renamed)**

  R: El archivo ha sido renombrado y el cambio ha sido añadido al staging area.

**C: Copiado (Copied)**

  C: El archivo ha sido copiado y el cambio ha sido añadido al staging area.

**U: Actualizado pero sin merge (Updated but unmerged)**

  U: El archivo tiene conflictos que no han sido resueltos después de un merge.


Ejemplo de salida:

```bash
M README.md
D  file.txt
A  newfile.js
?? untrackedfile.py
```

En este ejemplo:

 README.md ha sido modificado en el working directory pero no en el staging area.

 file.txt ha sido eliminado y el cambio está en el staging area.

 newfile.js es un archivo nuevo que ha sido añadido al staging area.

 untrackedfile.py es un archivo nuevo que no está siendo rastreado por Git.

####  Muestra info 

```bash
git remote -v
```

#### **6.6. Ver el Historial de Commits**

```bash
git log
```

#### **6.7. Manejo de Ramas**

- Crear una nueva rama:

```bash
git branch nombre_rama
```

- Cambiar a una rama:

```bash
git checkout nombre_rama
```

- Fusionar ramas:

```bash
git merge nombre_rama
```

---

### **7. Solución de Problemas Comunes**

#### **7.1. Error al Agregar un Remoto Repetido**

Si accidentalmente agregas el remoto dos veces, puedes eliminarlo y volver a agregarlo:

```bash
git remote -v
```

```bash
git remote remove origin
git remote add origin git@github.com:tu_usuario/tu_repositorio.git
```


Asi se tendria que ver el estado del origin

```bash
origin  git@github.com:marianognux/notasobsidian.git (fetch)
origin  git@github.com:marianognux/notasobsidian.git (push)
```

Y no asi:


```bash
origin  git@github.com:marianognux/notasobsidian.git (fetch)
origin  git@github.com:marianognux/notasobsidian.git (push)
origin  git@github.com:marianognux/notasobsidian.git (fetch)
origin  git@github.com:marianognux/notasobsidian.git (push)
```


#### **7.2. Confiar en la Clave SSH del Servidor**

Si Git muestra el mensaje:

```
The authenticity of host 'github.com' can't be established...
```

Responde con `yes` para confiar en la clave del servidor.

---

### **8. Uso de `.gitignore`**

Para ignorar archivos específicos en tu repositorio, crea un archivo llamado `.gitignore` y agrega los nombres de los archivos o carpetas que deseas ignorar.

---

### **9. Script para Configuración Automática de SSH y Git**

Puedes crear un script para configurar SSH y Git automáticamente:


```bash
#!/bin/bash
mkdir -p ~/.ssh
cp /ruta/a/pendrive/id_ed25519 ~/.ssh/
cp /ruta/a/pendrive/id_ed25519.pub ~/.ssh/
chmod 600 ~/.ssh/id_ed25519
chmod 600 ~/.ssh/id_ed25519.pub
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
git config --global user.name "Tu Nombre"
git config --global user.email "tuemail@ejemplo.com"
```

Scripts con datos verdaderos

```bash
#!/bin/bash
mkdir -p ~/.ssh
cp /media/user/bodzzy/sshKeys/id_ed25519 ~/.ssh/
cp /media/user/bodzzy/sshKeys/id_ed25519.pub ~/.ssh/
chmod 600 ~/.ssh/id_ed25519
chmod 600 ~/.ssh/id_ed25519.pub
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
git config --global user.name "rogeobsid"
git config --global user.email "2022lgk4@gmail.com"
```

---

### **10. Resumen de Comandos Útiles**

#### **10.1. Comandos de Git**
- Verificar estado:

```bash
git status
```

- Ver historial de commits:
- 
```bash
git log
```

- Subir cambios:

```bash
  git push
```
- Bajar cambios:

  ```bash
  git pull
  ```

#### **8.2. Comandos de SSH**
- Iniciar agente SSH:

  ```bash
  eval "$(ssh-agent -s)"
  ```

- Agregar clave SSH:

  ```bash
  ssh-add ~/.ssh/id_ed25519
  ```


---

## Comandos básicos de Git:


```bash
# Verifica el estado del repositorio (cambios pendientes, rama actual, etc.)
git status

# Añade todos los cambios al stage (prepara los archivos para el commit)
git add .

# Añade un archivo específico al stage
git add nombre_del_archivo

# Crea un commit con los cambios que están en el stage
git commit -m "Mensaje descriptivo del commit"

# Sube los cambios al repositorio remoto (requiere especificar la rama remota)
git push origin nombre_de_la_rama

# Sube los cambios y configura la rama remota como upstream (solo la primera vez)
git push -u origin nombre_de_la_rama

# Sube los cambios si ya configuraste el upstream (no necesitas especificar la rama)
git push

# Muestra todas las ramas locales y su relación con las ramas remotas
git branch -vv

# Cambia el upstream de la rama actual a una rama remota específica
git branch --set-upstream-to=origin/nombre_de_la_rama
```

Comandos relacionados con SSH:

```bash
# Inicia el agente SSH en segundo plano
eval "$(ssh-agent -s)"

# Añade una clave SSH privada al agente SSH
ssh-add ~/.ssh/id_ed25519

# Muestra las claves SSH cargadas en el agente SSH
ssh-add -l

# Prueba la conexión SSH con GitHub
ssh -T git@github.com
```

Comandos para configurar Git:

```bash
# Configura tu nombre de usuario globalmente en Git
git config --global user.name "Tu nombre de usuario"

# Configura tu correo electrónico globalmente en Git
git config --global user.email "tu_correo@ejemplo.com"

# Muestra la URL del repositorio remoto
git remote -v

# Cambia la URL del repositorio remoto
git remote set-url origin git@github.com:usuario/repositorio.git
```

Comandos para resolver problemas específicos:

```bash
# Confirma que confías en la clave SSH del servidor (cuando Git lo pregunta)
yes

# Verifica si tienes acceso al repositorio y si la clave SSH está configurada correctamente
ssh -T git@github.com
```

Explicación del mensaje de error y solución:

```bash
# Mensaje de Git: "The authenticity of host 'github.com' can't be established..."
# Solución: Responde "yes" para confiar en la clave del servidor.
yes

# Si el error persiste, verifica la conexión SSH y la configuración de la clave.
ssh -T git@github.com
```


---

### Git log y varias opciones

Con:

```bash
git log --una_de_92_opciones
```

Ejemplo:

```bash
git log --oneline
```

```bash
git log --color
```

1. **--abbrev**: Muestra los identificadores de commit abreviados.
2. **--max-parents=**: Limita los commits a aquellos con un número máximo de padres.
3. **--abbrev=**: Especifica la longitud de los identificadores abreviados.
4. **--merges**: Muestra solo commits que son merges (tienen más de un padre).
5. **--abbrev-commit**: Muestra los identificadores de commit abreviados.
6. **--min-age=**: Limita los commits a aquellos más antiguos que la fecha especificada.
7. **--after=**: Muestra commits realizados después de la fecha especificada.
8. **--minimal**: Realiza un diff más lento pero más preciso.
9. **--all**: Muestra todos los commits en todas las ramas.
10. **--min-parents=**: Limita los commits a aquellos con un número mínimo de padres.
11. **--all-match**: Filtra commits que cumplen con todos los criterios especificados.
12. **--name-only**: Muestra solo los nombres de los archivos modificados.
13. **--anchored=**: Filtra diffs basados en un patrón anclado.
14. **--name-status**: Muestra el estado y nombre de los archivos modificados.
15. **--author=**: Filtra commits por autor.
16. **--no-abbrev-commit**: Muestra los identificadores de commit completos.
17. **--before=**: Muestra commits realizados antes de la fecha especificada.
18. **--no-color**: Desactiva el coloreado de la salida.
19. **--binary**: Incluye archivos binarios en el diff.
20. **--no-color-moved**: Desactiva el coloreado de líneas movidas en el diff.
21. **--branches**: Muestra commits en las ramas especificadas.
22. **--no-color-moved-ws**: Desactiva el coloreado de espacios en líneas movidas.
23. **--check**: Verifica la integridad del patch.
24. **--no-decorate**: No muestra las referencias (ramas, tags) en los commits.
25. **--cherry-mark**: Marca commits que son cherry-picks.
26. **--no-expand-tabs**: No expande tabs en el diff.
27. **--cherry-pick**: Muestra solo commits que son cherry-picks.
28. **--no-ext-diff**: Desactiva diffs externos.
29. **--children**: Muestra los hijos de cada commit.
30. **--no-indent-heuristic**: Desactiva la heurística de indentación en el diff.
31. **--color**: Colorea la salida.
32. **--no-max-parents**: No limita el número máximo de padres.
33. **--color-moved**: Colorea las líneas movidas en el diff.
34. **--no-merges**: Oculta los commits de merge.
35. **--color-moved=**: Especifica cómo colorear las líneas movidas.
36. **--no-min-parents**: No limita el número mínimo de padres.
37. **--color-moved-ws=**: Especifica cómo colorear los espacios en líneas movidas.
38. **--no-notes**: No muestra notas asociadas a los commits.
39. **--color-words**: Colorea palabras en el diff.
40. **--no-patch**: No muestra el diff.
41. **--committer=**: Filtra commits por committer.
42. **--no-prefix**: No muestra prefijos en el diff.
43. **--cumulative**: Muestra estadísticas acumulativas en el diff.
44. **--no-renames**: No detecta renombres de archivos en el diff.
45. **--date=**: Filtra commits por fecha.
46. **--not**: Invierte la lógica de filtrado.
47. **--date-order**: Ordena los commits por fecha.
48. **--notes**: Muestra notas asociadas a los commits.
49. **--decorate**: Muestra referencias (ramas, tags) en los commits.
50. **--no-textconv**: Desactiva la conversión de texto en el diff.
51. **--decorate=**: Especifica cómo mostrar las referencias.
52. **--no-walk**: No recorre los commits padres.
53. **--dense**: Oculta commits que no son relevantes en el historial.
54. **--no-walk=**: Especifica cómo no recorrer los commits padres.
55. **--diff-algorithm=**: Especifica el algoritmo de diff a utilizar.
56. **--numstat**: Muestra estadísticas numéricas del diff.
57. **--diff-filter=**: Filtra archivos por tipo de cambio en el diff.
58. **--oneline**: Muestra cada commit en una sola línea.
59. **--dirstat**: Muestra estadísticas de directorios en el diff.
60. **--parents**: Muestra los padres de cada commit.
61. **--dirstat=**: Especifica cómo mostrar estadísticas de directorios.
62. **--patch**: Muestra el diff en formato patch.
63. **--dirstat-by-file**: Muestra estadísticas de directorios por archivo.
64. **--patch-with-stat**: Muestra el diff con estadísticas.
65. **--dirstat-by-file=**: Especifica cómo mostrar estadísticas por archivo.
66. **--patience**: Usa el algoritmo de diff "patience".
67. **--do-walk**: Recorre los commits padres (opuesto a --no-walk).
68. **--pickaxe-all**: Muestra todos los cambios cuando se usa pickaxe.
69. **--dst-prefix=**: Especifica el prefijo de destino en el diff.
70. **--pickaxe-regex**: Usa expresiones regulares con pickaxe.
71. **--exit-code**: Devuelve un código de salida basado en si hubo cambios.
72. **--pretty=**: Especifica el formato de salida de los commits.
73. **--expand-tabs**: Expande tabs en el diff.
74. **--quiet**: Suprime la salida, solo muestra errores.
75. **--expand-tabs=**: Especifica cómo expandir tabs en el diff.
76. **--raw**: Muestra el diff en formato raw.
77. **--ext-diff**: Permite el uso de diffs externos.
78. **--relative-date**: Muestra fechas en formato relativo.
79. **--find-copies-harder**: Esfuerza la detección de copias en el diff.
80. **--remotes**: Muestra commits en los remotos especificados.
81. **--first-parent**: Solo sigue el primer padre en los merges.
82. **--reverse**: Muestra los commits en orden inverso.
83. **--follow**: Sigue los renombres de archivos en el historial.
84. **--root**: Incluye el commit raíz en el historial.
85. **--format=**: Especifica un formato personalizado para la salida.
86. **--shortstat**: Muestra un resumen estadístico del diff.
87. **--full-diff**: Muestra el diff completo en lugar de solo los cambios.
88. **--show-signature**: Muestra la firma GPG de los commits.
89. **--full-history**: Muestra todo el historial sin simplificaciones.
90. **--simplify-by-decoration**: Simplifica el historial basado en commits decorados.
91. **--full-index**: Muestra el índice completo en el diff.
92. **--simplify-merges**: Simplifica los merges en el historial.





