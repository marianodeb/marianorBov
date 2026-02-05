

## Instalación Manual de Oh My Posh

### 1\. Preparación y Descarga de Archivos

Este bloque se encarga de descargar el ejecutable de Oh My Posh y todos los temas (configuraciones JSON) desde GitHub.

```bash
# 1. Instalar dependencias básicas si no existen (wget y unzip)
sudo apt update
sudo apt install -y wget unzip

# 2. Crear las carpetas de destino en tu directorio HOME
mkdir -p $HOME/.oh-my-posh/bin
mkdir -p $HOME/.oh-my-posh/themes

# 3. Descargar el binario (ejecutable) principal para Linux 64-bit
# La opción -O guarda el archivo con el nombre especificado
wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O $HOME/.oh-my-posh/bin/oh-my-posh

# 4. Descargar el archivo ZIP con todos los temas de configuración
wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/themes.zip -O $HOME/.oh-my-posh/themes/themes.zip

# 5. Descomprimir los temas en la carpeta de destino
unzip $HOME/.oh-my-posh/themes/themes.zip -d $HOME/.oh-my-posh/themes/

# 6. Dar permiso de ejecución al binario de Oh My Posh
chmod +x $HOME/.oh-my-posh/bin/oh-my-posh
```

### 2\. Configuración del Archivo `.bashrc`

Este bloque le indica a Bash dónde encontrar el ejecutable (`PATH`) y cómo usarlo para dibujar el *prompt* (`eval`).

1.  **Abre** tu archivo de configuración de Bash:

    ```bash
    nano ~/.bashrc
    ```

2.  **Busca y comenta (o elimina)** cualquier línea que defina tu *prompt* anterior (cualquier línea que comience con `PS1=`).

3.  **Agrega las siguientes líneas al FINAL del archivo** (y asegúrate de que Fastfetch/Neofetch vaya después de OMP si lo usas):

    ```bash
    # ----------------------------------------------------
    # CONFIGURACION OH MY POSH
    # ----------------------------------------------------
    # 1. Agrega el directorio de Oh My Posh al PATH para que Bash lo encuentre
    export PATH="$PATH:$HOME/.oh-my-posh/bin"

    # 2. Inicializa el prompt con el tema Gruvbox (el que te funcionó)
    # Si quieres cambiar el tema, reemplaza 'gruvbox.omp.json' por otro nombre.
    eval "$(oh-my-posh init bash --config $HOME/.oh-my-posh/themes/gruvbox.omp.json)"

    # ----------------------------------------------------
    # (Opcional) FASTFETCH - Asegúrate de que se ejecute después de OMP
    # ----------------------------------------------------
    # fastfetch
    ```

4.  **Guarda** y **cierra** el archivo (`Ctrl+S`, luego `Ctrl+X` en `nano`).

### 3\. Aplicar los Cambios

Para que los cambios surtan efecto en tu terminal actual (sin reiniciarla):

```bash
source ~/.bashrc
```



