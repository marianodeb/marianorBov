
## blkid

### **Definición y Significado**

**`blkid`** (Block ID) es un comando de Linux que muestra información detallada sobre **dispositivos de bloque** (discos duros, particiones, USB, etc.), como:

- **UUID** (Identificador Único Universal).  
- **Tipo de sistema de archivos** (ext4, ntfs, vfat, etc.).  
- **Etiquetas** (LABEL).  
- **Tamaño de bloque**, **PARTUUID** (UUID de partición GPT), y más.  

Funciona leyendo la base de datos de **udev** o escaneando directamente los dispositivos. Es parte del paquete **util-linux**.

---

### **Sintaxis**

```bash
blkid [opciones] [dispositivo]
```
- Si no se especifica un `[dispositivo]`, muestra información de **todos los dispositivos de bloque**.

---

### **Opciones Principales**

| Opción          | Descripción                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| `-c <archivo>`  | Usa un archivo de caché alternativo (por defecto: `/etc/blkid.tab`).        |
| `-g`            | Realiza una "recolección de basura" en la caché (elimina entradas inválidas). |
| `-o <formato>`  | Formato de salida: `value`, `device`, `list`, `full`, `export` (para scripts). |
| `-p`            | Modo de "sondeo" de bajo nivel (ignora la caché, útil para dispositivos nuevos). |
| `-i`            | Muestra información adicional (versión del sistema de archivos, tamaño, etc.). |
| `-s <tag>`      | Muestra solo un tag específico (ej: `-s UUID`, `-s TYPE`).                  |
| `-U <UUID>`     | Busca un dispositivo por su UUID (ej: `blkid -U 123e4567-e89b-12d3...`).    |
| `-L <etiqueta>` | Busca un dispositivo por su etiqueta (ej: `blkid -L "MI_DISCO"`).           |
| `-d`            | Muestra solo dispositivos sin sistema de archivos (ej: discos vacíos).      |

---

### **Ejemplos**

#### **1. Ejemplos Simples**

- Mostrar **todos los dispositivos de bloque**:

```bash
blkid
```
  Salida típica:
  
```bash
/dev/sda1: UUID="abcd-1234" TYPE="vfat" PARTLABEL="EFI System" PARTUUID="123e4567..."
/dev/sda2: UUID="5678-90ab" TYPE="ext4" LABEL="SISTEMA"
```

- Mostrar solo el **UUID de un dispositivo específico**:

```bash
blkid -s UUID -o value /dev/sda2
```
  Salida:
  
```bash
5678-90ab
```

#### **2. Ejemplos Complejos**

- Buscar un dispositivo por **UUID** y mostrar su ruta:

```bash
blkid -U 5678-90ab
```
  Salida:
  
```bash
/dev/sda2
```

- Usar formato `export` para usar en scripts (variables de entorno):

```bash
blkid -o export /dev/sda1
```

Salida:
  
```bash
DEVNAME=/dev/sda1
UUID=abcd-1234
TYPE=vfat
PARTLABEL=EFI System
```

- Probar un dispositivo USB recién conectado (ignorando la caché):

```bash
sudo blkid -p /dev/sdb1
```

---

### **Consejos**

1. **Permisos de Superusuario**:

Algunas opciones (como `-p`) requieren ejecutar `blkid` con `sudo` para acceder a datos en tiempo real.  

2. **Cache vs. Sondeo Directo**:

   - Si no ves cambios recientes (ej: formateo), usa `-p` para ignorar la caché.  
   - Usa `blkid -g` si la caché está corrupta.  

3. **Scripts Automatizados**:

   Usa `-o value` para obtener valores limpios (sin texto extra):
   
```bash
FS_TYPE=$(blkid -s TYPE -o value /dev/sda2)
```

4. **Compatibilidad con Fichero `/etc/fstab`**:

   Usa `blkid` para obtener UUIDs y evitar errores al montar particiones.  

---

### **Información Adicional**

- **Integración con udev**:

  `blkid` obtiene datos de la base de datos de **udev**, que se actualiza automáticamente al conectar dispositivos.  

- **Sistemas de Archivos Soportados**:

  Reconoce prácticamente todos los sistemas de archivos: ext2/3/4, NTFS, FAT, XFS, Btrfs, LVM, LUKS (criptografía), etc.  

- **Alternativas**:

  - `lsblk`: Muestra la jerarquía de dispositivos (pero sin UUIDs ni etiquetas).  
  - `findfs UUID=<valor>`: Busca dispositivos por UUID (similar a `blkid -U`).  

---

### **Casos de Uso Comunes**

1. **Configurar `/etc/fstab`**:

```bash
# Obtener UUID de una partición
blkid -s UUID -o value /dev/sda2 >> /etc/fstab
```

2. **Identificar Discos en Sistemas con Múltiples Unidades**:

```bash
blkid | grep "LABEL=\"BACKUP\""
```

3. **Depurar Problemas de Montaje**:

   Verificar si una partición tiene un sistema de archivos válido:
   
```bash
sudo blkid -p /dev/sdb1
```

---

### **Notas Finales**

- **Seguridad**: `blkid` es de solo lectura, no modifica dispositivos.  
- **Documentación**: Consulta el manual completo con `man blkid`.  
- **Sistemas sin `blkid`**: Instálalo desde el paquete `util-linux` (ya incluido en la mayoría de distribuciones).  


