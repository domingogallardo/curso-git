
# Sesión 1 #

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Índice ##

- Introducción
- Configuración de Git: instalación, configuración de cliente,
  servidor de git
- Configuración de GitHub: creación y configuración de cuenta
- Creación de repositorios
- Trabajo en una rama
  Commit, diffs, tags, checkout a commits anteriores, reset, amend, recuperar
  ficheros de commits anteriores
- Subida al repositorio remoto

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Comandos git a aprender en esta sesión##

```
$ git init
$ git status
$ git add
$ git commit
$ git diff
$ git tag
$ git chckout
$ git amend
$ git reset
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Los proyectos software se almacenan en un árbol de ficheros ##

<!-- .slide: class="image-right" -->

<img border:0px style="margin-left:50px" src="imagenes/directory-structure.png" width="400px"/>

- Un proyecto software se almacena en un conjunto de **ficheros de
  código** en una
  estructura de directorios. Esta estructura se denomina a veces
  **árbol de ficheros**.
- Dos de las características básicas de los **ficheros de código** (código
  fuente, código HTML, CSS, ...) son:
  - Son **ficheros de texto**, no son binarios: el contenido crudo del
    fichero se corresponde directamente con lo que vemos en el
    editor. Normalmente los caracteres están codificados en UTF-8 y no
    existen apenas caracteres de control (fines de línea y tabuladores
    a lo sumo).
  - Son ficheros que estamos **continuamente cambiando**. Conforme se
    desarrolla un proyecto, se añade código en los ficheros, se crean
    nuevos ficheros, se borra código, se reorganizan los directorios
    del proyecto cambiando de sitio los ficheros, etc.
- Gracias a ser ficheros de texto, los cambios entre una versión y
  otra de un fichero se pueden detectar y codificar fácilmente. Esta
  es la base de cualquier sistema de control de versiones.


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Ejemplo ##

- Fichero inicial `index.html`

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
        <title>Mi título de página</title>
  </head>
  <body>
  </body>
</html>
```

- Lo cambiamos, añadiendo contenido:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
        <title>Mi título de página</title>
  </head>
  <body>
  <h1>Stark Corp</h1>
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">Nuestra misión</a></li>
    <li><a href="#">Proyectos</a></li>
    <li><a href="#">Contacto</a></li>
  </ul>
  </body>
</html>
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Diferencia ##

- La diferencia entre la primera versión y la segunda son las líneas
  que se han añadido en el `body`:

```diff
<body>
+ <h1>Stark Corp</h1>
+ <ul>
+   <li><a href="#">Home</a></li>
+   <li><a href="#">Nuestra misión</a></li>
+   <li><a href="#">Proyectos</a></li>
+   <li><a href="#">Contacto</a></li>
+ </ul>
</body>
```

- El comando `diff` de UNIX/Linux permite comprobar las diferencias
  entre dos ficheros.
<!-- Tres líneas en blanco para la siguiente transparencia -->



## Comandos diff y patch ##

- `diff` y `patch` son dos comandos creados en el sistema operativo
  UNIX en la década de los 70 que permiten comprobar cambios y aplicar
  cambios a ficheros.
  
- Por ejemplo, si la primera versión la tenemos en el fichero
  `index.html` y la segunda en `index_nuevo.html`, el
  comando para obtener los cambios es:


```
$ diff index.html index_nuevo.html > index.diff
```


```diff
7a8,14
>   <h1>Stark Corp</h1>
>   <ul>
>     <li><a href="#">Home</a></li>
>     <li><a href="#">Nuestra misión</a></li>
>     <li><a href="#">Proyectos</a></li>
>     <li><a href="#">Contacto</a></li>
>   </ul>
```

- El comando anterior guarda la diferencia entre los dos ficheros en
  el fichero `index.diff`. Podríamos ahora enviar este fichero a un
  compañero que tuviera la primera versión para que la actualice
  usando el comando `patch` para cambiar el fichero inicial y
  convertirlo en la segunda versión:
  
```
$ patch index.html index.diff
```

- Estos comandos son la base del funcionamiento de los sistemas de
  control de versiones, y en concreto de Git.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Control de versiones rudimentario ##
<!-- .slide: class="image-right" -->

- Una forma de realizar un control de versiones rudimentario de un
  proyecto es manteniendo múltiples versiones del directorio del
  proyecto.

<img border:0px style="margin-left:20px" src="imagenes/arbol-web-curso-git.png" width="300px"/>

- Vamos a trabajar en esta sesión con un proyecto muy sencillo: una
  simple página formada por un fichero árbol de directorios básico. El
  directorio principal se llama `web-curso-git` y tiene un fichero
  `index.html` y otro directorio `imagenes` con el fichero
  `increibles.png`.

- La forma más rudimentaria de mantener distintas versiones conforme estamos
  elaborando la web es manteniendo múltiples copias del directorio
  
