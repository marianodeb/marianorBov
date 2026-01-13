
## Inatalcion 

pagina: https://docs.docker.com/engine/install/debian/

1. Prerrequisitos

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y ca-certificates curl gnupg
```

2. Agregar Clave GPG y Repositorio:

```bash
# Crear directorio para claves
sudo install -m 0755 -d /etc/apt/keyrings

# Descargar clave GPG
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Agregar repositorio (detecta automáticamente tu versión de Debian)
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

3. Instalar Docker:

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

4. Verificar Instalación:

```bash
sudo docker run hello-world
```
Configuración Post-Instalación:

1. Ejecutar Docker sin sudo (opcional):

```bash
sudo usermod -aG docker $USER
newgrp docker  # Recargar grupo sin reiniciar sesión
```

2. Habilitar inicio automático:

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

3. Verificar versión:

```bash
docker --version
docker compose version
```

## Comandos

```bash
$docker pull nombre_imagen   # descarga la imagen
```

```bash
$docker run nombre_imagen    # arranca el contenedor
```

\#   si la imagen no existe la baja y arranca

```bash
$docker images   # muestra las imagenes descargadas
```

```bash
$docker image ls   # muestra las imagenes descargadas
```

```bash
$docker images rm nombre_imagen   # elimina la imagen
```

```bash
$docker image inspect nombre_imagen   #muestra ifo de la imagen
```

```bash
$docker images | head
```

```bash
$docker iamges | tail
```

```bash
$docker ps  # muestra informacion de los contenedores 
```

```bash
$docker run -d nombre_imagen  
```

\# si el contenedor usa la terminal se utiliza la opcion -d para correrlo en background o segundo plano

```bash
$docker stop numero_id   # para el detener contenedor
```

```bash
$docker start numero_id   # arranca el contenedor
```

```bash
$docker ps -a   # muestra info
```

```bash
$docker logs numero_id   # muestra los logs
```

```bash
$docker logs -f numero_id   # muestra logs y cambios en vivo
```

```bash
$docker exec -it numero_id sh   
```

\# ejucata una terminal interactiva dentro del contenedor, el comando sh (ej sh) 

```bash
$docker run -d -p 8089:80 --name servidor-web hhttpd
```

\# -d (va liberara la terminal yse usara una segundo plano)
\# -p (puertos) el primero es del host 8089 y es segundo 89 es de contenedor
\# --name es para darle un nombre o alias al contenedor servidor-eb 
\# hhttpd (nombre de la imagen )

```bash
$docker network   # lista comandos de red para contenedores ej. connect, ls... etc
```

```bash
$docker network ls   # listas los contenedores y su info de network 
```

---

### Gestión y Operaciones Básicas:

- **docker run**: Ejecuta un contenedor a partir de una imagen.
- **docker start**: Inicia un contenedor detenido.
- **docker stop**: Detiene un contenedor en ejecución.
- **docker restart**: Reinicia un contenedor.
- **docker pause**: Pausa la ejecución de un contenedor.
- **docker unpause**: Reanuda la ejecución de un contenedor pausado.
- **docker kill**: Detiene abruptamente un contenedor.
- **docker rm**: Elimina uno o más contenedores.
- **docker rmi**: Elimina una o más imágenes.
- **docker ps**: Lista contenedores en ejecución.
- **docker ps -a**: Lista todos los contenedores (incluidos los detenidos).
- **docker logs**: Muestra los logs de un contenedor.
- **docker inspect**: Muestra información detallada sobre un objeto Docker.
- **docker stats**: Muestra estadísticas de uso de recursos de los contenedores.
- **docker top**: Muestra los procesos en ejecución en un contenedor.
- **docker exec**: Ejecuta un comando dentro de un contenedor en ejecución.

### Imágenes:

- **docker images**: Lista las imágenes disponibles localmente.
- **docker pull**: Descarga una imagen desde un registro.
- **docker push**: Sube una imagen a un registro.
- **docker build**: Construye una imagen a partir de un Dockerfile.
- **docker commit**: Crea una nueva imagen a partir de un contenedor en ejecución.

### Redes:

- **docker network ls**: Lista las redes creadas.
- **docker network create**: Crea una nueva red.
- **docker network inspect**: Muestra información detallada sobre una red.
- **docker network connect**: Conecta un contenedor a una red.
- **docker network disconnect**: Desconecta un contenedor de una red.

### Volumen:

- **docker volume ls**: Lista los volúmenes disponibles.
- **docker volume create**: Crea un nuevo volumen.
- **docker volume inspect**: Muestra información detallada sobre un volumen.

