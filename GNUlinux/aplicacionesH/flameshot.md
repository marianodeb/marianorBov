

## Flameshot

1. **1. Instalar Flameshot:** Instalación mediante la terminal.

Abre una terminal y ejecuta el siguiente comando:

```bash
sudo apt update && sudo apt install flameshot -y
```

*Verificación:* Ejecuta `flameshot --version` en la terminal. Debe devolver la versión instalada sin errores.


2. **2. Abrir la configuración del teclado:** Menú de XFCE.

1. Haz clic en el **Menú de aplicaciones** de XFCE.
2. Ve a **Configuración** $\rightarrow$ **Teclado**.
3. Selecciona la pestaña **Atajos de aplicación**.


3. **3. Eliminar el capturador por defecto:** Evitar conflictos de teclas.

1. Busca en la lista el comando asignado a la tecla `Print` (suele ser `xfce4-screenshooter`).
2. Selecciónalo y haz clic en el botón **Eliminar**.


4. **4. Crear el atajo para Flameshot:** Asignación del comando GUI.

1. Haz clic en el botón **Añadir**.
2. En el campo de comando escribe exactamente:

```bash
flameshot gui
```

3. Haz clic en **Aceptar**.
4. Presiona la tecla **Impr Pant** (`Print Screen`) para asignarla.

*Verificación:* Presiona la tecla **Impr Pant**. La pantalla debe oscurecerse e iniciar la interfaz de captura de Flameshot.


5. **5. Configurar inicio en segundo plano:** Inicio automático con el sistema.

1. Ve a **Menú de aplicaciones** $\rightarrow$ **Configuración** $\rightarrow$ **Sesión e inicio**.
2. Selecciona la pestaña **Inicio automático de aplicaciones**.
3. Haz clic en **Añadir**.
4. Completa los campos:
* **Nombre:** `Flameshot`
* **Comando:** `flameshot`
5. Haz clic en **Aceptar**.

*Verificación:* Reinicia la sesión. El icono de Flameshot debe aparecer en el área de notificación (bandeja del sistema).
