



Instalar MPD (Music Player Daemon)

```bash
sudo apt install mpd
```

Configurar MPD

Después de instalar MPD, debes configurarlo. El archivo de configuración se encuentra en /etc/mpd.conf. Puedes editarlo con un editor de texto como nano:

```bash
sudo nano /etc/mpd.conf
```

Aquí hay algunas configuraciones básicas que puedes ajustar:

Directorio de música: Especifica la ubicación de tus archivos de música.

```bash
music_directory "/ruta/a/tu/musica"
```

Directorio de la base de datos: Especifica dónde se almacenará la base de datos de MPD.

```bash
db_file "/var/lib/mpd/tag_cache"
```

Playlists: Especifica la ubicación de las listas de reproducción.

```bash
playlist_directory "/var/lib/mpd/playlists"
```

Permitir acceso desde la red (opcional): Si deseas controlar MPD desde otros dispositivos en la red, habilita esta opción:

```bash
bind_to_address "0.0.0.0"
```

Guarda los cambios y cierra el editor (Ctrl + O para guardar, Ctrl + X para salir).


Reiniciar MPD

Después de configurar MPD, reinicia el servicio para aplicar los cambios:

```bash
sudo systemctl restart mpd
```

Instalar NCMPCPP (cliente para MPD)

```bash
sudo apt install ncmpcpp
```

Configurar NCMPCPP

NCMPCPP se conecta automáticamente a MPD si está en la misma máquina. Si MPD está en otro dispositivo, puedes configurar la conexión editando el archivo de configuración de NCMPCPP:

```bash
nano ~/.ncmpcpp/config
```

Aquí puedes especificar la dirección IP y el puerto de MPD si es necesario:

```bash
mpd_host = "localhost"
mpd_port = "6600"
```

Iniciar NCMPCPP

Una vez configurado, puedes iniciar NCMPCPP ejecutando:

```bash
ncmpcpp
```

Agregar música a MPD

Para que MPD reconozca tu música, agrega los archivos a la base de datos:

```bash
mpc update
```

Reproducir música

Ahora puedes usar NCMPCPP para navegar por tu biblioteca y reproducir música. Algunos atajos útiles en NCMPCPP:


    1: Biblioteca musical.

    2: Lista de reproducción actual.

    3: Explorador de archivos.

    4: Buscar música.

    Space: Reproducir/pausar.

    q: Salir.


Opcional: Habilitar MPD al inicio

Si deseas que MPD se inicie automáticamente al arrancar el sistema, habilita el servicio:

```bash
sudo systemctl enable mpd
```

Alias para activar y desactivar mpd

Alias para iniciar MPD y NCMPCPP:

```bash
alias musicon="sudo systemctl start mpd && ncmpcpp"
```

Alias para detener MPD:

```bash
alias musicoff="sudo systemctl stop mpd"
```

Otros ideas para los alias

Verificar si MPD está activo antes de iniciarlo:

```bash
alias musicon="sudo systemctl is-active mpd || sudo systemctl start mpd && ncmpcpp"
```

Alias para reiniciar MPD:

Si hacemos cambios en la configuración de MPD, a veces necesitas reiniciarlo. Podrías agregar un alias para eso:

```bash
alias musicrestart="sudo systemctl restart mpd"
```

Alias para ver el estado de MPD:

Si quieres ver rápidamente si MPD está activo o no, podrías crear un alias:

```bash
alias musicstatus="systemctl status mpd"
```

Alias para detener MPD y salir de NCMPCPP:

Si quieres un comando que detenga MPD y cierre NCMPCPP al mismo tiempo, podrías combinarlos:

```bash
alias musicoffall="sudo systemctl stop mpd && pkill ncmpcpp"
```


Agrega tus alias al final del archivo: (~/.bashrc o ~/.zshrc).


```bash
alias musicon="sudo systemctl start mpd && ncmpcpp"
alias musicoff="sudo systemctl stop mpd"
alias musicrestart="sudo systemctl restart mpd"
alias musicstatus="systemctl status mpd"
alias musicoffall="sudo systemctl stop mpd && pkill ncmpcpp"
```

Recarga la configuración de la shell:

```bash
source ~/.bashrc
```




