

## Instalacion

### Opcion 1 del repositorio (recomendad):

```bash
curl -fsSL https://yazi-rs.github.io/builds/yazi-keyring.gpg | sudo tee /usr/share/keyrings/yazi-keyring.gpg >/dev/null
echo 'deb [signed-by=/usr/share/keyrings/yazi-keyring.gpg] https://yazi-rs.github.io/builds/ stable main' | sudo tee /etc/apt/sources.list.d/yazi.list >/dev/null
sudo apt update && sudo apt install yazi
```

### Opcion 2 compilar:

```bash
bash
# 1. Descargar e instalar el entorno oficial de Rust y Cargo
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# 2. Cargar las variables de entorno de Cargo en la sesión actual de la terminal
source "$HOME/.cargo/env"

# 3. Instalar dependencias para previsualizaciones (Videos, PDFs, JSON, SVG, Fuentes, ZIPs) y utilidades de búsqueda/portapapeles
sudo apt update && sudo apt install -y build-essential ffmpeg poppler-utils fd-find ripgrep fzf zoxide 7zip jq resvg imagemagick wl-clipboard xclip

# 4. Compilar e instalar Yazi y su CLI mediante Cargo
cargo install --force yazi-build

# 5. Iniciar Yazi para verificar que todo funcione correctamente
yazi
```

Aquí tenés la guía definitiva y en limpio, totalmente corregida y lista para guardar o tener a mano como machete:

### 🧭 Navegación Básica

| Tecla | Acción |
| --- | --- |
| `h` | Subir al directorio padre |
| `l` | Entrar al directorio / Abrir archivo |
| `j` / `k` | Moverse hacia abajo / arriba |
| `gg` / `G` | Ir al principio / final de la lista |
| `J` / `K` | Desplazar el contenido del panel de vista previa hacia abajo / arriba |
| `Alt` + `<número>` | Cambiar entre pestañas |
| `t` / `w` | Abrir nueva pestaña / Cerrar pestaña actual |
| `q` | Salir de Yazi |


### 🗂️ Gestión de Archivos

| Tecla | Acción |
| --- | --- |
| `y` / `x` | Copiar (Yank) / Cortar archivos seleccionados |
| `p` | Pegar archivos copiados o cortados |
| `d` / `D` | Mover a la papelera / Eliminar permanentemente |
| `r` | Renombrar (si seleccionás varios, abre el editor en masa) |
| `a` | Crear archivo (añadí `/` al final para crear una carpeta, ej: `mi-carpeta/`) |
| `.` | Mostrar u ocultar archivos ocultos (dotfiles) |
| `Espacio` | Seleccionar / Deseleccionar un archivo individual |
| `v` | Entrar en modo de selección visual |
| `Ctrl` + `a` | Seleccionar todos los archivos del directorio |
| `Ctrl` + `c` | Copiar la ruta absoluta al portapapeles |


### 🔍 Búsqueda y Filtrado

| Tecla | Acción |
| --- | --- |
| `/` | **Filtrar** archivos en tiempo real en la carpeta actual |
| `f` | Búsqueda difusa (**fzf**) en la carpeta y subcarpetas |
| `s` | Buscar archivos recursivamente por nombre (**fd**) |
| `S` | Buscar *dentro del contenido* de los archivos (**ripgrep**) |
| `z` | Salto inteligente a directorios frecuentes (**zoxide**) |
| `Esc` | Cancelar el filtro o la búsqueda activa |


### 💡 Utilidades y Ayuda

* `~` (o `F1`): Abre la **ayuda interactiva** con todos los atajos en pantalla.
* `;`: Abre una **línea de comandos (shell)** en el directorio actual.
* `e`: Abre el archivo seleccionado en tu **editor por defecto** (`$EDITOR`).


## Viso de pdf cat-md

### Kitty-Markdown-Viewer


https://github.com/parf/Kitty-Markdown-Viewer

### instalacion

```bash
# 1. Instalar las librerías de Python necesarias (Pillow para imágenes y Rich para formato de texto)
pip install rich pillow --break-system-packages

# 2. Descargar el repositorio oficial del visor desde GitHub
git clone https://github.com/parf/Kitty-Markdown-Viewer.git

# 3. Entrar a la carpeta que se acaba de descargar
cd Kitty-Markdown-Viewer

# 4. Darle permisos de ejecución al script principal de Python
chmod +x kitty-md.py

# 5. Mover el ejecutable a los binarios del sistema renombrándolo a 'kitty-md' para usarlo desde cualquier lugar
sudo mv kitty-md.py /usr/local/bin/kitty-md

# 6. (Opcional) Borrar la carpeta del repositorio clonado ya que el script quedó guardado en el sistema
cd .. && rm -rf Kitty-Markdown-Viewer

# 7. Probar el visor con cualquier archivo Markdown de tu equipo
kitty-md README.md

```

