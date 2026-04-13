
## **guía de inicio rápido Flask**. 

### 1. Instalación de Herramientas (En Debian)

En Debian, por seguridad y política del sistema, Python viene "desnudo". Necesitás instalar el gestor de paquetes y el módulo de entornos virtuales manualmente.

```bash
# Actualizar los repositorios
sudo apt update

# Instalar pip (gestor de paquetes) y venv (entornos virtuales)
sudo apt install python3-pip python3-venv

```

**Comandos de verificación:**

* `pip3 --version` (Verifica que pip esté instalado).
* `python3 -m venv --help` (Si despliega ayuda, el módulo venv está listo).


### 2. Estructura de Proyecto y Repositorio

Para crear el repositorio de Git, **siempre** debés pararte en la **carpeta raíz** de tu proyecto.

```bash
mkdir mi_proyecto_flask   # Creamos la carpeta del proyecto
cd mi_proyecto_flask      # ENTRAR ACÁ (Desde acá se hace todo)

git init                  # Iniciamos el repositorio aquí

```

### 3. Manejo del Entorno Virtual (Venv)

Es fundamental para no ensuciar el Python del sistema.

* **Creación:** `python3 -m venv venv` (Crea una carpeta llamada `venv`).
* **Activación:** `source venv/bin/activate` (Verás que el prompt cambia y dice `(venv)`).
* **Desactivación:** `deactivate` (Solo cuando termines de trabajar).


### 4. Instalación de Flask y Dependencias

Con el entorno **activado**, instalamos Flask:

```bash
pip install flask

```

**Creación del archivo `requirements.txt`:**
Este archivo sirve para que otra persona (o vos mismo en otra PC) instale todo lo necesario con un solo comando.

* **Comando para crearlo:** `pip freeze > requirements.txt`


### 5. El archivo `.gitignore`

Este archivo le dice a Git qué carpetas **no** debe subir a la nube (como GitHub). La carpeta del entorno virtual **nunca** se sube porque es pesada y específica de tu PC.

1. Creá el archivo: `touch .gitignore`
2. Abrilo y pegá esto adentro:

```text
venv/
__pycache__/
*.pyc
.env

```

### 6. Código Base (`app.py`) e Importaciones

Aquí tenés cómo se importa lo que pediste al principio de tu archivo:

```python
# Importamos la clase Flask y la función para renderizar HTML
from flask import Flask, render_template 

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html")

if __name__ == "__main__":
    app.run(debug=True)

```

### Resumen de Comandos

| Acción | Comando |
| --- | --- |
| **Instalar herramientas** | `sudo apt install python3-pip python3-venv` |
| **Crear Entorno** | `python3 -m venv venv` |
| **Activar Entorno** | `source venv/bin/activate` |
| **Instalar Flask** | `pip install flask` |
| **Congelar dependencias** | `pip freeze > requirements.txt` |
| **Iniciar Git** | `git init` (siempre en la raíz) |

### Reglas de funciones y nombre de archivos.

#### 1. Cuadro de Reglas (Lo que se respeta vs. Lo que se inventa)

| Elemento en `app.py` | ¿Quién manda? | ¿Qué se debe respetar? |
| --- | --- | --- |
| **`@app.route`** | **Flask** | Sintaxis fija. Siempre lleva el `@` y el nombre exacto. |
| **`"/nombre"`** | **Vos** | Es la URL. Debe ser única y empezar con `/`. |
| **`def funcion():`** | **Vos** | Nombre libre, pero **único** en todo el archivo. |
| **`render_template`** | **Flask** | Nombre de función fijo. Se importa de la librería. |
| **`"file.html"`** | **Vos** | Debe ser el nombre **exacto** del archivo en el disco. |


#### 2. Cuadro de Relevancia de Nombres

| Nombre | Relevancia | Impacto si se cambia |
| --- | --- | --- |
| **Ruta (`/`)** | Alta (Pública) | Cambia la dirección que el usuario escribe en el navegador. |
| **Función (`def`)** | Media (Interna) | Si se repite, Flask no arranca (`AssertionError`). |
| **Archivo HTML** | Crítica (Sistema) | Si no coincide exacto, da error `TemplateNotFound`. |


#### 3. Vista del Directorio (Estructura de Carpetas)

Para que Flask encuentre tus archivos, la carpeta se **debe** llamar `templates` (en minúsculas y plural).

```text
mi_proyecto_flask/
├── app.py                <-- Tu código Python
└── templates/            <-- Carpeta obligatoria
    ├── index.html        <-- El de la ruta "/"
    ├── contacto.html     <-- El de la ruta "/contacto"
    ├── servicios.html    <-- El de la ruta "/servicios"
    └── nosotros.html     <-- El de la ruta "/nosotros"

```


#### 4. Código Completo de `app.py`

Acá tenés los 4 bloques de ejemplo con comentarios detallados para tu Obsidian:

```python
from flask import Flask, render_template

app = Flask(__name__)

# BLOQUE 1: Inicio (Texto simple)
@app.route("/")
def home():
    # Esta función devuelve texto plano al navegador directamente.
    return "Bienvenido a la página principal"

# BLOQUE 2: Página de Contacto (Renderiza HTML)
@app.route("/contacto")
def seccion_contacto():
    # Busca el archivo 'contacto.html' dentro de la carpeta /templates.
    return render_template("contacto.html")

# BLOQUE 3: Página de Servicios
@app.route("/servicios")
def cualquier_nombre_aca():
    # El nombre de la función es libre, pero la ruta y el archivo mandan.
    return render_template("servicios.html")

# BLOQUE 4: Página Sobre Nosotros
@app.route("/nosotros")
def nosotros_info():
    # Importante: El archivo nosotros.html debe existir físicamente.
    return render_template("nosotros.html")

if __name__ == "__main__":
    app.run(debug=True)

```


**Recordár:** que en Flask, la "magia" sucede cuando el nombre que ponés dentro de `render_template("nombre.html")` coincide letra por letra con el archivo que creaste dentro de la carpeta `templates`.

