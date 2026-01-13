<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!--titlle - entre 55 y 65 caracteres-->
    <title>HTML</title>
        <!--Descriptions - no mas de 165 caracteres-->
    <meta name="descripcion" content="En esta pagina estamos aprendiendo los fundtamentos HTML"> 
    <link rel="canonical" href="hrrp://tudominio.com/la-url-canonical">
    <link rel="icon" href="assets/img/favicon.png">  
    <link rel="apple-touch-icon" href="assets/img/favicon.png">
    <meta name="theme-color" content="#ff6600">
    <meta property="og:tittle" content="Aprendiendo HTML">
    <meta property="og:descripcion" content="En esta pagina estamos aprendiendo los fundtamentos HTML">
    <meta property="og:image" content="https://tudominio.com/imag/_26x_c8bave2xo_1926022834.png">
    <meta property="og:url" content="https://tudominio.com/index.html">
    <meta name="twitter:card" content="summary">
    <meta name="twitter:site" content="@jonmircha">
    
    <style>
      h2 {
        color: rgb(43, 226, 150);
      }
    </style>
    <link rel="stylesheet" href="assets/estilos.css">
</head>
<body>
  <h2 id="inicio">Aprendiendo HTML</h2>
    
    <!-- https://emmet.io/
  - https://www.w3.org/html/
  - https://html.spec.whatwg.org/
  - https://www.w3.org/blog/news/archives...
  - https://developer.mozilla.org/es/docs...
  -https://htmlreference.io/ -->
  <!--ul>li*20>a-->
  <ul>
    <li><a href="index.html#encabezados">Encabezados HTML</a></li>
    <li><a href="index.html#texto-basico">Etiquetas de texto básicas</a></li>
    <li><a href="index.html#texto-semantica">Etiquetas de texto semánticas</a></li>
    <li><a href="index.html#etiqueta-saltos">Etiquetas de salto</a></li>   <!--L81 -->
    <li><a href="index.html#etiquetas-formateo">Etiquetas de formateo</a></li>
    <li><a href="index.html#etiquetas-semanticas-estructurales">Etiquetas Semánticas Estructurales</a></li>
    <li><a href="index.html#etiquetas-bloque-vs-linea">Etiquetas de Bloques vs etiquetas de Lineas</a></li>
    <li><a href="index.html#estilos-css-html">Estilos CSS en HTML</a></li>
    <li><a href="index.html#scripts">Scripts en HTML</a></li>  
    <li><a href="index.html#imagenes">Imagenes</a></li>   <!--L138 -->
    <li><a href="index.html#svg">SVG</a></li> <!--L146 -->
    <li><a href="index.html#figuras">Figuras</a></li>  <!--L167 -->
    <li><a href="index.html#listas-ordenadas">Listas Ordenadas</a></li>
    <li><a href="index.html#listas-desordenadas">Listas Desordenadas</a></li>
    <li><a href="index.html#listas-definicion">Listas de definicion</a></li>
    <li><a href="index.html#tablas">Tablas</a></li>           <!--L213 -->
    <li><a href="index.html#enlaces">Enlaces</a></li>     <!--L282 -->
    <li><a href="index.html#elementos-interactivos">Elementos interactivos</a></li>
    <li><a href="index.html#audio-video">Audio y Video</a></li>
    <li><a href="index.html#iframe">Iframe</a></li>
    <li><a href="index.html#formularios">Formularios</a></li>
    <li><a href="index.html#data-attributes">Data Attributes</a></li>
    <li><a href="index.html#meta-seo">Metaetiquetas para SEO</a></li>
    <li><a href="index.html#metaetiquetas-redes-s">Metaetiquetas para redes sociales</a></li>
    <li><a href="index.html#accesibilidad">Accesibilidad</a></li>
  </ul>
  <h2 id="encabezados">Encabezados HTML</h2>
  <h1>encabezaso 1 - solo puede sxistir uno por documento</h1>
  <h2>encabezaso 2</h2>
  <h3>encabezaso 3</h3>
  <h4>encabezaso 4</h4>
  <h5>encabezaso 5</h5>
  <h6>encabezaso 6</h6>
  <a href="index.html#inicio">🔼</a>
  <hr>
  <h2 id="texto-basico">Etiquetas de texto básicas</h2>
  <p>Un párrafo</p>
  <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quidem alias nobis aliquam eligendi quibusdam temporibus id dolores, consequatur voluptas voluptates ea omnis praesentium pariatur at vitae exercitationem in aliquid unde?</p>
  <p>
    Palabras en <b>negrita</b>, <i>italixa</i>, <u>subrayado</u>, e=mc<sup>2</sup>, H<sup>2</sup>O.
    <mark>marca de texto</mark> <small>letras pequñas</small>
  </p>
  <a href="index.html#inicio">🔼</a>
  <hr>
  <h2 id="texto-semantica">Etiquetas de texto semánticas</h2>
  <p>
    <blockquote>Yo solo sé, que no se nada</blockquote>
    <cite>Socrates</cite>
  </p>
  <p>
    <strong>Este texto es importante</strong>. <em>Este texto hace énfasis</em>
  </p>
  <a href="index.html#inicio">🔼</a>
  <hr>
  <h2 id="etiqueta-saltos">Etiquetas de salto</h2>
 <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit.<br> Vitae saepe ipsum temporibus facere molestias<br> possimus voluptatum asperiores delectus accusantium iste excepturi,<br> commodi alias maiores a qui quaerat dolorem doloribus ut.</p>
 <a href="index.html#inicio">🔼</a>
 <hr>
 <h2 id="etiquetas-formateo">Etiquetas de formateo</h2>
 <p>
    <pre>
      Tareas por hacer:
      -HTML
         -Terminar de grabar las secciones de este curso
         -Editar en un solo video 
      -CSS 
         -Comenzar a grabar secciones de -CSS 
         -Editar en un solo video
    </pre>
 </p>
 <p>
    <code>Este texto esta en formato de codigo</code>
 </p>
 <p>
    <pre>
      <cosde>
        import React fron "react";
        import Title from""./Title";

        function App {
            return &lt;Title /&gt;
        }
      </cosde>
    </pre>
 </p>
 <a href="index.html#inicio">🔼</a>
