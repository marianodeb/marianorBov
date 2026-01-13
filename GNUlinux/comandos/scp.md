
## **`scp`** (Secure Copy Protocol)

---

### **1. Significado**  

**SCP** (**S**ecure **C**opy **P**rotocol) es un protocolo basado en **SSH** que permite copiar archivos o directorios entre máquinas locales y remotas de forma **encriptada**. Es ideal para transferencias seguras en redes no confiables.

---

### **2. Uso**  

- Copiar archivos/directorios **de local a remoto**, **de remoto a local**, o **entre dos sistemas remotos**.  
- Mantiene la seguridad mediante autenticación y cifrado de SSH.  
- Es útil para backups, migraciones, o transferencias rápidas.

---

### **3. Sintaxis Básica**  

```bash
scp [opciones] origen destino
```

- **origen/destino**: Pueden ser rutas locales (`/ruta/archivo`) o remotas (`usuario@ip:/ruta/archivo`).  
- **Formato remoto**: `usuario@host:ruta`.

---

### **4. Opciones Principales**  

| Opción | Descripción |  
|--------|-------------|  
| `-P <puerto>` | Especifica el puerto SSH (por defecto: 22). |  
| `-r` | Copia directorios recursivamente. |  
| `-C` | Habilita compresión para acelerar la transferencia. |  
| `-i <clave_privada>` | Usa una clave SSH específica (ej: `.pem`). |  
| `-v` | Modo verbose (muestra detalles del proceso). |  
| `-q` | Modo silencioso (sin mensajes). |  
| `-p` | Preserva permisos y timestamps de los archivos. |  
| `-l <limite>` | Limita el ancho de banda (ej: `-l 1000` para 1000 Kbps). |  

---

### **5. Ejemplos**  

#### **Ejemplos Simples**  

- **De local a remoto**:  

```bash
 scp mi_archivo.txt usuario@192.168.1.10:/home/usuario/
```

- **De remoto a local**:  

```bash
scp usuario@192.168.1.10:/home/usuario/mi_archivo.txt /descargas/
```

- **Entre dos servidores remotos**:  

```bash
scp usuario1@servidor1:/ruta/archivo usuario2@servidor2:/ruta/destino
```

#### **Ejemplos Avanzados**  

- **Copiar un directorio completo** (usando `-r`):  

```bash
scp -r /carpeta_local usuario@192.168.1.10:/backups/
```

- **Usar puerto personalizado** (ej: 2222):  

```bash
scp -P 2222 archivo.txt usuario@192.168.1.10:/home/
```

- **Transferir con compresión** (`-C`) y límite de ancho de banda (`-l`):  

```bash
scp -C -l 500 archivo_grande.iso usuario@192.168.1.10:/home/
```

- **Autenticación con clave SSH** (`-i`):  

```bash
scp -i ~/.ssh/mi_clave.pem archivo_secreto.txt usuario@servidor:/ruta/
```

- **Preservar atributos** (`-p`):  

```bash
scp -p documento.pdf usuario@192.168.1.10:/docs/
```

---

### **6. Información Adicional**  

- **Seguridad**: Usa el mismo cifrado que SSH (como AES).  
- **Alternativas**: `rsync` (para sincronización avanzada) o `sftp` (transferencia interactiva).  
- **Wildcards**: Puedes usar `*` para múltiples archivos (ej: `scp *.txt usuario@host:/ruta`).  
- **Deprecación**: En algunas versiones recientes, `scp` está marcado como obsoleto. Se recomienda usar `rsync` o `sftp` para más funcionalidades.  

---

ejemplo práctico usando tu **Raspberry Pi** (a la que te conectas por SSH). La clave está en entender **desde dónde ejecutas el comando `scp`** y cómo se interpretan las rutas **"local"** vs **"remoto"**.

---

### **1. Concepto Clave**  

- **"Local"**: Es la máquina **desde donde ejecutas el comando `scp`**.  
- **"Remoto"**: Es el otro equipo involucrado en la transferencia.  

Si estás conectado por SSH a la Raspberry Pi (desde tu PC), **depende de dónde ejecutes `scp`**:

---

### **2. Casos Prácticos**  

#### **Caso A: Ejecutas `scp` desde tu PC (local) hacia la Raspberry Pi (remota)**  

- **Objetivo**: Copiar un archivo de tu PC a la Raspberry.  
- **Comando**:  

```bash
# Desde tu PC (local) -> Raspberry (remota)
scp archivo.txt pi@192.168.1.100:/home/pi/
```
  
  - **Local**: Tu PC (desde donde escribes el comando).  
  - **Remoto**: La Raspberry (`pi@192.168.1.100`).  

#### **Caso B: Ejecutas `scp` desde la Raspberry Pi (vía SSH) hacia tu PC**  

- **Objetivo**: Copiar un archivo de la Raspberry a tu PC.  
- **Comando** (desde la Raspberry):  

```bash
# Desde Raspberry (local) -> Tu PC (remoto)
scp archivo.txt usuario_pc@192.168.1.50:/ruta/destino/
```
  - **Local**: La Raspberry (porque ejecutas el comando allí).  
  - **Remoto**: Tu PC (`usuario_pc@192.168.1.50`).  

---

### **3. ¿Cómo saber cuál es cuál?**  

- **Si estás en la terminal de tu PC** (sin SSH):  

  - **Local**: Tu PC.  
  - **Remoto**: Cualquier máquina que tenga formato `usuario@ip:ruta`.  

- **Si estás conectado por SSH a la Raspberry**:  

  - **Local**: La Raspberry (porque ejecutas comandos desde allí).  
  - **Remoto**: Tu PC u otro servidor (debes usar su IP o dominio).  

