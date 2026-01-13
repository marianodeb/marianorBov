### **Comando `cp`**

`cp` (***copy***) es un comando en sistemas Unix/Linux para **copiar archivos y directorios**. Permite duplicar contenido en la misma ubicación o en rutas diferentes. Es esencial para backups, organización de archivos o mover datos sin eliminarlos del origen.

---

### **Sintaxis básica**  

```bash
cp [OPCIONES] ORIGEN DESTINO
cp [OPCIONES] ORIGEN1 ORIGEN2 ... DIRECTORIO_DESTINO
```

---

### **Opciones comunes**  

| Opción | Descripción |  
|--------|-------------|  
| `-r`   | Copia **directorios recursivamente** (incluyendo subdirectorios). |  
| `-i`   | Modo interactivo: **pregunta antes de sobrescribir** archivos. |  
| `-v`   | Modo **verbose**: muestra detalles de lo que se copia. |  
| `-n`   | **No sobrescribe** archivos existentes en el destino. |  
| `-p`   | **Preserva** atributos (permisos, fecha, propietario). |  
| `-u`   | Copia solo si el origen es **más reciente** que el destino. |  

---

### **Ejemplos simples**  

#### 1. **Copiar un archivo a otra ubicación**  

```bash
cp documento.txt /backup/
```

- **Explicación:** Copia `documento.txt` al directorio `/backup/`.  
- **Resultado:**  

```
/backup/documento.txt
```

#### 2. **Copiar y renombrar el archivo**  

```bash
cp foto.jpg vacaciones_2023.jpg
```

- **Explicación:** Copia `foto.jpg` a `vacaciones_2023.jpg` en el mismo directorio.

#### 3. **Copiar múltiples archivos a un directorio**  

```bash
cp *.txt /proyecto/docs/
```

- **Explicación:** Copia todos los archivos `.txt` al directorio `/proyecto/docs/`.

#### 4. **Copiar un directorio (con `-r`)**  

```bash
cp -r musica/ /backup/
```

- **Explicación:** Copia el directorio `musica/` y todo su contenido a `/backup/`.

---

### **Ejemplos complejos**  

#### 1. **Preservar permisos y fechas (`-p`)**  

```bash
cp -p -r /home/usuario/config/ /backup/
```

- **Explicación:**  

  Copia el directorio `config/` manteniendo los permisos y fechas originales.  
  
- **Uso típico:** Backups profesionales o migraciones.

#### 2. **Copiar solo archivos nuevos o modificados (`-u`)**  
```bash
cp -u *.log /backup/logs/
```

- **Explicación:**  

Copia archivos `.log` a `/backup/logs/` solo si son más recientes que los del destino.

#### 3. **Copiar interactivamente (preguntar antes de sobrescribir)** 
 
```bash
cp -i *.conf /etc/
```
- **Resultado:**  

```
cp: ¿sobrescribir '/etc/apache.conf'? (s/n)
```

#### 4. **Combinar con `find` para copiar archivos específicos**  

```bash
find . -name "*.pdf" -exec cp {} /backup/docs/ \;
```
- **Explicación:**  

Busca todos los archivos `.pdf` en el directorio actual y los copia a `/backup/docs/`.

#### 5. **Copiar excluyendo ciertos archivos**  

```bash
cp -r * /backup/ --exclude="*.tmp"
```
- **Explicación:**  

Copia todo el contenido del directorio actual a `/backup/`, excepto archivos `.tmp`.

---

### **Notas importantes**  
- **Sobrescritura silenciosa:**  

  Por defecto, `cp` **sobrescribe archivos** sin avisar. Usa `-i` o `-n` para evitar pérdidas de datos.  
  
- **Destino debe existir:**  

  Si copias múltiples archivos, el destino **debe ser un directorio existente**.  
  
- **Enlaces simbólicos:**  

  Usa `-L` para copiar el archivo original en lugar del enlace.  

---

### **Errores comunes**  

1. **Copiar un directorio sin `-r`:**  

```bash
cp documentos/ /backup/  # Error: Omite "-r" para directorios.
```
   
**Solución:**  
   
```bash
cp -r documentos/ /backup/
```

2. **Copiar a una ruta que no existe:**  

```bash
cp archivo.txt /ruta/inexistente/  # Error: Directorio no existe.
```
   
**Solución:**  
   
```bash
mkdir -p /ruta/inexistente/ && cp archivo.txt /ruta/inexistente/
```

---

### **Consejos avanzados**  

- **Copiar entre servidores con `scp`:**  

  Si necesitas copiar archivos a otro servidor, usa:  
  
```bash
scp -r archivo.txt usuario@servidor:/ruta/destino/
```
  
- **Alternativa para sincronización:**  

  Usa `rsync` para copias eficientes (solo cambios) y opciones avanzadas:  
  
```bash
rsync -avh origen/ destino/
```

---

### **Resumen de flujo de trabajo**  

1. **Backup rápido:**  

```bash
cp -rpv /datos/ /backup/  # Copia recursiva, preserva atributos y muestra detalles.
```
   
2. **Actualizar archivos modificados:** 
 
```bash
cp -u *.js /proyecto/web/  # Solo archivos JavaScript actualizados.
```
   
3. **Organizar fotos:**  

```bash
cp -i /cámara/*.jpg /fotos/2023/  # Pregunta antes de sobrescribir.
```
   
 **Tip clave:** Si trabajas con archivos críticos, usa siempre `-i` (interactivo) o `-n` (no sobrescribir) para evitar errores.
