##  Instalacion y Configuracion de VIM

```bash
$apt install vim 
```

```bash
$mkdir .vim
```

```bash
vim vimrc #crear el archivo de configuracion 
```

ir al repo : https://github.com/junegunn/vim-plug
en el archivo **vimrc** poner las siguientes lineas :

```vim

set number
set mouse=a
syntax enable
set showcmd
set encoding=utf-8
set showmatch
set relativenumber
set showcmd
set ruler
set cursorline
set clipboard=unnamed
set numberwidth=1
set ignorecase
set incsearch
set scrolloff=8
set wildmenu
set history=100
set nocompatible
set hlsearch
set clipboard=unnamedplus


call plug#begin()

"tema
Plug 'sainnhe/gruvbox-material'
Plug 'shinchu/lightlines-gruvbox.vim'
"tipeo
Plug 'jiangmiao/auto-pairs'
Plug 'alvan/vim-closetag'

"syntax
Plug 'sheerun/vim-polyglot'
"stutus bar
Plug 'maximbaz/lightline-ale'
Plug 'itchyny/lightline.vim'

"fuentes nerfonts
Plug 'ryanoasis/vim-devicons'


call plug#end()

"configuracion de gruvbox
set background=dark
"let g:gruvbox_amterial_bacrground='medium'
let g:gruvbox_amterial_bacrground='dark'
colorscheme gruvbox-material
"barra 
set laststatus=2
set noshowmode

let &t_ut=''

"configuracion de grvbox hacerla despues de instalar el plugin con el comando :Plugiinstall
set background=dark
let g:gruvbox_amterial_bacrground='medium'
colorscheme gruvbox-material
set laststatus=2
set noshowmode
```

eliminar plug:
eliminar del vimrc el plug
:source %
:Plug Clean

# NEOVIM


 Link de la instalacion  
  https://github.com/neovim/neovim/wiki/Building-Neovim
  
```bash
$git clone https://github.com/neovim/neovim
```

```bash
$cd neovim && make CMAKE_BUILD_TYPE=RelWithDebInfo
```

```bash
$git checkout stable
```

```bash
$sudo make install
```


configuracion  e intalar plugin

https://github.com/junegunn/vim-plug 

desacargar el repo 

```
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```
crear la carpeta nvim en ~/.config

```
mkdir ~/.config/nvim
```

crear el archivo init.vim
```
touch init.vim
```

copiar el directorio autoload que se desacargo en /home/oto/.local/share/nvim/site/  en el directorio ~/.config/nvim

configuracion e instalacion de plugins
https://www.youtube.com/watch?v=2dG_Nl_r6s0&t=271s&ab_channel=ManuelNinahuanca

---


### Atajos y configuracion de VIM

Descargar de la pag. https://github.com/junegunn/vim-plug
 Si el directorio .confi/nvim no está crearlo. Download plug.vim el archivo plug.vim en la carpeta nvim
creamos el directorio autoload y pegamos el archivo plug.vim
en el archivo init.vim escribir las siguientes líneas:
(si no está el archivo init.vim crearlo en ./conf/nvim)

```
set number
set mouse=a
syntax enable
set showcmd
set encoding=utf-8
set relativenumber 
set sw=2
set smartindent
set nowrap
set incsearch
set ignorecase
set showmatch
set autoindent
set laststatus=2
set bg=dark
set clipboard=unnamedplus

call plug#begin(‘~/.vim/plugged’)

Plug 'sainnhe/gruvbox-material'

call plug#end()

"configuraciòn de gruvbox
Plug 'vim-airline/vim-airline'
set background=dark
let g:gruvbox_material_background='medium'
colorscheme gruvbox-material
```
tener instalado los comandos: curl  git

#### BÁSICOS

:e nombrearchivo - Abre un archivo para su edición
:w – Guardar archivos
:q – Salir de Vim
:q! - Salir de Vim sin guardar
:x – Escribir en archivo (si se han hecho cambios) y salir
:sav  nombrearchivo – Guarda archivo como nombrearchivo
. - Repite el último cambio realizado en modo normal
5. - Repite 5 veces el último cambio realizado en modo normal

##### MOVIÉNDOSE POR EL ARCHIVO

k o Tecla arriba – Mueve el cursor arriba una línea
j o Tecla abajo – Mueve el cursor abajo una línea
e – Mueve el cursor al final de la palabra
b – Mueve el cursor al principio de la palabra
0 – Mueve el cursor al principio de la línea
G – Mueve el cursor al final de la línea
gg – Mueve el cursor al principio del fichero
L – Mueve el cursor al final de la pantalla
:59 – Mueve el cursor a la línea 59. Reemplaza el número 59, por la línea que desees
20| - Mueve el cursor a la columna 20
% - Mueve el cursor hasta el paréntesis que aparezca

#### CORTAR, COPIAR Y PEGAR

y – Copiar el texto seleccionado al portapapeles
p – Pegar el contenido del portapapeles
dd – Cortar la línea actual
yw – Copiar palabra
yy – Copiar la línea actual
y$ - Copiar al final de la línea
D – Cortar al final de la línea

##### BÚSQUEDA