<hr>
<h2 id="etiquetas-semanticas-estructurales">Etiquetas Semánticas Estructurales</h2>
<div>Es una etiqueta contenedora que no tienen semanántica</div>
<header>header - Cabecera de un sitio web o de una sección</header>
<main>
  main - Define la sección principal dl documento, sólo puede existir una etiqueta main por documento
</main>
<footer>footer - Pié de página de unsitio web o de una sección</footer>
<nav>nav - Representa una sección</nav>
<article>
  article - Representa una sección autocontenido (que por sí sola se explica)
</article>
<aside>aside - Representa contenido complementario o secundario</aside>
<section>sectio - Representa una sección de contenido genérico</section>
<address>address - Representa una información de contacto</address>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="etiquetas-bloque-vs-linea">Etiquetas de Bloques vs etiquetas de Lineas</h2>
<div style="background-color: green;">La etiqueta de bloque por excelencia es la div</div>
<span style="background-color: aquamarine;">La etiqueta de línea por excelencia es la span, una etiquta de línea que solo ocupa el espacio necesario que tiene su contenido</span>
<sapan>Hola soy otra etiqueta span</sapan>
<br>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="estilos-css-html">Estilos CSS en HTML</h2>
<h2 id="scripts">Scripts en HTML</h2>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="imagenes">Imagenes</h2>
<img src="assets/img/Periodic-Table-of-HTML-Elements.png" alt="tabla periodica html">
<img src="assets/img/htmlmariano.png" alt="tirando lineas en html">
<img src="assets/img/6f061d950a7b0208ba3e588a6dd9f2d3562cc8e2.gif" alt="gif codeando">
<img src="assets/img/deblogo.svg" alt="debieansvg">
<br>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="svg">SVG</h2>
<svg
  width="24"
  height="24"
  viewBox="0 0 24 24"
  fill="none"
  xmlns="http://www.w3.org/2000/svg"
>
  <path
    fill-rule="evenodd"
    clip-rule="evenodd"
    d="M17 21C15.8954 21 15 20.1046 15 19V15C15 13.8954 15.8954 13 17 13H19V12C19 8.13401 15.866 5 12 5C8.13401 5 5 8.13401 5 12V13H7C8.10457 13 9 13.8954 9 15V19C9 20.1046 8.10457 21 7 21H3V12C3 7.02944 7.02944 3 12 3C16.9706 3 21 7.02944 21 12V21H17ZM19 15H17V19H19V15ZM7 15H5V19H7V15Z"
    fill="currentColor"
  />
</svg>
<br>
< href="https://www.debian.org/index.es.html" target="_blank">
  <img src="assets/img/deblogo.svg" alt="Pagina oficial debian" width="40" height="40">
  <br>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="figuras">Figuras</h2>
