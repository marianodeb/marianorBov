
## Configuracion polybar

Todo se configura en el archivo `~/.config/polybar/config.ini`.

### 1. La Anatomía de la Barra (Sintaxis)

Cada barra que quieras crear empieza con un encabezado: `[bar/nombre_que_quieras]`.

#### Posición y Tamaño
Dentro de ese bloque, definís el cuerpo de la barra:

```ini
[bar/mi_principal]
; Si tenés varios monitores, podés elegir uno o dejarlo vacío para el principal
monitor = HDMI-1 

; Ancho y Alto (pueden ser píxeles o porcentaje)
width = 100%
height = 24pt

; Posición (top o bottom)
bottom = false 

; Centrar la barra (si el ancho es menor al 100%)
fixed-center = true

; Margen y redondeado (opcional)
radius = 10
offset-x = 5%
offset-y = 10
```

* **`width` / `height`**: Usá `90%` si querés que flote o `100%` si querés que ocupe todo el borde.
* **`offset-x` / `offset-y`**: Es lo que "despega" la barra de los bordes. Si ponés `offset-x = 10%` y `width = 80%`, la barra queda perfectamente centrada con aire a los costados.


### 2. Cómo crear más de una barra

Es muy común querer una barra arriba para info y otra abajo para tareas, o una en cada monitor. 

**Paso 1: Definir dos bloques en el `config.ini`**
```ini
[bar/barra_arriba]
monitor = ${env:MONITOR:} ; Variable para que detecte el monitor
width = 100%
height = 25
modules-left = bspwm
modules-center = date

[bar/barra_abajo]
bottom = true
width = 50%
offset-x = 25% ; Centrada
height = 30
modules-center = cpu memory
```

**Paso 2: El script de lanzamiento (`launch.sh`)**
Polybar no se lanza sola; usamos un script de Bash (el que seguramente ya tenés). Para dos barras, tenés que llamarlas por su nombre:

```bash
#!/bin/bash
killall -q polybar
polybar barra_arriba &
polybar barra_abajo &
```


### 3. Estética: Colores y Bordes

Para que no sea un bloque sólido aburrido, podés jugar con la transparencia y los bordes:

```ini
background = #aa282A36  ; Los primeros dos números (aa) son la transparencia (00 a ff)
foreground = #F8F8F2
border-size = 4
border-color = #00000000 ; Borde transparente para dar efecto de "aire"
```

### 4. Distribución de Módulos

La barra se divide en tres secciones. Vos elegís qué módulos van en cada una:

```ini
modules-left = bspwm xwindow
modules-center = date
modules-right = network pulseaudio battery powermenu
```


### 5. El "Truco" para bspwm

Como estás usando **bspwm**, hay dos cosas fundamentales en la configuración de la barra para que todo fluya:

1.  **`wm-restack = bspwm`**: Esto evita que las ventanas se metan "debajo" de la barra o que la barra tape menús de aplicaciones.
2.  **`override-redirect = true`**: Si querés que la barra "flote" (que no sea parte del tiling de bspwm), tenés que activar esto. **Ojo:** Si hacés esto, bspwm no sabrá que la barra existe y las ventanas la van a tapar. Tendrás que configurar un `padding` en bspwm:
    * En tu `bspwmrc`: `bspc config top_padding 35`

### Resumen de Sintaxis rápida:

* **Variables:** Podés definir colores arriba del todo como `[colors] azul = #0000ff` y usarlos como `${colors.azul}`.
* **Fuentes:** `font-0 = "JetBrainsMono Nerd Font:size=10;2"`. El `;2` es el ajuste vertical (offset).
* **Iconos:** Para usar iconos (como los de Rofi), necesitás tener instalada una **Nerd Font**.


---


## Sintaxis 

### 1. El uso de Variables (Sección `[colors]`)
En lugar de escribir el código hexadecimal (`#ffffff`) en cada módulo, lo definís una sola vez arriba. Esto te permite cambiar el tema de toda tu barra en un segundo.

```ini
[colors]
; Formato: #AARRGGBB (Alpha, Rojo, Verde, Azul)
background = #1e1e2e
background-alt = #313244
foreground = #cdd6f4
primary = #f5c2e7
secondary = #89b4fa
alert = #f38ba8
disabled = #707880

[bar/mi_barra]
; Referenciamos la variable con ${colors.nombre}
background = ${colors.background}
foreground = ${colors.foreground}
```


