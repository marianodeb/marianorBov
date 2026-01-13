
```bash
PS1='\[\033[01;36m\] \[\033[01;33m\]\u\[\033[01;31m\]@\h\[\033[01;34m\]\w\[\033[1;32m\]\n$(__git_ps1 " (%s)")\[\033[1;36m\]\$\[\033[00m\]'
```

```bash
export PS1='\u@\h\[\033[01;34m\] \w\[\033[0;32m\]$(__git_ps1 " (%s)")\[\033[01;34m\]$\[\033[00m\] '
```

valores

    \ u: usuario actual
    \ h: nombre de máquina (host)
    \ H: nombre de máquina completa
    \ w: directorio de trabajo actual
    \ W: directorio de trabajo actual con el nombre de base (último segmento) sólo
    $ (__ git_ps1 «% s»): rama actual si está en un repositorio git, si no muestra nada.
    
```bash
export PS1='\u@\h\[\033[01;34m\] \w\[\033[0;32m\]\n$(__git_ps1 " (%s)")\[\033[01;34m\]$\[\033[00m\] '
```

valor 

    \ n: salto de linea


colores

```bash
    azul: \[\033[0;34m\]
    rojo: \[\033[0;31m\]
    rojo fluorescente: \[\033[1;31m\]
    verde: \[\033[0;32m\]
    verde fluorescente: \[\033[1;32m\]
    blanco fuerte: \[\033[1;37m\]
    gris: \[\033[0;37m\]
    patrón: \[\033[0m\]
```

0;31m / red      0;31m / bold red
0;32m / green    0;32m / bold green
0;33m / yellow   0;33m / bold yellow 
0;34m / blue     0;34m / bold blue
0;35m / purple   0;35m / bold purple
0;36m / cyan     0;36m / bold cyan
0;37m / white    0;37m / bold white

 otro ejemplo
 
```bash
export PS1='\[\033[01;33m\]\u\[\033[01;31m\]@\h\[\033[01;34m\]\w\[\033[1;35m\]\n$(__git_ps1 " (%s)")\[\033[1;36m\]$\[\033[00m\]'  
```
 
 0 Texto normal (este es el valor predeterminado incluso si no se establece ningún atributo)
 1 En la Terminal Debian, este valor especifica texto en negrita
 2 texto oscuro
 3 Subrayado de texto
 4 Para texto parpadeante
 5 Invierte el texto y los colores de fond
 6 Para texto oculto
 7 
 8 
 
 
 
 
Un personaje de campana: `\a`
La fecha, en formato «Día de la semana Mes Fecha» (por ejemplo, «Martes 26 de mayo»): `\d`
El formato se pasa a strftime (3) y el resultado se inserta en la cadena de solicitud; un formato vacío da como resultado una representación de tiempo específica de la configuración regional. Los tirantes son necesarios: `\D{format}`
Un personaje de escape: `\e`
El nombre de host, hasta el primer ‘.’: `\h`https://www.youtube.com/watch?v=96HGbOLx-V0
El nombre de host: `\H`
La cantidad de trabajos actualmente administrados por el shell: `\j`
El nombre base del nombre del dispositivo terminal del shell: `\l`
Una nueva línea: `\n`
Un retorno de carro: `\r`
El nombre del shell, el nombre base de $ 0 (la parte que sigue a la barra final): `\s`
La hora, en formato HH: MM: SS de 24 horas: `\t`
La hora, en formato de 12 horas HH: MM: SS: `\T`
La hora, en formato de 12 horas am / pm: `\@`
La hora, en formato HH: MM de 24 horas: `\A`
El nombre de usuario del usuario actual: `\u`
La versión de Bash (por ejemplo, 2.00): `\v`
El lanzamiento de Bash, versión + nivel de parche (por ejemplo, 2.00.0): `\V`
El directorio de trabajo actual, con $ HOME abreviado con una tilde (usa la variable $ PROMPT_DIRTRIM): `\w`
El nombre base de $ PWD, con $ HOME abreviado con una tilde:`\W`
El número de historial de este comando:`\!`
El número de comando de este comando: `\#`
Si el uid efectivo es 0, #, de lo contrario $: `\$`
El carácter cuyo código ASCII es el valor octal nnn: `\nnn`
Una barra invertida: `\\`
Comience una secuencia de caracteres que no se impriman. Esto podría usarse para incrustar una secuencia de control de terminal en el indicador: `\[`
Finaliza una secuencia de caracteres que no se imprimen: `\]`
 
 
 
 
 
 
https://www.youtube.com/watch?v=wOUYzKrGZaA
https://www.youtube.com/watch?v=96HGbOLx-V0
 
 
 
 
 
 
 
 
 
  
