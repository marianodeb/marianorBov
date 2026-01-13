## **`chown`**

---

### **1. Significado**

`chown` (**Change Owner**) es un comando para **cambiar el propietario y/o grupo** de archivos o directorios. Es crucial para administrar permisos en sistemas multiusuario o servicios como servidores web.

---

### **2. Uso**

- Asignar un nuevo propietario o grupo a un recurso.  
- Modificar recursivamente la propiedad de directorios y su contenido.  
- Configurar archivos para servicios que requieren permisos específicos (ej: Apache/Nginx).  
- Corregir problemas de acceso cuando un usuario no puede leer/escribir archivos.

---

### **3. Sintaxis básica**

```bash
chown [opciones] <usuario[:grupo]> <archivo(s)_o_directorio(s)>
```

---

### **4. Opciones principales**

| Opción              | Descripción                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| `-R` o `--recursive` | Cambia la propiedad recursivamente (subdirectorios y contenido).          |
| `-v`                | Modo verbose: muestra los cambios realizados.                              |
| `-c`                | Similar a `-v`, pero solo muestra cambios efectivos.                       |
| `--reference=<archivo>` | Copia el usuario/grupo de un archivo de referencia.                       |
| `-h`                | Modifica enlaces simbólicos (no el archivo al que apuntan).                |
| `--from=<usuario:grupo>` | Cambia solo si el usuario/grupo actual coincide.                         |

---

### **5. Modos de especificación**

- **Usuario y grupo**: `usuario:grupo` (ej: `juan:developers`).  
- **Solo usuario**: `usuario` (ej: `juan`).  
- **Solo grupo**: `:grupo` (ej: `:www-data`).  
- **Usar UID/GID**: `1001:1002` (en lugar de nombres).

---

### **6. Ejemplos**

#### **Ejemplos simples**

1. **Cambiar propietario de un archivo**:

```bash
sudo chown juan archivo.txt  
```

2. **Cambiar grupo de un archivo**:

```bash
sudo chown :developers script.sh  
```

3. **Cambiar usuario y grupo simultáneamente**:

```bash
sudo chown juan:www-data /var/www/mi_sitio  
```

---

#### **Ejemplos complejos**

1. **Cambio recursivo para un directorio**:

```bash
sudo chown -R juan:developers proyecto/  # Aplica a todos los archivos dentro  
```

2. **Copiar propietario de otro archivo**:

```bash
sudo chown --reference=ejemplo.txt nuevo_archivo.txt  
```

3. **Usar UID y GID numéricos**:

```bash
sudo chown 1001:1002 backup.tar.gz  # Usuario UID=1001, grupo GID=1002  
```

4. **Cambiar solo si el propietario actual es "root"**:

```bash
sudo chown --from=root:root juan:juan config.ini  
```

5. **Modificar enlace simbólico (sin afectar el archivo original)**:

```bash
sudo chown -h juan enlace_simbolico  
```

---

### **7. Información adicional**

#### **Consideraciones clave**

- **Permisos necesarios**: Solo el **root** (o con `sudo`) puede cambiar el propietario de un archivo.  
- **Servicios comunes**:  
  - Servidores web (ej: `www-data` en Ubuntu para Apache/Nginx).  
  - Bases de datos (ej: `mysql:mysql` para MySQL/MariaDB).  
- **Seguridad**:  
  - Evitar asignar propiedad `root` a archivos innecesariamente.  
  - Usar grupos para gestionar accesos compartidos (ej: `developers`).  

#### **Comandos relacionados**

- `chmod`: Cambiar permisos.  
- `chgrp`: Cambiar solo el grupo (equivalente a `chown :grupo`).  
- `ls -l`: Ver propietario y grupo actual.  

---

### **8. Tabla de referencia rápida**

| Comando                          | Acción                                      |  
|----------------------------------|---------------------------------------------|  
| `chown usuario archivo`          | Cambia solo el propietario.                |  
| `chown :grupo archivo`           | Cambia solo el grupo.                      |  
| `chown usuario: archivo`         | Cambia usuario y establece su grupo primario. |  
| `chown usuario:grupo archivo`    | Cambia usuario y grupo específicos.        |  

---

### **9. Casos prácticos**

- **Servidor web**:

```bash
sudo chown -R www-data:www-data /var/www/html  # Para que Apache/Nginx acceda a los archivos  
```

- **Colaboración en proyectos**:

```bash
sudo chown -R :equipo_proyecto /opt/proyecto  # Todos en el grupo "equipo_proyecto" tienen acceso  
```

- **Corregir permisos de usuario**:
```bash
sudo chown -R $USER:$USER ~/documentos  # Asigna propiedad al usuario actual  
```

---

### **10. Notas finales**

- **Enlaces simbólicos vs archivos**: Por defecto, `chown` cambia el destino del enlace. Usa `-h` para modificar el enlace en sí.  
- **Archivos ocultos**: En directorios, `chown -R` afecta también a archivos ocultos (ej: `.config`).  
- **Ver cambios**: Usa `ls -l` para confirmar el nuevo propietario/grupo.  

Documentación completa:

```bash
man chown  
```  


