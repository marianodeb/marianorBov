Claro, aquí tienes la sintaxis, opciones comunes y ejemplos de los comandos `more` y `less` en sistemas Unix/Linux:

### 1. `more`

**Sintaxis:**
```bash
more [opciones] [archivo(s)]
```

**Opciones Comunes:**
- `-n`: Muestra la línea actual y el número total de líneas.
- `+n`: Comienza a mostrar desde la línea n (1-indexed).
- `/patrón`: Busca el siguiente patrón y lo muestra.

**Ejemplos:**
- Mostrar el contenido de un archivo página por página:
  ```bash
  more archivo.txt
  ```

- Mostrar el contenido de varios archivos, avanzando con la barra espaciadora:
  ```bash
  more archivo1.txt archivo2.txt
  ```

- Buscar y mostrar la primera ocurrencia de un patrón dentro de un archivo:
  ```bash
  more +/patrón archivo.txt
  ```

### 2. `less`

**Sintaxis:**
```bash
less [opciones] [archivo(s)]
```

**Opciones Comunes:**
- `-N`: Muestra el número de línea actual y el número total de líneas.
- `-i`: Ignora diferencias de mayúsculas y minúsculas durante la búsqueda.
- `/patrón`: Busca el siguiente patrón y lo muestra.

**Ejemplos:**
- Mostrar el contenido de un archivo página por página con capacidad de desplazamiento hacia arriba y hacia abajo:
  ```bash
  less archivo.txt
  ```

- Mostrar el contenido de varios archivos, avanzando con la barra espaciadora:
  ```bash
  less archivo1.txt archivo2.txt
  ```

- Buscar y mostrar todas las ocurrencias de un patrón dentro de un archivo, navegando con `n` (siguiente) y `N` (anterior):
  ```bash
  less +/patrón archivo.txt
  ```

- Mostrar el número de línea actual y el número total de líneas durante la visualización del archivo:
  ```bash
  less -N archivo.txt
  ```

### Notas Adicionales:
- **`more`** es más básico y muestra el contenido página por página, permitiendo avanzar una página a la vez con la barra espaciadora.
- **`less`** es más avanzado, ya que permite navegar hacia arriba y hacia abajo dentro del archivo, buscar patrones, y proporciona más opciones de visualización y navegación que `more`.

