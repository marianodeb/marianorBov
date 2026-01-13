## **CSS snippets** (fragmentos de CSS)

### **1. ¿Qué son los CSS snippets en Obsidian?**

Son archivos `.css` que contienen reglas de estilo para modificar la apariencia de Obsidian. Funcionan como "temas personalizados" que puedes activar/desactivar sin necesidad de crear un tema completo.

---

### **2. ¿Cómo agregar un snippet?**

**Pasos:**

1. **Crear el archivo CSS:**
   - Ve a la carpeta de tu vault de Obsidian (normalmente ubicada en `Documents/Obsidian/` o donde lo hayas configurado).
   - Abre la carpeta `.obsidian/snippets/` (si no existe, créala manualmente).
   - Crea un archivo nuevo con extensión `.css` (ej: `mi-estilo.css`).

2. **Habilitar el snippet:**
   - Abre Obsidian.
   - Ve a **Settings → Appearance**.
   - Baja hasta la sección **CSS snippets**.
   - Verás una lista de archivos en la carpeta `snippets`. Activa el toggle junto al nombre de tu archivo CSS.

---

### **3. ¿Cómo saber qué elementos modificar con CSS?**

Obsidian está construido con tecnologías web (HTML + CSS), por lo que puedes inspeccionar su estructura como si fuera una página web. Aquí las opciones:

#### **a) Usar el modo desarrollador de Obsidian:**

   - Abre Obsidian.
   - Presiona `Ctrl + Shift + I` (Windows/Linux) o `Cmd + Option + I` (Mac) para abrir las **herramientas de desarrollador**.
   - Usa el ícono de "inspeccionar elemento" (🔍) para seleccionar cualquier parte de la interfaz y ver su estructura HTML y clases CSS.

   Ejemplo:  
   Si inspeccionas un encabezado `# Hola`, verás algo como:
   
```html
<h1 class="cm-header-1">Hola</h1>
```
   Entonces, en tu CSS puedes apuntar a `.cm-header-1 { color: red; }`.

