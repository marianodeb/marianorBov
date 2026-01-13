
## **`rsync`**

### **1. Significado**

**`rsync`** (**R**emote **Sync**) es una herramienta avanzada para **sincronizar archivos y directorios** entre sistemas locales y remotos. Su principal ventaja es que **solo transfiere los cambios** (delta encoding), lo que lo hace **extremadamente eficiente** para backups, migraciones o mantener carpetas sincronizadas.  

---

### **2. Uso**

- **Sincronizar directorios** (eliminando archivos obsoletos en destino).  
- **Copiar archivos de forma eficiente** (solo lo modificado).  
- **Hacer backups incrementales**.  
- **Espejar datos** entre servidores.  
- **Preservar metadatos** (permisos, timestamps, ownership, etc.).  

---

### **3. Sintaxis General**

```bash
rsync [OPCIONES] ORIGEN DESTINO
```

- **Origen/Destino**: Pueden ser rutas locales (`/ruta/`) o remotas (`usuario@host:/ruta/`).  
- **Formato remoto**: Igual que `scp`: `usuario@host:ruta`.  

---

### **4. Opciones Principales**  

| Opción          | Descripción                                                                 |  
|-----------------|-----------------------------------------------------------------------------|  
| `-a`            | **Modo archivo** (equivale a `-rlptgoD`: preserva permisos, owner, timestamps, etc.). |  
| `-v`            | **Verbose** (muestra detalles de la transferencia).                        |  
| `-z`            | **Compresión** durante la transferencia (útil para redes lentas).          |  
| `-r`            | Copia **recursiva** (para directorios).                                    |  
| `-n`            | **Simulación** (dry-run: muestra qué haría sin ejecutarlo).                |  
| `--delete`      | **Elimina archivos en destino** que no están en origen (sincronización exacta). |  
| `-e "ssh"`      | Especifica el protocolo (ej: `-e "ssh -p 2222"` para cambiar puerto SSH).  |  
| `--exclude="*.tmp"` | **Excluye archivos** por patrón (ej: excluir `.log` o `node_modules/`). |  
| `--progress`     | Muestra **progreso** de la transferencia.                                  |  
| `-b`            | Crea **backups** de archivos existentes en destino (útil para evitar sobrescritura). |  
| `-h`            | **Formato legible** para tamaños (ej: 1K, 234M, 5G).                       |  
| `--bwlimit=1000` | **Limita el ancho de banda** (ej: 1000 KB/s).                             |  
| `--partial`      | **Continúa transferencias interrumpidas** (resume archivos parciales).    |  

---

### **5. Ejemplos**  

#### **Ejemplos Simples**

1. **Sincronizar una carpeta local a otra**:

```bash
rsync -av /ruta/origen/ /ruta/destino/
```
   
   ⚠️ **Importante**: La **barra final `/`** en el origen copia solo el **contenido** del directorio. Sin barra, copia el directorio completo.  

2. **Copiar de local a remoto**:

```bash
rsync -avz ~/Documentos/ usuario@192.168.1.100:/backups/docs/
```

3. **Traer archivos de remoto a local**:

```bash
rsync -avz usuario@192.168.1.100:/var/log/ ~/logs_servidor/
```

---

#### **Ejemplos Avanzados**

1. **Sincronizar eliminando archivos obsoletos en destino**:

```bash
rsync -av --delete /carpeta_local/ usuario@host:/carpeta_remota/
```

2. **Excluir archivos o carpetas específicas**:

```bash
rsync -av --exclude="*.tmp" --exclude="node_modules/" proyecto/ usuario@host:/backup/
```

3. **Usar SSH con puerto personalizado y compresión**:

```bash
rsync -avz -e "ssh -p 2222" /datos/ usuario@host:/backups/
```

4. **Limitar ancho de banda a 500 KB/s**:

```bash
rsync -av --bwlimit=500 /videos/ usuario@host:/media/
```

5. **Hacer backup de archivos existentes antes de sobrescribir**:

```bash
rsync -avb --backup-dir=/backups_old /origen/ /destino/
```

6. **Sincronizar parcialmente (útil para archivos grandes)**:

```bash
rsync -av --partial /iso/ usuario@host:/backups/
```

7. **Dry-run (simular sin ejecutar)**:

```bash
rsync -avn --delete /carpeta/ usuario@host:/backup/
```

---

### **6. Información Adicional**

#### **¿Cuándo usar `rsync` vs `scp`?**

- **`scp`**: Transferencias simples y rápidas (archivos pequeños, sin preocuparse por sincronización).  
- **`rsync`**: Sincronización inteligente, backups, directorios grandes o cambios incrementales.  

#### **Seguridad**

- Usa **SSH** para transferencias encriptadas (igual que `scp`).  
- Ejemplo con clave privada:

```bash
rsync -avz -e "ssh -i ~/.ssh/mi_clave.pem" /datos/ usuario@host:/backup/
```

#### **Alternativas**

- **`scp`**: Para transferencias básicas.  
- **`sftp`**: Transferencia interactiva.  
- **`Syncthing`**: Sincronización en tiempo real (GUI).  

---

### **7. Diagrama de Flujo de Rsync**

```
[ Origen ] → (Compara diferencias) → [ Solo envía cambios ] → [ Destino ]  
```

---

### **8. Errores Comunes**

