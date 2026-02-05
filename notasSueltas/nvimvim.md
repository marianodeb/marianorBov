




Neovim appimage

para ejecutar el appimage de nvim creamos el alias


```bash
alias nv='/media/user/bodzzy/appimage/nvim-linux-x86_64.appimage'
```

---

```
syntax enable

set guicursor=                                     " Disable blinking for the n-v-c modes
set termguicolors
set guioptions-=T                                   " No Tool bar

set cursorline                                     " Highlight the current line

set hidden                                         " When on a buffer becomes hidden when it is abandoned
set path+=**
set nowrap
set encoding=UTF-8

set number relativenumber

set smartindent
set smarttab
set tabstop=4 softtabstop=4
set shiftwidth=4
set expandtab
set smartcase
set incsearch
set nohlsearch
set completeopt=menuone,noinsert,noselect
set signcolumn=yes
set colorcolumn=80
highlight ColorColumn ctermbg=0 guibg=lightgrey

set noswapfile
set nobackup
set undofile
execute 'set undodir=' . g:nvim_data_root . '/undodir'


```




## Ecript para configurar nvim

crear el directorio vim

```bash
mkdir -p ~/.config/nvim
```

crear archvio init.vim 

```bash
touch ~/.config/nvim/init.vim
```

Administrador de pluggins

```bash
# En setup.sh
curl -fLo ~/.config/nvim/autoload/plug.vim --create-dirs \https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

### **Script configuracion nvim**

```bash
#!/bin/bash

# Crear el directorio de configuración de Neovim
mkdir -p ~/.config/nvim

# Crear el archivo init.vim con la configuración personalizada
cat <<EOL > ~/.config/nvim/init.vim
" Configuración básica
syntax enable
set number
set tabstop=4
set shiftwidth=4
set expandtab

" Configuración de vim-plug
call plug#begin('~/.config/nvim/plugged')

" Plugins para Python
Plug 'nvim-treesitter/nvim-treesitter', {'do': ':TSUpdate'}
Plug 'neoclide/coc.nvim', {'branch': 'release'}
Plug 'vim-python/python-syntax'
Plug 'davidhalter/jedi-vim'
Plug 'jmcantrell/vim-virtualenv'
Plug 'dense-analysis/ale'
Plug 'psf/black', { 'branch': 'stable' }
Plug 'heavenshell/vim-pydocstring', { 'do': 'make install' }

" Plugins generales
Plug 'preservim/nerdtree'
Plug 'tpope/vim-fugitive'

call plug#end()

" Configuración adicional
let g:python_highlight_all = 1
let g:coc_global_extensions = ['coc-pyright']
let g:ale_linters = {'python': ['flake8', 'pylint']}
let g:ale_fixers = {'python': ['black', 'isort']}
autocmd BufWritePre *.py execute ':Black'
EOL

echo "¡Configuración de Neovim completada!"
```


Dentro de Neovim, ejecuta el siguiente comando para verificar la ruta del archivo de configuración cargado:

```bash
:echo stdpath('config')
```


Verifica si existe alguna configuración en estas rutas:

```bash
cat /etc/xdg/nvim/sysinit.vim
cat /usr/share/nvim/sysinit.vim
```

Deshabilitar configuraciones globales:

```bash
set runtimepath-=/usr/share/nvim
```

Deshabilitar los signos $ y +

```bash
" Deshabilitar caracteres especiales al final de las líneas
set nolist          " Desactiva la visualización de caracteres especiales
set showbreak=      " Elimina el indicador de salto de línea
```

Instala vim-plug automáticamente en tu script:

```bash
# En setup.sh
curl -fLo ~/.config/nvim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
---

## Plugins enfocados en Python


### **Plugins recomendados para Python**

#### **1. **`nvim-treesitter`**
   - **Descripción**: Proporciona un resaltado de sintaxis mejorado y más preciso usando el sistema de "tree-sitter".
   
   - **Instalación**:
   
```vim
Plug 'nvim-treesitter/nvim-treesitter', {'do': ':TSUpdate'}
```
   - **Configuración básica**:
   