### Docker Compose:

- **docker-compose up**: Inicia servicios definidos en un archivo Docker Compose.
- **docker-compose down**: Detiene y elimina servicios definidos en un archivo Docker Compose.
- **docker-compose build**: Construye o reconstruye servicios definidos en un archivo Docker Compose.
- **docker-compose logs**: Muestra los logs de servicios definidos en un archivo Docker Compose.

### Docker Swarm (Orquestación):

- **docker swarm init**: Inicia un clúster de Docker Swarm.
- **docker swarm join**: Une un nodo al clúster de Docker Swarm.
- **docker service create**: Crea un servicio en Docker Swarm.
- **docker service ls**: Lista servicios en Docker Swarm.
- **docker node ls**: Lista nodos en Docker Swarm.
- **docker stack deploy**: Despliega una pila de servicios definidos en un archivo Docker Compose en Docker Swarm.

### Seguridad:

- **docker login**: Inicia sesión en un registro de Docker.
- **docker logout**: Cierra sesión de un registro de Docker.
- **docker scan**: Escanea imágenes en busca de vulnerabilidades.

### Otros Comandos Útiles:

- **docker history**: Muestra el historial de una imagen.
- **docker tag**: Etiqueta una imagen con un nuevo tag.
- **docker rename**: Cambia el nombre de un contenedor.
- **docker cp**: Copia archivos o directorios entre un contenedor y el sistema host.
- **docker export**: Exporta el sistema de archivos de un contenedor como un archivo tar.

### Limpieza y Mantenimiento:

- **docker system df**: Muestra el uso de espacio en disco de Docker.
- **docker system prune**: Limpia recursos no utilizados (contenedores detenidos, redes no utilizadas, etc.).
- **docker container prune**: Limpia contenedores detenidos.
- **docker image prune**: Limpia imágenes no utilizadas.
- **docker volume prune**: Limpia volúmenes no utilizados.
- **docker network prune**: Limpia redes no utilizadas.

### Debugging y Troubleshooting:

- **docker events**: Muestra eventos de Docker.
- **docker diff**: Muestra cambios en el sistema de archivos del contenedor.
- **docker port**: Muestra mapeos de puertos de un contenedor.
- **docker wait**: Espera a que un contenedor se detenga, luego imprime el código de salida.

### Interacción con Docker Hub y Registros:

- **docker search**: Busca imágenes en Docker Hub.
- **docker push**: Sube una imagen a Docker Hub.
- **docker pull**: Descarga una imagen desde Docker Hub.

### Ejecución de Scripts y Comandos:

- **docker-compose exec**: Ejecuta comandos dentro de servicios de Docker Compose.
- **docker-compose run**: Ejecuta comandos en un nuevo contenedor basado en un servicio definido en Docker Compose.

### Gestión de Recursos:

- **docker update**: Actualiza la configuración de recursos de un contenedor en ejecución.
- **docker attach**: Conecta a la entrada estándar de un contenedor en ejecución.

### Extensiones y Plugins:

- **docker plugin**: Gestiona plugins de Docker.
- **docker extension**: Gestiona extensiones de Docker (si están habilitadas).

### Información y Ayuda:

- **docker version**: Muestra la versión de Docker instalada.
- **docker info**: Muestra información del sistema Docker.
- **docker help**: Muestra ayuda sobre comandos de Docker.

### Integración con CI/CD y Automatización:

- **docker buildx**: Extensión para la construcción de imágenes multiplataforma con Docker.
- **docker-compose up -d**: Inicia servicios de Docker Compose en modo detached (en segundo plano).
- **docker save**: Guarda una imagen de Docker en un archivo tar.


### Servicio de Docker

##### Detener el servicio de Docker

    Detener el servicio principal y el socket:
    
```Bash
sudo systemctl stop docker.service
sudo systemctl stop docker.socket
```
    Este comando asegura que tanto el servicio principal como el punto de conexión se detengan por completo.

##### Iniciar el servicio de Docker

 Iniciar el servicio principal:

```Bash
sudo systemctl start docker.service
```

Esto iniciará el servicio principal de Docker, permitiendo que se ejecuten contenedores.

Deshabilitar el servicio de Docker (para que no se inicie al arrancar el sistema)

#####   Deshabilitar el servicio principal y el socket:
 
```Bash
    sudo systemctl disable docker.service
    sudo systemctl disable docker.socket
```

    Con esto, Docker no se iniciará automáticamente cuando reinicies tu sistema.