#### **b) Usar documentación de la comunidad:**

   - La estructura de clases de Obsidian puede cambiar entre versiones, así que es útil buscar referencias actualizadas:
     - **[Obsidian Advanced CSS](https://github.com/obsidian-community/obsidian-advanced-css)**: Guías y ejemplos de la comunidad.
     - **[Theme Development Docs](https://docs.obsidian.md/Reference/CSS+variables/CSS+variables)**: Documentación oficial de variables CSS de Obsidian.

---

### **4. ¿Cómo encontrar los elementos a personalizar?**

Algunos elementos comunes y sus selectores CSS:

| **Elemento**               | **Selector CSS de ejemplo**        |
|-----------------------------|------------------------------------|
| Texto en el editor          | `.cm-content`                      |
| Encabezados (h1, h2, etc.)  | `.cm-header-1`, `.cm-header-2`     |
| Citas (blockquotes)         | `.cm-quote`                        |
| Listas                     | `.cm-list`                         |
| Código en línea             | `.cm-inline-code`                  |
| Enlaces                     | `.cm-hmd-internal-link`            |
| Barra lateral izquierda     | `.workspace-drawer`                |
| Barra de búsqueda           | `.search-input-container`          |

---

### **5. Ejemplo práctico:**

Supongamos que quieres cambiar el color de los encabezados `h1` a rojo y el fondo de la app a negro:

```css
/* mi-estilo.css */
.cm-header-1 {
  color: red;
}

.workspace-tabs {
  background-color: #000;
  color: white;
}
```

---

### **6. Consejos clave:**

- **Prueba cambios pequeños:** Edita tu CSS, guarda el archivo y recarga Obsidian (`Ctrl + R` o `Cmd + R`) para ver los cambios.
- **Usa variables de Obsidian:** Algunos estilos pueden aprovechar variables CSS predefinidas (ej: `var(--text-normal)` para el color de texto).
- **Backup:** Guarda tus snippets en un lugar seguro (como GitHub) por si reinstalas Obsidian.

---

### **7. Errores comunes:**
- **El CSS no se aplica:**
  - Asegúrate de que el archivo esté en `.obsidian/snippets/`.
  - Verifica que el snippet esté activado en **Settings → Appearance → CSS snippets**.
  - Revisa la sintaxis CSS (ej: puntos y comas, llaves cerradas).
- **El selector no funciona:** Las clases CSS de Obsidian pueden cambiar con actualizaciones. Usa siempre el modo desarrollador para verificar.

---

### **Recursos adicionales:**
- **[Obsidian Forum - Themes & CSS](https://forum.obsidian.md/c/theme/14)**: Foro oficial para temas y CSS.
- **[CSS Snippets Gallery](https://github.com/Dmytro-Shulha/obsidian-css-snippets)**: Colección de snippets populares.

---

### **1. ¿Todo Obsidian es como un HTML?**

Sí, **toda la interfaz de Obsidian está construida con tecnologías web** (HTML, CSS y JavaScript). Esto incluye:
- **El editor de texto** (donde escribes tus notas).
- **La interfaz gráfica** (barras laterales, pestañas, menús, paneles, botones, etc.).
- **Componentes dinámicos** (búsqueda, gráficos, plugins, etc.).

Es decir, **todo lo que ves en Obsidian es renderizado como una página web**, por lo que puedes modificar su apariencia con CSS.  
*(Incluso puedes inspeccionar elementos como en Chrome/Firefox, como veremos más abajo).*

---

### **2. ¿Qué partes se pueden personalizar?**

#### **a) El editor de texto (contenido de las notas):**

- **Base:** Usa **[CodeMirror 6](https://codemirror.net/)** (biblioteca para editores de texto en web).
- **Clases CSS:** Empiezan con `.cm-` (ej: `.cm-line` para una línea de texto, `.cm-header` para encabezados).
- **Ejemplos de elementos:**
  - Encabezados: `.cm-header-1`, `.cm-header-2`, etc.
  - Listas: `.cm-list`, `.cm-list-item`.
  - Citas: `.cm-quote`.
  - Enlaces: `.cm-link`, `.cm-url`.

#### **b) La interfaz de usuario (UI):**

- **Paneles, barras, botones, etc.:** Tienen clases como `.workspace-`, `.modal-`, `.menu-`, `.setting-`, etc.
- **Ejemplos de elementos:**

  - Barra lateral izquierda: `.workspace-drawer`.
  - Tabs (pestañas): `.workspace-tab-header`.
  - Búsqueda: `.search-input-container`.
  - Menú de comandos: `.prompt`.

#### **c) Temas y variables CSS:**

- Obsidian usa **variables CSS personalizadas** para colores y estilos, lo que facilita la coherencia visual.  
  Ejemplo:  
  
```css
  body {
    --background-primary: #1a1a1a; /* Color de fondo */
    --text-normal: #ffffff; /* Color de texto */
  }
```

---

### **3. ¿Cómo identificar elementos y clases?**

La mejor forma es usar **Herramientas de Desarrollador** (DevTools) integradas en Obsidian:

#### **Pasos:**

1. **Abre las DevTools:**
   - **Windows/Linux:** `Ctrl + Shift + I`.
   - **Mac:** `Cmd + Option + I`.

2. **Inspecciona cualquier elemento:**

   - Haz clic en el ícono **"Select Element"** (🔍) en la barra superior de las DevTools.
   - Pasa el cursor sobre cualquier parte de Obsidian (editor, botones, paneles, etc.) y haz clic para seleccionarlo.

3. **Explora la pestaña "Elements" (Chrome) o "Inspector" (Firefox):**

   - Verás la estructura HTML completa del elemento seleccionado.
   - Las clases CSS asociadas aparecen en el panel de estilos (ej: `<div class="workspace-drawer">`).

---

### **4. Ejemplos de elementos comunes y sus clases**

Aquí tienes una tabla con elementos clave y sus selectores CSS:

| **Elemento**               | **Selector CSS**                          |
|----------------------------|-------------------------------------------|
| **Editor de texto**         | `.cm-content`                             |
| **Línea de texto**          | `.cm-line`                                |
| **Encabezado H1**           | `.cm-header-1`                            |
| **Enlace interno**          | `.cm-link`, `.cm-hmd-internal-link`       |
| **Código en línea**         | `.cm-inline-code`                         |
| **Barra lateral izquierda** | `.workspace-drawer`                       |
| **Pestañas de archivos**    | `.workspace-tab-header`                   |
| **Barra de estado**         | `.status-bar`                             |
| **Búsqueda global**         | `.search-input-container input`          |
| **Modal de configuración**  | `.modal-container`                        |
| **Botones**                 | `.clickable-icon`, `.mod-cta`            |

---

### **5. Ejemplo práctico: Personalizar dos áreas**

Supongamos que quieres:

- Cambiar el color de los enlaces internos a verde.
- Oscurecer el fondo de la barra lateral izquierda.

**Código CSS:**

```css
/* Enlaces internos en el editor */
.cm-hmd-internal-link {
  color: #00ff00 !important;
  text-decoration: underline;
}

/* Barra lateral izquierda */
.workspace-drawer {
  background-color: #1a1a1a !important;
  border-right: 1px solid #333;
}
```

---

### **6. Recursos para explorar más**

- **[Obsidian CSS Reference](https://docs.obsidian.md/Reference/CSS+variables/CSS+variables)**: Lista oficial de variables CSS.
- **[Obsidian Advanced CSS](https://github.com/obsidian-community/obsidian-advanced-css)**: Guías detalladas de la comunidad.
- **[Theme Development Docs](https://marcus.se.net/obsidian-plugin-docs/)**: Cómo crear temas completos (útil para snippets).

---

### **7. ¡Importante!**

- **Las clases pueden cambiar:** Obsidian actualiza su estructura HTML/CSS en nuevas versiones. Si un snippet deja de funcionar, revisa con las DevTools.
- **Usa `!important` con cuidado:** A veces es necesario para sobrescribir estilos predeterminados, pero no abuses.
- **Prueba en modo "Vault vacío":** Si tienes muchos plugins o temas, algunos estilos pueden interferir. Prueba en un vault limpio para aislar problemas.

---










