
## `chmod`

---

### **1. Significado**

`chmod` (**Change Mode**) es un comando para **cambiar los permisos** de acceso a archivos o directorios. Controla quién puede **leer**, **escribir** o **ejecutar** un recurso, asignando permisos al **propietario**, **grupo** y **otros usuarios**.

---

### **2. Uso**

- Modificar permisos de archivos/directorios usando **modo simbólico** (ej: `u+x`) o **modo numérico** (ej: `755`).  
- Aplicar permisos recursivamente a subdirectorios.  
- Configurar permisos especiales como **setuid**, **setgid** o **sticky bit**.  
- Restringir o permitir accesos en entornos multiusuario.

---

### **3. Sintaxis básica**

```bash
chmod [opciones] <modo> <archivo(s)_o_directorio(s)>
```

---

### **4. Opciones principales**

| Opción          | Descripción                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| `-R` o `--recursive` | Aplica permisos recursivamente a subdirectorios y su contenido.           |
| `-v`            | Modo verbose: muestra los cambios realizados.                              |
| `-c`            | Similar a `-v`, pero solo muestra cambios efectivos.                       |
| `--reference=<archivo>` | Copia los permisos de un archivo de referencia.                           |
| `-f`            | Suprime mensajes de error (force).                                         |

---

### **5. Modos de permisos**

#### **A. Modo simbólico**

- **Quién**: `u` (usuario), `g` (grupo), `o` (otros), `a` (todos).  
- **Operadores**: `+` (agregar), `-` (quitar), `=` (establecer).  
- **Permisos**: `r` (lectura), `w` (escritura), `x` (ejecución).  

#### **B. Modo numérico**

- **Valores**: `4` (lectura), `2` (escritura), `1` (ejecución).  
- **Suma**: `7` (4+2+1: rwx), `6` (4+2: rw-), `5` (4+1: r-x), etc.  
- **Estructura**: 3 dígitos (propietario, grupo, otros). Ej: `755`.  

---

### **6. Ejemplos**

#### **Ejemplos simples**

1. **Dar permiso de ejecución al propietario**:

```bash
chmod u+x script.sh  
```

2. **Permisos clásicos para un archivo (rw-r--r--)**:

```bash
chmod 644 archivo.txt  
```

3. **Permisos para directorio (rwxr-xr-x)**:

```bash
chmod 755 directorio/  
```

---

#### **Ejemplos complejos**

1. **Permisos recursivos para un proyecto web**:

```bash
chmod -R 755 /var/www/mi_sitio  # Directorios: rwxr-xr-x  
chmod -R 644 /var/www/mi_sitio/*.html  # Archivos: rw-r--r--  
```

2. **Permisos simbólicos combinados**:

```bash
chmod u=rwx,g=rx,o= private_file  # rwxr-x--- (750)  
```

3. **Setuid (permiso especial para ejecutar como propietario)**:

```bash
chmod u+s /usr/bin/mi_programa  # El programa se ejecuta con permisos del dueño  
```

4. **Sticky bit en directorios (solo el dueño puede borrar)**:

```bash
chmod +t /tmp/mi_directorio  # Permiso "t" en otros: drwxrwxrwt  
```

5. **Copiar permisos de otro archivo**:

```bash
chmod --reference=permisos_ejemplo.txt nuevo_archivo.txt  
```

---

### **7. Información adicional**

#### **Permisos especiales**

| Permiso | Símbolo | Número | Descripción                              |
|---------|---------|--------|------------------------------------------|
| **Setuid** | `s`    | `4000` | Ejecuta el archivo como su propietario.  |
| **Setgid** | `s`    | `2000` | Ejecuta el archivo como el grupo propietario. |
| **Sticky Bit** | `t` | `1000` | Restringe borrado en directorios (solo el dueño puede eliminar sus archivos). |

**Ejemplo numérico con Setuid**:

```bash
chmod 4755 script.sh  # -rwsr-xr-x  
```

---

#### **Consideraciones de seguridad**

