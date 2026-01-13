## **Comando `cksum`**

`cksum` es un comando en sistemas Unix/Linux que **calcula el checksum CRC (Cyclic Redundancy Check)** de uno o más archivos. Este checksum es un valor numérico que se usa para verificar la **integridad de un archivo**, detectando cambios accidentales (como errores de transmisión o corrupción).  
- **Diferencia con otros checksums:**  

- `cksum` usa el algoritmo **CRC-32**, menos seguro que otros (como SHA-256 o MD5), pero rápido y útil para verificaciones básicas.  
- No es recomendable para seguridad (no detecta cambios maliciosos), sino para errores no intencionales.

---

### **Sintaxis**  

```bash
cksum [ARCHIVO1] [ARCHIVO2] ...  
```

#### **Opciones comunes**  

En la mayoría de implementaciones, `cksum` no tiene opciones avanzadas. Algunas versiones soportan:  
| Opción       | Descripción                          |  
|--------------|--------------------------------------|  
| `--help`     | Muestra ayuda.                       |  
| `--version`  | Muestra la versión del comando.      |  

---

### **¿Cómo se utiliza?**  

- **Propósito principal:**  

- Verificar si un archivo ha sido modificado o dañado.  
- Comparar archivos en diferentes momentos o ubicaciones.  

- **Formato de salida:**  

```  
[CHECKSUM_CRC] [BYTES_DEL_ARCHIVO] [NOMBRE_ARCHIVO]  
```

---

### **Ejemplos simples**  

#### 1. **Calcular el checksum de un archivo**  

```bash
cksum documento.txt
```

**Salida:**  

```
3080464349 1045 documento.txt  
```

- **3080464349**: Checksum CRC.  
- **1045**: Tamaño en bytes.  

#### 2. **Comparar dos archivos**  

```bash
cksum archivo_original.txt archivo_copia.txt
```

**Salida si son iguales:**  

```
3080464349 1045 archivo_original.txt  
3080464349 1045 archivo_copia.txt  
```

**Salida si son diferentes:**  

```
3080464349 1045 archivo_original.txt  
1234567890 1045 archivo_copia.txt  # Checksum distinto = archivo modificado.
```

#### 3. **Verificar múltiples archivos**  

```bash
cksum *.jpg  # Checksum de todos los archivos .jpg en el directorio.
```

---

### **Ejemplos complejos**  

#### 1. **Guardar checksums para verificación futura**  

```bash
# Paso 1: Generar un registro de checksums.
cksum *.txt > checksums.txt

# Paso 2 (días después): Verificar si algún archivo cambió.
cksum -c checksums.txt  # Nota: En algunas versiones, `-c` no está disponible.  
```
- **Alternativa si `-c` no funciona:**  

```bash
cksum *.txt > nuevos_checksums.txt  
diff checksums.txt nuevos_checksums.txt  
```

#### 2. **Usar con `find` para verificar archivos en subdirectorios**  

```bash
find . -type f -name "*.log" -exec cksum {} \;  
```
**Salida:**  

```
3080464349 1045 ./dir1/error.log  
9876543210 2048 ./dir2/access.log  
```

#### 3. **Integrar en scripts para monitorear cambios**  

```bash
#!/bin/bash  
checksum_original=$(cksum backup.tar | awk '{print $1}')  
# ... (transferir backup.tar)  
checksum_nuevo=$(cksum backup.tar | awk '{print $1}')  

if [ "$checksum_original" != "$checksum_nuevo" ]; then  
  echo "¡Error: El archivo se corrompió durante la transferencia!"  
fi  
```

---

### **Notas importantes**  

- **Límites del CRC-32:**  
  - Puede haber **colisiones** (dos archivos diferentes con el mismo CRC).  
  - No es seguro para proteger contra modificaciones intencionales (usa `sha256sum` o `md5sum` para eso).  
- **Tamaño del archivo:**  
  - El checksum depende del contenido y tamaño en bytes. Si el tamaño cambia, el CRC también.  

---

### **Errores comunes**  

1. **Usar `cksum` para verificar archivos comprimidos:**  
   Si descomprimes un archivo y luego lo vuelves a comprimir, el CRC del archivo comprimido cambiará, aunque el contenido sea el mismo.  
2. **Comparar checksums entre sistemas diferentes:**  
   Algunas implementaciones de `cksum` varían entre sistemas operativos. Usa `md5sum` si necesitas portabilidad.  

---

### **Consejos**  

- **Para mayor seguridad:**  

```bash
md5sum archivo.txt    # Algoritmo MD5 (mejor que CRC-32).  
sha256sum archivo.txt # Algoritmo SHA-256 (recomendado para seguridad).  
```

- **Verificar integridad de descargas:**  

Si un sitio web proporciona un CRC, usa:  

```bash
cksum archivo_descargado.iso  
# Compara el resultado con el CRC publicado.  
```

---

### **Resumen**  

- **¿Cuándo usar `cksum`?**  
  - Verificación rápida de archivos en transferencias locales.  
  - Detectar corrupción accidental en backups o copias.  
- **¿Cuándo evitar `cksum`?**  
  - Si necesitas garantizar autenticidad o seguridad (ej: archivos críticos).
  
