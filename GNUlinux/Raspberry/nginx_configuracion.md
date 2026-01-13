Instalación y Configuración de Nginx


Nginx es un servidor web y proxy inverso conocido por su alto rendimiento, estabilidad y bajo uso de recursos. Es utilizado por muchas de las mayores empresas de tecnología para servir contenido web a gran escala. Este artículo te guiará a través de los pasos necesarios para instalar y configurar Nginx en un servidor Linux.

Nginx es un servidor web y proxy inverso conocido por su alto rendimiento, estabilidad y bajo uso de recursos. Es utilizado por muchas de las mayores empresas de tecnología para servir contenido web a gran escala. Este artículo te guiará a través de los pasos necesarios para instalar y configurar Nginx en un servidor Linux.
Paso 1: Instalación de Nginx
Para Distribuciones Basadas en Debian (Ubuntu, Debian):

###  Actualizar el Sistema:

sudo apt update
sudo apt upgrade

2. Instalar Nginx:

```bash
sudo apt install nginx
```

3. Iniciar y Habilitar Nginx:

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

#### Para Distribuciones Basadas en Red Hat (CentOS, Fedora):

    Actualizar el Sistema:

sudo yum update

2. Instalar Nginx:

```bash
sudo yum install epel-release
sudo yum install nginx
```

3. Iniciar y Habilitar Nginx:

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

Paso 2: Configuración Básica de Nginx
Estructura de Directorios de Nginx:


    /etc/nginx/: Directorio de configuración principal.
    /etc/nginx/nginx.conf: Archivo de configuración principal de Nginx.
    /etc/nginx/conf.d/: Directorio para archivos de configuración adicional.
    /etc/nginx/sites-available/: Directorio para archivos de configuración de sitios (no siempre presente por defecto).
    /etc/nginx/sites-enabled/: Directorio para enlaces simbólicos a sitios habilitados (no siempre presente por defecto).
    /var/www/: Directorio raíz para los archivos web.


### Configuración de un Bloque de Servidor (Servidor Virtual):

    Crear un Archivo de Configuración de Sitio:

```bash
sudo nano /etc/nginx/sites-available/mi_sitio
```

2. Añadir la Configuración del Sitio:
```
server {
    listen 80;
    server_name mi_sitio.com www.mi_sitio.com;

    root /var/www/mi_sitio;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    error_page 404 /404.html;
    location = /404.html {
        internal;
    }

    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        internal;
    }
}
```

3. Crear el Directorio Raíz y un Archivo de Índice:

sudo mkdir -p /var/www/mi_sitio
sudo nano /var/www/mi_sitio/index.html

4. Añadir Contenido al Archivo de Índice:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Bienvenido a mi_sitio</title>
</head>
<body>
    <h1>¡Funciona!</h1>