---

### **4. Ejemplo Detallado**  

Supongamos que:  

- **Tu PC**: IP `192.168.1.50`, usuario `tu_usuario`.  
- **Raspberry Pi**: IP `192.168.1.100`, usuario `pi`.  

#### **Ejemplo 1**: Quieres copiar `foto.jpg` desde tu PC a la Raspberry.  

- **Desde tu PC (local)**:  

```bash
scp /ruta/foto.jpg pi@192.168.1.100:/home/pi/
```

#### **Ejemplo 2**: Desde la Raspberry (vía SSH), copiar `datos.txt` a tu PC.  

1. **Conéctate a la Raspberry**:  

```bash
ssh pi@192.168.1.100
```
2. **Ejecuta `scp` desde la Raspberry**:  

```bash
scp datos.txt tu_usuario@192.168.1.50:/Escritorio/
```

---

### **5. Errores Comunes**  

- **Confundir local/remoto al estar en SSH**: Si ejecutas `scp` desde la Raspberry, ¡tu PC será el remoto!  
- **Usar rutas relativas incorrectas**: 
 
  - En **local**, las rutas son relativas al equipo donde ejecutas `scp`.  
  - En **remoto**, son relativas al home del usuario remoto (si usas `:` sin ruta absoluta).  

---

### **6. Tips para No Confundirte**  

1. **Mira el prompt de la terminal**:  

   - Si dice `pi@raspberrypi`, estás en la Raspberry (local = Raspberry).  
   - Si es tu usuario habitual, estás en tu PC (local = PC).  
   
2. **Usa `hostname`**:  

```bash
hostname  # Muestra el nombre del equipo actual (local).
```
3. **Prueba con IPs**: Si usas la IP de tu PC en el comando, es remoto; si no, es local.  

---

### **7. ¿Y si quiero copiar algo DESDE mi PC estando en SSH?**  

Necesitas salir de la Raspberry (volver a tu PC) o abrir **otra terminal** en tu PC para ejecutar `scp`. Otra opción es usar `scp` desde la Raspberry apuntando a tu PC:  

```bash
# Desde la Raspberry (SSH):
scp -r tu_usuario@192.168.1.50:/ruta/en_tu_pc /ruta/en_raspberry
```

---

### **Escenarios Claros**  

#### **1. Desde tu PC (local) → Raspberry (remota)**  

- **Comando**:  

```bash
scp -r /ruta/en_tu_pc usuario_pi@ip_raspberry:/ruta/destino
```
  
  - **Ejemplo**:  
  
```bash
scp -r ~/Documentos/proyecto pi@192.168.1.100:/home/pi/backups
```

#### **2. Desde Raspberry (remota) → Tu PC (local)**  

- **Comando**:  

```bash
scp -r usuario_pi@ip_raspberry:/ruta/en_raspberry /ruta/destino_en_tu_pc
```
  
  - **Ejemplo**:
  
```bash
scp -r pi@192.168.1.100:/home/pi/sensores/data ~/Descargas
```

---

### **¿Qué pasa si ya estoy en una sesión SSH de la Raspberry?**  

Si **ya estás conectado por SSH** a la Raspberry y quieres copiar algo desde allí a tu PC, **sí puedes usar `scp`**, pero en este caso:  

- **Local**: La Raspberry (porque ejecutas el comando desde allí).  
- **Remoto**: Tu PC (debes especificar su IP y usuario).  

**Ejemplo**:

```bash
# Dentro de la sesión SSH de la Raspberry:
scp -r /ruta/archivo_raspberry tu_usuario_pc@192.168.1.50:/ruta/destino_pc
```

⚠️ **Requiere que tu PC tenga un servidor SSH activo** (o que permita conexiones entrantes en el puerto 22).  

---

### **Resumen Visual**

```bash
# ┌─────────────┐               ┌─────────────┐
# │    Tu PC    │               │  Raspberry  │
# │  (local)    │               │  (remoto)   │
# └─────────────┘               └─────────────┘
scp -r archivo_LOCAL pi@IP_RASPBERRY:/ruta/REMOTA

# ┌─────────────┐               ┌─────────────┐
# │  Raspberry  │               │    Tu PC    │
# │  (remoto)   │               │  (local)    │
# └─────────────┘               └─────────────┘
scp -r pi@IP_RASPBERRY:/ruta/REMOTA /ruta_LOCAL
```

---

### **Consejos para No Confundirte**

1. **Ejecuta `scp` siempre desde tu PC** (sin SSH) para mayor simplicidad.  
2. **Usa `ping` o `arp -a`** para verificar la IP de la Raspberry si no la recuerdas.  
3. **Si tu PC es Windows**, usa herramientas como **WinSCP** (interfaz gráfica) o `scp` desde PowerShell/WSL.  

---

### **Ejemplo Real**

**Objetivo**: Copiar la carpeta `~/fotos` de tu PC a la Raspberry.  

```bash
# Desde tu PC (local):
scp -r ~/fotos pi@192.168.1.100:/home/pi/imagenes
```

**Objetivo**: Traer el archivo `~/informe.txt` de la Raspberry a tu PC.

```bash
# Desde tu PC (local):
scp pi@192.168.1.100:/home/pi/informe.txt ~/Documentos
```

---

### **¿Y si quiero evitar escribir la IP cada vez?**

Configura un **alias en tu PC** (en el archivo `/etc/hosts`):

```bash
# Agrega esta línea a /etc/hosts:
192.168.1.100   raspberry
```

Luego usa el alias:

```bash
scp -r informe.txt pi@raspberry:/home/pi/
```

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

