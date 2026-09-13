¡Perfecto! Te voy a explicar **ABSOLUTAMENTE TODO** paso a paso, como si nunca hubieras visto una terminal en tu vida. Voy a ser extremadamente detallado.

---

## PRIMERO: ¿Qué estamos haciendo y por qué?

### El problema:
Tu archivo `/etc/resolv.conf` (que es donde se guardan los DNS) se modifica solo constantemente. Esto pasa porque hay programas que lo actualizan automáticamente cuando cambia tu conexión de red.

### La solución que encontramos:
Vamos a decirle al programa que maneja tu red (NetworkManager) que **no** toque más ese archivo y que use los DNS que nosotros le digamos.

---

## PASO 1: Averiguar qué programa maneja mi red

Ejecutaste este comando:
```bash
systemctl status systemd-resolved
```

### Explicación línea por línea:
- **`systemctl`** = Es el comando para controlar "servicios" (programas que corren en segundo plano) en Linux.
- **`status`** = Le dice a systemctl que queremos ver el estado (si está funcionando o no) de un servicio.
- **`systemd-resolved`** = Es el nombre de un servicio que maneja DNS. 

### ¿Qué significa la respuesta que te dio?
```
Unit systemd-resolved.service could not be found.
```

**Traducción:** "No encontré ese servicio". Esto significa que **NO** tenés systemd-resolved instalado o activo. Entonces no lo usás.

---

## PASO 2: Ver mis conexiones de red

Ejecutaste:
```bash
nmcli connection show
```

### Explicación línea por línea:
- **`nmcli`** = Es el comando para controlar NetworkManager (el programa que maneja redes en tu PC).
- **`connection`** = Le decimos que queremos trabajar con conexiones.
- **`show`** = Le decimos que queremos VER (mostrar) las conexiones.

### ¿Qué significa la respuesta que te dio?
```
NAME                UUID                                  TYPE      DEVICE 
Wired connection 1  6ef97d07-0fda-454f-bbe4-c4c495fe782d  ethernet  enp3s0 
lo                  fe128097-b2db-4c30-9da2-05d2573acb4a  loopback  lo
```

Esto es una TABLA con 4 columnas:

| NAME | UUID | TYPE | DEVICE |
|------|------|------|--------|
| Wired connection 1 | 6ef97d07-0fda-454f-bbe4-c4c495fe782d | ethernet | enp3s0 |
| lo | fe128097-b2db-4c30-9da2-05d2573acb4a | loopback | lo |

### Explicación de CADA columna:

**1. NAME (NOMBRE):**
- Es el nombre que le puso el sistema a tu conexión.
- `Wired connection 1` = "Conexión por cable 1" (es tu internet por cable).
- `lo` = "loopback" (es una conexión virtual que usa la PC para comunicarse con sí misma, NO es tu internet).

**2. UUID:**
- Es un identificador único (como un DNI) de esa conexión. No lo necesitás para nada.

**3. TYPE (TIPO):**
- `ethernet` = Conexión por cable de red.
- `loopback` = Conexión virtual interna.

**4. DEVICE (DISPOSITIVO):**
- `enp3s0` = Es el nombre técnico de tu tarjeta de red (la que tiene el cable).
- `lo` = Dispositivo virtual loopback.

### ¿Cómo sé cuál es MI conexión?
**La que te interesa es la que tiene TYPE = ethernet y DEVICE = enp3s0**, porque es tu internet real.

Entonces el NOMBRE que tenés que usar es: **`Wired connection 1`**

---

## PASO 3: Los comandos que vamos a ejecutar (y qué hace cada cosa)

### Comando 1: Cambiar los DNS
```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dns "8.8.8.8 1.1.1.1"
```

**Explicación EXTRA-DETALLADA:**

- **`sudo`** = Ejecutar como superusuario (administrador). Te va a pedir tu contraseña.
- **`nmcli`** = El programa para controlar NetworkManager.
- **`connection`** = Estamos trabajando con conexiones.
- **`modify`** = Queremos MODIFICAR una conexión.
- **`"Wired connection 1"`** = El NOMBRE de la conexión que queremos modificar (va entre comillas porque tiene espacios).
- **`ipv4.dns`** = Es la "variable" que guarda los DNS de IPv4.
- **`"8.8.8.8 1.1.1.1"`** = Los nuevos DNS que vamos a poner (Google y Cloudflare). Van separados por un espacio.

