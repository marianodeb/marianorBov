

## Script para su instalacion

```bash
#!/bin/bash

echo "************************"
echo "*** Instalando kitty ***"
echo "************************"

#Descarga e instalacion
curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin

# Crear el directorio bin
mkdir -p ~/.local/bin

# Crear enlaces simbolicos
ln -sf ~/.local/kitty.app/bin/kitty ~/.local/kitty.app/bin/kitten ~/.local/bin/

# Agrefgar bin a al paht
export PATH=$HOME/.local/bin:$PATH

# Copiar el archivo kitty.desktop para que kitti aparezca en el menu de aplicaciones
cp ~/.local/kitty.app/share/applications/kitty.desktop ~/.local/share/applications/

# Esto hace que aparezca elicono en el menu de aplicaciones
sed -i "s|Icon=kitty|Icon=$HOME/.local/kitty.app/share/icons/hicolor/256x256/apps/kitty.png|g" ~/.local/share/applications/kitty.desktop
sed -i "s|Exec=kitty|Exec=$HOME/.local/kitty.app/bin/kitty|g" ~/.local/share/applications/kitty.desktop

update-desktop-database ~/.local/share/applications/

echo "************************"
echo "***** kitten themes ****"
echo "************************"

# link de computadoras y sensores instalacion y configuracion
# https://www.youtube.com/watch?v=_oqf2WgEyxo
# https://sw.kovidgoyal.net/kitty/
# https://sw.kovidgoyal.net/kitty/conf/

# CONFIGURACION
# Crear el archivo kitty.conf en el directorio ~/.config/kitty
# la mejor manera de crear el archivo kitty.conf es con: "Ctrl + shift + f2" donde viene todala configuracion comentada

# Cambiar Thema   https://sw.kovidgoyal.net/kitty/kittens/themes/
# Escribimos en la terminal: "kitten themes" y saldra el menu de tehme
# Para seleccionar el thema y quede guardado seleccionar la opciion M 
# Luego se creara un archivo con los themas.

```



## Solución: Error "unknown terminal type: xterm-kitty"

### Causa raíz

- Terminal local (Kitty) usa `TERM=xterm-kitty`
- Instalaciones mínimas de Linux no reconocen este terminal
- Falta archivo terminfo para kitty en el servidor

## Soluciones permanentes

### 1 Instalar terminfo en servidor

```bash
sudo apt update && sudo apt install ncurses-term
```

Agregar al archivo **.bashrc** la siguiente linea:

```bash
export TERM=xterm  # o export TERM=xterm-256color 
```

### 2. Alias recomendado (en máquina LOCAL)

Agregar en `~/.bashrc` o `~/.zshrc`:

```bash
alias ssh-vm='ssh -t usuario@IP "export TERM=xterm-256color; exec bash"'
```

Uso: `ssh-vm` (configura automáticamente terminal compatible)

### Comandos clave de verificación

- `echo $TERM` → Muestra terminal actual
- `infocmp` → Verifica capacidades del terminal
- `toe -a` → Lista terminales disponibles

### Atajos de Teclado Esenciales en Kitty

Kitty tiene una jerarquía de organización que es útil conocer:

* **Pestañas (Tabs):** Son como las pestañas de un navegador, contienen grupos de ventanas.
* **Ventanas (Windows):** Son los paneles individuales dentro de una pestaña. Puedes tener varias ventanas en una misma pestaña.

Aquí están los atajos por defecto, asumiendo que tu tecla modificadora es `Ctrl+Shift` (que es lo más común en Kitty):

#### Manejo de Pestañas (Tabs)

* **`Ctrl+Shift+t`**: Abre una **nueva pestaña** vacía.
* **`Ctrl+Shift+q`**: Cierra la **pestaña actual**. Si es la única pestaña, cierra Kitty.
* **`Ctrl+Shift+Right Arrow` (Flecha derecha)**: Va a la **siguiente pestaña**.
* **`Ctrl+Shift+Left Arrow` (Flecha izquierda)**: Va a la **pestaña anterior**.
* **`Ctrl+Shift+f`**: Busca texto en todas las pestañas y ventanas.
* **`Ctrl+Shift+.` (Punto)**: Renombra la pestaña actual.

#### Manejo de Ventanas (Windows / Panes)

* **`Ctrl+Shift+Enter`**: Abre una **nueva ventana** (pane) en la misma pestaña. Esta nueva ventana se abrirá en la configuración de diseño actual (generalmente dividiendo la ventana activa).
* **`Ctrl+Shift+w`**: Cierra la **ventana actual**.
* **`Ctrl+Shift+[` (Corchete abierto)**: Mueve el foco a la **ventana anterior**.
* **`Ctrl+Shift+]` (Corchete cerrado)**: Mueve el foco a la **siguiente ventana**.
* **`Ctrl+Shift+h`**: Mueve el foco a la ventana a la **izquierda**.
* **`Ctrl+Shift+l`**: Mueve el foco a la ventana a la **derecha**.
* **`Ctrl+Shift+j`**: Mueve el foco a la ventana **abajo**.
* **`Ctrl+Shift+k`**: Mueve el foco a la ventana **arriba**.
* **`Ctrl+Shift+r`**: Gira las ventanas en la pestaña actual.
* **`Ctrl+Shift+d`**: Muestra las ventanas actuales en un diseño "dividido" (generalmente horizontal o vertical, ajustándose al espacio).

#### Redimensionar Ventanas

* **`Ctrl+Shift+Alt+h`**: Disminuye el ancho de la ventana actual.
* **`Ctrl+Shift+Alt+l`**: Aumenta el ancho de la ventana actual.
* **`Ctrl+Shift+Alt+j`**: Disminuye la altura de la ventana actual.
* **`Ctrl+Shift+Alt+k`**: Aumenta la altura de la ventana actual.

#### Otras Utilidades

* **`Ctrl+Shift+c`**: **Copia** la selección al portapapeles.
* **`Ctrl+Shift+v`**: **Pega** el contenido del portapapeles.
* **`Ctrl+Shift+s`**: Guarda el historial de scrollback de la ventana actual en un archivo.
* **`Ctrl+Shift+u`**: Abre una URL detectada en el texto.
* **`Ctrl+Shift+p`**: Abre el "fuzzer" (buscador) de comandos de Kitty. Muy útil si olvidas un atajo.
* **`Ctrl+Shift+m`**: Maximiza la ventana actual. Vuelve a presionarlo para restaurar.
* **`Ctrl+Shift+PageUp`**: Desplazarse hacia arriba en el historial.
* **`Ctrl+Shift+PageDown`**: Desplazarse hacia abajo en el historial.

---