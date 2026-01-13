
## Entorno virtual

#### Pasos para crear un entorno virtual en Debian:

##### Instalar el paquete python3-venv:

Este paquete proporciona el módulo venv que es esencial para crear entornos virtuales. Abre una terminal y ejecuta el siguiente comando:

```Bash
sudo apt install python3-venv
```

##### Crear un directorio para el proyecto:

Crea un nuevo directorio donde deseas ubicar tu proyecto. Por ejemplo:

```Bash
mkdir mi_proyecto
cd mi_proyecto
```

##### Crear el entorno virtual:

Dentro del directorio de tu proyecto, ejecuta el siguiente comando para crear un entorno virtual llamado venv:

```Bash
python3 -m venv venv
```

El nombre venv es solo una convención. Puedes elegir cualquier nombre que desees ejemplo:

```Bash
python3 -m venv miproyecto_venv
```

Esto creará un subdirectorio llamado venv que contendrá el entorno virtual.

##### Activar el entorno virtual:

Para comenzar a utilizar el entorno virtual, debes activarlo. La forma de activarlo depende de tu shell. En Bash, por ejemplo, usarías:

```Bash
source venv/bin/activate
```

Verás que el nombre de tu terminal cambia para indicar que estás dentro del entorno virtual.

##### Instalar paquetes:

Una vez activado el entorno virtual, puedes instalar los paquetes que necesita tu proyecto usando pip:

```Bash
pip install numpy pandas matplotlib
```

##### Desactivar el entorno virtual:

Cuando termines de trabajar en el proyecto, puedes desactivar el entorno virtual con el comando:

```Bash
deactivate
```

##### Ejemplo completo:

```Bash
# Crear un directorio para el proyecto
mkdir mi_proyecto_web
cd mi_proyecto_web

# Crear el entorno virtual
python3 -m venv venv

# Activar el entorno virtual
source venv/bin/activate

# Instalar Flask
pip install Flask

# Crear un archivo app.py
nano app.py
```

##### Contenido de app.py:

```Python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return '¡Hola desde mi entorno virtual!'

if __name__ == '__main__':
    app.run(debug=True)
```

Ejecutar la aplicación:

```Bash
python app.py
```

Consideraciones adicionales:

**Ubicación del entorno virtual:** Puedes crear el entorno virtual en cualquier lugar, pero es recomendable hacerlo dentro del directorio del proyecto para mantener una mejor organización.
**Nombre del entorno virtual:** El nombre venv es solo una convención. Puedes elegir cualquier nombre que desees.
**Gestión de múltiples entornos virtuales:** Si tienes varios proyectos, puedes crear un entorno virtual para cada uno.
**Herramientas para gestionar entornos virtuales:** Existen herramientas como virtualenvwrapper que facilitan la creación y gestión de múltiples entornos virtuales.

En resumen:

Crear entornos virtuales en Debian es una práctica recomendada para organizar tus proyectos de Python. Al seguir estos pasos, podrás aislar las dependencias de cada proyecto y evitar conflictos entre ellos.

---

## Creando requirements.txt

1. **Instalar los paquetes necesarios:**

```Bash
pip install numpy pandas matplotlib
```

2. **Generar el archivo:**

```Bash
pip freeze > requirements.txt
```

Este comando crea un archivo requirements.txt en el directorio actual, listando todos los paquetes instalados en el entorno virtual activo.

**Editando requirements.txt**

Puedes editar manualmente el archivo requirements.txt para:

    Especificar versiones exactas: numpy==1.23.5
    Indicar un rango de versiones: pandas>=1.4.0
    Añadir comentarios: # Paquetes para visualización

**Instalando desde requirements.txt**

1. **Crear un nuevo entorno virtual (si es necesario):**

```Bash
python3 -m venv my_env
source my_env/bin/activate
```

2. **Instalar las dependencias:**

```Bash
pip install -r requirements.txt
```

**Ejemplos de requisitos.txt**
```
numpy==1.23.5
pandas>=1.4.0
matplotlib
scikit-learn
```