**Lo que hace:** Le dice a NetworkManager "en mi conexión 'Wired connection 1', poné estos DNS".

---

### Comando 2: Ignorar los DNS automáticos
```bash
sudo nmcli connection modify "Wired connection 1" ipv4.ignore-auto-dns yes
```

**Explicación EXTRA-DETALLADA:**

- **`sudo`** = Ejecutar como superusuario.
- **`nmcli`** = Controlar NetworkManager.
- **`connection`** = Trabajar con conexiones.
- **`modify`** = Modificar una conexión.
- **`"Wired connection 1"`** = La misma conexión de antes.
- **`ipv4.ignore-auto-dns`** = Es una "variable" que dice si ignoramos o no los DNS automáticos.
- **`yes`** = Le decimos que SÍ, que ignore los DNS que vienen automáticos (del DHCP).

**Lo que hace:** Le dice a NetworkManager "no hagas caso a los DNS que te mande el router, usá los que yo te puse en el comando anterior".

---

### Comando 3: Reiniciar la conexión para que los cambios se apliquen
```bash
sudo nmcli connection down "Wired connection 1" && sudo nmcli connection up "Wired connection 1"
```

**Explicación EXTRA-DETALLADA:**

**Primera parte:**
- **`sudo nmcli connection down "Wired connection 1"`**
  - **`down`** = Apagar/desconectar.
  - **Lo que hace:** Desconecta tu internet por un segundo.

- **`&&`** = Significa "Y". Solo ejecuta lo que sigue si lo anterior funcionó bien.

**Segunda parte:**
- **`sudo nmcli connection up "Wired connection 1"`**
  - **`up`** = Encender/conectar.
  - **Lo que hace:** Vuelve a conectar tu internet.

**Lo que hace en total:** Reinicia tu conexión de red para que los cambios que hiciste en los comandos 1 y 2 se apliquen.

---

## PASO 4: Verificar que funcionó
```bash
cat /etc/resolv.conf
```

**Explicación:**
- **`cat`** = Muestra el contenido de un archivo en la pantalla.
- **`/etc/resolv.conf`** = Es el archivo donde están los DNS.

**Lo que deberías ver:**
```
nameserver 8.8.8.8
nameserver 1.1.1.1
```

Si ves eso, ¡funcionó!

---

## PASO 5: El plan B (el que ya conocés)

Si después de todo esto el archivo sigue cambiando, podés usar el comando que ya conocés:

```bash
sudo chattr +i /etc/resolv.conf
```

**Explicación EXTRA-DETALLADA:**
- **`sudo`** = Ejecutar como superusuario.
- **`chattr`** = Es un comando que cambia "atributos" de archivos en Linux (no confundir con `chmod` que cambia permisos).
- **`+i`** = Le agrega el atributo "i" (inmutable). El `+` significa "agregar".
- **`/etc/resolv.conf`** = El archivo que querés hacer inmutable.

**¿Qué hace?** Hace que NADIE pueda modificar, renombrar o borrar ese archivo, ni siquiera el usuario root (administrador) hasta que se quite ese atributo.

**Para deshacerlo (si algún día necesitás cambiarlo):**
```bash
sudo chattr -i /etc/resolv.conf
```
(el `-i` significa "quitar el atributo i")

---

## RESUMEN de todo lo que aprendiste:

1. **`systemctl status`** = Ver si un servicio está activo.
2. **`nmcli connection show`** = Ver todas tus conexiones de red y sus nombres.
3. **Cómo identificar tu conexión real**: Buscá la que dice TYPE=ethernet (no la que dice loopback).
4. **`nmcli connection modify`** = Cambiar configuraciones de una conexión.
5. **`ipv4.dns`** = Los DNS que querés usar.
6. **`ipv4.ignore-auto-dns yes`** = Ignorar los DNS automáticos.
7. **`nmcli connection down/up`** = Reiniciar la conexión para aplicar cambios.
8. **`cat /etc/resolv.conf`** = Ver qué DNS tenés actualmente.
9. **`chattr +i/-i`** = Hacer inmutable o deshacer inmutable un archivo.

---