<img border:0px style="float:none" src="imagenes/versiones-rudimentarias.png" width="1200px"/>

- Cuando decidimos fijar una versión del proyecto, le asignamos al
  directorio un nombre único y copiamos todo el directorio en otro
  nuevo en el que seguimos trabajando con la versión actual.


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Contro de versiones ##

- Un **sistema de control de versiones** es un sistema que registra los
  **cambios** a lo largo del tiempo en un fichero o un conjunto de
  ficheros, de forma que es posible **recuperar** más tarde **versiones
  específicas**.
- Si eres un desarrollador trabajando en un equipo desarrollando
  conjuntamente un proyecto software, el sistema de control de
  versiones te va a permitir cosas como:
   - **Revertir** un conjunto de ficheros a un estado previo.
   - **Comparar cambios** a lo largo del tiempo.
   - **Consultar** quién ha sido el último que ha modificado algo en algún
     fichero que está causando problemas.
   - Desarrollar en **una rama** independiente del tronco principal e
     integrarla cuando el desarrollo esté terminado.
- Si usas un sistema de control de versiones es posible **recuperar
  un estado anterior estable** si has roto algo en los ficheros que
  estás tocando.

<img src="imagenes/historia-versiones.png" width="1000px"/>

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Ventaja del desarrollo con un sistema de control de versiones ##

- Un sistema de control de versiones es la herramienta básica
  fundamental para el desarrollo de software en equipo.
- Cualquier sistema o metodología de desarrollo en equipo tiene como
  prerrequisito la utilización de un sistema de control de
  versiones.
  
- Distribución de tareas entre miembros del equipo e integración
  posterior del código.
- Revisión de código.
- Sistema de integración continua
- Mantenimiento de distintas versiones del producto desarrollado.
- Compartir código con desarrolladores externos.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Revisión de código ##


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Sistemas de control de versiones distribuidos ##

<!-- .slide: class="image-right" -->

<img border:0px style="margin-left:50px" src="imagenes/version-control-distribuido.png" width="500px"/>

- Git y Mercurial son sistemas de control de versiones
  distribuidos.
- Cada desarrollador tiene un repositorio local completo, con toda la
  historia de cambios.
- Los cambios se realizan en cada repositorio local y se comparten con
  los comandos `push` (publicar cambios) y `pull` (bajar cambios).
- Suele haber un repositorio central remoto al que están conectados
  todos los desarrolladores del equipo y en el que se centraliza el
  desarrollo del proyecto.
- Se ubica en un servicio externo como GitHub o Bitbucket o en un
  servicio montando por nosotros (servidor de Git propio o servicio
  como GitLab).

<!-- Tres líneas en blanco para la siguiente transparencia -->



## GitHub ##

<!-- Tres líneas en blanco para la siguiente transparencia -->




## Ejercicio: Alta en GitHub ##
<!-- .slide: data-background="#cbe0fc"-->

<!-- Tres líneas en blanco para la siguiente transparencia -->




## Comandos relacionados con actualización ##

<!-- Tres líneas en blanco para la siguiente transparencia -->



## git commit ##

```bash
$ git status

On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean

$ git add imagenes
$ git commit -m "Añadidas las imágenes"
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Commits ##

- Un commit define un conjunto de cambios en el árbol de ficheros:
   - Cambios en el contenido de los ficheros:     <!-- .element: class="fragment" data-fragment-index="1" -->

   ```diff
    Este texto ya estaba
    -Este era el texto antiguo
    +Este es el texto cambiado
    +Y este texto se ha añadido
    Este es el texto que había```
    <!-- .element: class="fragment" data-fragment-index="1" -->
   
   - Ficheros añadidos  <!-- .element: class="fragment" data-fragment-index="2" -->
   - Ficheros eliminados   <!-- .element: class="fragment" data-fragment-index="3" -->
   - Ficheros cambiados de nombre    <!-- .element: class="fragment" data-fragment-index="4" -->

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Slide 2 ##

<img src="imagenes/certificados.png" height="400px"/>

- Ítem 1
- Ítem 2

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Slide 3 ##

<!-- .slide: class="image-right" -->

<img border:0px style="margin-left:20px" src="imagenes/certificados.png" height="400px"/>

- Ítem 10
- Ítem 20

<!-- Tres líneas en blanco para la siguiente transparencia -->



<!-- .slide: data-background-image="imagenes/gafas-adventure.gif"  -->


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Ejercicio: copiar los commits del proyecto de GitHub ##
<!-- .slide: data-background="#cbe0fc"-->

<!-- Tres líneas en blanco para la siguiente transparencia -->



## git commit ##

```bash
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   css/theme/white.css
	modified:   index.html
	modified:   sesion-01.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	imagenes/gafas-adventure.gif
	../reveal.js/

no changes added to commit (use "git add" and/or "git commit -a")
$ git add .
$ git commit -m "Actualizado el popup con el aviso de error"
$ git status
```
