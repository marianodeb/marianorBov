¡Claro! Aquí tienes toda la información sobre el comando **`wget`**, explicado de forma detallada y práctica. 🌐⬇️  

---

### **1. Significado**  
**`wget`** (**W**eb **Get**) es una herramienta de línea de comandos para **descargar archivos desde internet** usando protocolos como HTTP, HTTPS y FTP. Es **no interactivo** (ideal para scripts), **robusto** (resume descargas interrumpidas) y soporta descargas recursivas (para copiar sitios web completos).

---

### **2. Uso**  
- Descargar archivos individuales.  
- Descargar sitios web completos (mirroring).  
- Descargar en segundo plano.  
- Limitar velocidad de descarga.  
- Descargar múltiples archivos (usando listas).  
- Funciona en redes inestables (reintenta automáticamente).  

---

### **3. Sintaxis General**  
```bash
wget [OPCIONES] [URL]
```  

---

### **4. Opciones Principales**  

| Opción                  | Descripción                                                                 |  
|-------------------------|-----------------------------------------------------------------------------|  
| `-O <nombre>`           | Guarda el archivo con un nombre específico.                                |  
| `-c`                    | Continúa una descarga interrumpida (*resume*).                             |  
| `-r` o `--recursive`    | Descarga recursiva (para directorios o sitios web).                        |  
| `-np`                   | No subir a directorios padres (*no parent*).                               |  
| `-P <directorio>`       | Guarda los archivos en un directorio específico.                           |  
| `-b`                    | Ejecuta en segundo plano (*background*).                                   |  
| `-i <archivo.txt>`      | Lee URLs desde un archivo de texto.                                        |  
| `--limit-rate=<veloc>`  | Limita la velocidad de descarga (ej: `--limit-rate=500k`).                 |  
| `-q`                    | Modo silencioso (*quiet*).                                                 |  
| `--user=<usuario>`      | Usuario para autenticación HTTP/FTP.                                       |  
| `--password=<contr>`    | Contraseña para autenticación (⚠️ **evita usarlo en scripts**).            |  
| `--no-check-certificate`| Ignora la verificación de certificados SSL (útil para HTTPS autofirmados). |  
| `-U <agente>`           | Define un User-Agent personalizado (ej: `-U "Mozilla/5.0"`).              |  

---

### **5. Ejemplos**  

#### **Ejemplos Simples**  
1. **Descargar un archivo**:  
   ```bash
   wget https://ejemplo.com/archivo.zip
   ```  

2. **Guardar con nombre personalizado**:  
   ```bash
   wget -O backup.iso https://ejemplo.com/descargas/version-latest
   ```  

3. **Continuar descarga interrumpida**:  
   ```bash
   wget -c https://ejemplo.com/pelicula.mkv
   ```  

4. **Descargar en un directorio específico**:  
   ```bash
   wget -P ~/Descargas/ https://ejemplo.com/imagen.jpg
   ```  

---

#### **Ejemplos Avanzados**  
1. **Descargar un sitio web completo (mirror)**:  
   ```bash
   wget -r -np -k -p https://ejemplo.com/
   ```  
   - `-r`: Recursivo.  
   - `-np`: No subir a directorios padres.  
   - `-k`: Convierte enlaces para visualización local.  
   - `-p`: Descarga todos los recursos (CSS, imágenes).  

2. **Descargar múltiples URLs desde un archivo**:  
   ```bash
   wget -i lista_urls.txt
   ```  

3. **Limitar velocidad a 1 MB/s**:  
   ```bash
   wget --limit-rate=1m https://ejemplo.com/video.mp4
   ```  

4. **Autenticación HTTP/FTP**:  
   ```bash
   wget --user=admin --password=secreto https://ejemplo.com/privado.zip
   ```  

5. **Descargar en segundo plano**:  
   ```bash
   wget -b https://ejemplo.com/archivo_grande.iso
   ```  

6. **Ignorar certificado SSL**:  
   ```bash
   wget --no-check-certificate https://sitio-con-certificado-invalido.com
   ```  

7. **User-Agent personalizado**:  
   ```bash
   wget -U "Mozilla/5.0 (Windows NT 10.0; Win64; x64)" https://ejemplo.com
   ```  

---

### **6. Información Adicional**  

#### **¿Cuándo usar `wget` vs `curl`?**  
- **`wget`**: Ideal para descargas recursivas, mirroring, y scripts no interactivos.  
- **`curl`**: Mejor para interactuar con APIs HTTP, enviar datos, y usar en pipelines.  

#### **Ventajas de `wget`**  
- Soporte nativo para descargas recursivas.  
- Reintentos automáticos en fallos.  
- Funciona en segundo plano.  

#### **Seguridad**  
- **HTTPS**: Usa certificados SSL por defecto (a menos que uses `--no-check-certificate`).  
- **Contraseñas**: Evita usar `--password` en scripts (mejor usa archivos de configuración o variables de entorno).  

---

### **7. Errores Comunes**  
- **Descargar sin permisos**: Si el directorio de destino no tiene permisos de escritura.  
- **URL mal formada**: Asegúrate de incluir `http://` o `https://`.  
- **Recursividad sin límites**: Usa `-l` para limitar la profundidad (ej: `-l 2`).  

---

### **8. Diagrama de Flujo de `wget`**  
```  
[URL] → [Resolución DNS] → [Conexión HTTP(S)/FTP] → [Descarga] → [Guardar en disco]  
```  

---

### **9. Comandos Útiles para Debuggear**  
- **Ver detalles de la descarga**:  
  ```bash
  wget -o log.txt https://ejemplo.com/archivo.txt
  ```  
- **Simular descarga (sin guardar)**:  
  ```bash
  wget --spider https://ejemplo.com/
  ```  

---

¿Necesitas ayuda para un caso específico o más ejemplos? 😊 ¡Estoy aquí!