Habilitar el servicio de Docker (para que se inicie al arrancar el sistema)

#####    Habilitar el servicio principal:
 
```Bash
    sudo systemctl enable docker.service
```

    Esto hará que Docker se inicie automáticamente al arrancar tu sistema.

##### Verificar el estado de Docker

    Verificar si el servicio está en ejecución:

```Bash
    sudo systemctl status docker.service
```

    Este comando te mostrará si el servicio está activo, inactivo, o si hay algún error.

Otros comandos útiles

##### Reiniciar el servicio:

```Bash
sudo systemctl restart docker.service
```

##### Reiniciar el sistema (si es necesario):

```Bash
    sudo reboot
```

Importante:

    Permisos de root: Los comandos anteriores requieren permisos de administrador (root). El prefijo sudo te permite ejecutarlos con privilegios elevados.
    Distribución Linux: Estos comandos son específicos para sistemas basados en systemd, que es el gestor de arranque más común en las distribuciones Linux modernas. Si utilizas otra distribución, los comandos podrían variar ligeramente.

---

## Ejemplo de un servidor en una raspberry

¡Muchas gracias por tus palabras y por tu paciencia! 😊 Me alegra mucho que la explicación final haya sido clara y útil para ti. Aprender de tus comentarios es invaluable para mejorar cómo comunico los conceptos.

**Resumen final con los puntos clave que destacaste** (para que quede como referencia rápida):

---

### **1. `--restart unless-stopped`**
- **¿Para qué sirve?**  
  Para que Docker reinicie automáticamente el contenedor tras apagados, errores o reinicios del sistema.  
- **¿Es necesario?**  
  **Sí**, si quieres que el contenedor esté siempre activo sin intervención manual.  
  **No**, si prefieres controlarlo tú mismo.  

---

### **2. El script**
- **¿Para qué sirve?**  
  Para evitar escribir comandos largos cada vez que creas o recreas el contenedor.  
- **¿Es obligatorio?**  
  **No**, pero ahorra tiempo y evita errores.  
- **¿Cuándo usarlo?**  
  - Al crear el contenedor por primera vez.  
  - Si borras el contenedor y necesitas recrearlo.  

---

### **3. Relación entre `--restart` y el script**
- **Con `--restart`**:  
  - El script se usa **solo una vez** (para crear el contenedor).  
  - Docker maneja los reinicios automáticos.  
- **Sin `--restart`**:  
  - El script se usa **cada vez que quieras iniciar el contenedor** tras un apagado o borrado.  

---

### **4. Casos comunes**
- **Caso 1**: Quiero que el servidor esté siempre disponible.  
  **Solución**:  
  ```bash
  docker run ... --restart unless-stopped ...
  ```
- **Caso 2**: Solo necesito el servidor ocasionalmente.  
  **Solución**:  
  ```bash
  docker run ...  # Sin --restart
  docker start ... # Cuando lo necesites
  ```
- **Caso 3**: Me equivoqué en los parámetros del contenedor.  
  **Solución**:  
  ```bash
  docker rm compartir-archivos  # Borra el contenedor
  ./iniciar-servidor.sh         # Ejecuta el script para recrearlo
  ```

---

### **5. Verificaciones rápidas**
- **¿El contenedor está activo?**  
  ```bash
  docker ps
  ```
- **¿Por qué no funciona?**  
  ```bash
  docker logs compartir-archivos  # Revisa errores
  ```
- **¿El puerto 8000 está bloqueado?**  
  ```bash
  sudo lsof -i :8000
  ```

---

---

## **1. Comandos Básicos de Docker**

### **Gestión de Imágenes**

| Comando | Descripción |
|---------|-------------|
| `docker images` | Lista todas las imágenes descargadas. |
| `docker pull <imagen>:<tag>` | Descarga una imagen (ej: `docker pull nginx:latest`). |
| `docker rmi <imagen>` | Borra una imagen (ej: `docker rmi python:alpine`). |
| `docker build -t <nombre> .` | Crea una imagen desde un Dockerfile en el directorio actual. |

---

### **Gestión de Contenedores**

| Comando | Descripción |
|---------|-------------|
| `docker run -d --name <nombre> <imagen>` | Crea y ejecuta un contenedor en segundo plano. |
| `docker start <nombre>` | Inicia un contenedor detenido. |
| `docker stop <nombre>` | Detiene un contenedor (elegantemente). |
| `docker rm <nombre>` | Borra un contenedor detenido. |
| `docker ps` | Lista contenedores en ejecución. |
| `docker ps -a` | Lista **todos** los contenedores (incluyendo detenidos). |
| `docker logs <nombre>` | Muestra los logs (registros) de un contenedor. |
| `docker exec -it <nombre> sh` | Entra a la terminal de un contenedor en ejecución. |