Buenas prácticas

    Mantenerlo actualizado: Actualiza el archivo requirements.txt cada vez que añadas o elimines paquetes.
    Utilizar un gestor de versiones: Guarda el archivo requirements.txt en tu sistema de control de versiones (Git, Mercurial, etc.) para rastrear los cambios.
    Considerar herramientas de gestión de dependencias: Herramientas como pipenv y poetry ofrecen funcionalidades adicionales para gestionar entornos virtuales y dependencias de forma más eficiente.

**Ejemplo completo**

```Bash

# Crear un nuevo proyecto
mkdir my_project
cd my_project

# Crear un entorno virtual
python3 -m venv my_env
source my_env/bin/activate

# Instalar paquetes
pip install numpy pandas matplotlib

# Generar requirements.txt
pip freeze > requirements.txt

# Editar requirements.txt (si es necesario)

# Desactivar el entorno virtual
deactivate

# Clonar el proyecto en otro equipo
git clone https://github.com/tu_usuario/my_project.git

# Crear un nuevo entorno virtual y activarlo
# ...

# Instalar las dependencias desde requirements.txt
pip install -r requirements.txt
```

En resumen

El archivo requirements.txt es una herramienta esencial para gestionar las dependencias de tus proyectos Python, garantizando su reproducibilidad y facilitando la colaboración. Al seguir estas pautas, podrás crear y mantener proyectos Python de forma más eficiente y organizada.

---

Comandos básicos de pip

    Instalar un paquete:

```bash
pip install numpy
```

Desinstalar un paquete:

```Bash
pip uninstall numpy
```

Elimina el paquete numpy de tu entorno.

Listar los paquetes instalados:

```Bash
pip list
```

Muestra una lista de todos los paquetes instalados en tu entorno actual.

```Bash
pip freeze
```

Similar a pip list, pero muestra los paquetes en un formato que puede ser usado para recrear el entorno (por ejemplo, para crear un archivo requirements.txt).

Buscar un paquete:

```Bash
pip search pandas
```

Busca el paquete pandas en el índice de paquetes de Python (PyPI).

Mostrar información sobre un paquete:

```Bash
    pip show numpy
```

Muestra detalles sobre el paquete numpy, como la versión instalada, la ubicación, etc.

Comandos avanzados de pip

Instalar desde un archivo requirements.txt:

```Bash
pip install -r requirements.txt
```

Instala todos los paquetes listados en el archivo requirements.txt.
Actualizar un paquete:

```Bash
pip install --upgrade numpy
```

Actualiza el paquete numpy a la última versión disponible.
Instalar una versión específica:

```Bash
pip install numpy==1.23.5
```

Instala la versión 1.23.5 del paquete numpy.
Instalar desde una URL:

```Bash
pip install https://github.com/user/package/archive/main.zip
```

Instala un paquete desde un archivo ZIP descargado de una URL.
Instalar en modo editable (para desarrollo):

```Bash
    pip install -e .
```

Instala el paquete actual (en el directorio actual) en modo editable, lo que es útil para el desarrollo.

Otros comandos útiles

Descargar un paquete sin instalarlo:

```Bash
pip download numpy
```

Verificar la instalación de los paquetes:

```Bash
pip check
```

Limpiar la caché de pip:

```Bash
pip cache purge
```

Mostrar la versión de pip:

```Bash
    pip --version
```

Creando un archivo requirements.txt

El archivo requirements.txt es esencial para compartir y reproducir entornos de desarrollo. Para crearlo, simplemente ejecuta:

```Bash
pip freeze > requirements.txt
```
Visualización de un entorno virtual

Esta imagen muestra la estructura típica de un entorno virtual creado con venv y dónde se encuentra el archivo requirements.txt.

![[Structure-of-a-virtual-environment-on-the-basis-of-two-key-elements-system-requirements.jpg]]

Pip ofrece muchas más opciones y comandos. Para obtener una lista completa, ejecuta:

```Bash
pip --help
```
Nota: Es recomendable utilizar entornos virtuales para aislar las dependencias de cada proyecto. Esto te permitirá tener diferentes versiones de paquetes instalados sin generar conflictos.