### 2. Configuración Maestra de la Barra
Acá es donde definís el "cuerpo". Te paso los parámetros más importantes:

```ini
[bar/principal]
; Tamaño
width = 98%
height = 28pt
radius = 12          ; Bordes redondeados
offset-x = 1%        ; Centra la barra (1% aire + 98% barra + 1% aire)
offset-y = 5         ; La despega del borde superior

; Estética
line-size = 3pt      ; Grosor de la línea de adorno debajo de los módulos
border-size = 4pt
border-color = #00000000 ; Borde transparente (hace que la barra parezca flotar)

; Fuentes (Nerd Fonts son clave para los iconos)
; Sintaxis: "Nombre:size=tamaño;vertical-offset"
font-0 = "JetBrainsMono Nerd Font:size=11;2"
font-1 = "JetBrainsMono Nerd Font:size=13;3" ; Una más grande para iconos

; Módulos
modules-left = xworkspaces
modules-center = date
modules-right = pulseaudio memory cpu powermenu

; Interacción con bspwm
wm-restack = bspwm
cursor-click = pointer
```


### 3. Tipos de Módulos (Sintaxis y Ejemplos)

Hay tres tipos principales de módulos que vas a usar:

#### A. Módulos Internos (`internal/`)
Son los que ya vienen con Polybar y leen info del sistema.

```ini
[module/cpu]
type = internal/cpu
interval = 2
; Usamos variables de colores y prefijos con iconos
format-prefix = " "
format-prefix-foreground = ${colors.primary}
label = %percentage%%
```

#### B. Módulos de Texto Fijos (`custom/text`)
Ideales para logos o botones de menú (como el de Rofi).

```ini
[module/menu]
type = custom/text
content = " " ; Icono de Arch o el que quieras
content-foreground = ${colors.secondary}
; Al hacer clic abre tu lanzador Rofi
click-left = rofi -show drun
```

#### C. Módulos de Script (`custom/script`)
Para mostrar cosas que Polybar no sabe leer sola (clima, música, etc.).

```ini
[module/clima]
type = custom/script
exec = ~/scripts/clima.sh
interval = 600 ; Se ejecuta cada 10 minutos
label = %output%
```


### 4. El "Truco" de las RAMPAS y los NIVELES
Muchos módulos (como batería o volumen) permiten usar "rampas" para que el icono cambie según el nivel.

```ini
[module/audio]
type = internal/pulseaudio

; Definimos iconos para diferentes niveles
ramp-volume-0 = 
ramp-volume-1 = 
ramp-volume-2 = 

format-volume = <ramp-volume> <label-volume>
label-volume = %percentage%%
```


### 5. Cómo lanzar múltiples barras (Launch Script)
Si creaste `[bar/monitor1]` y `[bar/monitor2]` en tu config, tu script de inicio (`launch.sh`) debe verse así:

```bash
#!/usr/bin/env bash

# Terminar instancias previas
killall -q polybar

# Esperar a que se cierren
while pgrep -u $UID -x polybar >/dev/null; do sleep 1; done

# Lanzar barras
# Si tenés un solo monitor:
polybar principal 2>&1 | tee -a /tmp/polybar.log & disown

# Si tenés dos, lanzás la otra también:
# polybar secundaria 2>&1 &
```


### Tips Extras de "Chamaquito" a "Chamaquito":

1.  **Iconos:** Si ves cuadraditos en lugar de iconos, es porque no tenés instalada una **Nerd Font** (te recomiendo `fonts-jetbrains-mono-nerd`).
2.  **Color Picker:** Si querés colores exactos de tu fondo de pantalla, instalá `gcolor3` o usa una web como *Coolors*.
3.  **Transparencia:** Para que la transparencia de la barra funcione (`#aa1e1e2e`), necesitás tener un **compositor** corriendo, como `picom`. Sin `picom`, el color se verá sólido.
4.  **Recarga rápida:** Podés asignarle una tecla en `sxhkd` para reiniciar la barra sin reiniciar la sesión:
    ```bash
    super + shift + b
        ~/.config/polybar/launch.sh
    ```

