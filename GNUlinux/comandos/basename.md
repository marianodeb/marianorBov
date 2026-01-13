## **Comando `basename`**

`basename` es un comando en sistemas Unix/Linux que extrae el **nombre base** de una ruta de archivo o directorio, eliminando las rutas parentales (directorios) y, opcionalmente, un sufijo específico. Es útil para manipular nombres de archivos en scripts o terminal.  

**Ejemplo básico:**  

Si tienes la ruta `/home/usuario/documento.txt`, `basename` devuelve `documento.txt` (o `documento` si eliminas el sufijo `.txt`).

---

#### **¿Cómo utilizarlo?**  

- **Propósito principal:**  
  - Extraer el nombre de un archivo o directorio de una ruta completa.  
  - Eliminar extensiones de archivo (sufijos) si se especifican.  
- **Escenarios comunes:**  
  - Procesar rutas en scripts de shell.  
  - Renombrar archivos masivamente eliminando extensiones.  

---

#### **Sintaxis**  

```bash
basename [OPCIONES] NOMBRE [SUFIJO]
basename [OPCIONES] NOMBRE...
```

#### **Opciones principales**  
| Opción | Descripción                                                                 |
|--------|-----------------------------------------------------------------------------|
| `-a`   | Soporta múltiples rutas como argumentos (ej: `basename -a /ruta1 /ruta2`). |
| `-s`   | Elimina un sufijo específico (ej: `.txt`).                                 |
| `-z`   | Separa los resultados con caracteres nulos (útil para scripts).            |

---

#### **Ejemplos**  

1. **Extraer el nombre base de una ruta**  

```bash
basename /home/usuario/fotos/vacaciones.jpg
```
   
   **Salida:**  
   
```
vacaciones.jpg
```

2. **Eliminar un sufijo**  

```bash
basename /home/usuario/fotos/vacaciones.jpg .jpg
```
   
   **Salida:**  
   
```
vacaciones
```

3. **Múltiples rutas con `-a`**  

```bash
basename -a /var/log/syslog /tmp/backup.tar.gz
```
   
   **Salida:**  
   
```
syslog
backup.tar.gz
```

4. **Eliminar sufijo en múltiples archivos**  

```bash
basename -s .txt archivo1.txt archivo2.txt
```
   
**Salida:**  
   
```
archivo1
archivo2
```

5. **Usar `-z` para scripts (separación con nulos)**  

```bash
basename -z /ruta/archivo.conf
```
   
   **Salida:**  
   
```
archivo.conf%  # (El % indica un carácter nulo, no visible en terminal).
```

---

#### **Notas importantes**  

- **Sensibilidad a mayúsculas:** El sufijo debe coincidir exactamente (ej: `.TXT` no eliminará `.txt`).  
- **Rutas que terminan en `/`:** Si la ruta termina en `/`, `basename` ignora el último slash.  

```bash
basename /home/usuario/  # Salida: usuario
```
  
- **Relación con `dirname`:** Mientras `basename` extrae el nombre del archivo, `dirname` extrae la ruta parental.  

```bash
dirname /home/usuario/fotos/vacaciones.jpg  # Salida: /home/usuario/fotos
```

---

#### **Consejo**  

Úsalo en combinación con otros comandos para manipular archivos en lotes. Por ejemplo, eliminar la extensión `.bak` de varios archivos:  

```bash
for archivo in *.bak; do
  nuevo_nombre=$(basename $archivo .bak)
  mv $archivo $nuevo_nombre
done
```

**Tip adicional:** Si necesitas procesar rutas complejas, combínalo con `readlink -f` para obtener rutas absolutas antes de usar `basename`.