<figure>
  <img src="assets/img/_26x_c8bave2xo_1926022834.jpg" alt="Sin bateria">
  <figcaption>fig. Sin bateria</figcaption>
</figure>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="listas-ordenadas">Listas Ordenadas</h2>
<h3>Las estaciones del año</h3>
<ol>
  <li>Primavera</li>
  <li>Verano</li>
  <li>Otoño</li>
  <li>Invierno</li>
</ol>
<ol start="3">
  <li>Primavera</li>
  <li>Verano</li>
  <li>Otoño</li>
  <li>Invierno</li>
</ol>
<ol reversed>
  <li>Primavera</li>
  <li>Verano</li>
  <li>Otoño</li>
  <li>Invierno</li>
</ol>
<ol type="I">
  <li>Primavera</li>
  <li>Verano</li>
  <li>Otoño</li>
  <li>Invierno</li>
</ol>
<ol type="1">
  <li>Primavera</li>
  <li>Verano</li>
  <li>Otoño</li>
  <li>Invierno</li>
</ol>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="listas-desordenadas">Listas Desordenadas</h2>
<ul type="square">
  <li>Terminar de grabar los fragmentos del curso HTML</li>
  <li>Editar el video final</li>
  <li>subirlo a You Tube</li>
</ul>
<ul type="disc">
  <li>Terminar de grabar los fragmentos del curso HTML</li>
  <li>Editar el video final</li>
  <li>subirlo a You Tube</li>
</ul>
<ul type="circle">
  <li>Terminar de grabar los fragmentos del curso HTML</li>
  <li>Editar el video final</li>
  <li>subirlo a You Tube</li>
</ul>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="listas-definicion">Listas de definicion</h2>
<dl>
  <dt>HTML</dt>
  <dd>Es un lenguaje de marcado que define el contenido de una web</dd>
  <dt>CSS</dt>
  <dd>Es un lenguaje de definicion que da estilos al cÓdgio HTML</dd>
  <dt>Java Script</dt>
  <dd>Es el lenguaje de la web</dd>
</dl>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="tablas">Tablas</h2>
<table>
  <tr>
    <td>Nombre</td>
    <td>Constelación</td>
    <td>Tipo</td>
  </tr>
  <tr>
    <td>Ikki</td>
    <td>Fénix</td>
    <td>Bronce</td>
  </tr>
  <tr>
    <td>Shaina</td>
    <td>Ofiuco</td>
    <td>Plata</td>
  </tr>
  <tr>
    <td>Saga</td>
    <td>Géminis</td>
    <td>Dorado</td>
  </tr>
</table>
<br><br><br>
<table>
  <thead>
    <tr>
      <th colspan="3">Tabla de los Santos de Atenas</th>
    </tr>
  <tr>
<th>Nombre</th>
<th>Constelaciones</th>
<th>Tipo</th>
  </tr>
  </thead>
  <tbody>
  <tr>
    <td>Ikki</td>
    <td>Fénix</td>
    <td>Bronce</td>
  </tr>
  <tr>
    <td>Mistry</td>
    <td>Lagarto</td>
    <td>Plata</td>
  </tr>
  <tr>
    <td>Saga</td>
    <td>Géminis</td>
    <td>Dorado</td>
  </tr>
  <tr>
    <td>Shaina</td>
    <td rowspan="2">Ofiuco</td>
    <td>Plata</td>
  </tr>
  <tr>
    <td>Odiseo</td>
    <td>Dorado</td>
  </tr>
  </tbody>
  <tfoot>
<tr>
  <th colspan="3"><small>Sanit Seiya fue creado por masami Kurumada</small></th>
</tr>
  </tfoot>
</table>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="enlaces">Enalaces</h2>
<a href="hola.html" target="_blank">Pagina2</a>
<br>
<a href="https://jonmircha.com" target="_blank" rel="nofollow">Vista la pagina de jon</a>
<br>
<a href="https://www.debian.org/index.es.html" target="_blank">
  <img src="assets/img/deblogo.svg" alt="Pagina oficial debian" width="40" height="40">
  <br>
  <a href="https://youtube.com" target="_blank">
    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" clip-rule="evenodd" d="M5 7H19C19.5523 7 20 7.44771 20 8V16C20 16.5523 19.5523 17 19 17H5C4.44772 17 4 16.5523 4 16V8C4 7.44772 4.44772 7 5 7ZM2 8C2 6.34315 3.34315 5 5 5H19C20.6569 5 22 6.34315 22 8V16C22 17.6569 20.6569 19 19 19H5C3.34315 19 2 17.6569 2 16V8ZM10 9L14 12L10 15V9Z" fill="currentColor" /></svg>
  </a>