```vim
lua <<EOF
require'nvim-treesitter.configs'.setup {
  ensure_installed = "all",  " Instala soporte para todos los lenguajes
  highlight = {
    enable = true,           " Habilita resaltado de sintaxis
  },
}
EOF
```

#### **2. **`coc.nvim`**

   - **Descripción**: Un poderoso motor de autocompletado (LSP - Language Server Protocol) que soporta múltiples lenguajes, incluyendo Python.
   
   - **Instalación**:
   
```vim
Plug 'neoclide/coc.nvim', {'branch': 'release'}
```
   - **Configuración básica**:
   
```vim
" Configuración de coc.nvim
let g:coc_global_extensions = ['coc-pyright']  " Usa Pyright para Python
```

#### **3. **`python-syntax`**

   - **Descripción**: Mejora el resaltado de sintaxis para Python.
   
   - **Instalación**:
   
```vim
Plug 'vim-python/python-syntax'
```
   - **Configuración básica**:
   
```vim
let g:python_highlight_all = 1  " Habilita todas las opciones de resaltado
```

#### **4. **`jedi-vim`**

   - **Descripción**: Integra el autocompletado y análisis de código de Jedi (una herramienta popular para Python).
   
   - **Instalación**:
   
```vim
Plug 'davidhalter/jedi-vim'
```
   - **Configuración básica**:
   
```vim
let g:jedi#completions_enabled = 1  " Habilita autocompletado
let g:jedi#use_tabs_not_buffers = 1 " Usa pestañas en lugar de buffers
```

#### **5. **`vim-virtualenv`**

   - **Descripción**: Maneja automáticamente entornos virtuales de Python.
   
   - **Instalación**:
   
```vim
Plug 'jmcantrell/vim-virtualenv'
```
   - **Configuración básica**:
   
```vim
let g:virtualenv_auto_activate = 1  " Activa automáticamente el entorno virtual
```

#### **6. **`ale` (Asynchronous Lint Engine)**

   - **Descripción**: Proporciona linting (análisis de código) en tiempo real para Python y otros lenguajes.
   
   - **Instalación**:
   
```vim
Plug 'dense-analysis/ale'
```
   - **Configuración básica**:
   
```vim
let g:ale_linters = {'python': ['flake8', 'pylint']}  " Usa flake8 y pylint
let g:ale_fixers = {'python': ['black', 'isort']}    " Usa black e isort para formatear
```

#### **7. **`black` (formateador de código)**

   - **Descripción**: Integra el formateador de código `black` para Python.
   
   - **Instalación**:
   
```vim
Plug 'psf/black', { 'branch': 'stable' }
```
   - **Configuración básica**:
   
```vim
autocmd BufWritePre *.py execute ':Black'  " Formatea automáticamente al guardar
```

#### **8. **`vim-pydocstring`**

   - **Descripción**: Genera automáticamente docstrings para funciones y clases de Python.
   
   - **Instalación**:
   
```vim
Plug 'heavenshell/vim-pydocstring', { 'do': 'make install' }
```
   - **Configuración básica**:
   
```vim
let g:pydocstring_enable_mapping = 1  " Habilita atajos de teclado
```

#### **9. **`nerdtree`**

   - **Descripción**: Un explorador de archivos para Neovim.
   
   - **Instalación**:
   
```vim
Plug 'preservim/nerdtree'
```
   - **Configuración básica**:
   
```vim
map <C-n> :NERDTreeToggle<CR>  " Atajo para abrir/cerrar NERDTree
```

#### **10. **`vim-fugitive`**

   - **Descripción**: Integración con Git directamente en Neovim.
   
   - **Instalación**:
```vim
Plug 'tpope/vim-fugitive'
```

---

### **Script de configuración con plugins**
Aquí tienes un ejemplo de cómo configurar Neovim con estos plugins usando `vim-plug`:

```bash
#!/bin/bash

# Crear el directorio de configuración de Neovim
mkdir -p ~/.config/nvim

# Crear el archivo init.vim con la configuración personalizada
cat <<EOL > ~/.config/nvim/init.vim
" Configuración básica
syntax enable
set number
set tabstop=4
set shiftwidth=4
set expandtab

" Configuración de vim-plug
call plug#begin('~/.config/nvim/plugged')

" Plugins para Python
Plug 'nvim-treesitter/nvim-treesitter', {'do': ':TSUpdate'}
Plug 'neoclide/coc.nvim', {'branch': 'release'}
Plug 'vim-python/python-syntax'
Plug 'davidhalter/jedi-vim'
Plug 'jmcantrell/vim-virtualenv'
Plug 'dense-analysis/ale'
Plug 'psf/black', { 'branch': 'stable' }
Plug 'heavenshell/vim-pydocstring', { 'do': 'make install' }

" Plugins generales
Plug 'preservim/nerdtree'
Plug 'tpope/vim-fugitive'

call plug#end()

" Configuración adicional
let g:python_highlight_all = 1
let g:coc_global_extensions = ['coc-pyright']
let g:ale_linters = {'python': ['flake8', 'pylint']}
let g:ale_fixers = {'python': ['black', 'isort']}
autocmd BufWritePre *.py execute ':Black'
EOL

echo "¡Configuración de Neovim completada!"
```

---

### **Cómo instalar los plugins**

1. Guarda el script en un archivo, por ejemplo `setup_nvim.sh`.

2. Haz que el script sea ejecutable:

```bash
chmod +x setup_nvim.sh
```
3. Ejecuta el script:

```bash
./setup_nvim.sh
```
4. Abre Neovim e instala los plugins:

```bash
nvim
:PlugInstall
```

---


## Plugins y configuraciones para python

### **1. Script para configurar Neovim con plugins básicos**

Este script configura Neovim con plugins útiles para Python y desarrollo en general.

#### **Archivo: `setup_nvim.sh`**

```bash
#!/bin/bash

# Crear el directorio de configuración de Neovim
mkdir -p ~/.config/nvim

# Crear el archivo init.vim con la configuración personalizada
cat <<EOL > ~/.config/nvim/init.vim
" Configuración básica
syntax enable
set number
set tabstop=4
set shiftwidth=4
set expandtab

" Configuración de vim-plug
call plug#begin('~/.config/nvim/plugged')

" Plugins para Python
Plug 'nvim-treesitter/nvim-treesitter', {'do': ':TSUpdate'}
Plug 'neoclide/coc.nvim', {'branch': 'release'}
Plug 'vim-python/python-syntax'
Plug 'davidhalter/jedi-vim'
Plug 'jmcantrell/vim-virtualenv'
Plug 'dense-analysis/ale'
Plug 'psf/black', { 'branch': 'stable' }
Plug 'heavenshell/vim-pydocstring', { 'do': 'make install' }

" Plugins generales
Plug 'preservim/nerdtree'
Plug 'tpope/vim-fugitive'

call plug#end()

" Configuración adicional
let g:python_highlight_all = 1
let g:coc_global_extensions = ['coc-pyright']
let g:ale_linters = {'python': ['flake8', 'pylint']}
let g:ale_fixers = {'python': ['black', 'isort']}
autocmd BufWritePre *.py execute ':Black'
EOL

echo "¡Configuración de Neovim completada!"
```

#### **Cómo usarlo:**

1. Guarda el script en un archivo, por ejemplo `setup_nvim.sh`.
2. Haz que el script sea ejecutable:

```bash
chmod +x setup_nvim.sh
```

3. Ejecuta el script:

```bash
./setup_nvim.sh
```

4. Abre Neovim e instala los plugins:

```bash
nvim
:PlugInstall
```

---

### **2. Script para configurar el autocompletado con `coc.nvim`**

Este script configura `coc.nvim` para autocompletado en Python.

#### **Archivo: `setup_coc.sh`**

