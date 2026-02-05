
Crear archivo .lua

```lua
-- 2. Configuración básica de Neovim
vim.opt.number = true          -- Mostrar números de línea
vim.opt.relativenumber = true  -- Números de línea relativos
vim.opt.tabstop = 4            -- Tamaño de tabulación
vim.opt.shiftwidth = 4         -- Tamaño de indentación
vim.opt.expandtab = true       -- Usar espacios en lugar de tabs

```

---

Gestor de paquetes packer

dirigirse al repo :

https://github.com/wbthomason/packer.nvim

copiar el archivo Bootstrapping en el archivo con el nombre:
plugins-setup.lua

```lua
local ensure_packer = function()
  local fn = vim.fn
  local install_path = fn.stdpath('data')..'/site/pack/packer/start/packer.nvim'
  if fn.empty(fn.glob(install_path)) > 0 then
    fn.system({'git', 'clone', '--depth', '1', 'https://github.com/wbthomason/packer.nvim', install_path})
    vim.cmd [[packadd packer.nvim]]
    return true
  end
  return false
end

local packer_bootstrap = ensure_packer()

return require('packer').startup(function(use)
  use 'wbthomason/packer.nvim'
  -- My plugins here
  -- use 'foo1/bar1.nvim'
  -- use 'foo2/bar2.nvim'

  -- Automatically set up your configuration after cloning packer.nvim
  -- Put this at the end after all plugins
  if packer_bootstrap then
    require('packer').sync()
  end
end)
```






