---

### **Opciones Clave para `docker run`**

| Opción | Descripción |
|--------|-------------|
| `-p <host>:<contenedor>` | Mapea puertos (ej: `-p 8000:8000`). |
| `-v <ruta_host>:<ruta_contenedor>` | Monta un volumen (ej: `-v /home/tu_carpeta:/app`). |
| `--restart unless-stopped` | Reinicia automáticamente el contenedor. |
| `-e <variable>=<valor>` | Define variables de entorno (ej: `-e MYSQL_ROOT_PASSWORD=123`). |
| `-w <ruta>` | Define el directorio de trabajo dentro del contenedor. |

---

## **2. Comandos Avanzados**

### **Redes en Docker**

| Comando | Descripción |
|---------|-------------|
| `docker network ls` | Lista todas las redes. |
| `docker network create <nombre>` | Crea una red personalizada. |
| `docker network connect <red> <contenedor>` | Conecta un contenedor a una red. |

---

### **Volúmenes**

| Comando | Descripción |
|---------|-------------|
| `docker volume ls` | Lista todos los volúmenes. |
| `docker volume create <nombre>` | Crea un volumen. |
| `docker volume inspect <nombre>` | Muestra detalles de un volumen. |

---

### **Limpieza**

| Comando | Descripción |
|---------|-------------|
| `docker system prune` | Borra contenedores, redes e imágenes no usadas. |
| `docker volume prune` | Borra volúmenes no usados. |

---

## **3. Docker Compose (Para Proyectos Complejos)**

### **Archivo `docker-compose.yml` (Ejemplo)**

```yaml
version: '3'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
    restart: unless-stopped

  db:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: 123
```

### **Comandos Clave**

| Comando | Descripción |
|---------|-------------|
| `docker compose up -d` | Inicia los contenedores en segundo plano. |
| `docker compose down` | Detiene y borra los contenedores. |
| `docker compose logs` | Muestra los logs de todos los servicios. |

---

## **4. Consejos y Buenas Prácticas**

### **Para Evitar Problemas Comunes**

1. **Usa siempre `-v` para datos importantes**:

```bash
docker run -v /ruta/en/tu/pc:/ruta/en/contenedor ...
```
   
2. **No uses `latest` en producción**: Especifica la versión de la imagen (ej: `python:3.9`).  
3. **Monitorea el uso de recursos**:

```bash
docker stats
```

---

### **Analogías para Entender Docker**

- **Imagen** = Molde para hacer galletas.  
- **Contenedor** = Galleta hecha con el molde.  
- **Volumen** = Caja donde guardas las galletas para que no se pierdan.  
- **Docker Compose** = Receta para hacer varias galletas a la vez.  

---

## **5. Comandos Útiles para Debuggear**

| Comando | Descripción |
|---------|-------------|
| `docker inspect <nombre>` | Muestra toda la metadata de un contenedor/imagen. |
| `docker top <nombre>` | Lista procesos en ejecución dentro del contenedor. |
| `docker stats` | Muestra uso de CPU, memoria y red en tiempo real. |

---

## **6. Enlaces Clave**

