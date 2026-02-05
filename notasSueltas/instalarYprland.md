
Hyprland requiere algunas dependencias para funcionar correctamente. Instálalas con:

```bash
sudo apt install -y git cmake meson pkg-config libwayland-dev libxkbcommon-dev libwlroots-dev libpixman-1-dev libinput-dev libxcb-xinput-dev libxcb-composite0-dev libxcb-icccm4-dev libxcb-image0-dev libxcb-present-dev libxcb-randr0-dev libxcb-xfixes0-dev libxcb-xkb-dev libxcb-xrm-dev libxcb1-dev libxcb-ewmh-dev libxcb-dri3-dev libxcb-shm0-dev libxcb-sync-dev libxcb-xinerama0-dev libxcb-xinput-dev libxcb-xtest0-dev libxcb-xvmc-dev libxcb-xv-dev libxcb-res0-dev libxcb-record0-dev libxcb-render-util0-dev libxcb-render0-dev libxcb-shape0-dev libxcb-util-dev libxcb-xf86dri0-dev libxcb-xprint0-dev libxcb-xv0-dev libxcb-xvmc0-dev libxcb-keysyms1-dev libxcb-icccm4-dev libxcb-image0-dev libxcb-present-dev libxcb-randr0-dev libxcb-xfixes0-dev libxcb-xkb-dev libxcb-xrm-dev libxcb1-dev libxcb-ewmh-dev libxcb-dri3-dev libxcb-shm0-dev libxcb-sync-dev libxcb-xinerama0-dev libxcb-xinput-dev libxcb-xtest0-dev libxcb-xvmc-dev libxcb-xv-dev libxcb-res0-dev libxcb-record0-dev libxcb-render-util0-dev libxcb-render0-dev libxcb-shape0-dev libxcb-util-dev libxcb-xf86dri0-dev libxcb-xprint0-dev libxcb-xv0-dev libxcb-xvmc0-dev libxcb-keysyms1-dev
```

Hyprland no está en los repositorios oficiales de Debian, por lo que debes compilarlo desde el código fuente.
Clona el repositorio de Hyprland:

```bash
git clone https://github.com/hyprwm/Hyprland.git
cd Hyprland
```

Compila e instala Hyprland:

```bash
meson build
ninja -C build
sudo ninja -C build install
```

Configura el entorno de inicio

Si estás utilizando un gestor de inicio de sesión como lightdm o gdm, selecciona Hyprland como tu entorno de escritorio.

Si no tienes un gestor de inicio de sesión, puedes iniciar Hyprland manualmente desde la terminal agregando lo siguiente a tu archivo ~/.xinitrc:



```bash
exec Hyprland
```

Luego, inicia Hyprland con:

```bash
startx
```

Configura Hyprland

Hyprland utiliza un archivo de configuración en ~/.config/hypr/hyprland.conf. Puedes crear este archivo y personalizarlo según tus necesidades.

Ejemplo básico de configuración (~/.config/hypr/hyprland.conf):

```bash
exec-once = dbus-update-activation-environment --systemd DISPLAY WAYLAND_DISPLAY

monitor = ,preferred,auto,1

input {
    kb_layout = us
    follow_mouse = 1
}

general {
    gaps_in = 5
    gaps_out = 10
    border_size = 2
    col.active_border = rgba(33ccffee) rgba(00ff99ee) 45deg
    col.inactive_border = rgba(595959aa)
}

decoration {
    rounding = 10
    blur = true
    blur_size = 3
    blur_passes = 1
}

animations {
    enabled = yes
}

dwindle {
    pseudotile = yes
    preserve_split = yes
}

master {
    new_is_master = true
}

gestures {
    workspace_swipe = yes
}
```

Reinicia o inicia Hyprland

Si todo está configurado correctamente, reinicia tu sistema o inicia Hyprland manualmente.

Ejemplo de ~/.xinitrc

Si quieres iniciar Hyprland automáticamente al usar startx, tu archivo ~/.xinitrc podría verse as


```bash
#!/bin/bash
# Iniciar Hyprland
exec Hyprland
```
Pasos para usar ~/.xinitrc en Debian:

Crea el archivo:
Si no existe, crea el archivo en tu directorio home:

```bash
nano ~/.xinitrc
```



```bash

```

Agrega el comando para iniciar Hyprland:
Añade la línea exec Hyprland al archivo, como se muestra en el ejemplo anterior.

Haz que el archivo sea ejecutable:
Asegúrate de que el archivo tenga permisos de ejecución:

```bash
chmod +x ~/.xinitrc
```

nicia el entorno gráfico:
Ejecuta startx en la terminal para iniciar Hyprland:

```bash
startx
```



```bash

```


```bash

```



```bash

```


MPD
NCMPPCPP
CANTATA



