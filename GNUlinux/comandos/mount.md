¡Claro! Aquí tienes toda la información organizada sobre el comando `mount`, con opciones y ejemplos detallados.

## Comando `mount`

El comando `mount` se usa para montar sistemas de archivos en el árbol de directorios del sistema.

### Sintaxis Básica
```bash
mount [opciones] dispositivo punto_de_montaje
```

- **dispositivo**: La ubicación del dispositivo o archivo de sistema de archivos (ej. `/dev/sda1`, `/path/to/image.iso`).
- **punto_de_montaje**: El directorio donde se montará el sistema de archivos (ej. `/mnt/mi_disco`).

### Opciones y Ejemplos

#### 1. **Especificar el Tipo de Sistema de Archivos**
- **`-t tipo`**: Especifica el tipo de sistema de archivos.
  ```bash
  mount -t ext4 /dev/sda1 /mnt/mi_disco
  ```

#### 2. **Especificar Opciones de Montaje**
- **`-o opciones`**: Permite especificar opciones adicionales como:
  - **`rw`**: Modo lectura-escritura (por defecto).
  - **`ro`**: Modo solo lectura.
  - **`noexec`**: No ejecutar archivos.
  - **`nodev`**: No interpretar dispositivos especiales.
  - **`nosuid`**: Ignorar bits de setuid y setgid.
  - **`async`**: Operaciones de escritura asíncronas.
  - **`sync`**: Operaciones de escritura sincrónicas.
  ```bash
  mount -o ro,noexec /dev/sda1 /mnt/mi_disco
  ```

#### 3. **Montar en Modo Solo Lectura**
- **`-r`**: Montar el sistema de archivos en modo solo lectura.
  ```bash
  mount -r /dev/sda1 /mnt/mi_disco
  ```

#### 4. **Montar Todos los Sistemas de Archivos Listados en `/etc/fstab`**
- **`-a`**: Montar todos los sistemas de archivos especificados en el archivo `/etc/fstab`.
  ```bash
  mount -a
  ```

#### 5. **Simular el Montaje**
- **`-f`**: Solo simular el montaje sin hacer cambios reales.
  ```bash
  mount -f /dev/sda1 /mnt/test
  ```

#### 6. **No Actualizar el Archivo `/etc/mtab`**
- **`-n`**: No actualizar el archivo `/etc/mtab`, que mantiene un registro de los sistemas de archivos montados.
  ```bash
  mount -n /dev/sda1 /mnt/mi_disco
  ```

#### 7. **Mostrar Información Detallada**
- **`-v`**: Muestra información detallada durante el montaje (modo verbose).
  ```bash
  mount -v /dev/sda1 /mnt/mi_disco
  ```

#### 8. **Montar un Directorio en Otro Lugar en el Sistema de Archivos**
- **`--bind`**: Monta un directorio en otro lugar.
  ```bash
  mount --bind /home/usuario/documentos /mnt/documentos
  ```

#### 9. **Cambiar el Tipo de Montaje a `shared`**
- **`--make-shared`**: Cambia el punto de montaje para que sea compartido.
  ```bash
  mount --make-shared /mnt/mi_disco
  ```

#### 10. **Cambiar el Tipo de Montaje a `slave`**
- **`--make-slave`**: Cambia el punto de montaje para que sea esclavo.
  ```bash
  mount --make-slave /mnt/mi_disco
  ```

#### 11. **Cambiar el Tipo de Montaje a `private`**
- **`--make-private`**: Cambia el punto de montaje para que sea privado.
  ```bash
  mount --make-private /mnt/mi_disco
  ```

#### 12. **Cambiar el Tipo de Montaje a `unbindable`**
- **`--make-unbindable`**: Cambia el punto de montaje para que sea inbindeable.
  ```bash
  mount --make-unbindable /mnt/mi_disco
  ```

#### 13. **Montar un Archivo de Imagen**
- **`-o loop`**: Monta un archivo como si fuera un dispositivo de bloque.
  ```bash
  mount -o loop archivo.img /mnt/imagen
  ```

#### 14. **Especificar UID y GID para Permisos**
- **`-o uid=UID,gid=GID`**: Establece el UID y GID para la propiedad de archivos (útil para sistemas de archivos FAT o NTFS).
  ```bash
  mount -o uid=1000,gid=1000 /dev/sda1 /mnt/mi_disco
  ```

#### 15. **Establecer Máscara de Permisos**
- **`-o umask`**: Define una máscara de permisos para archivos y directorios.
  ```bash
  mount -o umask=0022 /dev/sda1 /mnt/mi_disco
  ```

#### 16. **Máscaras de Permisos para Directorios y Archivos**
- **`-o dmask`**, **`-o fmask`**: Define máscaras de permisos para directorios y archivos respectivamente (específicos para sistemas de archivos FAT).
  ```bash
  mount -o dmask=0022,fmask=0022 /dev/sda1 /mnt/mi_disco
  ```

### Desmontar un Sistema de Archivos

Para desmontar un sistema de archivos, utiliza el comando `umount`:

```bash
umount /mnt/mi_disco
```

Espero que esta organización te ayude a entender mejor el comando `mount` y sus opciones. Si tienes más preguntas o necesitas más detalles, no dudes en preguntar.