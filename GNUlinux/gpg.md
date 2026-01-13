


---

### **1. Conceptos básicos**

- **GPG**: Herramienta de cifrado asimétrico (usa un par de llaves: pública y privada).
- **Llave pública**: Para cifrar datos. Puedes compartirla con otros.
- **Llave privada**: Para descifrar datos. **Nunca la compartas**.
- **Use Case**: Encriptar archivos (notas) en Obsidian y desencriptarlos cuando los necesites.

---

### **2. Comandos esenciales para gestionar llaves GPG**

#### **Generar un par de llaves**

```bash
gpg --full-generate-key
```
- **Opciones recomendadas**:
  - Tipo de clave: `RSA (default)`.
  - Tamaño: `4096 bits` (más seguro).
  - Tiempo de expiración: `0` (no expira).
  - Ingresa tu nombre, email y contraseña segura.

---

#### **Listar llaves públicas**

```bash
gpg --list-keys
```

#### **Listar llaves privadas**

```bash
gpg --list-secret-keys
```

---

#### **Exportar llave pública**

```bash
gpg --armor --export TU_EMAIL_O_ID > public.key
```
- `--armor`: Genera el archivo en formato ASCII (legible).
- `public.key`: Nombre del archivo de salida.

#### **Exportar llave privada**

```bash
gpg --armor --export-secret-keys TU_EMAIL_O_ID > private.key
```

- **Importante**: Almacena este archivo en un lugar seguro (ej. USB cifrado).

---

#### **Importar una llave pública**

```bash
gpg --import public.key
```

#### **Importar una llave privada**

```bash
gpg --allow-secret-key-import --import private.key
```

---

#### **Eliminar una llave pública**

```bash
gpg --delete-key TU_EMAIL_O_ID
```

#### **Eliminar una llave privada**

```bash
gpg --delete-secret-key TU_EMAIL_O_ID
```

---

### **3. Encriptar y desencriptar archivos**

#### **Encriptar un archivo**

```bash
gpg --encrypt --recipient TU_EMAIL_O_ID --output nota.txt.gpg nota.txt
```

- `nota.txt`: Archivo original.
- `nota.txt.gpg`: Archivo encriptado.

#### **Firmar y encriptar**

```bash
gpg --encrypt --sign --recipient TU_EMAIL_O_ID nota.txt
```

---

#### **Desencriptar un archivo**

```bash
gpg --decrypt --output nota.txt nota.txt.gpg
```

- Te pedirá la contraseña de tu llave privada.

---

### **4. Gestión avanzada**

#### **Generar certificado de revocación**

```bash
gpg --gen-revoke TU_EMAIL_O_ID > revocation.crt
```

- **Importante**: Genera esto al crear la llave y guárdalo en un lugar seguro.

#### **Revocar una llave**

```bash
gpg --import revocation.crt
gpg --keyserver pgp.mit.edu --send-keys TU_ID_DE_LLAVE
```

---

### **5. Integración con Obsidian**

1. **Encriptar notas manualmente**:
   - Usa los comandos `gpg --encrypt` y `gpg --decrypt` desde la terminal.
2. **Automatizar con scripts**:
   - Crea un script en bash/Python para encriptar/desencriptar tu carpeta de notas.
3. **Plugins**:
   - Usa plugins como `ShellCommands` en Obsidian para ejecutar comandos GPG desde la interfaz.

---

### **6. Recomendaciones de seguridad**

- **Backup de llaves**: Guarda copias de tus llaves en medios físicos seguros.
- **Passphrase**: Usa una contraseña fuerte para proteger tu llave privada.
- **Gestor de contraseñas**: Almacena tu passphrase en un gestor como KeePassXC o Bitwarden.

---

### **7. Ejemplo de flujo de trabajo**

1. Creas una nota en Obsidian: `mi_secreto.md`.
2. La encriptas:

```bash
gpg --encrypt --recipient tu@email.com --output mi_secreto.md.gpg mi_secreto.md
```
3. Eliminas el archivo original (opcional).
4. Cuando necesites leerla:

```bash
gpg --decrypt --output mi_secreto.md mi_secreto.md.gpg
```

---

### **8. Troubleshooting**

- **Error de permisos**: Asegúrate de que los archivos `.gpg` tengan permisos adecuados.
- **Llave no encontrada**: Verifica que la llave esté en tu keyring (`gpg --list-keys`).



---

Qué observar en los errores

Cuando encuentres errores relacionados con apt o repositorios, presta atención a los siguientes detalles:

    Tipo de error:

- NO_PUBKEY: Falta una clave GPG.

- Release file is not valid yet: Problema de hora del sistema.

- Failed to fetch: Problema de conexión o repositorio no disponible.

    Repositorio afectado:
El mensaje de error suele indicar qué repositorio está causando el problema (por ejemplo, packages.mozilla.org o deb.parrot.sh).

    Clave GPG faltante:
Si el error menciona NO_PUBKEY, anota el ID de la clave faltante (por ejemplo, 7A8286AF0E81EE4A).

    Marca de tiempo:
Si el error menciona que un archivo "no es válido todavía" (not valid yet), es probable que la hora del sistema esté desincronizada.
        
        
Actualizar las claves GPG existentes:    

```bash
sudo apt-key list
sudo apt-key adv --refresh-keys
```

```bash
Sincronizar la hora del sistema:
```

```bash
timedatectl status
sudo timedatectl set-ntp true
```

---

---

### **1. ¿Cómo sé qué clave GPG usar?**

Cuando recibes un error como `NO_PUBKEY 7A8286AF0E81EE4A`, el sistema te está indicando que falta la clave pública con el ID `7A8286AF0E81EE4A` para verificar los paquetes del repositorio. **Este ID es la pista principal**.

