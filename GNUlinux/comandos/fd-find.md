

## **`fd-find`**

### **Definición y Significado**  

`fd-find` (comúnmente conocido como `fd`) es una herramienta de línea de comandos diseñada para buscar archivos y directorios en sistemas Unix/Linux. Es una alternativa moderna, rápida y amigable al comando tradicional `find`, optimizada para casos de uso comunes con configuraciones predeterminadas inteligentes. Entre sus características destacan:  

- **Búsqueda con expresiones regulares** (por defecto) o patrones glob.  
- **Ignorar archivos ocultos y `.gitignore`** por defecto .  
- **Salida colorizada** similar a `ls` para facilitar la identificación de tipos de archivo .  
- **Ejecución paralela** para mayor velocidad .  

### **Sintaxis**  

La sintaxis básica es:

```bash
fd [OPCIONES] [PATRÓN] [RUTA...]
```

Ejemplo:

```bash
fd -e txt ~/documentos  # Busca archivos .txt en ~/documentos
```

---

### **Todas sus Opciones**  

Las opciones se dividen en categorías clave:  

#### **Búsqueda**  

- `-H, --hidden`: Incluye archivos y directorios ocultos .  
- `-I, --no-ignore`: Ignora reglas de `.gitignore`, `.fdignore`, etc. .  
- `-s, --case-sensitive`: Búsqueda sensible a mayúsculas (por defecto: "smart case") .  
- `-g, --glob`: Usa patrones glob en lugar de regex .  
- `-p, --full-path`: Busca en la ruta completa, no solo en el nombre .  

#### **Filtrado**  

- `-t, --type`: Filtra por tipo: `f` (archivos), `d` (directorios), `l` (enlaces simbólicos), `x` (ejecutables), `e` (vacíos) .  
- `-e, --extension`: Filtra por extensión (ej. `-e md` para Markdown) .  
- `-S, --size`: Filtra por tamaño (ej. `-S +1M` para archivos >1MB) .  
- `--changed-within <tiempo>`: Filtra por fecha de modificación reciente (ej. `--changed-within 7d`) .  

#### **Ejecución de Comandos**  

- `-x, --exec`: Ejecuta un comando para cada resultado (ej. `-x rm` para eliminar) .  
- `-X, --exec-batch`: Ejecuta un comando con todos los resultados como argumentos .  

#### **Otros**  

- `-0, --print0`: Separa resultados con caracteres nulos (útil para `xargs`) .  
- `-d, --max-depth <nivel>`: Limita la profundidad de búsqueda .  


### **Ejemplos**  

#### **Simples**  

1. Buscar todos los archivos PDF en el directorio actual:  

```bash
   fd -e pdf
```

2. Buscar directorios llamados `src`:  

```bash
   fd -td src
```
3. Buscar archivos modificados en los últimos 2 días:  

```bash
   fd --changed-within 2d
```

#### **Complejos**

1. Convertir todos los archivos `.jpg` a `.png` en paralelo:

```bash
   fd -e jpg -x convert {} {.}.png
```

*Nota:* `{}` representa el nombre del archivo, `{.}` sin extensión .  

2. Buscar archivos de más de 100MB y eliminarlos:  

```bash
   fd -S +100M -x rm
```

3. Integración con `fzf` (fuzzy finder):  

```bash
   fd | fzf | xargs vim
```

### **Consejos**

1. **Alias en sistemas Debian/Ubuntu**:  

```bash
alias fd=fdfind  # El paquete se llama `fd-find`
```

2. **Ignorar archivos globalmente**: Crea `~/.config/fd/ignore` para exclusiones permanentes .  
3. **Rendimiento**: `fd` es más rápido que `find` gracias a la paralelización y algoritmos optimizados .  
4. **Integración con herramientas**: Usa `fd` con `ripgrep` (rg) para búsquedas de texto dentro de archivos .  

### **Información Adicional**  

- **Alternativas**: `fd` es actualmente el sustituto más popular de `find`. No hay un reemplazo más nuevo, pero se integra bien con `fzf` o `as-tree` para visualización .  
- **Comandos Relacionados**:  
  - `find`: Herramienta tradicional con más opciones, pero menos intuitiva .  
  - `ripgrep (rg)`: Búsqueda eficiente de texto dentro de archivos .  
- **Personalización**: Usa `--color=always` para mantener colores al redirigir salida .  

### **Referencias y Fuentes**  

Para más detalles, consulta:  
- [Documentación oficial de fd](https://github.com/sharkdp/fd) .  
- [Ejemplos avanzados en Baeldung](https://www.baeldung.com/linux/fd-find-alternative) .  
- [Comparación de rendimiento](https://github.com/sharkdp/fd/issues/693) .