- **Evitar `777`**: `chmod 777` da acceso total a todos (riesgo de seguridad).  
- **Archivos sensibles**: Configura permisos estrictos en `/etc/`, `~/.ssh/`, o claves privadas.  
- **Directorios vs Archivos**: Los directorios necesitan `x` para acceder a su contenido.  

#### **Comando relacionado**: `chown`

Cambia el propietario y grupo de un archivo/directorio:

```bash
chown usuario:grupo archivo  
```

---

### **8. Tabla de referencia rápida**

| Número | Permiso | Símbolo    |  
|--------|---------|------------|  
| 0      | `---`   | Ninguno    |  
| 1      | `--x`   | Ejecución  |  
| 2      | `-w-`   | Escritura  |  
| 3      | `-wx`   | Escritura + Ejecución |  
| 4      | `r--`   | Lectura    |  
| 5      | `r-x`   | Lectura + Ejecución |  
| 6      | `rw-`   | Lectura + Escritura |  
| 7      | `rwx`   | Todos      |  

---

### **9. Comando para ver permisos actuales**

```bash
ls -l archivo  
# Ejemplo de salida: -rwxr-xr-- 1 user group 0 Jan 1 12:00 archivo  
```

---

### **10. Notas finales**

- **Predeterminados**: Los permisos nuevos dependen del `umask` del usuario.  
- **Herramientas gráficas**: Alternativas como `chmod` en GUI (ej: administradores de archivos).  
- **Soporte extendido**: Para ver todas las opciones, ejecuta:

```bash
man chmod  
```

## PErmisos especiales

### **1. ¿Qué son los permisos especiales?**

Son permisos que van más allá de los básicos (lectura, escritura, ejecución). Hay 3 tipos:

1. **SUID** (Set User ID): Permite ejecutar un archivo con los privilegios del **propietario**.
2. **SGID** (Set Group ID): Permite ejecutar un archivo con los privilegios del **grupo** o heredar el grupo del directorio padre.
3. **Sticky Bit**: En directorios, restringe la eliminación de archivos (solo el dueño o root puede borrarlos).


### **2. Usuarios de ejemplo**

Supongamos 3 usuarios en un sistema:

- **Alice**: Dueña de un script administrativo.
- **Bob**: Miembro del grupo `developers`.
- **Charlie**: Usuario común sin privilegios especiales.


### **3. Casos prácticos con permisos especiales**

#### **A. Permiso SUID (Ejemplo: `chmod u+s`)**

- **Para qué sirve**: Ejecutar un archivo con los permisos de su **propietario**, aunque otro usuario lo ejecute.
- **Quién lo controla**: El dueño del archivo o root.

**Ejemplo**:

- Alice crea un script `/usr/bin/backup` que solo root puede modificar.
- Alice quiere que Bob y Charlie puedan ejecutarlo temporalmente como root.

```bash
sudo chmod u+s /usr/bin/backup  # Aplica SUID
ls -l /usr/bin/backup
# Resultado: -rwsr-xr-x 1 root root ...
```

- Ahora, cuando Bob o Charlie ejecuten `backup`, lo harán con permisos de **root** (¡Cuidado con esto por seguridad!).

#### **B. Permiso SGID (Ejemplo: `chmod g+s`)**

- **Para qué sirve**:

  - En **archivos**: Ejecutar con permisos del grupo propietario.
  - En **directorios**: Los archivos creados heredan el grupo del directorio (no el del usuario).

**Ejemplo**:

- Directorio `/projects` con grupo `developers`.
- Aplicamos SGID al directorio:

```bash
sudo chmod g+s /projects
ls -ld /projects
# Resultado: drwxr-sr-x 2 root developers ...
```

- Si Bob crea un archivo en `/projects`, su grupo será `developers` (no su grupo primario).
- Alice (si es parte de `developers`) puede editar los archivos de Bob sin problemas.

#### **C. Sticky Bit (Ejemplo: `chmod +t`)**