#### **Fuentes para obtener la clave:**

- **Documentación del repositorio**: 

  - Los repositorios oficiales (como Mozilla, Parrot, Ubuntu, etc.) suelen incluir en su documentación el comando para agregar su clave GPG.
  - Ejemplo: En el caso de Parrot OS, su [sitio web](https://www.parrotsec.org/docs/) o foros indicarán la clave requerida.
  
- **Keyservers públicos**: 

  - Las claves GPG se almacenan en servidores públicos como `keyserver.ubuntu.com` o `pgp.mit.edu`.
  - Puedes descargarlas usando el ID de la clave (como `7A8286AF0E81EE4A`).

---

### **2. ¿Dónde se guardan las claves GPG en el sistema?**

En sistemas basados en Debian/Ubuntu, las claves GPG para APT se almacenan en dos ubicaciones principales:

1. **Directorio tradicional**:

   - `/etc/apt/trusted.gpg.d/`: Aquí se guardan archivos de claves GPG en formato binario (`.gpg`) o ASCII (`.asc`).
   - Ejemplo: `packages.mozilla.org.asc`.

2. **Archivo central (obsoleto)**:

   - `/etc/apt/trusted.gpg`: Un archivo que contiene todas las claves confiables (ya no se recomienda su uso directo).

#### **Mejor práctica moderna**:

Ahora se recomienda **no usar `apt-key`** (que modifica `/etc/apt/trusted.gpg`), sino guardar las claves en `/etc/apt/keyrings/` y referenciarlas directamente en los archivos de repositorio.  
Ejemplo de configuración en `/etc/apt/sources.list.d/mozilla.list`:

```bash
deb [signed-by=/etc/apt/keyrings/packages.mozilla.org.asc] https://packages.mozilla.org/apt mozilla main
```

---

### **3. ¿Cómo obtener e instalar una clave GPG manualmente?**

#### **Método 1: Usar `apt-key` (heredado pero funcional)**

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7A8286AF0E81EE4A
```

- **Qué hace**: Descarga la clave del keyserver y la agrega a `/etc/apt/trusted.gpg.d/`.

#### **Método 2: Guardar la clave manualmente (recomendado)**

1. Descargar la clave desde el keyserver:

```bash
gpg --keyserver keyserver.ubuntu.com --recv-keys 7A8286AF0E81EE4A
```

2. Exportarla a un archivo:

```bash
gpg --export --armor 7A8286AF0E81EE4A | sudo tee /etc/apt/keyrings/parrot.asc > /dev/null
```

3. Referenciarla en el repositorio:

```bash
echo "deb [signed-by=/etc/apt/keyrings/parrot.asc] https://deb.parrot.sh/parrot lory main" | sudo tee /etc/apt/sources.list.d/parrot.list
```

---

### **4. Relación entre claves GPG y SSH**
Ambas son parte de la criptografía de clave pública, pero tienen propósitos diferentes:

| **Característica**       | **Claves GPG (APT)**                          | **Claves SSH**                          |
|--------------------------|-----------------------------------------------|-----------------------------------------|
| **Propósito**            | Verificar paquetes y repositorios.            | Autenticación en servidores remotos.    |
| **Ubicación típica**     | `/etc/apt/keyrings/` o `/etc/apt/trusted.gpg.d/` | `~/.ssh/` (ej: `id_rsa.pub`).           |
| **Gestión**              | Herramientas: `apt-key`, `gpg`, `wget`.       | Herramientas: `ssh-keygen`, `ssh-add`.  |
| **Formato**              | Binario (`.gpg`) o ASCII (`.asc`).            | Texto plano (ej: `ssh-rsa AAAAB3...`).  |

---

### **5. Verificar claves GPG instaladas**

Para listar todas las claves GPG que tu sistema confía:

```bash
sudo apt-key list
# o
gpg --list-keys --keyring /etc/apt/trusted.gpg.d/*
```

---

### **6. Ejemplo completo: Agregar un repositorio seguro**

Supongamos que quieres agregar el repositorio de **VSCode**:

1. **Obtener la clave GPG**:

```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /etc/apt/keyrings/vscode.gpg > /dev/null
```

2. **Agregar el repositorio**:

```bash
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/vscode.gpg] https://packages.microsoft.com/repos/vscode stable main" | sudo tee /etc/apt/sources.list.d/vscode.list
```

3. **Actualizar e instalar**:

```bash
sudo apt update && sudo apt install code
```

---

### **7. Consejos para evitar problemas**

1. **Siempre verifica la fuente**:

   - Descarga claves GPG solo desde sitios oficiales o documentación confiable.
   
2. **Compara fingerprints**:

   - Los repositorios suelen publicar el fingerprint de su clave (ej: `35BAA0B33E9EB396F59CA838C0BA5CE6DC6315A3`).
   - Verifícalo con:
   
```bash
gpg --fingerprint 7A8286AF0E81EE4A
```

3. **Usa `signed-by` en repositorios**:

   - Esto evita contaminar el almacén global de claves y hace la gestión más transparente.

---

### **Resumen final**

- **Clave GPG**: Es el "DNI" del repositorio. Sin ella, no puedes verificar la autenticidad de los paquetes.
- **Dónde guardarla**: En `/etc/apt/keyrings/` y referenciarla con `signed-by` en el archivo del repositorio.
- **Cómo obtenerla**: Desde el keyserver con `gpg --recv-keys` o descargarla desde la web oficial.
- **Relación con SSH**: Ambas usan criptografía asimétrica, pero para fines distintos.

























































