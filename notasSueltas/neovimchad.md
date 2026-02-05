


- Ejecuta :Lazy sync para actualizar los plugins.
- Instala los servidores LSP con Mason:
Abre Neovim y ejecuta :Mason, luego busca e instala html-lsp y css-lsp.




---

### **1. Instalar LSPs (con Mason)**  

**Mason** es el gestor de LSPs que usa NvChad. Así lo usas:

1. **Abre Neovim**.
2. **Ejecuta el comando**:  

```vim
:Mason
```

   Se abrirá una ventana con todos los LSPs, formateadores, linters, etc., disponibles.

3. **Navega con las teclas** `j`/`k` y presiona `i` para instalar un LSP.  

   Ejemplo:  
   
   - `html-lsp` → LSP para HTML.  
   - `css-lsp` → LSP para CSS.  
   - `tsserver` → LSP para TypeScript/JavaScript.  
   - `pyright` → LSP para Python.  
   - `rust_analyzer` → LSP para Rust.

4. **Para salir de Mason**, presiona `q`.

---

### **2. Listar LSPs instalados**  

#### **Opción A: Desde Mason**  

- Ejecuta `:Mason`, y busca los que tengan `installed` en su línea.  
  Mason UI

#### **Opción B: Desde Neovim (comando LSP)**  

- Abre un archivo del lenguaje que quieras (ej: `index.html`).  
- Ejecuta:  

```vim
:LspInfo
```
  Verás si el LSP está activo para ese buffer.  

---

### **3. Agregar más LSPs a tu configuración**  

Edita tu archivo `~/.config/nvim/lua/configs/lspconfig.lua` y agrega los servidores que quieras a la lista `servers`:

```lua
local servers = {
  "html",
  "cssls",
  "tsserver",       -- TypeScript/JavaScript
  "pyright",        -- Python
  "rust_analyzer",  -- Rust
  "gopls",          -- Go
  "clangd",         -- C/C++
}
```

Luego:  

1. **Instala los LSPs** con `:Mason` (como expliqué antes).  
2. **Reinicia Neovim**.

---

### **4. Ejemplo completo de `lspconfig.lua`**  

```lua
local on_attach = require("nvchad.configs.lspconfig").on_attach
local capabilities = require("nvchad.configs.lspconfig").capabilities

local lspconfig = require("lspconfig")

-- Lista de servidores LSP
local servers = {
  "html",
  "cssls",
  "tsserver",
  "pyright",
  "rust_analyzer",
}

-- Configurar cada servidor
for _, server in ipairs(servers) do
  lspconfig[server].setup({
    on_attach = on_attach,
    capabilities = capabilities,
  })
end
```

---

### **Troubleshooting**  
- **Si un LSP no se activa**:  
  - Verifica que lo hayas instalado con `:Mason`.  
  - Asegúrate de que el servidor esté en la lista `servers` de `lspconfig.lua`.  
  - Revisa que no haya errores de sintaxis en el archivo con `:checkhealth`.

- **Comando útil**:  
  ```vim
  :LspRestart  -- Reinicia el LSP del buffer actual.
  ```

---

### **Bonus**: Si usas **lazy.nvim** (gestor de plugins de NvChad):  

- Actualiza tus plugins con:  

```vim
:Lazy sync
```










