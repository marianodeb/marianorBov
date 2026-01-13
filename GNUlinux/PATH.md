

### ¿Qué es PATH?

En sistemas Unix y GNU/Linux, `PATH` es una variable de entorno que especifica las ubicaciones de directorios donde el sistema operativo busca programas ejecutables cuando se introduce un comando en la línea de comandos.

- **PATH**: Es una lista de directorios separados por dos puntos (`:`). Cada vez que intentas ejecutar un comando en la terminal, el sistema busca ese comando en cada uno de los directorios listados en `PATH`, en el orden en que están especificados.

### Cómo agregar un script al directorio PATH

Para hacer que un script sea ejecutable desde cualquier lugar del sistema sin especificar la ruta completa, puedes seguir estos pasos para agregar el directorio que contiene el script a la variable `PATH`:

1. **Ubica el directorio adecuado**: El directorio comúnmente utilizado para scripts personales en sistemas Unix/Linux es `/usr/local/bin`. Este directorio suele estar incluido en la `PATH` por defecto en muchas distribuciones.

2. **Mover el script**: Asegúrate de que tu script está en una ubicación accesible y que tiene permisos de ejecución (puedes usar `chmod +x` para darle permisos de ejecución).

   ```bash
   chmod +x mi_comando.sh
   ```

3. **Agregar el script al PATH temporalmente**: Si solo necesitas acceder al script durante la sesión actual, puedes agregar temporalmente el directorio al PATH en el terminal actual usando el siguiente comando:

   ```bash
   export PATH=$PATH:/ruta/del/directorio/del/script
   ```

   Por ejemplo:

   ```bash
   export PATH=$PATH:/home/tu_usuario/mis_scripts
   ```

   Esto añadirá temporalmente `/home/tu_usuario/mis_scripts` al `PATH` de la sesión actual. Puedes ejecutar tu script solo escribiendo `mi_comando.sh` desde cualquier ubicación en la terminal.

4. **Agregar el script al PATH permanentemente**: Si deseas que el script sea accesible desde cualquier sesión o terminal, debes agregar el directorio al `PATH` de manera permanente. Para hacerlo de manera permanente, puedes modificar el archivo de configuración de tu shell, que puede ser `~/.bashrc`, `~/.bash_profile`, `~/.zshrc`, o similar, dependiendo de la shell que estés usando.

   - Abre el archivo de configuración de tu shell en un editor de texto:

     ```bash
     nano ~/.bashrc
     ```

   - Agrega la línea al final del archivo para incluir el directorio que contiene tu script:

     ```bash
     export PATH=$PATH:/ruta/del/directorio/del/script
     ```

     Por ejemplo:

     ```bash
     export PATH=$PATH:/home/tu_usuario/mis_scripts
     ```

   - Guarda y cierra el archivo (`Ctrl + O` para guardar en `nano`, luego `Enter`, y `Ctrl + X` para salir en `nano`).

   - Recarga el archivo de configuración para que los cambios surtan efecto en tu sesión actual:

     ```bash
     source ~/.bashrc
     ```

5. **Verificación**: Para verificar que el script está ahora en tu `PATH`, puedes ejecutar:

   ```bash
   echo $PATH
   ```

   Deberías ver la ruta que acabas de agregar al `PATH`.

Con estos pasos, el script Bash debería ser accesible como un comando desde cualquier ubicación en tu sistema. 

## Verificar si el nombre del comando o alias exite
 
which: Este comando te mostrará la ubicación del ejecutable de un comando. Si no encuentra nada, significa que no hay un comando con ese nombre.

```bash

which kr
```


