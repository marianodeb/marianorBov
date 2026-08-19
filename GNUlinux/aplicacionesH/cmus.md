### Instalacion

```bash
sudo apt update
sudo apt install cmus
```
### 🎯 Control de Reproducción (Básico e Imprescindible)

Estas son las teclas que usarás el 90% del tiempo. Las letras están elegidas para que puedas usarlas sin mirar el teclado.

| Tecla | Acción | Por qué la necesitas |
| :--- | :--- | :--- |
| `c` | **Pausar / Reanudar** | La más importante. Úsala para silenciar la música rápido.  |
| `b` | **Canción siguiente** | Pasa a la siguiente pista.  |
| `z` | **Canción anterior** | Vuelve a la pista anterior.  |
| `x` | **Reiniciar canción** | Vuelve al segundo 0 de la pista actual.  |
| `v` | **Detener** | Para la música y rebobina la pista.  |
| `q` | **Salir de cmus** | Cierra el programa por completo.  |


### 🎚️ Control de Volumen y Búsqueda (Navegación Fina)

Estas teclas te permiten ajustar el sonido y moverte dentro de una canción.

| Tecla | Acción | Detalle |
| :--- | :--- | :--- |
| `+` o `=` | **Subir volumen** | Sube el volumen en un 10%.  |
| `-` | **Bajar volumen** | Baja el volumen en un 10%.  |
| `Izquierda` / `h` | **Retroceder 5 segundos** | Muy útil para volver a escuchar una frase.  |
| `Derecha` / `l` | **Avanzar 5 segundos** | Para saltarte una parte.  |
| `,` (coma) | **Retroceder 1 minuto** | Ideal para saltos grandes hacia atrás.  |
| `.` (punto) | **Avanzar 1 minuto** | Ideal para saltos grandes hacia adelante.  |


### 🔁 Modos de Reproducción (Para no tener que tocar nada)

Activa estos modos para que la música no pare nunca.

| Tecla | Modo | Efecto |
| :--- | :--- | :--- |
| `s` | **Aleatorio (Shuffle)** | Reproduce las canciones en orden aleatorio.  |
| `r` | **Repetir lista (Repeat)** | Al terminar la lista, empieza de nuevo desde el principio.  |
| `Ctrl + r` | **Repetir una (Repeat One)** | Repite la misma canción una y otra vez.  |
| `Shift + c` | **Continuar (Continue)** | Hace que cmus no se detenga al terminar la lista. *Actívalo siempre*.  |


### 🗂️ Gestión de la Biblioteca y Cola (Organiza tu música)

Cuando quieras crear listas o añadir canciones a la cola.

| Tecla | Acción | Contexto |
| :--- | :--- | :--- |
| `e` | **Añadir a la cola (Queue)** | Añade la canción seleccionada a la "Lista de ahora". Se reproduce después de la actual.  |
| `y` | **Añadir a una lista** | Añade la canción seleccionada a la **lista de reproducción** que tengas activa en ese momento.  |
| `Shift + d` | **Eliminar** | Borra la canción seleccionada de la lista o cola actual.  |
| `p` | **Mover elemento abajo** | Dentro de la vista de Cola o Lista, mueve la canción seleccionada hacia abajo.  |
| `Shift + p` | **Mover elemento arriba** | Dentro de la vista de Cola o Lista, mueve la canción seleccionada hacia arriba.  |


### 🖥️ Navegación entre Ventanas (Para moverte por la interfaz)

Cmus tiene **7 vistas** diferentes. Cámbiate entre ellas con los números del 1 al 7.

| Tecla | Vista | ¿Para qué sirve? |
| :--- | :--- | :--- |
| `1` | **Álbumes / Artistas** | Ver tu música organizada por carpeta de artista/álbum.  |
| `2` | **Biblioteca completa** | Ver todas las canciones en una sola lista (la más útil para buscar).  |
| `3` | **Listas de reproducción** | Gestionar tus playlists.  |
| `4` | **Cola de reproducción** | Ver qué sonará a continuación.  |
| `5` | **Navegador de archivos** | Explorar tus carpetas en el disco duro para añadir música.  |
| `6` | **Filtros** | Configurar filtros inteligentes.  |
| `7` | **Configuración** | Cambiar teclas o colores.  |
| `Tab` | **Cambiar panel** | Cuando una vista tiene dos paneles (ej: vista 1 o 3), cambia el foco de uno a otro.  |
| `j` / `k` | **Moverse arriba/abajo** | Alternativa a las flechas del teclado (estilo vim).  |
| `Enter` | **Reproducir / Entrar** | Reproduce una canción o entra a una carpeta/álbum.  |