- **Documentación Oficial**: [https://docs.docker.com](https://docs.docker.com)  
- **Docker Hub**: [https://hub.docker.com](https://hub.docker.com) (Repositorio de imágenes públicas).

---

## **Docker Compose**

---

## **1. ¿Qué es Docker Compose?**

Es una herramienta que permite definir y ejecutar **múltiples contenedores** de forma coordinada usando un solo archivo YAML (`docker-compose.yml`). Simplifica la orquestación de servicios interconectados (como bases de datos, backends, frontends, etc.).

### **¿Cómo se complementa con Docker?**

- **Docker**: Gestiona contenedores individuales.  
- **Docker Compose**: Orquesta varios contenedores como una sola aplicación.

---

## **2. Utilidad de Docker Compose**

- **Definir entornos complejos** en un solo archivo (evita comandos largos).  
- **Automatizar** la creación de redes, volúmenes y servicios conectados.  
- **Reproducir entornos** de desarrollo, testing o producción de forma consistente.  
- **Simplificar el trabajo en equipo** (todos usan la misma configuración).

---

## **3. Sintaxis Básica del Archivo `docker-compose.yml`**

```yaml
version: '3.8'  # Versión de Compose
services:       # Lista de servicios (contenedores)
  servicio1:    # Nombre del servicio
    image: nginx:latest  # Imagen a usar
    ports:
      - "80:80"         # Mapeo de puertos
    volumes:
      - ./html:/usr/share/nginx/html  # Volúmenes
    environment:         # Variables de entorno
      - DEBUG=1
    depends_on:          # Dependencias entre servicios
      - servicio2

  servicio2:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: contraseña

volumes:        # Volúmenes persistentes
  datos-mysql:
```

---

## **4. Comandos Esenciales de Docker Compose**

| Comando | Descripción |
|---------|-------------|
| `docker compose up -d` | Inicia los contenedores en segundo plano. |
| `docker compose down` | Detiene y elimina contenedores, redes y volúmenes. |
| `docker compose build` | Reconstruye imágenes desde Dockerfiles. |
| `docker compose logs` | Muestra los logs de todos los servicios. |
| `docker compose ps` | Lista los contenedores en ejecución. |
| `docker compose exec <servicio> sh` | Entra al terminal de un servicio. |

---

## **5. Ejemplo Práctico: Aplicación Web + Base de Datos**

### **Estructura del Proyecto**

```
mi-app/
├── docker-compose.yml
├── frontend/
│   ├── Dockerfile
│   └── ...
├── backend/
│   ├── Dockerfile
│   └── ...
└── database/
    └── datos/  # Carpeta para persistencia de la DB
```

### **Archivo `docker-compose.yml`**

```yaml
version: '3.8'

services:
  frontend:
    build: ./frontend  # Usa el Dockerfile de la carpeta frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend

  backend:
    build: ./backend
    environment:
      DB_HOST: db
      DB_USER: root
    depends_on:
      - db

  db:
    image: mysql:8.0
    volumes:
      - ./database/datos:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: secreto
      MYSQL_DATABASE: mi_app
```

---

## **6. Pasos para Usar Docker Compose**

1. **Crea el archivo `docker-compose.yml`** en la raíz del proyecto.  
2. **Ejecuta**:

   ```bash
   docker compose up -d  # Inicia todos los servicios
   ```
   
3. **Verifica**:

```bash
docker compose ps     # Muestra los contenedores activos
```
4. **Detén todo**:

```bash
docker compose down   # Elimina contenedores, redes y volúmenes
```

---

## **7. Casos de Uso Comunes**

1. **Desarrollo Full-Stack**:

   - Frontend (React), Backend (Node.js), Base de Datos (MySQL).  
   
2. **CMS con Base de Datos**:

   - WordPress + MySQL.
   
3. **Microservicios**:

   - API Gateway, Servicio de Autenticación, Servicio de Notificaciones.  

---

## **8. Ventajas Clave**

- **Portabilidad**: El mismo archivo funciona en cualquier máquina con Docker.  
- **Versionado**: El `docker-compose.yml` puede guardarse en Git.  
- **Escalabilidad**: Fácil añadir nuevos servicios (ej: un Redis para caché).

---

## **9. Consejos Profesionales**

- **Usa variables de entorno** para contraseñas o configuraciones sensibles:

```yaml
environment:
  - DB_PASSWORD=${DB_PASSWORD}  # Lee desde un archivo .env
```
  
- **Evita `latest`** en imágenes para producción. Usa versiones específicas.  
- **Limpia regularmente**:

```bash
docker compose down --volumes  # Borra volúmenes al detener
```

---

## **10. Ejemplo Avanzado: Redes Personalizadas**

```yaml
version: '3.8'

services:
  app:
    image: mi-app:1.0
    networks:
      - frontend

  db:
    image: postgres:13
    networks:
      - backend

networks:
  frontend:
  backend:
```
- **Beneficio**: Aísla la red de la base de datos del frontend para mayor seguridad.

---

## **11. Integración con Docker Swarm/Kubernetes**

Docker Compose es ideal para entornos de desarrollo, pero en producción puedes usar:
- **Docker Swarm**: Para orquestación simple.  
- **Kubernetes**: Para aplicaciones complejas y escalables.  

---

## **12. Documentación Oficial**
- **Docker Compose CLI**: [https://docs.docker.com/compose/reference/](https://docs.docker.com/compose/reference/)  
- **Guía de Referencia YAML**: [https://docs.docker.com/compose/compose-file/](https://docs.docker.com/compose/compose-file/)  

---


