Acá tenés la guía definitiva y corregida, adaptada exactamente a lo que aprendimos y resolvimos sobre tu sistema Debian (con la configuración de permisos correcta, usuario `mariano`, y todos los comandos explicados línea por línea) para que la copies directamente a **Obsidian**.


# Guía: Servidor Multimedia DLNA con MiniDLNA (ReadyMedia) en Debian



## 📌 Resumen General y Funcionamiento

- **¿Qué es DLNA/UPnP?**: Es un protocolo de red local que permite compartir archivos de audio, video e imágenes con otros dispositivos de la red (TVs, consolas, celulares, otras PCs) sin necesidad de usar un pendrive USB.
- **¿Por qué MiniDLNA?**: Es un servidor extremadamente liviano que no transcodifica video. 
  - **Uso de RAM**: ~5 a 15 MB.
  - **Uso de CPU**: Prácticamente 0% (el trabajo de procesamiento lo hace la pantalla que reproduce).
- **Consumo e impacto**: No afecta el rendimiento de la PC y se puede dejar funcionando en segundo plano 24/7.



## 🛠️ Paso 1: Instalación del paquete en Debian

Abre la terminal de Debian e instala el servidor desde los repositorios oficiales:

```bash
sudo apt update
sudo apt install minidlna -y

```


## ⚙️ Paso 2: Configuración de rutas y nombres (`/etc/minidlna.conf`)

Abre el archivo de configuración con un editor de texto de terminal:

```bash
sudo nano /etc/minidlna.conf

```

### Líneas clave modificadas dentro del archivo:

```
# Deshabilitar la ruta de ejemplo por defecto
#media_dir=/var/lib/minidlna

# Ruta de tus carpetas (la 'V,' le aclara a MiniDLNA que SOLO busque Videos para acelerar el escaneo)
media_dir=V,/home/mariano/Descargas/SERIES/

# Nombre visible del servidor en la TV o dispositivos conectados
friendly_name=Debian Media Server

# Detección automática de nuevos archivos agregados a la carpeta
inotify=yes

```


## 🔐 Paso 3: Solución de Permisos de Sistema (Paso Crítico)

Para evitar que el servidor muestre `Video files: 0` debido a las restricciones de carpetas personales en Debian, configuramos el servicio para que corra con tu propio usuario (`mariano`):

```bash
# 1. Cambia el usuario que ejecuta el servicio en la configuración del sistema
sudo sed -i 's/USER="minidlna"/USER="mariano"/' /etc/default/minidlna

# 2. Le da la propiedad al usuario mariano de los directorios de trabajo de MiniDLNA
sudo chown -R mariano:mariano /var/lib/minidlna /var/log/minidlna

# 3. Otorga permisos de ejecución en tu carpeta de usuario para que el servicio pueda navegar hasta las series
chmod o+x /home/mariano
chmod o+x /home/mariano/Descargas
chmod -R a+r /home/mariano/Descargas/SERIES

```

### Explicación de los comandos:

* `sed -i ...`: Modifica dentro de `/etc/default/minidlna` la variable `USER` reemplazando el usuario predeterminado por `mariano`.
* `chown -R ...`: Asigna a `mariano` como dueño de las bases de datos y registros del programa.
* `chmod o+x ...`: Le da permisos a otros procesos para "atravesar" las carpetas superiores y llegar hasta `SERIES`.
* `chmod -R a+r ...`: Asegura que todos los archivos de video tengan permiso de lectura.



## 🚀 Paso 4: Iniciar, Reindexar y Gestionar el Servicio

Cada vez que agregues muchos videos nuevos o hagas cambios estructurales, forzá un reescaneo:

```bash
# Reiniciar el servicio
sudo systemctl restart minidlna

# Forzar una reconstrucción completa de la base de datos de videos
sudo minidlnad -R
sudo systemctl restart minidlna

# Habilitar para que inicie automáticamente al encender la PC
sudo systemctl enable minidlna

```


## 🔍 Paso 5: Panel de Monitoreo y Verificación

Puedes verificar que el servidor esté detectando tus videos abriendo el navegador web en tu PC e ingresando a:

👉 **`http://localhost:8200/`** (o con tu IP local: `http://192.168.0.31:8200/`)

### ¿Qué verificar?

* **Video files**: Debe mostrar una cifra mayor a `0` (ejemplo: `124`). Si muestra `0`, hay un problema de permisos o de ruta.
* **Connected clients**: Muestra la lista de TVs, celulares o PCs conectados en ese momento.

---

## 📺 Paso 6: Cómo Conectar y Ver en Cada Dispositivo

### 1. En Smart TV compatibles (Con soporte DLNA/Red):

* No requiere instalar apps.
* Abrí la app integrada de la tele para ver fotos/videos (llamada habitualmente **Media**, **Archivos** o desde el botón **Source/Entradas**).
* Seleccioná la fuente de red llamada **"Debian Media Server"**.

### 2. En el Celular (Android / iOS):

* Descargá la app gratuita **VLC** desde la tienda.
* Conéctate al Wi-Fi de tu casa.
* Entrá a la pestaña **Red** (Local Network) en VLC y tocá sobre el servidor Debian.

### 3. Desde otra PC (Windows / Linux / Mac):

* **Con VLC:** Abrí VLC -> Pestaña **Red Local** -> **UPnP** -> Entrar al servidor.
* **En Windows:** Abrí el *Explorador de Archivos* -> Sección *Red* -> *Dispositivos Multimedia*.

---

## ⚠️ Aspectos de Seguridad y Limitaciones

1. **Seguridad Privada:** MiniDLNA **solo funciona dentro de tu red local (Wi-Fi/LAN)**. Nadie desde Internet puede acceder a tus archivos ni a tu PC.
2. **Acceso de Solo Lectura:** Las TVs y dispositivos solo pueden **leer y reproducir**; no tienen permisos para borrar, renombrar ni modificar el disco de tu PC.
3. **Subtítulos (.srt):** Para que la TV los reconozca automáticamente, el archivo de video y el subtítulo deben estar en la misma carpeta y llamarse exactamente igual (Ejemplo: `capitulo1.mkv` y `capitulo1.srt`).
4. **TVs sin soporte DLNA:** Si una TV solo reconoce pendrives físicos por USB, requerirá un dispositivo externo conectado por HDMI (tipo *Fire TV Stick*, *Chromecast con Google TV* o *Roku*) con la app VLC o Jellyfin instalada.