```bash
#!/bin/bash

# Crear el directorio de configuración de Neovim
mkdir -p ~/.config/nvim

# Crear el archivo init.vim con la configuración de coc.nvim
cat <<EOL > ~/.config/nvim/init.vim
" Configuración básica
syntax enable
set number
set tabstop=4
set shiftwidth=4
set expandtab

" Configuración de vim-plug
call plug#begin('~/.config/nvim/plugged')

Plug 'neoclide/coc.nvim', {'branch': 'release'}

call plug#end()

" Configuración de coc.nvim
let g:coc_global_extensions = ['coc-pyright']

" Atajos de teclado para autocompletado
inoremap <silent><expr> <TAB>
      \ coc#pum#visible() ? coc#pum#next(1) :
      \ CheckBackspace() ? "\<Tab>" :
      \ coc#refresh()
inoremap <expr><S-TAB> coc#pum#visible() ? coc#pum#prev(1) : "\<C-h>"

" Confirmar autocompletado con Enter
inoremap <silent><expr> <CR> coc#pum#visible() ? coc#pum#confirm() : "\<C-g>u\<CR>"
EOL

echo "¡Configuración de coc.nvim completada!"
```

#### **Cómo usarlo:**

1. Guarda el script en un archivo, por ejemplo `setup_coc.sh`.

2. Haz que el script sea ejecutable:

```bash
chmod +x setup_coc.sh
```
3. Ejecuta el script:

```bash
./setup_coc.sh
```

4. Abre Neovim e instala `coc.nvim`:

```bash
nvim
:PlugInstall
```
   
5. Instala el servidor LSP para Python:

```vim
:CocInstall coc-pyright
```

---

### **3. Script para configurar `nerdtree`**

Este script configura `nerdtree`, un explorador de archivos para Neovim.

#### **Archivo: `setup_nerdtree.sh`**

```bash
#!/bin/bash

# Crear el directorio de configuración de Neovim
mkdir -p ~/.config/nvim

# Crear el archivo init.vim con la configuración de nerdtree
cat <<EOL > ~/.config/nvim/init.vim
" Configuración básica
syntax enable
set number

" Configuración de vim-plug
call plug#begin('~/.config/nvim/plugged')

Plug 'preservim/nerdtree'

call plug#end()

" Atajo para abrir/cerrar NERDTree
map <C-n> :NERDTreeToggle<CR>
EOL

echo "¡Configuración de nerdtree completada!"
```

#### **Cómo usarlo:**

1. Guarda el script en un archivo, por ejemplo `setup_nerdtree.sh`.

2. Haz que el script sea ejecutable:

```bash
chmod +x setup_nerdtree.sh
```
   
3. Ejecuta el script:

```bash
./setup_nerdtree.sh
```
4. Abre Neovim e instala `nerdtree`:

```bash
nvim
:PlugInstall
```

---

### **4. Script para configurar `black` (formateador de código)**

Este script configura `black`, un formateador de código para Python.

#### **Archivo: `setup_black.sh`**

```bash
#!/bin/bash

# Crear el directorio de configuración de Neovim
mkdir -p ~/.config/nvim

# Crear el archivo init.vim con la configuración de black
cat <<EOL > ~/.config/nvim/init.vim
" Configuración básica
syntax enable
set number

" Configuración de vim-plug
call plug#begin('~/.config/nvim/plugged')

Plug 'psf/black', { 'branch': 'stable' }

call plug#end()

" Formatear automáticamente al guardar
autocmd BufWritePre *.py execute ':Black'
EOL

echo "¡Configuración de black completada!"
```

#### **Cómo usarlo:**

1. Guarda el script en un archivo, por ejemplo `setup_black.sh`.

2. Haz que el script sea ejecutable:

```bash
chmod +x setup_black.sh
```
   
3. Ejecuta el script:

```bash
./setup_black.sh
```

4. Abre Neovim e instala `black`:

```bash
nvim
:PlugInstall
```

---

### **Consejos generales**

1. **Verifica dependencias**:

   - Asegúrate de tener instalado `git` y `curl` en tu sistema.
   - Para `black`, necesitas tener Python instalado.

2. **Reinicia Neovim**:

   - Después de instalar los plugins, reinicia Neovim para que los cambios surtan efecto.