/palabra – Buscar palabra desde el inicio hasta el final
?palabra – Buscar palabra desde el final hasta el principio
* - Buscar palabra a continuación del cursor
/cpalabra – Busca palabra sin distinguir entre mayúsculas y minúsculas
/jo[ha]n – Busca john o joan
/< por - Busca por, portátil o porra
/por> - Busca por o vapor
/< por> - Busca por
/< ¦.> - Busca todas las palabras de cuatro letras
// - Busca fred pero no alfred o frederick
/fred|joe – Busca fred o joe
/ - Busca exáctamente 4 dígitos
/^n{3} – Busca 3 líneas vacías
:bufdo /palabra/ - Busca en todos los archivos abiertos
bufdo %s/algo/algomas/g – Busca algo en todos los ficheros abiertos y lo reemplaza por algo más

#### REEMPLAZAR

:%s/viejo/nuevo/g – Reemplaza todas las ocurrencias de viejo por nuevo en el fichero
:%s/viejo/nuevo/gi – Reemplaza todas las ocurrencias de viejo por nuevo en el fichero distinguiendo entre mayúsculas y minúsculas
:%s/viejo/nuevo/gc – Reemplaza todas las ocurrencias con confirmación
:2,35s/viejo/nuevo/g - Reemplaza todas las ocurrencias entre la línea 2 y 35
:5,$s/old/new/g – Reemplaza todas las ocurrencias desde la línea 5 hasta el final
:%s/^/hola/g – Reemplaza cada principio de línea por un hola
:%s/$/Jorge/g – Reemplaza cada final de línea por un Jorge
:%s/ *$//g – Borra todos los espacios en blanco
:g/palabra/d – Elimina todas las líneas que contienen palabra
:v/palabra/d – Elimina todas las líneas que no contienen palabra
:s/Bill/Steve/ - Reemplaza la primera ocurrencia de Bill por Steve en la línea actual
:s/Bill/Steve/g - Reemplaza Bill por Steve en la línea actual
:%s/Bill/Steve/g - Reemplaza Bill por Steve en todo el fichero
:%s/^M//g – Elimina los retornos de carro
:%s/r/r/g – Elimina los retornos de carro en los returns
:%s#<[^>]+>##g – Elimina los tags de HTML pero conserva el texto
:%s/^(.*)n1$/1/ - Elimina líneas duplicadas
Ctrl+a – Incrementa el número bajo el cursor
Ctrl+x – Decrementa el número bajo el cursor
ggVGg? - Cambia el texto a Rot13

#### TRANSFORMACIÓN

Vu - Minúsculas
VU - Mayúsculas
g~~ - Invertir
vEU – Cambiar palabra a mayúsculas
vE~ - Modificar el tipo de la palabra
ggguG – Transformar todos los textos a minúsculas
gggUG Set – Transformar todos los textos a mayúsculas
:set ignorecase – Ignorar el tipo en las búsquedas
:set smartcase – Ignorar el tipo en las búsquedas excepto si se usa una letra mayúscula
:%s/<./u&/g – Define la primera letra de cada palabra a mayúsculas
:%s/<./l&/g – Define la primera letra de cada palabra a minúsculas
:%s/.*/u& – Define la primera letra de cada línea a mayúsculas
:%s/.*/l& – Define la primera letra de cada línea a minúsculas

#### LEER/ESCRIBIR ARCHIVOS

:1,10 w otrofichero - Guarda desde la línea 1 a la 10 en otro fichero
:1,10 w >> otrofichero – Adjunta desde la línea 1 a la 10 en otro fichero
:r otrofichero – Inserta el contenido de otro fichero
:23r infile – Inserta el contenido de otro fichero desde la línea 23

#### EXPLORADOR DE ARCHIVOS

:e . - Abre el explorador de archivos integrado
:Sex – Divide la ventana y abre el explorador de archivos integrado
:Sex! - Lo mismo que :Sex pero dividiendo la ventana verticalmente
:browse e – Explorador de archivos gráfico
:ls – Listar buffers
:cd .. - Moverse al directorio padre
:args – Listar ficheros
:args *.php – Lista ficheros con la extensión php
:grep expresion *.php – Lista ficheros con la extensión php que contienen expresión

#### ALINEACIÓN

:%!fmt - Alinear todas las líneas
!}fmt – Alinear todas las líneas en la posición actual
5!!fmt – Alinear las próximas 5 líneas
TABS/VENTANAS
:tabnew – Crea un nuevo tab
gt – Muestra el siguiente tab
:tabfirst – Muestra el primer tab
:tablast - Muestra el último tab
:tabm n(posicion) – Ir al tab posicion
:tabdo %s/foo/bar/g – Ejecuta un comando en todos los tabs
:tab ball – Pone todos los archivos abiertos en tabs
:new abc.txt – Edita el archivo abc.txt en una nueva ventana

#### AUTO-COMPLETADOR

Ctrl+n Ctrl+p (en modo inserción) – Completar palabra
Ctrl+x Ctrl+l – Completar línea
:set dictionary=dict – Define dict como un diccionario
Ctrl+x Ctrl+k - Completar con diccionario

#### ABREVIATURAS

:ab mail [email protected] – Define mail como abreviatura de [email protected]

#### INDENTACIÓN DE TEXTO

:set autoindent - Configurar auto indentación
:set smartindent – Configurar autoindentación inteligente
:set shiftwidth=4 – Definir 4 espacios como tamaño de indentación
ctrl-t, ctrl-d – Indentar o desindentar en modo inserción
>> - Indentar
<< - Desindentar
=% - Indentar el código entre paréntesis
1GVG= - Indentar todo el fichero



---








