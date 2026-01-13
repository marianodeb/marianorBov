---
Created: 01-05-2022 / 20:27:29
Last Modified: 04-05-2022 / 14:30:24
---

Los t�tulos en Obsidian se escriben con un # seguido de un espacio.

# T�tulo nivel 1
## T�tulo nivel 2
### T�tulo nivel 3
#### T�tulo nivel 4
##### T�tulo nivel 5
###### T�tulo nivel 6

# Ctrl + F para buscar

# Formateo del texto

**negrita** y __negrita__
*cursiva* y _cursiva_
***negrita y cursiva***
___negrita y cursiva___
==resaltado==
~~tachar texto~~ - un car�cter especial: ~~ (pulsar dos veces: Alt Gr + 4) 

Markdown no permite el subrayado para no confundirlo con los enlaces, aunque con HTML se puede conseguir.

Markdown tampoco permite tener m�s de dos l�neas en blanco. Si esto pasa, se ver�n en previsualizaci�n como una, como un simple espacio.

# Divisores y presentaciones

Los divisores se crean con tres guiones seguidos. Podr�amos crear presentaciones siempre y cuando cada diapositiva est� delimitada por 2 divisores.

![[Pasted image 20220502165419.png|443]]

---

presentaci�n 1
texto de la presentaci�n 1

---

presentaci�n 2
texto de la presentaci�n 2

---
---
---

# Citas
S�mbolo de mayor que (>) + espacio + texto de la cita

> Lo importante no es lo que sabes, sino lo que haces con lo que sabes


# Etiquetas
Las etiquetas son palabras (o palabra) que va precedido de una almohadilla (#) sin espacio. Por ejemplo: #To-Do #InProgress #Completed #tag

> Si click en la etiqueta, se nos mostrar�n todas las notas que posean dicha etiqueta.


# Listas
## Lista sin numerar

Se crean con un gui�n + espacio:
- Elemento 1
	- Elemento 1.1
	- Elemento 1.2
		- Elemento 1.2.1
		- Elemento 1.2.2
	- Elemento 1.3
- Elemento 2
	- Elemento 2.1
- Elemento 3


## Lista numerada

Se crean con un n�mero seguido de un punto y de un espacio:
1. Elemento 1
	1. Elemento 1.1
	2. Elemento 1.2
		1. Elemento 1.2.1
		2. Elemento 1.2.2
2. Elemento 2
3. Elemento 3

## Lista mixta (sin y con n�meros)

1. Elemento 1
	- Elemento 1.1
	- Elemento 1.2
		1. Elemento 1.2.1
		2. Elemento 1.2.2
- Elemento 2
- Elemento 3

## Lista de tareas

Se crean con un gui�n, espacio, abrimos corchetes, dejamos espacio o la marcamos con la x, espacio
- [ ] Tarea 1
	- [x] Tarea 1.1
	- [ ] Tarea 1.2
- [x] Tarea 2
- [x] Tarea 3
- [ ] Tarea 4


# Im�genes

Si se copia cualquier imagen en el portapapeles y se pega en obsidian, vemos el formato de la imagen, que es ![[]], con el nombre del archivo + su extensi�n precedida por un punto.

![[Pasted image 20220502170802.png]]

Para redimensionar la imagen ponemos el s�mbolo barra vertical (| - Alt Gr + 1) seguido del n�mero de p�xeles m�ximos en anchura o altidud, guardando las proporciones de la imagen. Si a�adimos n� x n� (anchura x altura) la redimensionaremos a nuestro gusto, sin guardar la proporci�n original.

![[Pasted image 20220502170802.png|222]]

![[Pasted image 20220502170802.png|222x111]]

Pero si la imagen estuviera fuera del alcance de nuestra b�veda, es decir, si no la tenemos en ninguna carpeta el formato ser� como un enlace externo precedido de una exclamaci�n (!), haciendo referencia a que est� empotrado. Se puede modificar sus dimensiones como lo hemos visto anteriormente.

![Engelbart](https://www.foodspring.es/magazine/wp-content/uploads/2020/11/essen_foodspring-2.jpg)

![Engelbart|100](https://www.foodspring.es/magazine/wp-content/uploads/2020/11/essen_foodspring-2.jpg)


# Bloques c�digo

Para crear bloques de c�digo, tenemos que usar la comilla a la derecha de la P en el teclado espa�ol dos veces. As� podemos incluir alg�n c�digo de lenguajes de programaci�n.

```js
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```

# Comentarios para que no compile Markdown

Gracias a no compilar comentarios en Markdown, en el editor vemos dicho comentario pero en previsualizaci�n no aparece. Es como un metadato.

%%
Es es un comentario: suscr�bete a Vict�logo :)
%%

# Car�cteres markdown que no quieras compilar

A�adir \ (barra invertida - Alt Gr + �) delante del car�cter (no detr�s):
\[\[no compila]]
\*\*no compila\*\*


# Tablas

| Nombre  | Valor |
| ------- | ----- |
| Docena  | 12    |
| Centena | 100   |
| Mil     | 1000  |
| Dos mil | 2000  |

# Enlaces externos 

## Enlaces externos con Markdown

 - https://obsidian.md/
	 - copiar y pegar directamente una URL
 - [Web de obsidian](https://obsidian.md/)
	 - Seleccionar texto y pulsar Ctrl + K y en el par�ntesis () poner la URL
	 - O pulsar Ctrl + K y en los corchetes [] escribir dentro el texto y en el par�ntesis () la URL
 - Ctrl+K sale el formato para incluir una url 

## Enlaces externos formato Obsidian

Recurso externo en mi equipo o red local, mediante obsidian, esto no es markdown:
[Link to note](obsidian://open?path=D:%2Fpath%2Fto%2Fficheroquesea.md)


`/` codificados con `%2F` 
` ` Espacios en blanco`%20`



## Enlaces entre notas con wikilinks

Se crean escribiendo dos \[\[ seguido de la nota que queremos hipervincular o enlazar y la seleccionamos.

Ej.: [[GU�A - Reglas de Markdown y HTML]]

Se puede cambiar el nombre de un link [[GU�A - Reglas de Markdown y HTML|si ponemos barra vertical dentro del nombre de la nota y despu�s del �ltimo caracter de esta]].

[M�s info](https://github.com/agathauy/wikilinks-to-mdlinks-obsidian)

## Transclusiones o notas empotradas (embeded) vs links

Archivo empotrado: \!\[\[GU�A - Reglas de Markdown y HTML]] - el archivo o nota se ve directamente en la nota, no hace falta salir de obsidian para ir a buscar el archivo o nota.

Link \[\[nota]] - vemos un link que si pinchamos nos conduce al archivo (en la ruta en la que existe).

Podemos decir con un # detr�s del �ltimo car�cter de la nota que queremos que la nota empiece o se vea desde un cabezado en espec�fico, as� no perderemos tiempo buscando el encabezado que queremos.

Link: \[\[Titulo#tituloencabezado]]

# Footnotes o notas a pie de p�gina

Ahora os[^nota2] ense�o el "c�digo" dentro[^nota1] de Obsidian para hacer una nota a pie de p�gina. [^nota1]

[^nota1]: Esto es una nota a pie de p�gina cualquiera.
[^nota2]: Nota 2: hola que tal

# Info extra
- Podemos poner enlaces a notas en encabezados







