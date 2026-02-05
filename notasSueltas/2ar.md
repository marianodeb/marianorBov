El archivo **/etc/fstab** (del inglés, *file systems table*) es un archivo de configuración en sistemas operativos tipo Unix, como Linux, que contiene información sobre todos los sistemas de archivos disponibles en el sistema.
Su función principal es definir cómo y dónde se deben montar automáticamente las particiones, discos duros, y otras unidades de almacenamiento durante el arranque del sistema.

-----

### Estructura y Sintaxis de fstab

Cada línea en el archivo `fstab` representa un sistema de archivos que se va a montar y consta de seis campos obligatorios, separados por espacios o tabulaciones.

```
<dispositivo>  <punto_montaje>  <tipo_fs>  <opciones>  <dump>  <pass>
```

1.  **`<dispositivo>`**: La partición o el dispositivo a montar. Es mejor usar el **UUID** (identificador único universal) o la **etiqueta (LABEL)** en lugar del nombre del dispositivo (`/dev/sda1`), ya que estos no cambian si se añaden o quitan discos.
2.  **`<punto_montaje>`**: El directorio donde se montará el sistema de archivos. Este directorio debe existir antes de que se monte la unidad.
3.  **`<tipo_fs>`**: El tipo de sistema de archivos (ej. `ext4`, `xfs`, `ntfs`, `vfat`, `swap`).
4.  **`<opciones>`**: Opciones de montaje, separadas por comas.
      * `defaults`: un conjunto de opciones predeterminadas (`rw`, `suid`, `dev`, `exec`, `auto`, `nouser`, `async`).
      * `auto`: el sistema de archivos se monta automáticamente en el arranque.
      * `noauto`: no se monta automáticamente, solo manualmente con `mount -a`.
      * `ro`: solo lectura.
      * `rw`: lectura y escritura.
      * `sync`: Todas las operaciones de E/S se realizan de forma sincrónica.
      * `async`: Todas las operaciones de E/S se realizan de forma asíncrona.
      * `user`: permite a los usuarios normales montar la unidad.
      * `nouser`: Solo el `root` puede montar el sistema de archivos.
      * `nofail`: ignora errores si el dispositivo no se encuentra, permitiendo que el sistema arranque.
5.  **`<dump>`**: Usado por el comando `dump` para copias de seguridad. `0` significa que no se debe hacer una copia de seguridad.
6.  **`<pass>`**: El orden en que el programa `fsck` comprueba si hay errores en el sistema de archivos al arrancar. `0` significa que no se comprueba. `1` es para la partición raíz (`/`), y `2` para el resto.

-----

### Cómo Configurar una Unidad Nueva

Para añadir una unidad de forma permanente, sigue estos pasos:

1.  **Identifica la unidad**: Usa el comando `lsblk` o `fdisk -l` para ver la lista de dispositivos de bloque y sus particiones.
2.  **Formatea la unidad**: Si es nueva, crea un sistema de archivos. Por ejemplo, para crear una partición `ext4` en `/dev/sdb1`:

```bash
    sudo mkfs.ext4 /dev/sdb1
```

3.  **Obtén el UUID**: Usa el comando `sudo blkid` para obtener el UUID de la nueva partición.
El UUID es la forma más fiable de identificar una partición en `fstab`.

```bash
    sudo blkid /dev/sdb1
    # Ejemplo: UUID="a1b2c3d4-e5f6-7890-1234-567890abcdef"
```
4.  **Crea el punto de montaje**: Crea un directorio donde se montará la unidad, si no existe.

```bash
    sudo mkdir /mnt/datos
```
5.  **Edita el archivo fstab**: Abre `/etc/fstab` con un editor de texto (como `nano` o `vim`). Se recomienda hacer una copia de seguridad antes.

```bash
    sudo cp /etc/fstab /etc/fstab.bak
    sudo nano /etc/fstab
```

6.  **Añade la nueva línea**: Agrega la información de la nueva unidad al final del archivo.

```
    UUID=a1b2c3d4-e5f6-7890-1234-567890abcdef  /mnt/datos  ext4  defaults,nofail  0  2
```

Ejemplo 2:

  * Añade una nueva línea al final del archivo con la información de tu partición:

```
    # Nueva unidad de datos
    UUID=a1b2c3d4-e5f6-7890-1234-567890abcdef  /mnt/datos  ext4  defaults  0  2
```

    Reemplaza el UUID con el que obtuviste.
      * **UUID**: Identificador único de la partición.
      * **Punto de montaje**: `/mnt/datos`.
      * **Tipo de FS**: `ext4`.
      * **Opciones**: `defaults` (lectura/escritura, etc.).
      * **Dump**: `0` (no hacer backup).
      * **Pass**: `2` (revisar en segundo lugar).

7.  **Verifica la configuración**: Guarda el archivo y ejecuta `sudo mount -a`. Si no hay errores, la configuración es correcta y la unidad se montará en cada reinicio.
Si el comando no muestra errores, la partición se ha montado correctamente. Puedes verificarlo con `df -h`.


### Qué Se Puede y Qué No Se Puede Hacer

#### ✅ Qué Se Puede Hacer

  * **Montaje automático**: Configurar unidades de disco internas, externas, particiones, unidades de red (NFS, SMB) y sistemas de archivos virtuales para que se monten al inicio.
  * **Personalización**: Definir opciones específicas de montaje, como permisos, modo de solo lectura o lectura/escritura, y la forma en que el sistema maneja errores de montaje.
  * **Robustez**: Usar el UUID de las particiones en lugar de los nombres de dispositivos (ej. `/dev/sda1`) para asegurar que el montaje sea correcto incluso si el orden de los discos cambia. La opción `nofail` es ideal para unidades extraíbles.

#### ❌ Qué No Se Puede Hacer

  * **Errores de sintaxis**: Un error en `fstab`, especialmente en la línea de la partición raíz (`/`), puede impedir que el sistema arranque. Por ello, siempre se debe hacer una copia de seguridad.
  * **Eliminar o modificar sin cuidado**: Borrar o alterar una línea de `fstab` sin saber su propósito puede causar inestabilidad o fallos en el sistema.
  * **Uso de nombres de dispositivos**: Depender de `/dev/sda1` u otros nombres de dispositivos es una mala práctica, ya que estos pueden cambiar. El **UUID** es la forma segura y profesional.
