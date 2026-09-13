## Configuracion de rofi

### 1. El concepto clave: `rofi -dmenu`
Para entender los menús de apagado o de Wi-Fi, tenés que conocer el modo **dmenu**. 
* **Modo normal:** `rofi -show drun` (Busca apps instaladas).
* **Modo manual:** Si vos le pasás una lista de texto a Rofi, él te la muestra como un menú y te devuelve lo que elegiste.

Ejemplo rápido en terminal:
```bash
echo -e "Opción A\nOpción B\nOpción C" | rofi -dmenu
```


### 2. Menú de Apagado (Power Menu)
Para Polybar, lo que hacés es crear un **módulo de tipo "custom/text"**. Cuando hacés clic, ejecutás un script que lanza Rofi.

#### El Script (`powermenu.sh`):
```bash
#!/bin/bash
opciones="Log out\nReboot\nShutdown"
seleccion=$(echo -e "$opciones" | rofi -dmenu -p "Sistema:")

case $seleccion in
    "Log out") bspc quit ;;
    "Reboot") reboot ;;
    "Shutdown") poweroff ;;
esac
```

#### En tu config de Polybar:
```ini
[module/powermenu]
type = custom/text
content = "⏻"
click-left = ~/ruta/al/script/powermenu.sh
```

### 3. Menú de Wi-Fi (SSIDs)
Lo que viste de los "SID" (SSIDs) es generalmente un script llamado `rofi-network-manager`. Lo que hace es:
1. Usar el comando `nmcli` para escanear redes.
2. Pasarle la lista de nombres de Wi-Fi a Rofi.
3. Al elegir uno, te pide la contraseña (también por Rofi) y se conecta.

Podés bajar uno ya hecho de GitHub o configurar tu Polybar para que al tocar el ícono de red ejecute el comando:
`click-left = nmcli device wifi rescan && rofi-network-manager`


### 4. Configuración y Estética
Rofi no se configura desde Polybar ni desde sxhkd, sino en su propio archivo: `~/.config/rofi/config.rasi`.

Ahí podés cambiar:
* **El tema:** Hay cientos de temas `.rasi` que lo hacen ver increíble (redondo, cuadrado, lateral, etc.).
* **El comando:** Podés generarlo con `rofi -dump-config > ~/.config/rofi/config.rasi` para ver todas las opciones de personalización.

### 5. Integración con sxhkd
Como bien dijiste, en tu `~/.config/sxhkd/sxhkdrc` deberías tener algo así para lanzarlo rápido:

```bash
# Lanzar lanzador de aplicaciones
super + d
    rofi -show drun -show-icons

# Lanzar el menú de apagado que creamos antes
super + escape
    ~/ruta/al/script/powermenu.sh
```


**Resumen para tu instalación:**
1. **Rofi** es el motor.
2. **Polybar** solo es el "botón" que le da la orden de arrancar.
3. **Scripts de Bash** son el cerebro que le dice a Rofi qué opciones mostrar (Apagar, Wi-Fi, etc.).

---

## sintaxis y la lógica con tres ejemplos prácticos.


### 1. La Sintaxis Básica

#### En Polybar (Módulos `custom/script` o `custom/text`)
Polybar usa archivos `.ini`. Para llamar a un script de Rofi, usamos generalmente:
* **`type = custom/text`**: Si solo querés un icono fijo que al tocarlo haga algo.
* **`click-left`**: El comando que se ejecuta al hacer clic izquierdo.

#### En Rofi (Scripts de Bash)
Para que Rofi funcione como un menú personalizado, usamos la sintaxis:
`echo -e "Opción 1\nOpción 2" | rofi -dmenu`
* **`echo -e`**: Imprime las opciones separadas por un salto de línea (`\n`).
* **`|` (pipe)**: Le pasa esa lista a Rofi.
* **`-dmenu`**: Le dice a Rofi: "No busques apps, mostrá lo que te acabo de pasar".


### 2. Ejemplo 1: Menú de Apagado (Básico)

Este es el más útil para tu bspwm.

**Paso A: Crear el script (`~/.config/rofi/scripts/power.sh`)**
```bash
#!/bin/bash
# Definimos las opciones
opciones="󰐥 Apagar\n󰑐 Reiniciar\n󰍃 Salir"

# Lanzamos rofi y guardamos lo que el usuario elija en la variable 'elegido'
elegido=$(echo -e "$opciones" | rofi -dmenu -p "Sistema" -i)

# Lógica para decidir qué hacer según lo elegido
case $elegido in
    *Apagar) poweroff ;;
    *Reiniciar) reboot ;;
    *Salir) bspc quit ;;
esac
```
*(No te olvides de darle permisos: `chmod +x ~/.config/rofi/scripts/power.sh`)*

**Paso B: Configurar Polybar**
```ini
[module/power]
type = custom/text
content = "󰐥"
content-foreground = #ff5555
; Aquí llamamos al script que creamos arriba
click-left = ~/.config/rofi/scripts/power.sh
```


### 3. Ejemplo 2: Lanzador de Carpetas Favoritas

Imaginá que querés un menú para abrir rápido tus carpetas en el gestor de archivos (Thunar, PCManFM, etc.).

**Paso A: El Script (`~/.config/rofi/scripts/carpetas.sh`)**
```bash
#!/bin/bash
declare -a carpetas=( "Descargas" "Documentos" "Imágenes" "GitHub" )

# Unimos el array en una lista para Rofi
seleccion=$(printf "%s\n" "${carpetas[@]}" | rofi -dmenu -p "Abrir:")

# Si seleccionó algo, lo abrimos con thunar (o tu gestor)
if [ ! -z "$seleccion" ]; then
    thunar "~/$seleccion"
fi
```

**Paso B: Configurar Polybar**
```ini
[module/archivos]
type = custom/text
content = "󰉋"
click-left = ~/.config/rofi/scripts/carpetas.sh
```


### 4. Ejemplo 3: Selector de Redes Wi-Fi

Para este, lo más común es usar un script que ya interactúe con `nmcli` (Network Manager).

**Sintaxis en Polybar:**
A diferencia de los anteriores, aquí podrías querer que el icono cambie según el estado del Wi-Fi, pero el "clic" sigue siendo igual:

```ini
[module/network]
type = internal/network
interface = wlan0
; El icono cambia solo por ser tipo internal/network
format-connected = <label-connected>
label-connected = 󰖩 
; Pero el clic lanza nuestro menú de Rofi para cambiar de red
label-connected-click-left = nmcli device wifi rescan && rofi-network-manager
```


### Resumen de Parámetros de Rofi para tus Scripts

Cuando configures tus comandos de Rofi en los scripts, estos modifican mucho la apariencia:

| Parámetro | Función |
| :--- | :--- |
| `-p "Texto"` | Cambia el mensaje que sale a la izquierda (el "Prompt"). |
| `-i` | Hace que no importe si escribís en mayúsculas o minúsculas. |
| `-l 5` | Limita la lista a 5 líneas (útil para menús cortos). |
| `-theme` | Podés decirle que use un archivo `.rasi` específico para ese menú. |
| `-monitor -1` | Hace que Rofi se abra en el monitor donde tenés el mouse. |

**Tip extra:** Como estás en **bspwm**, recordá que si Rofi se ve "atrás" de las ventanas o algo raro, podés ajustar la propiedad `wm-restack = bspwm` en tu archivo de configuración de Polybar para que las capas se respeten correctamente.