**No, `cat-md` es un visor exclusivamente de lectura (Read-Only).** No permite editar el texto directamente sobre la pantalla como lo harías en Neovim o Nano. Su único objetivo es tomar el archivo `.md` y renderizarlo de forma visual (títulos gigantes, imágenes integradas, tablas con bordes y enlaces cliqueables).

Para editar, el flujo de trabajo ideal es abrir el archivo en tu editor favorito (como Neovim) y usar `cat-md` para visualizar el resultado final.

### Modos de uso y comandos de terminal

`cat-md` funciona directamente desde la terminal pasando archivos o recibiendo texto por tuberías (`pipes`).

* `cat-md archivo.md`: Renderiza un archivo Markdown individual.
* `cat-md nota1.md nota2.md`: Renderiza varias notas en secuencia, una detrás de otra.
* `cat mi_nota.md | cat-md`: Lee el contenido desde una tubería (stdin).
* `cat-md [https://sitio.com/README.md](https://sitio.com/README.md)`: Descarga y renderiza una nota o README guardado en la web.
* `cat-md --theme light archivo.md`: Fuerza el tema claro (por defecto auto-detecta si usás terminal oscura o clara).
* `cat-md --theme dark archivo.md`: Fuerza el tema oscuro.
* `cat-md --init-config`: Crea los archivos de configuración y temas en `~/.config/cat-md/` por si querés cambiarles los colores a futuro.

### Control de navegación dentro del visor (El Pager)

Cuando la nota supera el tamaño de tu pantalla, `cat-md` usa automáticamente un paginador (`less -r`). Esto hace que la pantalla se detenga y te permita navegar usando **atajos al estilo Vim** sin modificar el archivo original.

**Atajos de teclado dentro de la vista:**

* `j` o **Flecha Abajo**: Bajar una línea.
* `k` o **Flecha Arriba**: Subir una línea.
* `Espacio` o `Ctrl` + `f`: Avanzar una página entera hacia abajo.
* `b` o `Ctrl` + `b`: Retroceder una página entera hacia arriba.
* `g`: Ir al principio del documento.
* `G`: Ir al final del documento.
* `/`: Entrar en **modo de búsqueda**. Tipeás la palabra que buscás y presionás `Enter`.
* `n`: Ir a la **siguiente** coincidencia de la búsqueda.
* `N`: Ir a la coincidencia **anterior**.


* `q`: **Salir** del visor y volver a la terminal limpia.

*(Nota: En este modo de lectura **no hay modos de inserción** como en Neovim. No hace falta tocar `Esc` salvo para borrar lo que escribiste en la barra de búsqueda `/`)*.

### Sintaxis para tomar notas en Markdown (Compatibles con `cat-md`)

Para sacarle provecho a lo que el visor puede renderizar, podés estructurar tus notas en tu editor usando la siguiente sintaxis estándar:

```markdown
# Título Gigante (H1)
## Subtítulo Mediano (H2)
### Sección con subrayado de color (H3)

*Texto en cursiva* y **Texto en negrita**
~~Texto tachado~~ y `código en línea`

---
(Línea horizontal separadora)

# Enlaces e imágenes
[Texto del Enlace Cliqueable](https://google.com)
![Texto alternativo de imagen](assets/imagen.png)

# Bloque de código con resaltado
```python
def hola_mundo():
    print("Hola desde la nota")

```

# Listas de tareas

* [x] Tarea completada
* [ ] Tarea pendiente

# Cajas de aviso destacadas (Callouts)

> [!NOTE]
> Nota importante para revisar después.

> [!WARNING]
> Cuidado con modificar este archivo de configuración.

> [!TIP]
> Un consejo rápido para la terminal.

```

<Elicitations message="¿Querés integrar la visualización de notas en tu flujo de trabajo?">
  <Elicitation label="Integrar con Yazi" query="¿Cómo configuro Yazi para previsualizar notas .md con cat-md al moverme sobre ellas?"/>
  <Elicitation label="Crear un alias de acceso rápido" query="¿Cómo creo un alias para abrir el editor y el visor con un solo comando?"/>
</Elicitations>

```




