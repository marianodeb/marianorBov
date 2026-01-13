fdisk es una utilidad de línea de comandos que se utiliza para gestionar las particiones de un disco. En términos más simples, fdisk te permite crear, eliminar, redimensionar y modificar las secciones en las que se divide tu disco.

Crear particiones: Dividir el disco en secciones para asignar diferentes sistemas de archivos.
Eliminar particiones: Borrar una partición existente.
Modificar particiones: Cambiar el tamaño, tipo o ubicación de una partición.
Ver información: Mostrar la tabla de particiones actual del disco.

¿Cómo se utiliza fdisk?

Abrir una terminal: Accede a la línea de comandos de tu sistema operativo.Ejecutar el comando fdisk: Escribe sudo fdisk /dev/sdX y presiona Enter, donde /dev/sdX es la ruta de tu disco (por ejemplo, /dev/sda). Necesitarás permisos de administrador (sudo) para realizar cambios.

Interactuar con el menú: 

Aparecerá un menú interactivo con opciones numeradas.
Lasopciones más comunes son:

**p**: Imprimir la tabla de particiones.
**n**: Crear una nueva partición.
**d:** Eliminar una partición.
**w**:Escribir los cambios en el disco.
**q**: Salir sin guardar cambios.

Seguir las instrucciones: Cada opción te guiará a través de un proceso para realizar la tarea seleccionada. Por ejemplo, al crear una partición, te pedirá el tipo de partición (primaria o extendida), el primer sector y el último sector.

Opciones comunes de fdisk:

**-l**: Lista todas las particiones de todos los discos.
**-b**: Especifica el tamaño de sector en bytes.
**-u**: Utiliza unidades de cilindros en lugar de sectores.

Ejemplo básico:

```bash
sudo fdisk /dev/sda
```

Esto abrirá fdisk para el primer disco duro (/dev/sda). Luego, puedes usar las opciones del menú para crear una nueva partición:

```
Command (m for help): n
Command action
   e extended
   p primary partition (1-4)
p
Partition number (1-4): 1
First sector (2048-1048575): 
Last sector, +size, or +sizeM/G/T: +10G
```

En este ejemplo, estamos creando una partición primaria de 10 GB en la primera partición disponible.

Importante: Las opciones y el comportamiento exacto de fdisk pueden variar ligeramente entre diferentes distribuciones de Linux.
fdisk solo crea las particiones. Para hacer que una partición sea utilizable, debes formatearla con un sistema de archivos (como ext4, NTFS, etc.) utilizando herramientas como **mkfs**.


