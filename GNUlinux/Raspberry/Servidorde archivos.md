

### **Guía Definitiva: Servidor de Archivos con Docker en Raspberry Pi**

**Objetivo**: Crear un servidor liviano para compartir archivos en tu red local, usando Docker y Python.  

---

### **Prerrequisitos**
1. **Carpeta con archivos**:

   - Ejemplo: `~/TU_DIRECTORIO` (en tu home).  
   - Crea al menos un archivo de prueba:
   
```bash
mkdir ~/TU_DIRECTORIO && echo "Hola Docker!" > ~/TU_DIRECTORIO/prueba.txt
```

2. **Docker instalado**: Asegúrate de que funciona con:

```bash
docker --version
```

---

### **Paso a Paso (Comando Mejorado)**

```bash
# 1. Detener y eliminar contenedores previos (si existen)
docker stop compartir-archivos 2>/dev/null; docker rm -f compartir-archivos 2>/dev/null

# 2. Ejecutar el contenedor con variables dinámicas
docker run -d \
  --name compartir-archivos \
  -p 8000:8000 \
  -v "/home/$USER/TU_DIRECTORIO:/app" \
  -w /app \
  python:alpine \
  python -m http.server 8000
```

---

### **Explicación Detallada del Comando**

| Parte del Comando | ¿Qué hace? | ¿Por qué es importante? |  
|--------------------|------------|--------------------------|  
| `-v "/home/$USER/TU_DIRECTORIO:/app"` | Monta tu carpeta local en `/app` del contenedor. | **`$USER`** es tu usuario actual (ej: `pi`, `raspberry`). **`TU_DIRECTORIO`** debe ser el nombre exacto de tu carpeta. |  
| `-w /app` | Fija el directorio de trabajo dentro del contenedor. | Sin esto, Python serviría archivos desde la raíz del contenedor (¡y verías `bin/`, `dev/`, etc!). |  
| `python:alpine` | Usa la imagen oficial de Python en su versión Alpine (ultra-liviana). | Ideal para Raspberry Pi por su bajo consumo de recursos. |  
| `python -m http.server 8000` | Inicia el servidor web de Python en el puerto 8000. | Sirve los archivos de la carpeta montada (`/app`). |  

---

### **Verificación**

1. **Desde tu Raspberry Pi**:  
```bash
curl http://localhost:8000  # Deberías ver "prueba.txt".
```
   
2. **Desde otro dispositivo**:

   - Averigua la IP de tu Raspberry Pi:
   
```bash
hostname -I
```
     
   - Accede desde el navegador: `http://[IP]:8000`.  

---

### **Errores Comunes y Soluciones**

| Error | Causa | Solución |  
|-------|-------|----------|  
| **`Cannot start container: invalid volume path`** | La ruta de la carpeta no existe. | Verifica que `TU_DIRECTORIO` existe: `ls /home/$USER/TU_DIRECTORIO`. |  
| **`403 Forbidden`** | Permisos insuficientes en la carpeta. | Ejecuta: `chmod -R 755 ~/TU_DIRECTORIO`. |  
| **Ves `bin/`, `dev/`, etc.** | El volumen no se montó correctamente. | Revisa que `-v` y `-w` están bien escritos. |  

---

### **Tips Clave**

- **Usa `$USER`**: Evita errores de rutas manuales.  
- **Alpine siempre**: Imágenes más pequeñas = menos recursos.  
- **Limpia contenedores**: Si ya no los usas:

```bash
docker system prune
```

---

### **¿Qué Aprendiste?**

1. **Montar volúmenes**: Conectar carpetas locales al contenedor.  
2. **Trabajar con variables dinámicas**: `$USER` para rutas personalizables.  
3. **Servir archivos estáticos**: Usar Python como servidor web sencillo.  

---