- **Para qué sirve**: En directorios, evita que usuarios eliminen archivos de otros (solo el dueño o root puede borrarlos).
- **Quién lo controla**: Root o el dueño del directorio.

**Ejemplo**:

- Directorio `/public` donde todos pueden escribir, pero no borrar archivos ajenos.

```bash
sudo chmod +t /public
ls -ld /public
# Resultado: drwxrwxrwt 2 root root ...
```

- Si Charlie crea `file.txt` en `/public`, Bob no podrá borrarlo (aunque tenga permisos de escritura en el directorio).

### **4. Escenarios combinados con los 3 usuarios**

#### **Escenario 1: SUID + SGID**

- Archivo `/usr/bin/update_system` (propietario: root, grupo: admins).
- Permisos: `-rwsr-sr-x` (SUID y SGID activos).
- Charlie ejecuta `update_system`: 
  - El proceso corre como **root** (SUID) y con el grupo **admins** (SGID).

#### **Escenario 2: SGID en directorio compartido**

- Directorio `/team_docs` con SGID y grupo `team`.
- Alice (grupo `team`) crea `report.doc` en `/team_docs`.
- Bob (grupo `team`) puede editar `report.doc` porque hereda el grupo `team`.

#### **Escenario 3: Sticky Bit en /tmp**

- Directorio `/tmp` con sticky bit: `drwxrwxrwt`.
- Charlie crea `/tmp/charlie_temp.txt`.
- Bob no puede borrarlo, aunque tenga acceso al directorio.

### **5. Comandos clave**

- Asignar permisos especiales:
  - SUID: `chmod u+s archivo`
  - SGID: `chmod g+s directorio`
  - Sticky Bit: `chmod +t directorio`
- Ver permisos: Busca `s`, `S`, `t`, o `T` en `ls -l`.

### **6. Seguridad**
- **SUID/SGID mal usados** son un riesgo: ¡No los asignes a archivos inseguros!
- **Sticky Bit** es útil en directorios públicos como `/tmp`.

---

### **1. Símbolos de los permisos especiales**

Los permisos especiales **no tienen su propia "sección"** como `rwx`, sino que **reemplazan la letra `x`** en los permisos básicos (cuando están activos). Aquí la clave:

| Permiso Especial | Símbolo | Posición en `ls -l` | Ejemplo Visual |
|-------------------|---------|---------------------|----------------|
| **SUID**          | `s` o `S` | Reemplaza la `x` del **usuario** (primer trio). | `-rwsr-xr-x` |
| **SGID**          | `s` o `S` | Reemplaza la `x` del **grupo** (segundo trio). | `-rwxr-sr-x` |
| **Sticky Bit**    | `t` o `T` | Reemplaza la `x` de **otros** (tercer trio). | `drwxrwxrwt` |

#### **¿`s` minúscula o `S` mayúscula?**

- **`s` o `t` minúscula**: El permiso de ejecución (`x`) **está activo** *y* el permiso especial también.
- **`S` o `T` mayúscula**: El permiso de ejecución (`x`) **no está activo**, pero el permiso especial sí.

**Ejemplo**:

- `-rwsr-xr-x`: SUID activo + usuario tiene ejecución (`x`).
- `-rwSr--r--`: SUID activo + usuario **no** tiene ejecución (`x`).

### **2. ¿Dónde se aplican los permisos especiales?**

Tienes razón: los permisos especiales están ligados a **u** (usuario), **g** (grupo), y **o** (otros), pero cada uno tiene su propio permiso especial:

| Permiso Especial | Se aplica a | Comando para activar |
|-------------------|------------|----------------------|
| **SUID**          | Usuario (u) | `chmod u+s archivo` |
| **SGID**          | Grupo (g)  | `chmod g+s directorio` |
| **Sticky Bit**    | Otros (o)  | `chmod o+t directorio` |

#### **Ejemplo 1: SUID en un archivo binario**

```bash
chmod u+s /usr/bin/mi_script
ls -l /usr/bin/mi_script
# Resultado: -rwsr-xr-x 1 root root ...
```

