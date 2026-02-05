

## Atajos importantes

**nvim-tree** (explorador de archivos)
**bufferline** (gestión de pestañas) 
**Telescope** (búsqueda rápida) en **NvChad**.  


### **1. Explorador de archivos (`nvim-tree.lua`)**  

**Atajos principales** (modo normal):  

| Acción                  | Atajo          |
|-------------------------|----------------|
| Abrir/cerrar explorador | `<Leader>e` (normalmente `Espacio + e`) |
| Crear archivo/carpeta   | `a`            |
| Eliminar archivo        | `d`            |
| Renombrar               | `r`            |
| Copiar nombre de ruta   | `y`            |
| Pegar archivo           | `p`            |
| Refrescar explorador    | `<C-r>`        |
| Navegar por archivos    | `hjkl` o flechas |
| Cerrar nodo/carpeta     | `h` o `Left`   |
| Abrir nodo/carpeta      | `l` o `Right`  |
| Abrir en ventana vertical/horizontal | `v` / `s` |
| Ir al directorio padre  | `-`            |



### **2. Gestión de buffers/pestañas (`bufferline`)**  

**Atajos principales**:  

| Acción                     | Atajo               |
|----------------------------|---------------------|
| Cambiar al siguiente buffer| `<Tab>` o `:bnext`  |
| Cambiar al anterior buffer | `<S-Tab>` o `:bprev`|
| Cerrar buffer actual       | `:bd`               |
| Cerrar todos los buffers   | `:%bd`              |
| Mover buffer a la izquierda| `<Leader>bh`        |
| Mover buffer a la derecha  | `<Leader>bl`        |
| Ir a buffer específico     | `Alt + número` (ej. `Alt+1` para el primer buffer) |

*(Nota: `<Leader>` suele ser la tecla `Espacio` en NvChad)*  


### **3. Búsqueda rápida (`Telescope`)**  

**Atajos principales**:  

#### **Buscar archivos (`<Leader>ff`)**  

| Acción                     | Atajo          |
|----------------------------|----------------|
| Buscar archivo por nombre  | `<Leader>ff`   |
| Navegar resultados         | `↑` / `↓`      |
| Abrir archivo seleccionado | `<Enter>`      |
| Abrir en ventana vertical  | `<C-v>`        |
| Abrir en ventana horizontal| `<C-x>`        |
| Previsualizar archivo      | `<C-p>`        |
| Cerrar Telescope           | `<Esc>` o `<C-c>` |


### **Buscar texto en archivos (`<Leader>fg`)**  

| Acción                     | Atajo          |
|----------------------------|----------------|
| Buscar texto (grep)        | `<Leader>fg`   |
| Buscar palabra bajo cursor | `<Leader>fw`   |
| Cambiar entre modos (grep, live_grep) | `<C-q>` |


### **Buscar en directorios/proyectos**  

| Acción                     | Atajo          |
|----------------------------|----------------|
| Buscar en proyectos recientes | `<Leader>fp` |
| Buscar en directorio actual| `<Leader>fd`   |


### **Otros comandos útiles de Telescope**  

| Acción                     | Comando/Atajo  |
|----------------------------|----------------|
| Buscar comandos de Neovim  | `<Leader>fc`   |
| Buscar temas de color      | `<Leader>ft`   |
| Buscar buffers abiertos    | `<Leader>fb`   |
| Buscar ayuda (`:help`)     | `<Leader>fh`   |



### **Resumen de los atajos más útiles**  

| Categoría       | Atajo Principal       | Uso                     |
|-----------------|-----------------------|-------------------------|
| **Explorador**  | `<Leader>e`           | Abrir/cerrar nvim-tree  |
| **Buffers**     | `<Tab>` / `<S-Tab>`   | Cambiar entre buffers   |
| **Buscar**      | `<Leader>ff`          | Buscar archivos         |
| **Buscar texto**| `<Leader>fg`          | Buscar texto en archivos |


###  **Personalización (opcional)**  

Si quieres cambiar los atajos, puedes editar:  

```lua
~/.config/nvim/lua/custom/mappings.lua
```

Ejemplo para cambiar el atajo de `nvim-tree`:  

```lua
vim.api.nvim_set_keymap("n", "<Leader>t", ":NvimTreeToggle<CR>", { noremap = true })
```


