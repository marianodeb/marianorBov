

## Variable de entorno **LS_COLORS**

Los colores que ves al usar ls dependen de la variable de entorno LS_COLORS, que define cómo se resaltan archivos y directorios según su tipo o permisos.

**¿Por qué se ve el fondo en `ls`?**

- **Permisos 777**: En sistemas FAT32/exFAT (pendrives), los directorios tienen permisos `drwxrwxrwx`, lo que los marca como "otros escriturables" (`ow`).  
- **Formato de color en `LS_COLORS`**: El código `ow=34;42` asigna **texto azul (34)** y **fondo verde (42)**.  

**Soluciones aplicadas**:

1. **Modificar `ow` para quitar el fondo**:

Modificacion que solo sera util para la sesion actual. Una vez se cierre volvera a la normalidad

```bash
export LS_COLORS="${LS_COLORS/ow=34;42/ow=34}"  # Texto azul sin fondo
```

Modificacion que sera para todas las sesiones

```bash
echo 'export LS_COLORS="${LS_COLORS/ow=34;42/ow=34}"' >> ~/.bashrc
source ~/.bashrc
```

2. **Configuración permanente**:

Añadir el comando anterior a `~/.bashrc` o usar `dircolors`.  

---

### **Tabla de códigos de `LS_COLORS`**
 
Cada entrada sigue el formato `[tipo]=[estilo];[texto];[fondo]`.

| Código | Tipo/Descripción                     | Color/Estilo                    |  
|--------|--------------------------------------|---------------------------------|  
| `rs=0` | Resetear colores                     | Sin estilo (0)                  |  
| `di=01;34` | Directorio normal                | **Texto azul brillante** (01;34)|  
| `ln=01;36` | Enlace simbólico                 | Texto cyan brillante (01;36)    |  
| `mh=00`    | Enlace físico (hardlink)         | Sin estilo (00)                 |  
| `pi=40;33` | Named pipe (FIFO)                | **Fondo negro** (40), texto amarillo (33)|  
| `so=01;35` | Socket                           | Texto magenta brillante (01;35)|  
| `do=01;35` | Door (sistemas Solaris)          | Igual que `so`                  |  
| `bd=40;33;01` | Bloque device               | Fondo negro (40), texto amarillo brillante (33;01)|  
| `cd=40;33;01` | Character device             | Igual que `bd`                  |  
| `or=40;31;01` | Enlace roto                   | Fondo negro (40), texto rojo brillante (31;01)|  
| `mi=00`    | Archivo perdido (missing)        | Sin estilo                      |  
| `su=37;41` | Archivo con SUID                 | Texto blanco (37), fondo rojo (41)|  
| `sg=30;43` | Archivo con SGID                 | Texto negro (30), fondo amarillo (43)|  
| `ca=00`    | Archivo con capacidades          | Sin estilo                      |  
| `tw=30;42` | Sticky + otros escriturables     | Texto negro (30), fondo verde (42)|  
| `ow=34;42` | **Directorio otros escriturables** | Texto azul (34), fondo verde (42) |  
| `st=37;44` | Sticky directory                 | Texto blanco (37), fondo azul (44)|  
| `ex=01;32` | Archivo ejecutable               | Texto verde brillante (01;32)   |  

---

### **Códigos de colores ANSI**

| Código | Texto          | Fondo          | Estilo         |  
|--------|----------------|----------------|----------------|  
| **30** | Negro          | **40**         |                |  
| **31** | Rojo           | **41**         | **00** (normal)|  
| **32** | Verde          | **42**         | **01** (bold)  |  
| **33** | Amarillo       | **43**         | **04** (subrayado)|  
| **34** | Azul           | **44**         | **05** (parpadeo)|  
| **35** | Magenta        | **45**         | **07** (inverso)|  
| **36** | Cyan           | **46**         | **08** (oculto)|  
| **37** | Blanco         | **47**         |                |  

**Ejemplo**:

- `34;42` → Texto azul (`34`) + fondo verde (`42`).  
- `01;32` → Texto verde brillante (`01` + `32`).  

**Nota**: Los códigos como `*.tar=01;31` definen colores para extensiones específicas (ej: archivos `.tar` en rojo brillante).

---

### **Tabla Completa de `LS_COLORS`**  

Basada en tu variable proporcionada:

| **Código**          | **Tipo/Extensión**                          | **Color/Estilo**                                  |  
|----------------------|--------------------------------------------|---------------------------------------------------|  
| **`rs=0`**           | Resetear colores                           | Sin estilo (`0`)                                  |  
| **`di=01;34`**       | Directorio                                 | Texto azul brillante (`01;34`)                    |  
| **`ln=01;36`**       | Enlace simbólico                           | Texto cyan brillante (`01;36`)                    |  
| **`mh=00`**          | Enlace físico (hardlink)                   | Sin estilo (`00`)                                 |  
| **`pi=40;33`**       | Named pipe (FIFO)                          | Fondo negro (`40`), texto amarillo (`33`)         |  
| **`so=01;35`**       | Socket                                     | Texto magenta brillante (`01;35`)                 |  
| **`do=01;35`**       | Door (sistemas Solaris)                    | Igual que `so`                                    |  
| **`bd=40;33;01`**    | Bloque device                              | Fondo negro (`40`), texto amarillo brillante (`33;01`)|  
| **`cd=40;33;01`**    | Character device                           | Igual que `bd`                                    |  
| **`or=40;31;01`**    | Enlace roto                                | Fondo negro (`40`), texto rojo brillante (`31;01`)|  
| **`mi=00`**          | Archivo perdido (missing)                  | Sin estilo                                        |  
| **`su=37;41`**       | Archivo con SUID                           | Texto blanco (`37`), fondo rojo (`41`)            |  
| **`sg=30;43`**       | Archivo con SGID                           | Texto negro (`30`), fondo amarillo (`43`)         |  
| **`ca=00`**          | Archivo con capacidades                    | Sin estilo                                        |  
| **`tw=30;42`**       | Sticky + otros escriturables               | Texto negro (`30`), fondo verde (`42`)            |  
| **`ow=34`**          | Directorio "otros escriturables"           | Texto azul (`34`)                                 |  
| **`st=37;44`**       | Sticky directory                           | Texto blanco (`37`), fondo azul (`44`)            |  
| **`ex=01;32`**       | Archivo ejecutable                         | Texto verde brillante (`01;32`)                   |  

---

### **Extensiones de Archivos y sus Colores**

#### **Archivos Comprimidos (rojo brillante `01;31`):**

| **Código**              | **Extensión**       | **Descripción**                                  |  
|-------------------------|---------------------|-------------------------------------------------|  
| **`*.tar=01;31`**       | .tar                | Archivo TAR sin compresión                      |  
| **`*.tgz=01;31`**       | .tgz                | TAR comprimido con GZip                         |  
| **`*.arc=01;31`**       | .arc                | Formato de compresión ARC                       |  
| **`*.arj=01;31`**       | .arj                | Archivo ARJ (menos común)                       |  
| **`*.zip=01;31`**       | .zip                | Archivo ZIP                                     |  
| **`*.bz2=01;31`**       | .bz2                | Comprimido con BZip2                            |  
| **`*.deb=01;31`**       | .deb                | Paquete Debian                                  |  
| **`*.rpm=01;31`**       | .rpm                | Paquete Red Hat                                 |  
| **`*.7z=01;31`**        | .7z                 | Archivo 7-Zip                                   |  


#### **Imágenes (magenta brillante `01;35`):**

| **Código**              | **Extensión**       | **Descripción**                                  |  
|-------------------------|---------------------|-------------------------------------------------|  
| **`*.jpg=01;35`**       | .jpg                | Imagen JPEG                                     |  
| **`*.png=01;35`**       | .png                | Imagen PNG                                      |  
| **`*.gif=01;35`**       | .gif                | Imagen GIF                                      |  
| **`*.svg=01;35`**       | .svg                | Gráfico vectorial SVG                           |  
| **`*.webp=01;35`**      | .webp               | Imagen WebP                                     |  


#### **Multimedia (magenta brillante `01;35`):**

| **Código**              | **Extensión**       | **Descripción**                                  |  
|-------------------------|---------------------|-------------------------------------------------|  
| **`*.mp4=01;35`**       | .mp4                | Video MP4                                       |  
| **`*.avi=01;35`**       | .avi                | Video AVI                                       |  
| **`*.mkv=01;35`**       | .mkv                | Video Matroska                                  |  
| **`*.mp3=00;36`**       | .mp3                | Audio MP3 (cyan normal `00;36`)                 |  
| **`*.flac=00;36`**      | .flac               | Audio FLAC (sin pérdida)                        |  


#### **Archivos Temporales/Backups (gris `00;90`):**

| **Código**              | **Extensión**       | **Descripción**                                  |  
|-------------------------|---------------------|-------------------------------------------------|  
| **`*~=00;90`**          | ~                   | Archivo temporal (ej: `archivo.txt~`)           |  
| **`*.bak=00;90`**       | .bak                | Backup                                          |  
| **`*.tmp=00;90`**       | .tmp                | Archivo temporal                                |  
| **`*.swp=00;90`**       | .swp                | Archivo de swap (Vim)                           |  

---

### **Códigos ANSI Usados en tu Configuración**

| **Código** | **Significado**          |  
|------------|--------------------------|  
| **00**     | Sin estilo               |  
| **01**     | Texto brillante (bold)   |  
| **30-37**  | Colores de texto         |  
| **40-47**  | Colores de fondo         |  
| **90**     | Texto gris oscuro        |  

#### **Colores Principales:**

- **31**: Rojo (texto).  
- **32**: Verde (texto).  
- **34**: Azul (texto).  
- **35**: Magenta (texto).  
- **36**: Cyan (texto).  
- **90**: Gris oscuro (texto).  

---

### **¿Cómo leer un código como `01;35`?**

- **`01`**: Estilo brillante (bold).  
- **`35`**: Color magenta.  
- **Ejemplo**: `*.png=01;35` → Archivos PNG en **magenta brillante**.  

---

### **Key Takeaways**

1. **Directorios con fondo verde**: Ya lo resolvimos modificando `ow=34;42` → `ow=34`.  
2. **Archivos comprimidos en rojo**: `.tar`, `.zip`, etc., usan `01;31` (rojo brillante).  
3. **Archivos temporales en gris**: `*~`, `*.bak`, etc., usan `00;90` (gris oscuro).  