### 🔍 Cómo Buscar Canciones (El "Ctrl+F" de cmus)

Si tienes muchos artistas, usa la búsqueda.

1.  Estando en la vista `2` (Biblioteca), presiona `/` (barra inclinada) .
2.  Escribe el nombre del artista o canción (la búsqueda es **en vivo**, se filtra mientras escribes) .
3.  Presiona `Enter` para confirmar.
4.  Usa `n` para saltar al **siguiente** resultado de la búsqueda y `N` para el **anterior** .


### ⚙️ La Tecla "Mágica": `:`

Si en algún momento te lías o necesitas hacer algo muy concreto (como añadir una carpeta entera), presiona `:` (dos puntos).
Esto abre la **línea de comandos** .

- Escribe `add /ruta/de/tu/musica` y presiona `Enter` para añadir toda esa carpeta a tu biblioteca .
- Escribe `clear` para vaciar la lista de reproducción actual .
- Puedes ver todos los comandos posibles con `help`.


### 🎮 Bonus: Controlar cmus desde el juego (sin cambiar de ventana)

Si no quieres salir de **0 A.D.** ni pulsar `Alt+Tab`, puedes usar la terminal desde la que lanzaste cmus.

1.  Antes de abrir el juego, presiona `Ctrl+Z` en la terminal para pausar cmus y enviarlo a segundo plano.
2.  Abre 0 A.D. normalmente.
3.  Para controlar la música sin cerrar el juego:
    - Vuelve a la terminal (puedes usar `Ctrl+Alt+F1`/`F2` para cambiar de TTY si tu escritorio se bloquea, aunque lo más fácil es usar `tmux` como te expliqué antes).
    - Una vez en la terminal, escribe estos comandos y presiona `Enter`:
        - `cmus-remote -u` → **Pausar / Reanudar** la música .
        - `cmus-remote -n` → **Canción siguiente** .
        - `cmus-remote -r` → **Canción anterior** .
        - `cmus-remote -s` → **Detener** la música .

**Resumen práctico:** Con que te aprendas **`c`** (pausa), **`b`** (siguiente), **`v`** (stop), las **flechas** (volumen) y el **`/`** (buscar), ya tienes el 90% del control. El resto (modos `s` o `r`) lo activas solo cuando quieras cambiar el orden de la música.


**IR A UN DIRECTORIO Y TENER MUSICA**
```
cmus /ruta/de/tu/musica
```
- Entra directo ahi. La musica que este ahi adentro ya esta lista 

**VER LA MUSICA QUE TENES**
`2` - Ver biblioteca (todas las canciones en lista) 

**SELECCIONAR CANCION**
`j` - Bajar
`k` - Subir
`Enter` - Reproducir 

**CONTROLES BASICOS**
`c` - Pausar/reanudar
`b` - Siguiente cancion
`z` - Canción anterior
`v` - Detener
`q` - Salir 

**VOLUMEN**
`+` o `-` - Subir/bajar 


**AGREGAR MUSICA A LA BIBLIOTECA**

`5` - Abrir navegador de archivos
`j/k` - Moverse
`Enter` - Entrar a carpeta
`a` - Agregar cancion o carpeta seleccionada a la biblioteca
`:save` - Guardar biblioteca

**VER MUSICA QUE AGREGAS**

`2` - Ver biblioteca ordenada (lista plana, ahi se ve todo)

**SI SIGUE SIN APARECER**

`:add /ruta/completa/de/tu/musica` - Agregar por comando

**FORMATO SOPORTADO**
Si tenes .m4a o .aac, instalar ffmpeg:
`sudo apt install ffmpeg`

**VERIFICAR**
`:add` agrega. `2` muestra. Si no hay nada -> archivos no compatibles o biblioteca vacia.