</a>
<br>
<a href="mailto:krozok13@gmail.com">Enlace a correo electrónico</a>
<br>
<a href="tel:1135708696">Enlace a télefono</a>
<br>
<a href="https://api.whatsapp.com/send?phone=1135708696&text=Hola">Enlace hacia whatsapp</a>
<br>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="elementos-interactivos">Elementos interactivos</h2>
<button onclick="alert('Le diste click al botón')">Este es un boón</button>
<details>
  <summary>Titulo del acordeon</summary>
  <article>
    <h3>Contenido del acordeón</h3>
    <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Mollitia vel perspiciatis, accusamus quia quaerat dicta eveniet veniam, necessitatibus minima explicabo reiciendis et obcaecati accusantium iste quae natus expedita eum facilis.</p>
    <img src="assets/img/_26x_c8bave2xo_1926022834.jpg">
    <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Mollitia vel perspiciatis, accusamus quia quaerat dicta eveniet veniam, necessitatibus minima explicabo reiciendis et obcaecati accusantium iste quae natus expedita eum facilis.</p>
    <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Mollitia vel perspiciatis, accusamus quia quaerat dicta eveniet veniam, necessitatibus minima explicabo reiciendis et obcaecati accusantium iste quae natus expedita eum facilis.</p>
  </article>
</details>
<details>
  <summary>Metas a realizar</summary>
  <h3>Lista de tareas</h3>
  <ol>
    <li>Aprender HTML</li>
    <li>Aprender CSS</li>
    <li>Aprender JS basico</li>
    <li>Aprender logica de programacion</li>
    <li>Aprender lo basico de python</li>
    <li>Aprender lo basico de git</li>
    <li>Aprender lo basico de base de datos</li>
  </ol>
  <img src="assets/img/htmlmariano.png">
</details>
<dialog open>
  Esto es una ventana modal en HTML
</dialog>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="audio-video">Audio y Video</h2>
<audio src="assets/media/Y&V - Lune [NCS Release] (128kbit_AAC).m4a" controls preload=""></audio>
<br>
<video src="assets/media/El mal uso de la tecnología.mp4" controls></video>
<br>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="iframe">Iframes</h2>
<iframe src="hola.html" frameborder="1"></iframe>
<br>
<iframe src="https://www.compucalitv.com/"frameborder="1"></iframe>
<br>
<iframe src="assets/media/emmet-cheat-sheet.pdf" frameborder="1"></iframe>
<br>
<iframe src="https://www.google.com/maps/embed?pb=!1m10!1m8!1m3!1d404.1686357591267!2d-58.37835075047691!3d-34.81126478756043!3m2!1i1024!2i768!4f13.1!5e1!3m2!1ses-419!2sar!4v1691691070921!5m2!1ses-419!2sar" width="600" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
<br>
<iframe width="560" height="315" src="https://www.youtube.com/embed/WQmGwmc-XUY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="formularios">Formularios</h2>
<input type="text">
<br>
<input type="checkbox">
<br>
<input type="radio">
<br>
<input type="date">
<br>
<input type="color">
<br>
<input type="button" value="Botón">
<br>
<input type="submit">
<br>
<input type="reset">
<br>
<input type="file">
<br>
<input type="file" multiple>
<br>
<input type="hidden" name="idioma" value="es">
<br>
<input type="email">
<br>
<input type="number">
<br>
<input type="tel">
<br>
<input type="password">
<br>
<input type="search"">
<br>
<textarea cols="50" rows="10"></textarea>
<br>
<select name="" id="">
  <option value="">HTML</option>
  <option value="">CSS</option>
  <option value="">JS</option>
  <option value="">PHP</option>
  <option value="">Phyton</option>
</select>
<br>
<select name="" id="" multiple>
  <option value="">HTML</option>
  <option value="">CSS</option>
  <option value="">JS</option>
  <option value="">PHP</option>
  <option value="">Phyton</option>
</select>
<br>
<input type="text" value="mariano" readonly disabled>
<br>
<input type="text" placeholder="Mandale tu nombre perri">
<br>
<h3>Ejemplo de Formulario</h3>
<h4>Fromulario de Login</h4>
<!--
  https://miservidor.com/?usuario=marianoc
  https://miservidor.com/?usuario=mariano&password=1234
