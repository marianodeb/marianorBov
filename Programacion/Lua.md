

## **Lua**

### **1. ¿Qué es Lua?**

- **Lenguaje de scripting**: Ligero, rápido y diseñado para ser embebido en aplicaciones (ej: Neovim lo usa para su configuración).
- **No es nativo del sistema**: A diferencia de Bash (que es parte de GNU/Linux) o Python (que requiere su intérprete), **Lua necesita instalarse manualmente**.

### Sintaxis  --crear enlace a lua sintaxis 

### **2. Instalar el intérprete de Lua**

#### **Linux (Debian/Ubuntu):**

```bash
sudo apt install lua5.4
```

#### **Windows:**

- Descarga el instalador desde [LuaBinaries](https://luabinaries.sourceforge.net/) y añade la ruta de instalación al `PATH`.

#### **macOS:**

```bash
brew install lua
```

---

### **3. Ejecutar un archivo `.lua`**
#### **Opción A: Directamente con el intérprete**

```bash
lua nombre_del_archivo.lua
```

#### **Opción B: Hacer el script ejecutable (como un `.sh`)**

1. Añade este **shebang** al inicio del archivo `.lua`:

```lua
#!/usr/bin/env lua
```

2. Dale permisos de ejecución:

```bash
chmod +x archivo.lua
```
   
3. Ejecútalo:

```bash
./archivo.lua
```

### **Ejemplo práctico**

1. **Crea un archivo `hola.lua`:**

```lua
#!/usr/bin/env lua
print("¡Hola desde Lua!")
```

2. **Ejecútalo:**

```bash
lua hola.lua       # Opción A
./hola.lua         # Opción B (tras dar permisos)
```

### **Comparación con otros lenguajes**

| Lenguaje | Comando para ejecutar       | Requiere instalación previa |
|----------|-----------------------------|-----------------------------|
| **Bash** | `./script.sh` o `bash script.sh` | No (es parte del sistema)   |
| **Python**| `python script.py`          | Sí (Python instalado)       |
| **Lua**  | `lua script.lua`            | Sí (Lua instalado)          |


### **4. ¿Por qué Neovim usa Lua si no es nativo?**

- **Lua está integrado en Neovim**: No necesitas instalarlo aparte para configurar Neovim, ya que viene con su propio **intérprete Lua embebido**.
- **Ejecutar scripts externos**: Si quieres correr archivos `.lua` fuera de Neovim, sí necesitas el intérprete de Lua instalado.


### **5. Solución de errores comunes**

#### **Error: `lua: command not found`**

- **Causa**: Lua no está instalado o no está en el `PATH`.
- **Solución**:  

  - Linux: `sudo apt install lua5.4`.  
  - Windows: Revisa la instalación y el `PATH`.

#### **Error: `Permission denied` al ejecutar `./archivo.lua`**

- **Solución**:  

```bash
chmod +x archivo.lua
```
---

¡Buena pregunta! Cuando digo que Lua está **"diseñado para ser embebido en aplicaciones"**, me refiero a que su arquitectura está optimizada para integrarse como un **lenguaje de scripting dentro de otros programas o aplicaciones**, permitiendo extender o personalizar su funcionamiento. 

### **¿Qué significa esto en la práctica?**
Imagina que tienes una aplicación principal (ej: un videojuego, un editor de texto como Neovim, o un navegador web). En lugar de modificar directamente el código fuente de la aplicación (lo cual es complejo y riesgoso), puedes usar Lua para añadir comportamientos personalizados *sin tocar el núcleo del programa*. 


### **Ejemplos concretos**

#### 1. **Neovim (tu caso de uso)**:

   - **Aplicación principal**: Neovim (editor de texto).
   - **Lenguaje embebido**: Lua.
   - **Cómo funciona**:
     - Neovim tiene un **intérprete de Lua integrado**.
     - Tú escribes scripts en Lua para configurar atajos de teclado, plugins, temas, etc.
     - Neovim ejecuta tu código Lua para personalizar su comportamiento, pero el núcleo del editor (escrito en C) no se modifica.

#### 2. **Videojuegos (ej: World of Warcraft, Roblox)**:

   - **Aplicación principal**: Motor del juego (escrito en C++ o C#).
   - **Lenguaje embebido**: Lua.
   - **Cómo funciona**:
     - Los jugadores o desarrolladores escriben scripts en Lua para crear misiones, interfaces de usuario (UI), o comportamientos de personajes.
     - El motor del juego ejecuta esos scripts sin necesidad de recompilar todo el código base.

#### 3. **Aplicaciones como Wireshark o Adobe Lightroom**:

   - Usan Lua para permitir a los usuarios automatizar tareas o crear plugins.

### **Características de Lua que lo hacen ideal para esto**

1. **Ligero**: Ocupa muy pocos recursos (el intérprete de Lua ocupa ~1MB).
2. **Portable**: Funciona en casi cualquier sistema operativo sin modificaciones.
3. **API sencilla**: Los desarrolladores pueden integrar Lua en su aplicación con pocas líneas de código.
4. **Flexible**: Permite exponer funciones de la aplicación principal a Lua (ej: en Neovim, la función `vim.api` permite acceder al editor desde Lua).

### **Comparación con otros lenguajes**

| Lenguaje | ¿Se usa como embebido? | Ejemplo de uso embebido          |
|----------|------------------------|-----------------------------------|
| **Lua**  | Sí (diseño principal)  | Neovim, World of Warcraft, Roblox|
| **Python**| Raramente             | Blender (para scripts de 3D)     |
| **JavaScript** | Sí           | Navegadores web (Chrome, Firefox)|

### **¿Por qué no usar Bash o Python para esto?**

- **Bash**: Es un lenguaje nativo de sistemas Unix, pero está limitado a tareas de shell y no es fácil de integrar en aplicaciones complejas.
- **Python**: Aunque es poderoso, es mucho más pesado (~25MB solo el intérprete) y su integración requiere más esfuerzo.

### **En resumen**

Lua es como un **"mini motor"** que las aplicaciones incluyen para permitirte personalizarlas o automatizar tareas, sin necesidad de modificar su código interno. Es la razón por la que Neovim lo eligió para su configuración: ¡tú escribes Lua, y Neovim lo traduce a acciones dentro del editor! 🛠️