</body>
</html>
```

5. Habilitar el Sitio Creando un Enlace Simbólico:

```bash
sudo ln -s /etc/nginx/sites-available/mi_sitio /etc/nginx/sites-enabled/
```

6. Probar la Configuración y Recargar Nginx:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

Paso 3: Configuración Adicional
Configurar HTTPS con Let’s Encrypt:

### Instalar Certbot: Para distribuciones basadas en Debian:

```bash
sudo apt install certbot python3-certbot-nginx
```

### Para distribuciones basadas en Red Hat:

```bash
sudo yum install certbot python3-certbot-nginx
```

2. Obtener un Certificado SSL:

```bash
sudo certbot --nginx -d mi_sitio.com -d www.mi_sitio.com
```

3. Renovar Certificados Automáticamente:

Certbot instala automáticamente un cron job para renovar los certificados. Puedes verificarlo con:

```bash
sudo systemctl status certbot.timer
```

Paso 4: Monitorización y Mantenimiento
Monitorizar el Rendimiento de Nginx:

    Acceder a los Logs:
        Acceso: /var/log/nginx/access.log
        Errores: /var/log/nginx/error.log
    Herramientas de Monitorización:
        Munin: Monitorea el rendimiento del servidor.
        Grafana: Visualiza métricas de rendimiento.

### Actualizar Nginx:

Mantén Nginx actualizado para aprovechar las últimas características y correcciones de seguridad:

```bash
sudo apt update && sudo apt upgrade nginx  # Para Debian/Ubuntu
sudo yum update nginx  # Para CentOS/Fedora
```

Conclusión

Nginx es una herramienta poderosa y flexible para servir contenido web. Su configuración inicial es sencilla y ofrece un rendimiento excelente incluso bajo alta carga. Al seguir estos pasos, puedes instalar y configurar Nginx para servir tus sitios web de manera segura y eficiente. Asegúrate de mantener tu servidor actualizado y monitorizado para garantizar un funcionamiento continuo y seguro.

---

¡Excelente pregunta! Vamos a aclarar el **rol de cada directorio** y cómo se relacionan con `/var/www/`. Aquí tienes la explicación detallada:

---

### **1. Diferencia entre `sites-available` y `sites-enabled` en Nginx**

| Directorio | Propósito | ¿Se usa directamente? |
|------------|-----------|-----------------------|
| **`/etc/nginx/sites-available/**` | Aquí guardas **todas las configuraciones** de tus sitios web (ej: `misitio`, `wordpress`, `api`). <br> - Archivos de ejemplo: `default`, `mi-proyecto.conf`. | ❌ No. Son solo plantillas. |
| **`/etc/nginx/sites-enabled/**` | Contiene **enlaces simbólicos** (atajos) a los archivos de `sites-available` que **quieres activar**. <br> - Ejemplo: `mi-proyecto.conf -> /etc/nginx/sites-available/mi-proyecto.conf`. | ✅ Sí. Nginx solo lee los archivos aquí. |

#### **¿Por qué esta separación?**  

- **Organización**: Puedes tener múltiples configuraciones en `sites-available` pero activar solo las necesarias.  
- **Seguridad**: Si un sitio tiene errores, lo desactivas eliminando el enlace en `sites-enabled` sin borrar la configuración original.  

#### **Comandos clave**:

```bash
# Crear enlace (activar sitio):
sudo ln -s /etc/nginx/sites-available/misitio /etc/nginx/sites-enabled/

# Eliminar enlace (desactivar sitio):
sudo rm /etc/nginx/sites-enabled/misitio
```

---

### **2. El directorio `/var/www/` y sus permisos**

Aquí es donde **se alojan los archivos de tus sitios web** (HTML, PHP, imágenes, etc.).  
Estructura típica:

```
/var/www/
├── mi-sitio/          # Carpeta del proyecto 1
│   ├── index.html     # Archivo principal
│   └── css/           # Estilos
└── wordpress/         # Carpeta del proyecto 2
    ├── wp-admin/
    └── wp-content/
```

#### ** Problema común**: Permisos incorrectos (Nginx no puede leer/escribir).

#### **Solución**:

1. **Asignar el usuario/grupo correcto** (Nginx usa `www-data` en Ubuntu/Debian):

```bash
sudo chown -R www-data:www-data /var/www/mi-sitio
```
2. **Dar permisos de lectura/escritura**:

```bash
sudo chmod -R 755 /var/www/mi-sitio  # Para archivos estáticos (HTML, JS)
sudo chmod -R 775 /var/www/wordpress # Si usas WordPress (necesita escribir en wp-content)
```

---

### **3. Flujo de trabajo típico con Nginx**

1. **Creas la configuración** en `sites-available`:

```bash
sudo nano /etc/nginx/sites-available/misitio
```
   
2. **Habilitas el sitio**:

```bash
sudo ln -s /etc/nginx/sites-available/misitio /etc/nginx/sites-enabled/
```
   
3. **Subes tus archivos** a `/var/www/misitio/`:

```bash
sudo cp -r ~/mis-archivos-html/* /var/www/misitio/
```

4. **Verificas y reinicias Nginx**:

```bash
sudo nginx -t  # Testear errores
sudo systemctl restart nginx
```

---

### **4. Ejemplo práctico: Configurar un sitio estático (HTML)**

#### **Paso 1: Crear estructura de archivos**

```bash
sudo mkdir -p /var/www/miweb/{html,css,js}
sudo nano /var/www/miweb/html/index.html
```
Contenido de `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Mi Sitio</title>
</head>
<body>
    <h1>¡Funciona!</h1>
</body>
</html>
```

#### **Paso 2: Configuración Nginx (`miweb` en `sites-available`)**

```bash
sudo nano /etc/nginx/sites-available/miweb
```

Contenido:

```nginx
server {
    listen 80;
    server_name tu-ip-o-dominio.com;
    root /var/www/miweb/html;
    index index.html;
}
```

#### **Paso 3: Activar y probar**

```bash
sudo ln -s /etc/nginx/sites-available/miweb /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl restart nginx
```

Ahora visita `http://tu-ip-o-dominio.com` en tu navegador.

---

### **Resumen visual**

```
/etc/nginx/
├── sites-available/  # 📁 Aquí defines proyectos (no se usan directamente)
│   └── miweb.conf   # 🛠️  Configuración de ejemplo
└── sites-enabled/    # 🔗 Enlaces a sitios activos
    └── miweb.conf -> /etc/nginx/sites-available/miweb.conf  # ⚡ Este sí lo lee Nginx

/var/www/
└── miweb/            # 🌐 Archivos del sitio (HTML, CSS, etc.)
    └── html/
        └── index.html
```

---




