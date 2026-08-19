## 1. Cómo instalar FFmpeg en Debian

Al estar en Debian, FFmpeg ya se encuentra en los repositorios oficiales. Abre tu terminal y ejecuta los siguientes comandos:

```bash
sudo apt update
sudo apt install ffmpeg

```

Para verificar que se instaló correctamente, puedes revisar su versión con:

```bash
ffmpeg -version

```

## 2. Lo básico: Pasar de Video a Audio (Extraer MP3 o WAV)

Si tienes un video (por ejemplo, en `.mp4` o `.mkv`) y solo quieres quedarte con el sonido en un archivo `.mp3`:

```bash
ffmpeg -i video_original.mp4 -vn -acodec libmp3lame -q:a 2 archivo_audio.mp3

```

### ¿Qué significa cada parte del comando?

* **`-i video_original.mp4`**: Es el archivo de **i**nput (entrada).
* **`-vn`**: Le dice a FFmpeg: "**v**ideo **n**o" (ignora la pista de video).
* **`-acodec libmp3lame`**: El codec que usará para comprimir el audio en MP3.
* **`-q:a 2`**: Calidad del audio (VBR). El `2` es una calidad excelente (equivalente a unos 192-256 kbps). Si quieres máxima calidad fija (320 kbps), puedes cambiarlo por `-b:a 320k`.

Si quieres **mantener el audio original** sin perder nada de calidad (por ejemplo, si el video ya tiene audio AAC y lo quieres en `.m4a`), puedes usar `copy` para que sea instantáneo:

```bash
ffmpeg -i video.mp4 -vn -acodec copy audio.m4a

```

## 3. Cambiar formatos de Video y Audio

FFmpeg es tan inteligente que la mayoría de las veces **entiende lo que quieres hacer solo con leer la extensión** del archivo de salida.

### Cambiar de un formato de video a otro (ej. de MKV a MP4)

Si no quieres complicarte y quieres que FFmpeg elija los mejores parámetros automáticamente:

```bash
ffmpeg -i video.mkv video_nuevo.mp4

```

Si quieres cambiar el formato **sin volver a codificar** (lo que tarda apenas 2 segundos porque solo cambia el "contenedor"):

```bash
ffmpeg -i video.mkv -c:v copy -c:a copy video_nuevo.mp4

```

> ⚠️ *Nota: Esto último solo funciona si los codecs internos del MKV ya son compatibles con MP4 (como H.264 y AAC).*

### Cambiar de un formato de audio a otro (ej. de WAV a MP3)

```bash
ffmpeg -i audio.wav -acodec libmp3lame -b:a 256k audio.mp3

```

## 4. Cómo convertir videos para enviar por WhatsApp

WhatsApp tiene dos límites molestos: el **tamaño del archivo** (generalmente hasta 64 MB para videos normales, o hasta 2 GB si se envía como documento) y el **formato** (prefiere estrictamente **MP4 con video H.264 y audio AAC**).

Si tienes un video enorme o en un formato raro y quieres asegurarte de que WhatsApp lo acepte y lo reproduzca directamente, usa este comando:

```bash
ffmpeg -i video_pesado.mkv -vcodec libx264 -crf 23 -acodec aac -b:a 128k -pix_fmt yuv420p video_para_whatsapp.mp4

```

### Explicación de los "trucos" para WhatsApp:

* **`-vcodec libx264`**: Convierte el video al formato H.264, que es el más compatible del planeta (lo lee cualquier celular).
* **`-crf 23`**: Controla la calidad del video. El rango va de 0 a 51. Un número entre `20` y `24` mantiene una calidad excelente achicando muchísimo el peso del archivo. Si el video sigue pesando mucho, sube este número a `28` o `30`.
* **`-acodec aac -b:a 128k`**: Convierte el audio a AAC a 128 kbps (el estándar que pide WhatsApp).
* **`-pix_fmt yuv420p`**: **Esto es vital.** Muchos reproductores de celulares no pueden leer videos si no están en este formato de color específico.

### 💡 Un tip extra para la terminal
