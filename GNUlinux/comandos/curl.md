## **`curl`**

---

### **1. Significado**  

**`curl`** (**C**lient **URL**) es una herramienta para **transferir datos desde o hacia un servidor** usando protocolos como HTTP, HTTPS, FTP, SFTP, SMTP y más. Es ideal para interactuar con APIs, probar endpoints, enviar datos, y descargar/upload archivos con un alto nivel de personalización.  

---

### **2. Uso**

- Enviar o recibir datos de APIs RESTful (GET, POST, PUT, DELETE).  
- Descargar archivos desde la web.  
- Enviar formularios web o archivos.  
- Autenticación (Basic, OAuth, tokens).  
- Simular peticiones HTTP con headers personalizados.  
- Depurar conexiones y analizar respuestas.  

---

### **3. Sintaxis General**

```bash  
curl [OPCIONES] [URL]  
```

---

### **4. Opciones Principales**  

| Opción                  | Descripción                                                                 |  
|-------------------------|-----------------------------------------------------------------------------|  
| `-o <archivo>`          | Guarda la respuesta en un archivo (ej: `-o salida.html`).                  |  
| `-O`                    | Guarda la respuesta con el nombre original del archivo en la URL.          |  
| `-L`                    | Sigue redirecciones HTTP/HTTPS automáticamente.                            |  
| `-X <método>`           | Especifica el método HTTP (GET, POST, PUT, DELETE).                        |  
| `-H "Header: valor"`    | Agrega headers personalizados (ej: `-H "Content-Type: application/json"`). |  
| `-d "datos"`            | Envía datos en el cuerpo de la petición (usado en POST/PUT).               |  
| `-F "nombre=@archivo"`  | Envía archivos como formulario multipart/form-data.                        |  
| `-u usuario:contraseña` | Autenticación básica (ej: `-u admin:secreto`).                             |  
| `-k`                    | Ignora la verificación de certificados SSL (⚠️ uso cauteloso).             |  
| `-v`                    | Modo verbose (muestra detalles de la petición y respuesta).                |  
| `--limit-rate <veloc>`  | Limita la velocidad de transferencia (ej: `--limit-rate 1M`).              |  
| `-A "User-Agent"`       | Define un User-Agent personalizado.                                        |  
| `-s`                    | Modo silencioso (no muestra errores ni barras de progreso).                |  
| `-b <cookie>`           | Envía cookies en la petición.                                              |  
| `-c <archivo>`          | Guarda cookies en un archivo después de la petición.                       |  

---

### **5. Ejemplos**

#### **Ejemplos Simples**

1. **Descargar un archivo**:

```bash  
curl -O https://ejemplo.com/imagen.jpg  
```

2. **Guardar contenido en un archivo**:

```bash  
curl -o pagina.html https://ejemplo.com  
```

3. **Seguir redirecciones (ej: URL acortada)**:

```bash  
curl -L https://bit.ly/3ejemplo  
```

4. **Enviar una petición GET a una API**:

```bash  
curl https://jsonplaceholder.typicode.com/posts/1  
```

---

#### **Ejemplos Avanzados**

1. **Enviar datos POST con JSON**:

```bash  
curl -X POST -H "Content-Type: application/json" -d '{"title":"Hola", "body":"Mundo"}' https://ejemplo.com/api/posts  
```

2. **Subir un archivo con multipart/form-data**:

```bash
curl -F "foto=@/ruta/foto.jpg" -F "nombre=ejemplo" https://ejemplo.com/upload  
```

3. **Autenticación básica**:

```bash  
curl -u usuario:contraseña https://api.ejemplo.com/privado  
```

4. **Usar headers personalizados (ej: token JWT)**:

```bash  
curl -H "Authorization: Bearer eyJhbGciOiJ..." https://api.ejemplo.com/data  
```

5. **Limitar velocidad de descarga a 500 KB/s**:

```bash
curl --limit-rate 500K -O https://ejemplo.com/video.mp4  
```

6. **Depurar una petición (verbose)**:

```bash
curl -v https://ejemplo.com  
```

7. **Enviar cookies y guardar nuevas**:

```bash
curl -b "session=1234" -c cookies.txt https://ejemplo.com/login  
```

8. **Ignorar certificado SSL inválido**:

```bash  
curl -k https://sitio-con-certificado-invalido.com  
```

---

### **6. Información Adicional**

#### **¿Cuándo usar `curl` vs `wget`?**

- **`curl`**:

  - Ideal para interactuar con APIs, enviar datos, y pruebas rápidas.  
  - Soporta más protocolos (como SMTP, SMB).  
  - Mejor integración en scripts para procesar respuestas.
  
- **`wget`**:

  - Mejor para descargar sitios web completos (mirroring) o archivos grandes.  
  - Soporte nativo para descargas recursivas.  

#### **Seguridad**

- **HTTPS**: Verifica certificados SSL/TLS por defecto (usa `-k` con precaución).  
- **Datos sensibles**: Evita exponer contraseñas en la línea de comandos (mejor usa variables de entorno o archivos).  

#### **Formatos de Datos**

- **JSON**: Usa `jq` para procesar respuestas JSON en combinación con `curl`:

```bash
curl -s https://api.ejemplo.com/data | jq .  
```

---

### **7. Errores Comunes**

- **Olvidar comillas en datos JSON**: Si el JSON incluye espacios, usa comillas simples o dobles.  
- **No seguir redirecciones**: Si una URL redirige, usa `-L` para obtener el contenido final.  
- **User-Agent bloqueado**: Algunos sitios bloquean `curl`; usa `-A "Mozilla/5.0"`.  

---

### **8. Diagrama de Flujo de `curl`**

```
[URL] → [Resolución DNS] → [Conexión al servidor] → [Envío de petición] → [Procesamiento de respuesta]  
```

---

### **9. Comandos Útiles para Depurar**

- **Ver tiempo de respuesta**:

```bash
curl -w "Tiempo total: %{time_total}s\n" https://ejemplo.com  
```
  
- **Mostrar solo el código HTTP**:

```bash
curl -s -o /dev/null -w "%{http_code}" https://ejemplo.com  
```
  
- **Probar conectividad a un puerto**:

```bash
curl -v telnet://ejemplo.com:80  
```

---


