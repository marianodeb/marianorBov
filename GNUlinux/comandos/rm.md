

## `rm`

### Definición y Significado

`rm` (remove) es un comando fundamental en sistemas Unix/Linux para **eliminar archivos y directorios**. Es un comando potente pero peligroso, ya que los archivos eliminados generalmente no se pueden recuperar fácilmente.

Significado: Su función principal es borrar elementos del sistema de archivos, con opciones para manejar archivos protegidos, directorios vacíos o con contenido, y operaciones recursivas.

### Sintaxis Básica
```
rm [OPCIONES]... ARCHIVO...
```

### Todas sus Opciones Principales

#### Opciones básicas:

- `-f`, `--force` - Eliminar sin preguntar, ignorar archivos inexistentes
- `-i` - Preguntar antes de cada eliminación (interactivo)
- `-I` - Preguntar antes de eliminar muchos archivos (más seguro para operaciones masivas)
- `-r`, `-R`, `--recursive` - Eliminar directorios y su contenido recursivamente
- `-d`, `--dir` - Eliminar directorios vacíos (similar a rmdir)
- `-v`, `--verbose` - Mostrar lo que se está eliminando
- `--one-file-system` - No eliminar archivos en otros sistemas de archivos
- `--no-preserve-root` - No tratar '/' especialmente (peligroso)
- `--preserve-root` - No eliminar recursivamente en '/' (comportamiento por defecto)
- `--help` - Mostrar ayuda
- `--version` - Mostrar versión

### Ejemplos

#### Ejemplos simples:

1. Eliminar un archivo:

```bash
rm archivo.txt
```

2. Eliminar varios archivos:

```bash
rm archivo1.txt archivo2.txt archivo3.log
```

3. Eliminar con confirmación:

```bash
rm -i documento.pdf
```

4. Eliminar un directorio vacío:

```bash
rm -d directorio_vacio/
```

#### Ejemplos complejos:

1. Eliminar directorio y todo su contenido recursivamente:

```bash
rm -r directorio_con_archivos/
```

2. Eliminar todos los archivos .tmp sin preguntar:

```bash
rm -f *.tmp
```

3. Eliminar recursivamente mostrando lo que se borra:

```bash
rm -rv carpeta_proyecto/
```

4. Eliminar todos los archivos excepto los que coincidan con un patrón:

```bash
rm -v !(*.jpg|*.png)
```

5. Eliminar archivos más antiguos que 30 días:

```bash
find /ruta/carpeta -type f -mtime +30 -exec rm {} \;
```

### Consejos de Seguridad (MUY IMPORTANTES)

1. **Alias de seguridad**: Muchos usuarios configuran este alias en su `.bashrc`:

```bash
alias rm='rm -i'
```
   Esto hace que `rm` siempre pregunte antes de borrar.

2. **Alternativa segura**: Usar `trash-cli` (mueve a papelera en lugar de borrar):

```bash
sudo apt install trash-cli
trash-put archivo.txt  # En lugar de rm
```

3. **Doble verificación**: Antes de usar `rm -rf`, verifica la ruta exacta.

4. **Protección contra borrado accidental de root**:

```bash
rm --preserve-root -rf /  # No borrará el sistema
```

5. **Usar variables intermedias**:

```bash
ARCHIVOS_A_BORRAR=$(ls *.tmp)
echo "Se borrarán: $ARCHIVOS_A_BORRAR"
rm $ARCHIVOS_A_BORRAR
```

### Información Adicional

#### Comandos relacionados:

1. `rmdir` - Elimina solo directorios vacíos
2. `unlink` - Elimina un solo archivo (versión de bajo nivel)
3. `shred` - Borra archivos sobrescribiéndolos (más seguro)
4. `find` + `-delete` - Alternativa para borrado selectivo
5. `trash-cli` - Alternativa más segura (mueve a papelera)

#### ¿Hay alternativas modernas?

- `trash-cli` es la mejor alternativa para evitar borrados accidentales
- Algunos sistemas de archivos modernos tienen "papeleras" implementadas
- GUI como Nautilus, Dolphin tienen sus propias implementaciones de borrado

#### Estadísticas de accidentes:

El famoso "rm -rf /" o "rm -rf *" en directorios equivocados ha causado:

- Pérdida de datos personales
- Caídas de servidores
- Borrado de bases de datos
- Pérdida de meses de trabajo

#### Recuperación de archivos borrados:

Es posible pero difícil:

1. `testdisk`, `photorec` - Herramientas de recuperación
2. `extundelete` - Para sistemas de archivos ext3/ext4
3. Servicios profesionales - Costosos, no garantizados

#### Documentación oficial:

- Manual completo: `man rm`
- Estándar POSIX: https://pubs.opengroup.org/onlinepubs/9699919799/utilities/rm.html
- Código fuente: Parte del coreutils de GNU

#### Trucos avanzados:

1. Borrar archivos con espacios:

```bash
rm "archivo con espacios.txt"
```

2. Borrar por inodo (útil para archivos con nombres extraños):

```bash
find . -inum NUMERO_INODO -exec rm {} \;
```

3. Borrar archivos vacíos:

```bash
find . -type f -empty -delete
```

4. Borrar por permisos:

```bash
find . -type f ! -perm 644 -exec rm {} \;
```