3. **Verifica errores**:

   - Si algo no funciona, usa `:messages` en Neovim para ver los errores.

---


### Configuracion con lua



Instalacion de packer.ivim

```
-- Archivo: ~/.config/nvim/init.lua

-- Instalar Packer.nvim si no está instalado
local fn = vim.fn
local install_path = fn.stdpath('data') .. '/site/pack/packer/start/packer.nvim'

if fn.empty(fn.glob(install_path)) > 0 then
  fn.system({ 'git', 'clone', '--depth', '1', 'https://github.com/wbthomason/packer.nvim', install_path })
  vim.cmd [[packadd packer.nvim]]
end

-- Cargar Packer.nvim
require('packer').startup(function(use)
  -- Packer puede gestionarse a sí mismo
  use 'wbthomason/packer.nvim'

  -- Aquí añadiremos los plugins más adelante
end)

```

Configuracion init.lua

```
-- Archivo: ~/.config/nvim/init.lua

-- 1. Cargar packer.nvim (gestor de plugins)
require('packer').startup(function(use)
  -- Packer puede gestionarse a sí mismo
  use 'wbthomason/packer.nvim'

  -- Tema de colores (opcional)
  use 'folke/tokyonight.nvim'

  -- LSP config
  use 'neovim/nvim-lspconfig'
  use 'williamboman/mason.nvim'
  use 'williamboman/mason-lspconfig.nvim'

  -- Autocompletado
  use 'hrsh7th/nvim-cmp'
  use 'hrsh7th/cmp-nvim-lsp'
  use 'L3MON4D3/LuaSnip'

  -- File explorer (nvim-tree.lua)
  use 'nvim-tree/nvim-tree.lua'

  -- Búsqueda (telescope.nvim)
  use 'nvim-telescope/telescope.nvim'
  use 'nvim-lua/plenary.nvim'  -- Dependencia de telescope

  -- Barra de estado (lualine.nvim)
  use 'nvim-lualine/lualine.nvim'
end)

-- 2. Configuración básica de Neovim
vim.opt.number = true          -- Mostrar números de línea
vim.opt.relativenumber = true  -- Números de línea relativos
vim.opt.tabstop = 4            -- Tamaño de tabulación
vim.opt.shiftwidth = 4         -- Tamaño de indentación
vim.opt.expandtab = true       -- Usar espacios en lugar de tabs

-- 3. Configuración de LSP
require('mason').setup()
require('mason-lspconfig').setup({
  ensure_installed = { 'pyright', 'bashls', 'tsserver' }  -- Servidores para Python, Bash, JS/TS
})

local lspconfig = require('lspconfig')
lspconfig.pyright.setup({})  -- LSP para Python
lspconfig.bashls.setup({})   -- LSP para Bash
lspconfig.tsserver.setup({}) -- LSP para JavaScript/TypeScript

-- 4. Configuración de autocompletado (nvim-cmp)
local cmp = require('cmp')
cmp.setup({
  snippet = {
    expand = function(args)
      require('luasnip').lsp_expand(args.body)
    end,
  },
  mapping = cmp.mapping.preset.insert({
    ['<C-b>'] = cmp.mapping.scroll_docs(-4),
    ['<C-f>'] = cmp.mapping.scroll_docs(4),
    ['<C-Space>'] = cmp.mapping.complete(),
    ['<C-e>'] = cmp.mapping.abort(),
    ['<CR>'] = cmp.mapping.confirm({ select = true }),
  }),
  sources = cmp.config.sources({
    { name = 'nvim_lsp' },
    { name = 'luasnip' },
  })
})

-- 5. Configuración de nvim-tree.lua (File explorer)
require('nvim-tree').setup({
  view = {
    width = 30,  -- Ancho del explorador
  },
  actions = {
    open_file = {
      quit_on_open = true,  -- Cerrar el explorador al abrir un archivo
    },
  },
})

-- Atajo para abrir/cerrar el explorador de archivos
vim.api.nvim_set_keymap('n', '<C-n>', ':NvimTreeToggle<CR>', { noremap = true, silent = true })

-- 6. Configuración de telescope.nvim (Búsqueda)
require('telescope').setup({
  defaults = {
    mappings = {
      i = {
        ['<C-j>'] = 'move_selection_next',  -- Moverse hacia abajo en los resultados
        ['<C-k>'] = 'move_selection_previous',  -- Moverse hacia arriba en los resultados
      },
    },
  },
})

-- Atajos para buscar archivos y texto
vim.api.nvim_set_keymap('n', '<leader>ff', ':Telescope find_files<CR>', { noremap = true, silent = true })
vim.api.nvim_set_keymap('n', '<leader>fg', ':Telescope live_grep<CR>', { noremap = true, silent = true })

-- 7. Configuración de lualine.nvim (Barra de estado)
require('lualine').setup({
  options = {
    theme = 'tokyonight',  -- Usar el tema tokyonight
  },
})

```