-->
<form action="https://miservidor.com" method="post" autocomplete="off">
  <label for="usuario">usuario:</label>
  <input type="text" name="usuario" id="usuario" placeholder="Ecribe tu usuario" pattern="^[A-Za-z]+$" title="El campo solo acepta letas" required>
  <br>
  <label for="password">contraseña:</label>
  <input type="password" name="password" id="password" placeholder="Escribe tu contraseña" required>
  <br>
  <input type="submit">
  <br>
  <input type="reset">
  <br>
</form>
 <br>
 <h4>Selects, Radio y Checkbox</h4>
 <form>
  <p>Elige tu idioma</p>
 <select name="idioma">
  <option value="">Elige un opción</option>
  <option value="es">Español</option>
  <option value="en">Ingles</option>
  <option value="fr">Frances</option>
  <option value="it">Italiano</option>
  <option value="pt">Portugues</option>
  <input type="submit">
  <input type="reset">
 </select>
  <P>Elige tu lenguaje de programacion</P>
  <input type="radio" name="lenguaje" id="radio-js" value="js">
  <label for="radio-js">JavaScripts</label>
  <input type="radio" name="lenguaje" id="radio-py" value="py">
  <label for="radip-py">Python</label>
  <input type="radio" name="lenguaje" id="radio-php" value="php">
  <label for="">PHP</label>
  <p>Elige tus intereses:</p>
  <label>
    <input type="checkbox" name="intereses" value="deportes">
    Deporte
  </label>
  <label>
    <input type="checkbox" name="intereses" value="Finanzas">
    Finanzas
  </label>
  <label>
    <input type="checkbox" name="intereses" value="salud">
    Salud
  </label>
  <label>
    <input type="checkbox" name="intereses" value="politica">
    Politica
  </label>
  <label>
    <input type="checkbox" name="intereses" value="ecologia">
    Ecología
  </label>
  <p>
    <label>
      <input type="checkbox" name="terminos" required>
      ¿Acepta terminos y condiciones?
    </label>
  </p>
  <input type="submit">
  <input type="reset">
</form>
<h4>Formulario de contacto</h4>
<form action="https://formsubmit.co/krozok13@gmail.com" method="post">
  <input type="text" name="nobmre" placeholder="Escribe tu nombre" pattern="^[A-Za-zÑñÁáÉéÍíÓóÚúÜü\s]+$" title="Nombre solo acepta letras y espacios en blanco" required>
  <br>
  <input type="email" name="correo" placeholder="Escribe tu coreeo" pattern="^(\w+[/./-]?){1,}@[a-z]+[/.]\w{2,}$" title="Formato de correo invalido" required>
  <br>
  <textarea name="comentario" cols="30" rows="10" required></textarea>
  <br>
  <input type="submit">
</form>
<a href="index.html#inicio">🔼</a>
<hr>
<h2 id="data-attributes">Data Attributes</h2>
<ul>
  <li data-id="1" data-name="spring">Primaver</li>
  <li data-id="2" data-name="summer">Verano</li>
  <li data-id="3" data-name="autumn">Otoño</li>
  <li data-id="4" data-name="wineter">Invierno</li>
</ul>
<hr>
<a href="index.html#inicio">🔼</a>
<h2 id="meta-seo">Metaetiquetas para SEO y moviles</h2>
<hr>
<a href="index.html#inicio">🔼</a>
<h2 id="metaetiquetas-redes-s">Metaetiquetas para redes sociales</h2>
<hr>
<a href="index.html#inicio">🔼</a>
<h2 id="accesibilidad">Accesibilidad</h2>
<h3 role="title">Las estaciones del año</h3>
<ul role="list">
  <li tabindex="1" role="listitem">Primavera</li>
  <li tabindex="2" role="listitem">Verano</li>
  <li tabindex="3" role="listitem">Otoño</li>
  <li tabindex="4" role="listitem">Invierno</li>
</ul>
<a role="link" aria-label="En este enlace encontraras más información sobre estaciones del año" href="#" target="_blank">Mas información...</a>
<hr>
<br><br><br><br><br><br><br><br><br><br><br><br><br><br>
<script>
  
  console.log("Hola estamos aprendiendo HTML");
</script> 
<script src="assets/ codigos.js"></script>
<hr>
<!--https://www.youtube.com/watch?v=-oK6zL01fNM&list=PLvq-jIkSeTUZYcX9SYwVe7f66afwd9qk_&ab_channel=jonmircha
        04/08/23  --- 13 Titulo y descripcion  
        05/08/23  ---24 
        06/08/23  ---34 
        09/08/23  ---38 
                         https://t.me/markroxo              -->
</body>
</html>