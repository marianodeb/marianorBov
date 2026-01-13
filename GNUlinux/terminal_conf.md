


### Atajos terminal


Alt+B : mover palabras hacia la izquierda 
Alt+F : mover palabras hacia la derecha
Alt+< : mover palabras hacia la izquierda
Alt+> : mover palabras hacia la derecha
Ctrl+<: mover palabras hacia la izquierda
Ctrl+>: mover palabras hacia la derecha
CTRL + A: (mover al inicio) 
CTRL + E: (mover al final) 

CTRL + C: (matar proceso) CTRL + D: (salir) Equivale al comando exit. Sirve para cerrar la sesión de un usuario
CTRL + G: (salir de búsqueda) Con este atajo de teclado saldremos de la búsqueda
CTRL + K: Nos sirve para borrar desde la posición del cursor hasta el final de la línea
CTRL + L: (limpiar la terminal o consola)
CTRL + Q: Sirve para reanudar la impresión por pantalla que se había pausado
CTRL + R: (buscar en historial de comandos) 
CTRL + S: (pausar impresión) Sirve para pausar lo que se está imprimiendo por pantalla
CTRL + Y: (deshacer borrado) Deshacer el último borrado realizado
CTRL + Z: (enviar proceso segundo plano) Enviar a segundo plano el proceso que se está ejecutando. Para volver al mismo, escribiremos el comando fg.

CTRL + U: (borrar línea) Atajo para borrar la línea entera 
CTRL + W: (borrar palabra anterior) 
Ctrl+D  o Borrar : Borra el carácter debajo del cursor.
Alt+D : Elimina todos los caracteres después del cursor en la línea actual.
Ctrl+H  o Retroceso : Elimina el carácter antes del cursor.
Alt+U : Poner en mayúscula cada carácter desde el cursor hasta el final de la palabra actual, convirtiendo los caracteres a mayúsculas.
Alt+L : Elimina todos los caracteres desde el cursor hasta el final de la palabra actual, convirtiendo los caracteres a minúsculas.
Alt+C : escribe en mayúscula el carácter debajo del cursor. Su cursor se moverá al final de la palabra actual.




Ctrl+R : recupera el último comando que coincida con los caracteres que proporcionaste. Presione este atajo y comience a escribir para buscar un comando en su historial de bash.
Ctrl+O : ejecuta un comando que hayas encontrado con Ctrl+R.
Ctrl+G : Salir del modo de búsqueda de historial sin ejecutar un comando.

CTRL + SHIFT + C: (copiar texto) Atajo que nos sirve para copiar texto seleccionado en la terminal
CTRL + SHIFT + V: (pegar texto) Y con este atajo de teclado pegaremos el texto copiado en la terminal


TAB: (autocompletar) El tabulador nos permite autocompletar lo que se está escribiendo o navegar entre posibles opciones

Ctrl+Shift+f: abre un diálogo para hacer una búsqueda de texto en la salida de la terminal.
Ctrl+Shift+g: busca la siguiente ocurrencia de la búsqueda previa en la terminal.
Ctrl+Shift+h: busca la anterior ocurrencia de la búsqueda previa en la terminal.
Ctrl+Shift+c: copia el texto seleccionado de la terminal al portapapeles.
Ctrl+Shift+v: pega el texto del portapapeles en la línea de comandos.
Up: establece en la línea de comandos el comando anterior del historial, igual que Ctrl+p.
Down: establece en la línea de comandos el siguiente comando del historial.
Left Mouse: selecciona líneas de texto de la terminal.
Ctrl+Left Mouse: selecciona bloques de texto de la terminal.


---

## kitty


### Instalacion 

1. Descargar e instalar Kitty manualmente

```bash
curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin
```
Esto instalará Kitty en el directorio ~/.local/kitty.app/.

2. Crear los enlaces simbólicos

Para que puedas ejecutar kitty y kitten desde cualquier terminal:

   1. Asegúrate de que el directorio ~/.local/bin/ exista:

```bash
mkdir -p ~/.local/bin
```

   2. Crea los enlaces simbólicos:

```bash
ln -sf ~/.local/kitty.app/bin/kitty ~/.local/kitty.app/bin/kitten ~/.local/bin/
```

   3. Asegúrate de que ~/.local/bin/ esté en tu variable PATH: Agrega esta línea a tu archivo de configuración de shell (~/.bashrc o ~/.zshrc):

```bash
export PATH=$HOME/.local/bin:$PATH
```

Luego recarga el archivo:

```bash
source ~/.bashrc
```

O, si usas zsh:

```bash
source ~/.zshrc
```

3. Verificar que Kitty y Kitten funcionan

Comprueba que los comandos kitty y kitten funcionan correctamente ejecutando:

```bash
kitty --version
kitten --version
```