Qué hacer después de crear el archivo?

1. Guardar el archivo:

Guarda el archivo como ~/.config/nvim/init.lua. Si la carpeta ~/.config/nvim no existe, créala.

2. Instalar los plugins:

Abre Neovim (nvim).

Ejecuta el siguiente comando para instalar los plugins:
vim
Copy

```vim
:PackerSync
```

Esto descargará e instalará todos los plugins que configuraste en init.lua.

3. Configurar atajos de teclado:

En el archivo init.lua ya configuré algunos atajos útiles:

 <C-n>: Abre/cierra el explorador de archivos (nvim-tree).

 <leader>ff: Busca archivos con telescope.

 <leader>fg: Busca texto en archivos con telescope.

 Puedes personalizar estos atajos según tus preferencias.

4. Probar la configuración:

Cierra y vuelve a abrir Neovim.

 Prueba los siguientes comandos:

<C-n>: Debería abrir el explorador de archivos a la izquierda.

<leader>ff: Debería abrir un buscador de archivos.

<leader>fg: Debería abrir un buscador de texto en archivos.

Verifica que el autocompletado funcione al escribir código en Python, Bash, etc.

5. Personalizar:

Si quieres cambiar el tema de colores, puedes modificar la línea theme = 'tokyonight' en la configuración de lualine y usar otro tema como gruvbox o onedark.

Si quieres añadir más plugins, agrégalos en la sección de require('packer').startup.

---

Estructura de tu configuración

Después de seguir estos pasos, tu configuración de Neovim debería tener:

1. Explorador de archivos: Usando nvim-tree.lua (se abre con <C-n>).

2. Búsqueda: Usando telescope.nvim (busca archivos con <leader>ff y texto con <leader>fg).

3. Barra de estado: Usando lualine.nvim (con el tema tokyonight).

4. Autocompletado: Usando nvim-cmp y LSP.

5. LSP: Configurado para Python, Bash, JavaScript/TypeScript.

---

Consejos adicionales

Aprende los atajos de teclado: Neovim es muy potente cuando dominas sus atajos. Por ejemplo:

:help para acceder a la documentación.

:Telescope commands para ver todos los comandos disponibles.

--- 

Solucion a errores e instalacion de otras herramientas


El error que estás viendo indica que **pyright**, el servidor de lenguaje para Python, no está instalado o no está en tu `PATH`. Vamos a solucionarlo paso a paso.

---

### **¿Qué está pasando?**

1. **`tsserver is deprecated, use ts_ls instead`**:
   - Este mensaje es una advertencia que indica que `tsserver` (el servidor de lenguaje para TypeScript/JavaScript) está obsoleto y deberías usar `typescript-language-server` (ts_ls) en su lugar. Esto no afecta a Python, pero lo solucionaremos más adelante.

2. **Error con `pyright`**:
   - El servidor de lenguaje `pyright` no está instalado o no es ejecutable. Esto impide que Neovim pueda ofrecer funcionalidades como autocompletado, detección de errores, etc., para Python.

---

### **Solución paso a paso**

#### **Paso 1: Instalar pyright**

`pyright` es el servidor de lenguaje para Python. Neovim no lo instala automáticamente, así que debes instalarlo manualmente.

