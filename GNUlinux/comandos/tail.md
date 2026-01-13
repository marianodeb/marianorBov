
## **Comando `tail`**

`tail` es un comando en sistemas Unix/Linux que **muestra las últimas líneas o bytes de un archivo** (por defecto, las últimas 10 líneas). Es ideal para:  
- Ver el final de archivos grandes (ej: logs en tiempo real).  
- Monitorear cambios en archivos dinámicos.  
- Integrarse con otros comandos para análisis de datos.  

---

### **Sintaxis básica**  

```bash
tail [OPCIONES] [ARCHIVO1] [ARCHIVO2] ...
```

---

### **Opciones principales**  

| Opción | Descripción |  
|--------|-------------|  
| `-n N` | Muestra las **últimas `N` líneas** (ej: `-n 20`). |  
| `-c N` | Muestra los **últimos `N` bytes** (ej: `-c 500`). |  
| `-f`   | **Sigue** el archivo en tiempo real (actualizaciones continuas). |  
| `-F`   | Como `-f`, pero **reabre el archivo** si se borra o recrea (útil para logs rotativos). |  
| `-v`   | **Muestra el nombre del archivo** antes del contenido. |  
| `-q`   | **Oculta el nombre del archivo**. |  

---

### **Ejemplos simples**  

#### 1. **Ver las últimas 10 líneas de un archivo**  

```bash
tail servidor.log
```

#### 2. **Mostrar las últimas 5 líneas**  

```bash
tail -n 5 errores.txt
```

**Salida**:  

```
[ERROR] Conexión fallida.  
[ERROR] Tiempo de espera agotado.  
[ERROR] Servidor no responde.  
[ERROR] Disco lleno.  
[ERROR] Permiso denegado.  
```

#### 3. **Ver los últimos 200 bytes de un binario**  

```bash
tail -c 200 backup.tar.gz
```

#### 4. **Monitorear un log en tiempo real**  

```bash
tail -f /var/log/syslog
```

**Salida**:  

```
...  
[Actualización en tiempo real]  
```

---

### **Ejemplos avanzados**  

#### 1. **Ignorar las primeras `N` líneas**  

```bash
tail -n +20 datos.csv  # Muestra desde la línea 20 hasta el final.
```

#### 2. **Combinar con `grep` para filtrar errores en tiempo real**  

```bash
tail -f app.log | grep "CRITICAL"
```

#### 3. **Ver el final de múltiples archivos**  

```bash
tail -n 3 archivo1.txt archivo2.txt
```

**Salida**:  

```
==> archivo1.txt <==
Línea 8
Línea 9
Línea 10

==> archivo2.txt <==
Línea 18
Línea 19
Línea 20
```

#### 4. **Monitorear logs rotativos (ej: con logrotate)**  

```bash
tail -F /var/log/nginx/access.log  # Reabre el archivo si se reinicia el servicio.
```

#### 5. **Extraer las últimas líneas de un archivo comprimido**  

```bash
zcat access.log.1.gz | tail -n 50  # Últimas 50 líneas del log comprimido.
```

---

### **Casos de uso comunes**  

- **Depurar errores recientes**:  

```bash
tail -n 100 /var/log/auth.log | grep "Failed"  # Últimos 100 intentos fallidos de login.
```
  
- **Analizar métricas en tiempo real**:  

```bash
tail -f /var/log/metricas.csv | awk -F ',' '{print $3}'  # Tercera columna en vivo.
```
  
- **Verificar la finalización de procesos**:  

```bash
tail -n 1 resultado.txt  # Última línea de un proceso largo.
```

---

### **Errores frecuentes**  
1. **Confundir `tail` con `head`**:  

   - `tail` muestra el **final** del archivo.  
   - `head` muestra el **inicio**.  
2. **Usar `-f` sin salir**:  

```bash
tail -f archivo.log  # No olvides usar Ctrl + C para salir.
```

---

### **Consejos**  

- **Para archivos gigantes**:  

  `tail` es más eficiente que `cat` o `less`, ya que no carga todo en memoria.  
  
- **Combinar con `watch` para actualizaciones periódicas**:  

```bash
watch -n 5 "tail -n 10 status.log"  # Actualiza cada 5 segundos.
```
  
- **Alternativa avanzada**:  

Usa `multitail` para monitorear múltiples archivos en una sola ventana.  

---

### **Resumen de opciones clave**  

| Propósito               | Comando Ejemplo             |  
|-------------------------|-----------------------------|  
| **Ver final de archivo** | `tail -n 50 archivo.txt`   |  
| **Monitorear logs**     | `tail -f /var/log/app.log` |  
| **Saltar primeras líneas** | `tail -n +100 datos.csv` |  

**Tip**: `tail` + `head` = ✨ **Combinación poderosa**. Ejemplo para extraer líneas 50-60 de un archivo:  

```bash
cat archivo.txt | head -n 60 | tail -n 11  # Líneas 50 a 60.
```  