Ambos comandos deben devolver información sobre la versión instalada.

4. Configurar Kitty para que aparezca en el menú de aplicaciones

   1. Copia el archivo .desktop a la ubicación correcta:

```bash
cp ~/.local/kitty.app/share/applications/kitty.desktop ~/.local/share/applications/
```

   2. Edita el archivo .desktop para usar las rutas correctas:

```bash
sed -i "s|Icon=kitty|Icon=$HOME/.local/kitty.app/share/icons/hicolor/256x256/apps/kitty.png|g" ~/.local/share/applications/kitty.desktop
sed -i "s|Exec=kitty|Exec=$HOME/.local/kitty.app/bin/kitty|g" ~/.local/share/applications/kitty.desktop
```

   3. Actualiza la base de datos de aplicaciones:

```bash
update-desktop-database ~/.local/share/applications/
```

5. Probar kitten themes

   1. Abre Kitty desde el menú o ejecuta:

```bash
kitty
```

   2. Dentro de Kitty, ejecuta:

```bash
kitten themes
```

Esto debería mostrarte la lista de temas disponibles para elegir.


6. (Opcional) Verifica la existencia del ícono

Si el ícono no aparece, asegúrate de que exista el archivo:

```bash
~/.local/kitty.app/share/icons/hicolor/256x256/apps/kitty.png
```

Si no está, usa este comando para copiarlo desde la instalación de Kitty:

```bash
cp ~/.local/kitty.app/share/kitty.png ~/.local/kitty.app/share/icons/hicolor/256x25
```

7. (Opcional) Agregar soporte para abrir archivos desde el administrador de archivos

Si deseas abrir archivos de texto e imágenes en Kitty directamente desde tu administrador de archivos, agrega el archivo kitty-open.desktop:

   1. Copia el archivo kitty-open.desktop a la ubicación correcta:

```bash
cp ~/.local/kitty.app/share/applications/kitty-open.desktop ~/.local/share/applications/
```

   2. Actualiza la base de datos de aplicaciones:

```bash
update-desktop-database ~/.local/share/applications/
```

Ahora podrás seleccionar Kitty como aplicación para abrir archivos desde el menú "Abrir con" de tu administrador de archivos.

#1d2021
linea 1225 background_opacity
---

BASH
configuracion de .bashrc   previamente instalar lsd https://github.com/lsd-rs/lsd

para refrescar y se produzcan los cambior ejucutar:
source ~./bashrc
fuentes: https://www.nerdfonts.com/
para refrescar cache y fuente:
 fc-cache -f -v


## Script para instalar kitty

```bash
#!/bin/bash

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

```

#### STARSHIP

 https://starship.rs/es-es/
 https://starship.rs/es-es/presets/pastel-powerline.html

instalar

```bash
curl -sS https://starship.rs/install.sh | sh
```

```bash
mkdir -p ~/.config && touch ~/.config/starship.toml
```
Copiar el script dentro del archivo que se creo anteriormente: starship.toml

```bash
# Get editor completions based on the config schema
"$schema" = 'https://starship.rs/config-schema.json'

# Inserts a blank line between shell prompts
add_newline = true

# Replace the '❯' symbol in the prompt with '➜'
[character] # The name of the module we are configuring is 'character'
success_symbol = '[➜](bold green)' # The 'success_symbol' segment is being set to '➜' with the color 'bold green'

# Disable the package module, hiding it from the prompt completely
[package]
disabled = true
```

```bash
export STARSHIP_CONFIG=~/example/non/default/path/starship.toml
```

Añade la siguiente línea al final de ~/.bashrc:

```bash
eval "$(starship init bash)"
```





Añade el siguiente código al final de ~/.zshrc:

```bash
eval "$(starship init zsh)"
```

En la pagina https://starship.rs/presets/ elegir el tema ejemplo: Pastel Powerline

```bash
starship preset pastel-powerline -o ~/.config/starship.toml
```

---

El texto en la terminal se puede clasificar en función de la paleta de colores que utiliza:

- **ASCII plano:** monocromático. Es el texto típico.
    
- **Colores ANSI:** es una paleta de ocho colores. Soportada por casi todas las terminales.
    
- **Colores de 8 bits:** es una paleta de 256 colores. Soportada por la mayoría de las terminales.
    
- **Color de 24 bits o color verdadero:** es una paleta de más de 16 millones de colores. Soportada por pocas terminales (por ejemplo, _Konsole_ o _UXterm_).

A continuación explicaremos como utilizar las diferentes paletas de colores. Para imprimir textos puedes utilizar el comando **_printf_** (no imprime un salto de línea, **_\n_** al final) o el comando **_echo -e_** (sí imprime un salto de línea al final).

## Colores ANSI

A continuación describiremos el esquema general que hay que seguir para imprimir textos coloreados, independientemente de la paleta de colores que se utilice:

```bash
"\x1b[1;XYmTEXTO\x1b[0m"
```

**o**

```bash
"\033[1;XYmTEXTO\033[0m"
```

- **_\x1b[_** o **_\033[_**. Estos caracteres son obligatorios al principio del código de color. Indican que se va a utilizar un carácter ANSI.
    
- **_1;_**. **Es opcional**. Indica que el color a utilizar es **brillante**. Elimínalo si quieres un color **normal**.
    
- **_X_**. Indica si el color que se va a cambiar es del texto o el del fondo.

| x   | signifigcado     |
| --- | ---------------- |
| 3   | Color del texto  |
| 4   | Color del fontdo |
Se pueden combinar:

```bash
"\x1b[1;3Y;1;4YmTEXTO\x1b[0m"
```

El **_1;3Y_** indica el color del texto y el **_1;4Y_** el color del fondo.

- **_Y_**. Selecciona el color.

| y   | significado                                                  |
| --- | ------------------------------------------------------------ |
| o   | negras                                                       |
| 1   | rojo                                                         |
| 2   | verde                                                        |
| 3   | amarillo                                                     |
| 4   | azul                                                         |
| 5   | magenta                                                      |
| 6   | cian                                                         |
| 7   | blanco                                                       |
| 8   | otro. Se utiliza para indicar<br>colores de 8bit y 24bit<br> |

- **_m_**. Indica el final del código de color.
    
- **_TEXTO_**. El texto que quieres colorear. Se pueden insertar en él tantos códigos de color como se quiera. Si un código de color cambiar el color del texto pero no el color del fondo, el color del texto se reemplaza por el nuevo color pero el del fondo no, y viceversa.
    
- **_\x1b[0m_**. Devuelve el texto a sus colores por defecto.
    

Ejemplo:

```bash
echo -e "\x1b[1;31m ESTO ES ROJO BRILLANTE\x1b[42m CON FONDO VERDE NORMAL\x1b[0m"
```

El siguiente _script_ en _Bash_ muestra las diferentes combinaciones de colores ANSI:

```bash
```bash
#!/bin/bash
T='Texto'
echo -e "\n                 40m     41m     42m     43m     44m     45m     46m     47m";
for FGs in '    m' '   1m' '  30m' '1;30m' '  31m' '1;31m' '  32m' '1;32m' '  33m' '1;33m' '  34m' '1;34m' '  35m' '1;35m' '  36m' '1;36m' '  37m' '1;37m';
  do FG=${FGs// /}
  echo -en " $FGs \033[$FG  $T  "
  for BG in 40m 41m 42m 43m 44m 45m 46m 47m;
    do echo -en "$EINS \033[$FG\033[$BG  $T \033[0m\033[$BG \033[0m";
  done
  echo;
done
echo
```

Este _script_ se ha modificado a partir del _script_ original de _Daniel Crisman_ (ver [aquí](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html); licencia [GFDL](http://www.gnu.org/copyleft/fdl.html))

Guardalo como **_ANSI_colors_** y ejecutalo así:

```bash
chmod +x ./ANSI_colors
./ANSI_colors
```

Estos colores también se pueden imprimir con **_tput_**:

- **tput setaf Y**. Indica el color del texto.
    
- **tput setab Y**. Indica el color del fondo.
    
- **tput sgr0**. Devuelve el color del texto y del fondo a sus valores por defecto.
    

Puedes seguir el siguiente esquema para imprimirlos así:

```bash
echo -e "$(tput setaf Y)$(tput setab Y)TEXTO$(tput sgr0)"
```

Ejemplo:

```bash
echo -e "$(tput setaf 1) ESTO ES ROJO $(tput setab 2) CON FONDO VERDE $(tput sgr0)"
```

El siguiente _script_ muestra las combinaciones de colores que puede imprimir **tput**:

```bash
```bash
#!/bin/bash
echo " B0  B1  B2  B3  B4  B5  B6  B7 "
for af in {0..7}
do
  for ab in {0..7}
  do
    printf "$(tput setaf $af)$(tput setab $ab) F$af "
  done
  echo "$(tput sgr0)"
done
```

Guardalo como **_tput_colors_** y ejecutalo así:

```bash
chmod +x ./tput_colors
./tput_colors
```

## Colores de 8 bits

Siguen el siguiente esquema:

```bash
"\x1b[1;X8;5;ZZZmTEXTO\x1b[0m"
```

Donde:

- **_X_**: 3 para el color del texto, 4 para el del fondo.
    
- **_5;_**: indica que la paleta de colores que se va a utilizar es de 8 bits.
    
- **_ZZZ_**: es un número de 0 a 255 que indica el color dentro de la paleta.
    

El siguiente _script_ muestra los 256 colores de esta paleta:

```bash
```bash
#!/bin/bash
echo -en "\n   +  "
for i in {0..35}; do
  printf "%2b " $i
done

printf "\n\n %3b  " 0
for i in {0..15}; do
  echo -en "\033[48;5;${i}m  \033[m "
done

#for i in 16 52 88 124 160 196 232; do
for i in {0..6}; do
  let "i = i*36 +16"
  printf "\n\n %3b  " $i
  for j in {0..35}; do
    let "val = i+j"
    echo -en "\033[48;5;${val}m  \033[m "
  done
done

echo -e "\n"
```

Este _script_ se ha modificado a partir del _script_ original de _Michael Plotke_ (ver [aquí](http://bitmote.com/index.php?post/2012/11/19/Using-ANSI-Color-Codes-to-Colorize-Your-Bash-Prompt-on-Linux); licencia [CC BY](http://creativecommons.org/licenses/by/3.0/))

## Colores de 24 bits

Siguen el siguiente esquema:

```bash
"\x1b[1;X8;2;RRR;GGG;BBBmTEXTO\x1b[0m"
```

Donde:

- **_X_**: 3 para el color del texto, 4 para el del fondo.
    
- **_2;_**: indica que la paleta de colores que se va a utilizar es de 24 bits.
    
- **_RRR_**: es un número de 0 a 255 que indica la cantidad de rojo que contendrá el color seleccionado.
    
- **_GGG_**: es un número de 0 a 255 que indica la cantidad de verde que contendrá el color seleccionado.
    
- **_BBB_**: es un número de 0 a 255 que indica la cantidad de azul que contendrá el color seleccionado.
    

Para seleccionar colores en esta paleta puedes utilizar la heramienta online [HTML Color Picker](http://www.w3schools.com/tags/ref_colorpicker.asp) de [W3Schools](http://www.w3schools.com/).

---


En el lenguaje de programación Shell Script, los colores son códigos especiales que se utilizan para cambiar el color del texto o el fondo en la terminal. Estos códigos se pueden insertar en el código del script y se mostrarán cuando se ejecute el script.

Para usar colores en Shell Script, se deben usar secuencias de escape especiales, que comienzan con una barra invertida seguida de una letra "e" y luego de un código de color en formato octal. Por ejemplo, la secuencia de escape "\e\[31m" cambiará el color del texto a rojo. Para volver al color original, se puede usar la secuencia de escape "\e\[0m".

Es importante tener en cuenta que estos códigos de color solo funcionarán en terminales que soporten colores ANSI. Algunos terminales no lo hacen, por lo que es importante asegurarse de que el script funcione correctamente en todas las plataformas.

Puede agregar color a su terminal Linux usando configuraciones especiales de codificación ANSI, ya sea dinámicamente en un comando de terminal o en archivos de configuración, o puede usar temas listos para usar en su emulador de terminal. De cualquier manera, el texto nostálgico en verde o ámbar en una pantalla negra es totalmente opcional. Este artículo demuestra cómo puede hacer que Linux sea tan colorido (o monocromático) como desee.

## Capacidades terminales

Los sistemas modernos generalmente tienen por defecto al menos xterm-256color, pero si intenta agregar color a su terminal sin éxito, debe verificar la configuración de TERM.

En resumen, los terminales Unix son dispositivos de entrada y salida que permiten a los usuarios interactuar con un sistema informático a través de comandos de texto. En la actualidad, la mayoría de los terminales son software y se ejecutan en una computadora personal, pero aún tienen raíces en los dispositivos de teletipo y monitores CRT del pasado. La configuración de TERM es importante para asegurar que el terminal tenga la capacidad de mostrar todos los colores y características necesarias para una experiencia de usuario óptima.

Por ejemplo, el nuevo y elegante VT100 lanzado en 1978 admitía el color ANSI, por lo que si un usuario identificaba el tipo de terminal como vt100, entonces una computadora podría entregar salida en color, mientras que un dispositivo serial básico podría no tener esa opción. El mismo principio se aplica hoy en día, y lo establece la variable de entorno TERM . Puede verificar su definición de TERM con **echo** :

```bash
 echo $TERM  
 xterm-256color
```

El archivo /etc/termcap está obsoleto (pero aún mantenido en algunos sistemas en aras de la compatibilidad con versiones anteriores) definía las capacidades de los terminales y las impresoras. La versión moderna de eso es terminfo, ubicada en /etc o /usr/share, dependiendo de su distribución. Estos archivos enumeran las características disponibles en diferentes tipos de terminales, muchas de las cuales están definidas por hardware histórico: existen definiciones para vt100 a vt220, así como para emuladores de software modernos como xterm y Xfce. A la mayoría del software no le importa qué tipo de terminal esté utilizando; en raras ocasiones, es posible que reciba una advertencia o error sobre un tipo de terminal incorrecto al iniciar sesión en un servidor que verifica las funciones compatibles. Si su terminal está configurado en un perfil con muy pocas funciones, pero sabe que el emulador que usa es capaz de más,luego puede cambiar su configuración definiendo la variable de entorno TERM. Puede hacer esto exportando la variable TERM en su archivo de configuración ~/ .bashrc:

```bash
export TERM=xterm-256color
```

Guarde el archivo y vuelva a cargar su configuración:

```bash
$ source ~/.bashrc
```

## Códigos de color ANSI

A continuación se presenta una lista de algunos códigos de color comunes en Shell Script:

- "\\e\[30m" para hacer el texto negro
- "\\e\[31m" para hacer el texto rojo
- "\\e\[32m" para hacer el texto verde
- "\\e\[33m" para hacer el texto amarillo
- "\\e\[34m" para hacer el texto azul
- "\\e\[35m" para hacer el texto morado
- "\\e\[36m" para hacer el texto cian
- "\\e\[37m" para hacer el texto blanco

También se pueden usar códigos de color para el fondo de la terminal, utilizando los mismos códigos de color pero agregando un "4" antes del código de color. Por ejemplo, 
"\\e\[44m" cambiaría el color del fondo a azul.

Los terminales modernos han heredado secuencias de escape ANSI para funciones "meta". Se trata de secuencias especiales de caracteres que un terminal interpreta como acciones en lugar de caracteres. Por ejemplo, esta secuencia limpia la pantalla hasta el siguiente mensaje:

```bash
$ printf `\033[2J`
```

No borra tu historial; simplemente aclara la pantalla en su emulador de terminal, por lo que es una secuencia de escape ANSI segura y demostrativa.

ANSI también tiene secuencias para configurar el color de su terminal. Por ejemplo, escribir este código cambia el texto siguiente a verde:

```bash
$ printf '\033[32m'
```

Siempre que vea el color de la misma manera que lo hace su computadora, puede usar el color para ayudarlo a recordar en qué sistema está conectado. Por ejemplo, si usa SSH regularmente en su servidor, puede configurar el indicador del servidor en verde para ayudarlo a diferenciarlo de un vistazo del indicador local. Para un mensaje verde, use el código ANSI para el verde antes de su carácter de mensaje y termínelo con el código que representa su color predeterminado normal:

```bsdh
export PS1=`printf "\033[32m$ \033[39m"`
```

## Primer plano y fondo

No está limitado a configurar el color de su texto. Con los códigos ANSI, puede controlar el color de fondo de su texto y aplicar un estilo rudimentario.

Por ejemplo, con 
\\033 \[4m , puede hacer que el texto esté subrayado, o con \\033 \[5m
puede configurarlo para que parpadee. Eso puede parecer una tontería al principio, porque probablemente no configurará su terminal para subrayar todo el texto y parpadear todo el día, pero puede ser útil para determinadas funciones. Por ejemplo, puede configurar un error urgente producido por un script de shell para que parpadee (como una alerta para su usuario), o puede subrayar una URL.

Para su referencia, aquí están los códigos de color de primer plano y de fondo. Los colores de primer plano están en el rango de 30, mientras que los colores de fondo están en el rango de 40:


| color                                                 | primerplano | fondo       |
| ----------------------------------------------------- | ----------- | ----------- |
| Negro                                                 | \\033 \[30m | \\033 \[40m |
| Rojo                                                  | \\033 \[31m | \\033 \[41m |
| Verde                                                 | \\033 \[32m | \\033 \[42m |
| Naranja                                               | \\033 \[33m | \\033 \[43m |
| Azul                                                  | \\033 \[34m | \\033 \[44m |
| Magenta                                               | \\033 \[35m | \\033 \[45m |
| Cian                                                  | \\033 \[36m | \\033 \[46m |
| Gris claro                                            | \\033 \[37m | \\033 \[47m |
| Retorno al valor predeterminado<br>de la distribucion | \\033 \[39m | \\033 \[49m |
Hay algunos colores adicionales disponibles para el fonco:

| Color         | Fondo        |
| ------------- | ------------ |
| Gris oscuro   | \\033 \[100m |
| Luz rojoa     | \\033 \[101m |
| Verde claro   | \\033 \[102m |
| Amarillo      | \\033 \[103m |
| Azul claro    | \\033 \[104m |
| Morado claro  | \\033 \[105m |
| Verde azulado | \\033 \[106m |
| Blanco        | \\033 \[107m |

## Permanencia

Establecer colores en su sesión de terminal es solo temporal y relativamente incondicional. A veces, el efecto dura unas pocas líneas; eso se debe a que este método de establecer colores se basa en una declaración printf para establecer un modo que dura solo hasta que algo más lo anula.

La forma en que un emulador de terminal generalmente recibe instrucciones sobre qué colores usar es a partir de la configuración de la variable de entorno LS_COLORS, que a su vez se completa con la configuración de dircolors. Puede ver su configuración actual con una declaración de eco:

```bash
$ echo $LS_COLORS

rs=0:di=38;5;33:ln=38;5;51:mh=00:pi=40;
38;5;11:so=38;5;13:do=38;5;5:bd=48;5;
232;38;5;11:cd=48;5;232;38;5;3:or=48;
5;232;38;5;9:mi=01;05;37;41:su=48;5;
196;38;5;15:sg=48;5;11;38;5;16:ca=48;5;
196;38;5;226:tw=48;5;10;38;5;16:ow=48;5;
[...]
```

O puede usar dircolors directamente:

```bash
> $ dircolors --print-database
> 
> [ ... ]
> # formatos de imagen
> 
> .jpg 01;35
> .jpeg 01;35
> .mjpg 01;35
> .mjpeg 01;35
> .gif 01;35
> .bmp 01;35
> .pbm 01;35
> .tif 01;35
> .tiff 01;35
> 
> [ ... ]
```

Si eso parece críptico, es porque lo es. El primer dígito después de un tipo de archivo es el código de atributo y tiene seis opciones:

- 00 ninguno
- 01 negrita
- 04 subrayado
- 05 parpadeo
- 07 marcha atrás
- 08 oculto

El siguiente dígito es el código de color en forma simplificada. Puede obtener el código de color tomando el último dígito del código ANSII (32 para primer plano verde, 42 para fondo verde; 31 o 41 para rojo, y así sucesivamente).

Su distribución probablemente establece LS_COLORS globalmente, por lo que todos los usuarios de su sistema heredan los mismos colores. Si desea un conjunto de colores personalizado, puede usar dircolors para eso. Primero, genere una copia local de su configuración de color:

```bash
$ dircolors --print-database > ~/.dircolors
```

Edite su lista local como desee. Cuando esté satisfecho con sus opciones, guarde el archivo. Su configuración de color es solo una base de datos y [ls](https://opensource-com.translate.goog/article/19/7/master-ls-command?_x_tr_sl=en&_x_tr_tl=es&_x_tr_hl=es) no puede usarla directamente , pero puede usar dircolors para obtener el código de shell que puede usar para configurar LS_COLORS:

```bash
$ dircolors --bourne-shell ~/.dircolors 
LS_COLORS='rs=0:di=01;34:ln=01;36:mh=00:
pi=40;33:so=01;35:do=01;35:bd=40;33;01: 
cd=40;33;01:or=40;31;01:mi=00:su=37;41:
sg=30;43:ca=30;41:tw=30;42:ow=34;
[...]
export LS_COLORS
```

Copie y pegue esa salida en su archivo ~ / .bashrc y vuelva a cargar. Alternativamente, puede volcar esa salida directamente en su archivo .bashrc y volver a cargar.

```bash
$ dircolors --bourne-shell ~/.dircolors >> ~/.bashrc
$ source ~/.bashrc
```

También puede hacer que Bash resuelva .dircolors al iniciar en lugar de realizar la conversión manualmente. Siendo realistas, probablemente no cambiará los colores con frecuencia, por lo que esto puede ser demasiado agresivo, pero es una opción si planea cambiar mucho su esquema de color. En su archivo .bashrc, agregue esta regla:

```bash
[[ -e $HOME/.dircolors ]] && eval "`dircolors --sh $HOME/.dircolors`"
```

Si tiene un archivo .dircolors en su directorio de inicio, Bash lo evalúa al iniciarse y establece LS_COLORS en consecuencia.

## Color

En general, es importante tener en cuenta que los colores en un terminal pueden ser útiles para mejorar la eficiencia y la claridad, pero no deben ser el único medio para transmitir información importante. Si depende demasiado de los colores para transmitir información importante, es posible que no pueda acceder a esa información si alguna vez se encuentra en un entorno sin colores o con colores diferentes. Por lo tanto, es recomendable utilizar los colores de manera judiciosa y asegurarse de que la información esencial también se presente de manera clara y concisa sin depender de ellos.

Dejando esas advertencias a un lado, los colores pueden ser útiles y divertidos en algunos flujos de trabajo, así que cree una base de datos .dircolor y personalícela a su gusto.

```bash
#!/bin/bash
# Definimos colores, primer plano
PNegro='\033[30m'		# 1
PRojo='\033[31m'		# 2
PVerde='\033[32m'		# 3
PNaranja='\033[33m'		# 4
PAzul='\033[34m'		# 5
PMagenta='\033[35m'		# 6
PCian='\033[36m'		# 7
PGris='\033[37m'		# 8
PBlanco='\e[37m'		# 9
NC='\033[39m'
# Colores de fondo, video inverso o segundo plano
IGris='\033[100m'		# 8 Gris oscuro
IRojo='\033[101m'		# 7 Luz roja
IVerde='\033[102m'		# 6 Verde claro
IAmarillo='\033[103m'		# 5 Amarillo
IAzul='\033[104m'		# 4 Azul claro
IMagenta='\033[105m'		# 3 Morado claro
ICian='\033[106m'		# 2 Verde azulado
IBlanco='\033[107m'		# 1 Blanco
INC='\033[40m'
clear
# -----------
**printf** "${PRojo}${IAmarillo}"
**echo** "Hola Caracola"
**printf** "${PNegro}${IVerde}"
**echo** "Cada Texto"
**printf** "${PAzul}${ICian}"
**echo** "En un color"
**printf** "${PCian}${IMagenta}"
**echo** "Cian Magenta"
**printf** "${PBlanco}${IMagenta}"
**echo** "Blanco Magenta"
**printf** "${NC}${INC}"
**echo** "Y vuelta a la normalidad"
**echo** "Otros ejemplos"
**printf** "${IBlanco}${PNegro}Fondo Blanco, Letras Negras\n${ICian}${PRojo}Fondo Cian, Letras en Rojo\n${IMagenta}${PVerde}Fondo magenta, letras verdes\n"
**printf** "${IAzul}${PNaranja}Fondo Azul, Letras Naranja\n${IAmarillo}${PAzul}Fondo Amarillo, Letras en Azul\n${IVerde}${PMagenta}Fondo Verde, letras Cian\n"
**printf** "${IRojo}${PCian}Fondo Rojo, Letras Cian\n${IGris}${PBlanco}Fondo Gris, Letras en Blanco\n${IGris}${PNegro}Fondo Gris, letras Negro\n"
```


## Cambiar indicador de Bash actual

Puede ver el estado actual de Bash Prompt ejecutando este comando a continuación:

```bash
# echo $PS1
[u@h W]$
```

De forma predeterminada, el símbolo del sistema está configurado en \[u@h W\]PS Cada carácter especial de escape con barra invertida se puede decodificar de la siguiente manera:

- `u` : Muestra el nombre de usuario actual.
- `h` : Muestra el nombre de host
- `W` : Imprime la base del directorio de trabajo actual.
- `$` : Mostrar # (indica el usuario root) si el UID efectivo es 0; de lo contrario, muestre un $.

Para un usuario de Unix que no sea root, se mostrará como se muestra a continuación:

\[linodadmin@centos-01 ~\]$

## Modificar el indicador de Bash

Como se discutió anteriormente, el indicador de bash está controlado por una variable llamada PS1, y podemos ajustar esta variable en su archivo .bashrc para personalizar su indicador.

Además, si desea que estos cambios estén disponibles para todos los usuarios del sistema en el sistema o globalmente, todo lo que necesita hacer es modificar esta variable en el archivo /etc/bash.bashrc (en sistemas Debian y Ubuntu) o / etc / bashrc (en otras distribuciones de Linux) en lugar de ~ / .bashrc.

Bash le permite utilizar algunos atajos para recuperar detalles, como el nombre de usuario, el nombre del host, el directorio de trabajo actual, fecha y hora, etc. Estos atajos se denominan secuencias de escape.

Tome un ejemplo, desea mostrar el nombre del usuario, el nombre de host, el directorio actual y la hora en formato de 12 horas seguido de $. Luego, se puede recuperar modificando la variable PS1 con estas secuencias de escape que muestran la información requerida como se muestra a continuación:

- `u` : Muestra el nombre de usuario actual.
- `h` : Muestra el nombre de host
- `W` : Imprime la base del directorio de trabajo actual.
- `@` : Muestra la hora actual en formato de 12 horas am / pm

```bash
$ export PS1="[\u@\h \W \@]\$"
[linodadmin@centos-01 ~ 01:50 PM]$
```

Esto permitirá solo un cambio temporal en su indicador de Bash. Si necesita realizar un cambio permanente en los terminales siguientes, puede editar el archivo ~ .bashrc con este valor de PS1 (PS1 = «\[\\u@\\h \\W \\@\]\\ $ «) hacia el final del archivo.

Consulte algunas de las listas de secuencias de escape que nos ayudarán a recuperar la información requerida.

- `u` Nombre de usuario del usuario actual,
- `w` El directorio de trabajo actual
- `W` El último fragmento del directorio de trabajo actual. Por ejemplo, si se encuentra actualmente en / home / linodadmin / var, esto le dará var.
- `h` El nombre de la computadora, hasta un punto (.). Por ejemplo, si su computadora se llama centos-01.linoxide.com, esto le da centos-01.
- `H` Nombre de host FQDN
- `d` La fecha en formato «Día de la semana Mes Fecha» (por ejemplo, «Martes 21 de marzo»)
- `t` La hora actual en formato de 24 horas HH: MM: SS
- `T` La hora actual en formato de 12 horas HH: MM: SS
- `@` La hora actual en formato de 12 horas AM / PM
- `n` Pasa a la siguiente línea.
- `!` : el número de historial de este comando
- `#` : el número de comando de este comando
- `$` : si el UID efectivo es 0, un #, de lo contrario un $
- `j` : el número de trabajos gestionados actualmente por el shell

## Agregar colores al mensaje

En su mayoría, a los administradores del sistema les gustaría agregar algo de color a su aburrido indicador de shell. Esto se puede lograr con la ayuda de secuencias de escape ANSI en la variable PS1. Estas secuencias de escape deben incluirse entre [ and ] para que funcione correctamente. De una manera simple, podemos usar esta sintaxis de comando para agregar colores a la línea de comandos.

'mi\[x;ym $PS1 e\[m'

Where:

- `e[` : Start color scheme.
- `x;y` : Color pair to use (x;y)
- `$PS1` : Your shell prompt variable.
- `e[m` : Stop color scheme.

Check out the list of color codes which can be used:

**txtblk='e[0;30m' # Black - Regular**
txtred='e\[0;31m' # Red
txtgrn='e\[0;32m' # Green
txtylw='e\[0;33m' # 
txtblu='e\[0;34m' # Blue
txtpur="e\[0;35m" # Purple
txtcyn='e\[0;36m' # Cyan
txtwht="e\[0;37m" # White

**bldblk='e\[1;30m' # Black - Bold**
bldred='e\[1;31m' # Red
bldgrn='e\[1;32m' # Green
bldylw='e\[1;33m' # 
bldblu='e\[1;34m' # Blue
bldpur="e\[1;35m" # Purple
bldcyn='e\[1;36m' # Cyan
bldwht="e\[1;37m" # White

**unkblk='e\[4;30m' # Black - Underline**
undred='e\[4;31m' # Red
undgrn='e\[4;32m' # Green
undylw='e\[4;33m' # 
undblu='e\[4;34m' # Blue
undpur="e\[4;35m" # Purple
undcyn='e\[4;36m' # Cyan
undwht="e\[4;37m" # White

**bakblk='e\[40m' # Black - Background**
bakred='e\[41m' # Red
bakgrn='e\[42m' # Green
bakylw='e\[43m' # 
bakblu='e\[44m' # Blue
bakpur="e\[45m" # Purple
bakcyn='e\[46m' # Cyan
bakwht="e\[47m" # White
txtrst="e\[0m" # Text Reset


![[colores-consola-01.png]]

Suponga que desea usar diferentes colores en una declaración de terminal como si desea mostrar el nombre de usuario y la ruta del directorio en cian, seguido de un símbolo $ en negrita. Debe utilizar secuencias de escape por separado según sea necesario. Por ejemplo, la secuencia de escape para el rojo es e\[31m, para el cian, es e\[36m, y para, es e\[33m. Para texto en negrita, necesitamos usar e\[1m. Además, necesitamos restablecer la secuencia de escape ANSI, que evita que los estilos afecten al resto del texto en el shell. La secuencia de reinicio es e\[0m. La variable PS1 para esto se verá así.

export PS1='\[e\[32mu\] \[e\[36mw\] \[e\[33m\]\[e\[1m\]PS\[e\[0m\]'

![[colores-consola-02.png]]

La declaración de exportación debe agregarse a su archivo $ HOME / .bashrc para cambios permanentes.

## Usando el comando tput

Incluso podemos usar el comando tput para modificar la configuración del indicador. Por ejemplo, para mostrar el indicador de color usando un tput, podemos usar este comando a continuación:

export PS1="\[$(**tput setaf 3**)]u@h:w $ \[$(**tput sgr0**)\]"

Lista de algunas de las opciones de la línea de comando tput a continuación:

- `tput bold` – Efecto atrevido
- `tput rev` – Mostrar colores inversos
- `tput sgr0` – Restablecer todo
- `tput setaf {CODE}`– Establezca el color de primer plano, consulte la tabla de {CÓDIGO} de colores a continuación para obtener más información.
- `tput setab {CODE}`– Establezca el color de fondo, consulte la tabla de {CÓDIGO} de colores a continuación para obtener más información.

### Códigos de color para las opciones de línea de comandos de tput

| Colore {code} | Color   |
| ------------- | ------- |
| 0             | Black   |
| 1             | Red     |
| 2             | Green   |
| 3             | Yellow  |
| 4             | Blue    |
| 5             | Magenta |
| 6             | Cyan    |
| 7             | White   |

Consulte los ejemplos que utilizan estos comandos tput a continuación:

![[colores-consola-04.png]]


```bash
```

 
 

