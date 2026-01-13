

## `md5sum`

### Definición y Significado

**`md5sum`** es una herramienta en sistemas Unix/Linux para calcular y verificar **sumas de comprobación MD5** (Message Digest Algorithm 5).  
- **MD5**: Algoritmo criptográfico que genera un valor hash de 128 bits (32 caracteres hexadecimales).  
- **Uso principal**: Verificar la integridad de archivos (detectar cambios o corrupción).  

**Significado**:

- **Generación**: Crea una "huella digital" única de un archivo.  
- **Verificación**: Compara el hash actual con uno previamente generado para confirmar que el archivo no ha sido alterado.  

::: warning
**Nota de seguridad**: MD5 está **obsoleto para usos criptográficos** por vulnerabilidades conocidas, pero sigue siendo útil para verificación de integridad básica.  
:::  

### Sintaxis

```bash  
md5sum [OPCIONES]... [ARCHIVO]...  
```

- Si no se especifica un archivo, lee desde la entrada estándar (stdin).  

### Todas sus Opciones Principales  

| Opción          | Descripción |  
|-----------------|-------------|  
| `-b`, `--binary` | Modo binario (para sistemas Windows-compatibles). |  
| `-c`, `--check`  | Verificar hashes desde un archivo de sumas. |  
| `--tag`          | Generar hash en formato BSD (ej: `MD5 (archivo.txt) = ...`). |  
| `-t`, `--text`   | Modo texto (por defecto en sistemas Unix). |  
| `--quiet`        | No mostrar mensajes de éxito, solo errores. |  
| `--status`       | No mostrar salida, usar código de salida (0: éxito, 1: error). |  
| `--strict`       | Tratar formatos no válidos como errores. |  
| `--ignore-missing`| Ignorar archivos faltantes al verificar. |  
| `--warn`         | Mostrar advertencias sobre formatos inválidos (activo por defecto). |  
| `--help`         | Mostrar ayuda. |  
| `--version`      | Mostrar versión. |  

### Ejemplos  

#### Ejemplos Simples:

1. **Generar hash MD5 de un archivo**:

```bash  
md5sum imagen.iso  
```
   
Salida:
   
```  
d41d8cd98f00b204e9800998ecf8427e  imagen.iso  
```

2. **Verificar archivo contra un hash conocido**:

```bash  
echo "d41d8cd98f00b204e9800998ecf8427e  imagen.iso" | md5sum -c -  
```

3. **Generar hash en formato BSD**:

```bash  
md5sum --tag imagen.iso  
```
   
   Salida:
   
```
MD5 (imagen.iso) = d41d8cd98f00b204e9800998ecf8427e  
```

#### Ejemplos Complejos:

1. **Verificar múltiples archivos con un archivo de sumas**:

```bash
md5sum *.iso > checksums.md5  
md5sum -c checksums.md5  
```

2. **Comparar directorios usando hashes**:

```bash
find directorio/ -type f -exec md5sum {} \; > dir_hashes.md5  
md5sum -c dir_hashes.md5  
```

3. **Verificar archivos descargados desde una URL**:

```bash
curl -s https://ejemplo.com/archivo.txt | md5sum  
```

4. **Generar hash de una cadena de texto**:

```bash  
echo -n "texto secreto" | md5sum  
```

### Consejos

1. **Alternativas seguras**: Usa `sha256sum` o `sha512sum` para mayor seguridad.  
2. **Verificación automática**: Integra `md5sum -c` en scripts para validar archivos críticos.  
3. **Evita espacios en nombres**: Si un archivo tiene espacios, usa comillas:

```bash  
md5sum "archivo con espacios.txt"  
```
   
4. **Generación masiva**: Para crear un archivo de hashes de todos los archivos en un directorio:

```bash  
find /ruta/ -type f -exec md5sum {} \; > hashes_totales.md5  
```

### Información Adicional  

#### Limitaciones de MD5

- **Colisiones**: Es posible generar dos archivos diferentes con el mismo hash MD5.  
- **No para seguridad**: No lo uses para contraseñas, firmas digitales o protección anti-temperado.  

#### Comandos Relacionados

| Comando         | Descripción |  
|-----------------|-------------|  
| `sha256sum`     | Versión segura (SHA-2 de 256 bits). |  
| `sha512sum`     | Versión más larga (SHA-2 de 512 bits). |  
| `cksum`         | Checksum CRC32 (menos seguro, pero rápido). |  
| `b2sum`         | BLAKE2 (alternativa moderna a MD5/SHA). |  
| `hashdeep`      | Herramienta avanzada para hashes múltiples. |  

#### Sustitutos Modernos

- **SHA-256/512**: Estándar actual para integridad y seguridad.  
- **BLAKE3**: Algoritmo más rápido y seguro que SHA-2.  

#### Curiosidades

- El hash MD5 vacío (archivo de 0 bytes) es `d41d8cd98f00b204e9800998ecf8427e`.  
- En sistemas BSD/macOS, el comando equivalente es `md5`.  

#### Recuperar Hashes de Paquetes Instalados

En Debian/Ubuntu, los hashes MD5 de los paquetes instalados se guardan en:

```bash  
cat /var/lib/dpkg/info/*.md5sums  
```  

¿Necesitas profundizar en algún uso específico de `md5sum`?