1. **Instalar pyright con npm**:

- Asegúrate de tener `npm` (Node.js Package Manager) instalado. Si no lo tienes, instálalo:
```bash
sudo apt update
sudo apt install nodejs npm
```
- Instala `pyright` globalmente:
 
```bash
sudo npm install -g pyright
```

2. **Verificar la instalación**:

- Ejecuta el siguiente comando para asegurarte de que `pyright` esté instalado:

```bash
pyright --version
```
   - Deberías ver la versión de `pyright` instalada.

3. **Agregar `pyright` al PATH**:

- Si `pyright` no está en tu `PATH`, agrega la ruta de instalación de `npm` a tu `PATH`. Normalmente, `npm` instala los binarios globales en `~/.npm-global/bin`. Agrega esto a tu `.bashrc` o `.zshrc`:

```bash
export PATH="$HOME/.npm-global/bin:$PATH"
```
   - Luego, recarga tu shell:
   
```bash
source ~/.bashrc  # o source ~/.zshrc
```

---

#### **Paso 2: Configurar el servidor de lenguaje para TypeScript**

La advertencia `tsserver is deprecated, use ts_ls instead` indica que debes usar `typescript-language-server` en lugar de `tsserver`.

1. **Instalar typescript-language-server**:

- Instálalo globalmente con `npm`:

```bash
sudo npm install -g typescript-language-server typescript
```

2. **Actualizar la configuración de LSP en `init.lua`**:

- Reemplaza la configuración de `tsserver` por `typescript-language-server` en tu archivo `init.lua`:

```lua
lspconfig.tsserver.setup({})  -- Línea antigua (obsoleta)
```
     Por:
     
```lua
lspconfig.tsserver.setup({
  cmd = { "typescript-language-server", "--stdio" },
})
```

---

#### **Paso 3: Verificar la configuración de LSP**

Asegúrate de que tu archivo `init.lua` tenga la configuración correcta para `pyright` y `typescript-language-server`. Aquí te dejo un ejemplo:

```lua
-- Configuración de LSP
require('mason').setup()
require('mason-lspconfig').setup({
  ensure_installed = { 'pyright', 'bashls', 'tsserver' }  -- Servidores para Python, Bash, JS/TS
})

local lspconfig = require('lspconfig')
lspconfig.pyright.setup({})  -- LSP para Python
lspconfig.bashls.setup({})   -- LSP para Bash
lspconfig.tsserver.setup({    -- LSP para JavaScript/TypeScript
  cmd = { "typescript-language-server", "--stdio" },
})
```

---

#### **Paso 4: Reiniciar Neovim**

1. Guarda el archivo `init.lua` (`:w`).
2. Cierra Neovim (`:q`).
3. Vuelve a abrir Neovim:

```bash
nvim mi.py
```

---

#### **Paso 5: Verificar que todo funcione**

1. **Autocompletado**:

   - Escribe código en Python y verifica que el autocompletado funcione.

2. **Detección de errores**:

   - Introduce un error en tu código (por ejemplo, una variable no definida) y verifica que Neovim lo resalte.

3. **Explorador de archivos**:

   - Presiona `<C-n>` para abrir el explorador de archivos.

4. **Búsqueda**:

   - Usa `<leader>ff` para buscar archivos y `<leader>fg` para buscar texto.

---

### **Si el error persiste**

1. **Verifica que `pyright` esté en tu `PATH`**:
   - Ejecuta:
   
```bash
which pyright
```
   - Si no devuelve una ruta, asegúrate de que `~/.npm-global/bin` esté en tu `PATH`.

2. **Reinstala los plugins**:

   - Ejecuta `:PackerSync` en Neovim para reinstalar los plugins.

3. **Revisa los logs de LSP**:

   - Ejecuta `:LspInfo` en Neovim para ver el estado de los servidores de lenguaje.

---

### **Resumen**

1. Instala `pyright` con `npm`.
2. Instala `typescript-language-server` con `npm`.
3. Actualiza la configuración de LSP en `init.lua`.
4. Reinicia Neovim y verifica que todo funcione.





