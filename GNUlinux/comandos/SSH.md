
### Instalar ssh 

```bash
$sudo apt install openssh-server openssh-client
```

### Conexion

```bash
$ssh $USER@<ip ej: 192.168.13>
```

```bash
$ss <ip ej:192.168.13> -l $USER
```

Por default se comunica por el puert 22 . 
Para ahcerlo mas seguro se puede cambiar el puerto en el archivo:

```bash
$/etc/ssh/sshd_config .
```

Luego de configurar el archivo se reinicia el servicio para que el cambio se efectue. Con:

```bash
$systemctl restart ssh
```

Para conectarse se le agrega **\-p** \<numero_de_puerto\> 
En el ejmplo se configuro el puerto 50015  

```bash
$ssh <ip ej:192.168.13> -l $USER -p 50015
```

### Arrancar, Reiniciar y Parar **ssh**

```bash
$sudo /etc/init.d/ssh start
```

```bash
$sudo /etc/init.d/ssh restart
```

```bash
$sudo /etc/init.d/ssh stop
```

### Clave/Usuario

Para este modo siempre que uno se conecta debe introducir usuario y clave el nodo de conf es:

**PaswordAuthentication yes**

### Clave/Pulicas
Para usar clave publica la configuracion debe tener estas dos opciones de la siguiente manera:

**PaswordAuthentication no**
**PubkeyAuthentication yes**

### Crear Claves 

Para crear claves  ssh y copiarla en servidor. la key se guarda en **.ss/id_rsa.pub** luego se pega en el archivo del servidor en:

**.ssh/authorized_keys**

Tres maneras de generar claves. **-b 4096** hace referencias a la cantidad de bit 

```bash
$ssh-keygen 
```

```bash
$ssh-keygen -t rsa
```

```bash
$ssh-keygen -t rsa -b 4096
```