- **Olvidar `-a`**: Pierdes permisos, ownership y metadatos.  
- **Confundir rutas con/sin `/`**:

  - `rsync /carpeta/ /destino/` → Copia **contenido** de `/carpeta/` a `/destino/`.  
  - `rsync /carpeta /destino/` → Copia la **carpeta** `/carpeta` dentro de `/destino/`.  
- **No usar `--dry-run` en operaciones críticas**: Siempre prueba con `-n` antes de sincronizar.  

---


### **1. ¿Necesito una conexión SSH previa para usar SCP/RSYNC?**

**No necesitas una sesión SSH activa**, pero **ambos comandos usan el protocolo SSH** para autenticarse y transferir datos de forma segura. Es decir:  
- **SCP** y **RSYNC** (cuando se usan con rutas remotas) **se conectan bajo el capó mediante SSH**.  
- Si es la **primera vez** que te conectas a un servidor remoto, se te pedirá que **verifiques la huella SSH** del host (igual que cuando usas `ssh` por primera vez).  

---

### **2. Flujo de Autenticación**

Cuando ejecutas `scp` o `rsync` hacia un destino remoto:

#### **a) Si usas autenticación por contraseña**:

- El comando te pedirá la **contraseña del usuario remoto** (igual que SSH).  
- **Ejemplo con SCP**:

```bash
scp archivo.txt usuario@192.168.1.100:/ruta/
# Pide la contraseña de "usuario" en 192.168.1.100
```

#### **b) Si usas claves SSH**:

- **No te pedirá contraseña** (siempre que hayas configurado las claves públicas/privadas correctamente).  
- **Requisitos**:

  1. Tener un par de claves SSH en tu máquina local (generadas con `ssh-keygen`).  
  2. Haber copiado la clave pública al servidor remoto (con `ssh-copy-id usuario@host`).  

---

### **3. ¿Se crean claves automáticamente?**

**No**. Las claves SSH **no se generan automáticamente** al usar `scp` o `rsync`. Debes crearlas manualmente si quieres evitar escribir la contraseña cada vez.  

#### **Pasos para configurar claves SSH**:

1. **Generar claves** (en tu PC local):

```bash
ssh-keygen -t ed25519
```
⚠️ Esto crea dos archivos: `~/.ssh/id_ed25519` (clave privada) y `~/.ssh/id_ed25519.pub` (clave pública).  

2. **Copiar clave pública al servidor remoto**:

```bash
ssh-copy-id usuario@ip_servidor
```

🔑 Ahora podrás conectarte (o usar `scp`/`rsync`) sin contraseña.  

---

### **4. Ejemplos Prácticos**

#### **SCP con contraseña**:

```bash
# Te pedirá la contraseña de "pi" en la Raspberry:
scp foto.jpg pi@192.168.1.100:/home/pi/
```

#### **RSYNC con clave SSH**:

```bash
# Sin contraseña (si las claves están configuradas):
rsync -avz -e "ssh -i ~/.ssh/mi_clave_privada" /backups/ usuario@servidor:/backups_remotos/
```

---

### **5. ¿Y si el servidor remoto tiene un puerto SSH diferente al default (22)?**

Usa la opción `-P` en `scp` o `-e "ssh -p puerto"` en `rsync`:

#### **SCP con puerto 2222**:

```bash
scp -P 2222 archivo.txt usuario@host:/ruta/
```

#### **RSYNC con puerto 2222**:

```bash
rsync -avz -e "ssh -p 2222" /datos/ usuario@host:/backup/
```

---

### **6. Seguridad: Contraseña vs Claves SSH**

- **Contraseña**:  
  - ✅ Fácil de usar.  
  - ❌ Riesgo de ataques de fuerza bruta.  
  - ❌ Debes escribirla cada vez.  
- **Claves SSH**:  
  - ✅ Más seguras (criptografía asimétrica).  
  - ✅ No necesitas escribir contraseña.  
  - ❌ Requiere configuración inicial.  

---

### **7. ¿Qué pasa si nunca me he conectado por SSH al servidor?**

En la **primera conexión**, verás un mensaje como:

```bash
The authenticity of host '192.168.1.100' can't be established.
ECDSA key fingerprint is SHA256:xxxxxxxxxxxx.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

- Debes escribir **`yes`** para guardar la huella del servidor en `~/.ssh/known_hosts`.  
- Si no lo haces, `scp` o `rsync` **fallarán** por motivos de seguridad.  

---

### **8. Resumen Visual**

```bash
# Autenticación con SCP/RSYNC:
┌───────────┐                          ┌───────────┐
│   Tu PC   │                          │  Servidor │
│  (local)  │                          │  (remoto) │
└─────┬─────┘                          └─────┬─────┘
      │                                        │
      │─1. ¿Claves SSH configuradas? ────────>│
      │                                        │
      │                                        │
      │─2. Si NO: Pide contraseña ────────────>│
      │                                        │
      │─3. Si SÍ: Usa clave pública/privada ──>│
```

---

### **9. Consejos Finales**  
- **Siempre usa claves SSH** para servidores remotos (es más seguro y práctico).  
- **Guarda las huellas SSH**: El archivo `~/.ssh/known_hosts` evita ataques de tipo *Man-in-the-Middle*.  
- **Prueba con `-v`**: Usa el modo verbose en `scp` o `rsync` para ver detalles de la conexión (ej: `scp -v ...`).  

---