- La `s` en el primer trio (usuario) indica **SUID activo**.

#### **Ejemplo 2: SGID en un directorio**

```bash
chmod g+s /equipo
ls -ld /equipo
# Resultado: drwxr-sr-x 2 root developers ...
```

- La `s` en el segundo trio (grupo) indica **SGID activo**.

#### **Ejemplo 3: Sticky Bit en /tmp**

```bash
chmod o+t /tmp
ls -ld /tmp
# Resultado: drwxrwxrwt 10 root root ...
```

- La `t` en el tercer trio (otros) indica **Sticky Bit activo**.

### **3. ¿Por qué no hay un símbolo separado para los permisos especiales?**

Es una decisión de diseño histórico en Unix, pero puedes entenderlo así:
- Los permisos especiales **son bits adicionales** (no son parte de `rwx`).
- Ocupan el mismo espacio que la `x` para ahorrar caracteres en la visualización.

### **4. Ejemplo con tus 3 usuarios**

Imaginemos un archivo `auditar.log` con los siguientes permisos:

```bash
ls -l auditar.log
# Resultado: -rwsr-Sr-T 1 Alice developers 0 Jul 10 12:00 auditar.log
```

- **SUID**: `s` en usuario → Cualquiera que ejecute el archivo lo hará como **Alice**.
- **SGID**: `S` en grupo → SGID activo, pero el grupo **no tiene ejecución**.
- **Sticky Bit**: `T` en otros → Sticky Bit activo, pero otros **no tienen ejecución**.

### **5. ¿Cómo se representan en modo numérico (octal)?**

Los permisos especiales se agregan como un cuarto dígito al inicio:

- **SUID**: `4` (ej: `4755`).
- **SGID**: `2` (ej: `2775`).
- **Sticky Bit**: `1` (ej: `1777`).

**Ejemplos**:

```bash
chmod 4755 archivo  # SUID + rwxr-xr-x
chmod 2770 directorio  # SGID + rwxrws---
chmod 1777 /publico  # Sticky Bit + rwxrwxrwt
```

### **6. ¿Por qué no hay permisos especiales para "otros"?**

¡Los hay! El **Sticky Bit** es el permiso especial para "otros" (se aplica con `o+t`). Pero:

- **SUID** y **SGID** están asociados a usuario y grupo.
- **Sticky Bit** es el único permiso especial para "otros", pero solo funciona en **directorios**.

### **Tabla resumen final**

| Permiso | Símbolo | Posición | Afecta a | Uso común |
|---------|---------|----------|----------|-----------|
| SUID    | `s`/`S` | Usuario  | Archivos | Ejecutar como propietario. |
| SGID    | `s`/`S` | Grupo    | Archivos/Directorios | Ejecutar como grupo o heredar grupo. |
| Sticky  | `t`/`T` | Otros    | Directorios | Evitar borrado de archivos ajenos. |

### **7. Caso hipotético según tu sugerencia**

Tú dijiste: *"rwx-rwx-rws"*. En realidad, la `s` final (en otros) no corresponde a SUID, sino al **Sticky Bit**. Pero aquí hay un error común:
- Si vieras `rwx-rwx-rws`, la `s` en el tercer trio sería **Sticky Bit**, pero en Unix, el Sticky Bit se representa con `t`, no `s`. Sería `rws` solo en usuario (SUID) o grupo (SGID).

**Corrección**:

- `rwsr-xr-x` → SUID activo.
- `rwxr-sr-x` → SGID activo.
- `rwxrwxrwt` → Sticky Bit activo.

### **Conclusión**

Sí, los permisos especiales están ligados a **u**, **g**, y **o**, pero cada uno tiene su propio tipo:

- `u+s` (SUID),
- `g+s` (SGID),
- `o+t` (Sticky Bit).

La notación con `s` y `t` en lugar de `x` es la forma que tiene Unix de decir: *"Ojo, este archivo/directorio tiene algo especial"* 😎. 


