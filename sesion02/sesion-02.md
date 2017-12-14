
# Sesión 2 #

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Índice ##

- Trabajo con el repositorio remoto
- Cómo cambiar la historia
- Ramas

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Comandos git a aprender en esta sesión##

```txt
$ git clone
$ git pull
$ git fetch
$ git amend
$ git reset
$ git branch
$ git checkout -b
$ git merge
$ git rebase
$ git cherry-pick
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Repositorios remotos ##

<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/dos-repos-remotos.png" width=400px/>

- La naturaleza distribuida de Git hace posible tener tantos
  repositorios remotos como queramos.
- Git permite darles un nombre lógico a cada uno de ellos. El nombre
  por defecto del primero de ellos es `origin`.
- Por ejemplo, supongamos que queremos publicar un proyecto open
  source. Podemos tener un repositorio remoto privado (sólo
  accesible por nosotros) en el que trabajamos hasta tener una nueva
  versión y un repositorio público al que subiremos los cambios cuando
  los hayamos comprobado bien en el repo privado.


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Repositorios remotos en proyectos open source ##

<img src="imagenes/repos-open-source.png" width=600px/>

- Normalmente el equipo de desarrollo tiene un único repositorio
  remoto sobre el que se trabaja, pero son posibles otras
  configuraciones.
- Cuando queremos aportar una modificación a un proyecto open source
  es habitual trabajar con dos repositorios remotos:
  - el del proyecto original (se suele llamar `upstream`) sobre el que
  no realizamos cambios directos.
  - nuestra copia particular obtenida con un **fork**, que es en la
    que realizamos las modificaciones (`origin`).
- Varios compañeros podemos trabajar añadiendo commits a nuestro
  repositorio.
- Cuando se ha terminado se solicita un _pull request_ al repositorio
  del proyecto original para incorporar nuestras aportaciones.
- Trabajaremos más adelante con los pull requests.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Comando "git clone" ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/dos-repos-locales.png" width=370px/>

- Vamos a practicar con los comandos de git para trabajar con repositorios
  remotos.
- Trabajaremos como indica la figura, con un repositorio remoto (el
  que ya tenemos) conectado a dos repositorios locales (uno de ellos
  ya lo tenemos también).
- Vamos a crear el otro. Nos movemos al directorio padre del
  directorio `web-ejemplo` y clonamos allí el repositorio remoto dándole
  otro nombre al directorio de descarga:

```txt
$ cd ..
$ git clone https://github.com/domingogallardo/curso-git-repo1.git web-ejemplo2
Cloning into 'web-ejemplo2'...
remote: Counting objects: 33, done.
remote: Compressing objects: 100% (19/19), done.
remote: Total 33 (delta 7), reused 31 (delta 5), pack-reused 0
Unpacking objects: 100% (33/33), done.
```

- Ahora tenemos dos directorios con repositorios locales conectados al
  mismo repositorio remoto:
  
```txt
$ ls -a
total 0
drwxr-xr-x   4 domingo  staff  128  8 dic 09:45 .
drwxr-xr-x  10 domingo  staff  320  8 dic 09:44 ..
drwxr-xr-x   7 domingo  staff  224  7 dic 18:06 web-ejemplo
drwxr-xr-x   7 domingo  staff  224  8 dic 09:45 web-ejemplo2
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Trabajamos en el nuevo repositorio descargado ##
<!-- .slide: data-background="#cbe0fc"-->

- Si nos movemos al nuevo directorio podemos comprobar que se han
  descargado todos los commits y etiquetas:
  
```txt
$ cd web-ejemplo2
$ git log --oneline
```

- Cargamos el directorio `web-ejemplo2` en una nueva carpeta de proyecto en Atom.
- Hacemos un nuevo commit en este nuevo repositorio y lo subimos al
  repositorio remoto.
  
```txt
# Modificamos el fichero index.html
$ git status
$ git commit -am "Cambiado el título de la web"
$ git push
```

- Comprobamos en GitHub que se ha subido el nuevo commit.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Nos movemos al repo local original ##
<!-- .slide: data-background="#cbe0fc"-->

- Cambios al repositorio `web-ejemplo` y comprobamos el estado del
  repositorio remoto con el comando `git remote show origin`:
  
```txt
$ cd ..
$ cd web-ejemplo
$ git remote show origin
```

<img src="imagenes/remote-show-origin.png" width="700px"/>

- El comando `git status` nos informa también de que estamos atrás con
  respecto al repo remoto.

```txt
$ git status
```

<img src="imagenes/git-status.png" width="800px"/>

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Comando "git pull" ##
<!-- .slide: data-background="#cbe0fc"-->

- Descargamos los cambios del repositorio remoto con el comando `git pull`:

```txt
$ git pull
```

<img src="imagenes/git-pull.png" width="700px"/>


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Añadimos un nuevo repositorio remoto ##
<!-- .slide: data-background="#cbe0fc"-->


- Podemos conectar el repo local con un nuevo repositorio remoto con `git remote add
  <nombre> <url>`.
  
- Para comprobarlo, creamos un nuevo repositorio en GitHub, con el nombre de
  `curso-git-repo2`, lo conectamos como repositorio remoto y subimos
  también allí el repositorio local:
  
```txt
$ git remote add remoto2 https://github.com/domingogallardo/curso-git-repo2.git
$ git push remoto2 master
Counting objects: 35, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (26/26), done.
Writing objects: 100% (35/35), 50.07 KiB | 6.26 MiB/s, done.
Total 35 (delta 9), reused 0 (delta 0)
remote: Resolving deltas: 100% (9/9), done.
To https://github.com/domingogallardo/curso-git-repo2.git
 * [new branch]      master -> master
```

- Comprobamos en GitHub que se ha subido el repositorio.

- El comando `git remote -v` nos da información sobre los nombres y
  las urls de los repositorios remotos:

```txt
$ git remote -v
origin	https://github.com/domingogallardo/curso-git-repo1.git (fetch)
origin	https://github.com/domingogallardo/curso-git-repo1.git (push)
remoto2	https://github.com/domingogallardo/curso-git-repo2.git (fetch)
remoto2	https://github.com/domingogallardo/curso-git-repo2.git (push)
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Dejamos de hablar de remotos y vamos con una pregunta muy frecuente: ##
## "Me he equivocado al hacer el último commit. ¿Es posible cambiarlo?" ##
<!-- Tres líneas en blanco para la siguiente transparencia -->



<!-- .slide: data-background-image="imagenes/boca-abierta.gif"  -->
<!-- Tres líneas en blanco para la siguiente transparencia -->



## Cambios en el último commit##

- Si todavía no hemos subido el commit al repositorio remoto tenemos
  varias opciones para cambiar el último commit.
- Si queremos cambiar **sólo el mensaje** del commit: 

   ```txt
   $ git commit --amend -m "<nuevo mensaje>"
   ```

- Si queremos **deshacer el commit**, pero no los cambios introducidos en
  él:
  
  ```txt
  $ git reset HEAD^
  ```
  
  - El espacio de trabajo no cambia, pero el commit se ha desecho.
  - `HEAD^` significa "el commit anterior a HEAD". Es equivalente a
    poner el número de commit anterior al actual:
    
  ```txt
  $ git reset <commit-anterior>
  ```
  
- Si queremos **eliminar los cambios** del último commit del espacio
  de trabajo y empezar de nuevo:
  
  ```txt
  $ git reset --hard HEAD^
  ```
  
<!-- Tres líneas en blanco para la siguiente transparencia -->



## Probamos "git commit --amend" ##
<!-- .slide: data-background="#cbe0fc"-->

- Seguimos en `web-ejemplo`. 
- Volvemos a modificar el fichero `index.html` y creamos un commit
  nuevo (sin subirlo al repositorio remoto):

```txt
# Modificamos index.html
$ git commit -am "Commit a eliminar"
$ git log --oneline
36cb05d (HEAD -> master) Commit a eliminar
d02dbfb (remoto2/master, origin/master) Nuevo título de la web
e498cdc (tag: v0.1) Últimos ajustes
...
```

- Ahora podemos cambiar el mensaje del commit:

```txt
$ git commit --amend -m "Nuevo mensaje a eliminar"
[master 0358a98] Nuevo mensaje a eliminar
 Date: Fri Dec 8 19:05:50 2017 +0100
 1 file changed, 1 insertion(+), 1 deletion(-)
$ git log --oneline
0358a98 (HEAD -> master) Nuevo mensaje a eliminar
d02dbfb (remoto2/master, origin/master) Nuevo título de la web
e498cdc (tag: v0.1) Últimos ajustes
...
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Probamos "git reset" ##
<!-- .slide: data-background="#cbe0fc"-->

- Vamos a deshacer el último commit, pero manteniendo los cambios
  realizados:

```txt
$ git reset HEAD^
Unstaged changes after reset:
M	index.html
$ git status
```

<img src="imagenes/git-status2.png" width="800px"/>

```txt
$ git log --oneline
d02dbfb (HEAD -> master, remoto2/master, origin/master) Nuevo título de la web
e498cdc (tag: v0.1) Últimos ajustes
...
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Probamos "git reset --hard" ##
<!-- .slide: data-background="#cbe0fc"-->

- Volvemos a hacer el commit con el cambio que hay en el espacio de
  trabajo:
  
```txt
$ git commit -am "Este commit sí que lo eliminamos"
[master 81a5217] Este commit sí que lo eliminamos
 1 file changed, 1 insertion(+), 1 deletion(-)
$ git log --oneline
81a5217 (HEAD -> master) Este commit sí que lo eliminamos
d02dbfb (remoto2/master, origin/master) Nuevo título de la web
e498cdc (tag: v0.1) Últimos ajustes
...
```

- Y ahora eliminamos definitivamente el último commit y sus cambios:

```txt
$ git reset --hard HEAD^
HEAD is now at d02dbfb Nuevo título de la web
$ git log --oneline
d02dbfb (HEAD -> master, remoto2/master, origin/master) Nuevo título de la web
e498cdc (tag: v0.1) Últimos ajustes
...
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Nuevos comandos ##

|Comando | Explicación |
|-------|--------------|
| `git clone <URL repositorio>` | Se descarga el repositorio remoto |
| `git remote show <remoto>` | Se conecta con el repositorio remoto y comprueba su estado |
| `git pull` | Actualiza el repo local con los últimos cambios del repo remoto  |
| `git remote add <remoto> <URL>` | Añade un repositorio remoto al repo local |
| `git remote -v` | Describe nombres y URLs de los repos remotos conectados al repo local |
| `git commit --amend -m "<mensaje>"` | Actualiza el mensaje del último commit |
| `git reset HEAD^` | Elimina el último commit de la historia local, manteniendo los cambios en el espacio de trabajo |
| `git reset --hard HEAD^`| Elimina el último commit y los cambios introducidos |
| `git reset <commit-anterior>` | Elimina todos los commits hasta el commit indicado, manteniendo los cambios en el espacio de trabajo |
| `git reset --hard <commit-anterior>` | Elimina todos los commits hasta el commit indicado y los cambios introducidos |

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Empezamos con las ramas ##
<!-- Tres líneas en blanco para la siguiente transparencia -->



<!-- .slide: data-background-image="imagenes/volando.gif"  -->
<!-- Tres líneas en blanco para la siguiente transparencia -->



## Ramas ##

- El modelo de ramas de Git es una de sus características más
  importantes y que más lo diferencia del resto de SCVs.
- Git permite realizar ramas de forma **increíblemente ligera**, haciendo
  las operaciones relacionadas con ellas y permitiendo movernos de una
  rama a otra de forma casi instantánea.
- A diferencia de otros SVCs (como subversion), Git hace fácil y
  promueve el uso flujos de trabajo en los que se **abren ramas y se
  mezclan a menudo**, incluso múltiples veces a lo largo del día.
- Si entiendes y dominas el uso de esta característica tendrás una
  potente herramienta que cambiará para siempre la forma en la que tú
  y tu equipo desarrolla.

<img src="imagenes/rama.png" width="700px"/>


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Desarrollo usando ramas  ##

- Una rama nos permite probar cambios en el proyecto **sin
  afectar** el proyecto principal.
- Podemos **abrir una rama** para experimentar introduciendo cambios,
  publicarlos en el repositorio remoto para que otros compañeros
  trabajen con ellos.
- El desarrollo principal puede también continuar avanzando sin
  necesidad de esperar a terminar la rama.
- Si el desarrollo termina gustándonos, **mezclaremos la rama** con
  el proyecto principal.
- Podemos usar esta estrategia distintas veces al mismo tiempo y tener
  múltiples ramas abiertas con **desarrollo simultáneo de múltiples
  características** que terminan integrándose en el proyecto de forma asíncrona.

<img src="imagenes/mezcla-rama.png" width="900px"/>

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Primera aproximación al trabajo con ramas ##
<!-- .slide: class="image-right" -->
<!-- .slide: data-background="#cbe0fc"-->

<img style="margin-left:40px" src="imagenes/antes-de-abrir-ramas.png" width="600px"/>

- Nos vamos al directorio `web-ejemplo`. Y hacemos

 ```txt
 $ git log --oneline
 ```

- En el directorio de trabajo (HEAD) tenemos el último commit de la
  rama `master`.
- La rama `master` es la única rama con la que hemos trabajado hasta
  ahora. Es la rama que se crea por defecto cuando se inicializa el
  repositorio de Git.

<!-- Tres líneas en blanco para la siguiente transparencia -->



##  Comando "git branch"##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/nueva-rama.png" width="400px"/>

- Creamos una nueva rama con el comando `git branch <nombre-rama>` y
  la llamamos `prueba`:

 ```txt
 $ git branch prueba
 ```

- ¿Cómo sabe Git en qué rama nos encontramos? Para eso utiliza el
  puntero especial llamado `HEAD`. En el caso actual HEAD sigue
  apuntando a `master` ya que el comando `git branch` simplemente crea
  la nueva rama, pero no nos mueve a ella.

```txt
$ git log --oneline
d02dbfb (HEAD -> master, prueba) Nuevo título de la web
e498cdc (tag: v0.1) Últimos ajustes
77a127a Añadida tipografía y colores
0bf82cd Layout principal y margen
...
```


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Nos cambiamos de rama ##
<!-- .slide: data-background="#cbe0fc"-->

- Para cambiarnos de rama debemos usar el comando `git checkout
  <rama>`:
  
```txt
$ git checkout prueba
```

<img style="margin-left:40px" src="imagenes/checkout-nueva-rama.png" width="500px"/>

- ¿Qué significa esto? Vamos a comprobarlo haciendo un nuevo commit en
  la nueva rama.
  
<!-- Tres líneas en blanco para la siguiente transparencia -->



## Hacemos cambios en la nueva rama ##
<!-- .slide: data-background="#cbe0fc"-->

- Por ejemplo, hacemos los siguientes cambios para que el pie de
  página sea más pequeño.
  
- Fichero `index.html`:

```diff
  </main>

+  <footer>
   <p>©Copyright 2050 by nobody. All rights reversed.</p>
+  </footer>
  </body>
```

- En el fichero `layout.css` añadimos:

```css
footer p {
  font-size: 10px;
}
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Y hacemos un commit ##
<!-- .slide: data-background="#cbe0fc"-->

- Hacemos un commit:

```txt
$ git commit -m "Pie de página pequeño"
[master 251b64a] Pie de página pequeño
 2 files changed, 6 insertions(+)
```

<img src="imagenes/avanza-la-rama.png" width="700px"/>

- La rama `prueba` se ha movido hacia adelante, junto con el nuevo
  commit, pero la rama `master` todavía apunta al commit en el que
  estábamos cuando hicimos `git checkout` para cambiar de rama.

- Comprobamos cargando la página en el navegador que el pie de página
  ha cambiado de tamaño.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Volvemos a master ##
<!-- .slide: data-background="#cbe0fc"-->

- Volvemos a `master` con otro `git checkout`:

```txt
$ git checkout master
```

<img src="imagenes/volvemos-a-master.png" width="700px"/>

- El puntero `HEAD` vuelve a apuntar a `master` y todos los ficheros
  del espacio de trabajo han cambiado al contenido de ese commit.
- Si comprobamos en el navegador veremos que el pie de página ha
  vuelto a tener el tamaño original.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Cambio de rama en Git ##

> Cuando en Git cambiamos de rama, cambian los ficheros del directorio
> de trabajo de forma instantánea.

- Si cambias a una rama antigua, los ficheros de tu directorio de
trabajo se cambiarán a cómo eran en la última vez que comiteaste en
esa rama.

- Si en tu espacio de trabajo hay cambios no comiteados, cuando
  cambias de rama los cambios se mantendrán en el espacio de trabajo
  (si no quieres que pase eso, puedes comitear los cambios antes de
  cambiar de rama o hacer _stash_; lo veremos más adelante).
  
- Si Git no puede cambiar limpiamente los ficheros del espacio de
  trabajo por los de la rama, no te dejará cambiar de rama.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Hacemos otro commit en master ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->


<img style="margin-left:40px" src="imagenes/nuevo-commit-master.png" width="600px"/>


- Ahora, estando en `master`, cambiamos otra vez el título de la
  página web:

```diff
   </head>
   <body>
 
-   <h1>Mi página web</h1>
+   <h1>Mi nueva página web</h1>
 
    <nav>
```

- Y hacemos un commit (estando en la rama `master`):

```txt
$ git commit -am "Cambiado el título"
[master 41c360f] Cambiado el título
 1 file changed, 1 insertion(+), 1 deletion(-)
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Vemos la historia del repositorio ##
<!-- .slide: data-background="#cbe0fc"-->

- Podemos ver la historia del repositorio usando `git log` con el
  parámetro `--graph` y `--all`:
  
```txt
$ git log --oneline --graph --all
* 41c360f (HEAD -> master) Cambiado el título
| * ec7e05b (prueba) Pie de página pequeño
|/  
* d02dbfb Nuevo título de la web
* e498cdc (tag: v0.1) Últimos ajustes
* 77a127a Añadida tipografía y colores
* 0bf82cd Layout principal y margen
* 3fd14f1 Añadimos cabecera de navegación
* 59e0464 Añadidos márgenes al documento
...
```

- La historia se lee de abajo a arriba. 
- Vemos que `HEAD` apunta a `master` (el espacio de trabajo está en
  `master`) y que es una historia que diverge en el commit `d02dbfb`.
- Cuando mezclemos ambas ramas, Git buscará ese commit inicial y
  comprobará si los cambios entre las dos ramas pueden realizarse sin
  que unos entren en conflicto con otros.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Mezclamos la rama prueba ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->


- Estando en la rama `master` mezclamos la rama `prueba`:

```txt
$ git merge prueba -m "Mezclamos la rama prueba"
Auto-merging index.html
Merge made by the 'recursive' strategy.
 css/layout.css | 4 ++++
 index.html     | 2 ++
 2 files changed, 6 insertions(+)
```

- Se crea un nuevo commit de merge, con el mensaje que hemos
  indicado. Es un commit especial que tiene dos padres y que realiza
  la mezcla de los cambios de las dos ramas.

<img style="margin-left:40px" src="imagenes/git-log-merge.png" width="600px"/>

- Podemos comprobar la historia de commits igual que antes:

```txt
$ git log --oneline --graph --all
```

- Comprobamos que la página web contiene ahora los cambios de las dos
ramas: nuevo título y nuevo pie de página.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Representación gráfica ##
<!-- .slide: data-background="#cbe0fc"-->


<img src="imagenes/merge.png" width="800px"/>


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Borramos la rama prueba ##
<!-- .slide: data-background="#cbe0fc"-->

- Como ya está integrada en `master` podemos borrar la rama `prueba`:

```txt
$ git branch -d prueba
Deleted branch prueba (was ec7e05b).
```

- El efecto del borrado consiste simplemente en que se elimina el
  puntero de la rama:
  
<img src="imagenes/rama-borrada.png" width="700px"/>

- Por último subimos el resultado al repositorio remoto:

```txt
$ git push
Counting objects: 11, done.
...
To https://github.com/domingogallardo/curso-git-repo1.git
   d02dbfb..fb8f62b  master -> master
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Creamos y mezclamos _issues_   ##
<!-- .slide: data-background="#cbe0fc"-->

- Vamos a probar un ejemplo común de flujo de trabajo con ramas y
  merge, que se usa continuamente en el mundo real.


1. Creamos una rama en para un _issue_ (característica a implementar)
   que queremos realizar en la web.
2. Trabajamos en la rama para desarrollar el _issue_.
3. Nos llega una incidencia de un arreglo crítico que hay que hacer en
   la web y tenemos que realizar un _hotfix_:
   1. Cambiamos a la rama de producción (`master`)
   2. Creamos una rama para realizar el _hotfix_.
   3. Después de que están probados los cambios, mezclamos el _hotfix_ y
      lo _pusheamos_ a producción.
4. Volvemos a nuestra historia original y seguimos trabajando hasta
   que probamos y mezclamos el _issue_.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Creamos la rama con el _issue_ ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/ejemplo-issue1.png" width="400px"/>

- Representamos el estado inicial del proyecto con la figura
  anterior. 
  
- Hemos decidido trabajar en el _issue_ número 53, que escogemos del
  sistema de tracking de _issues_ que nuestra empresa esté usando.

- Creamos una rama nueva en la que trabajar con el comando `git
  checkout` con el parámetro `-b`:

<img style="margin-left:40px" src="imagenes/ejemplo-issue2.png" width="400px"/>

```txt
$ git checkout -b iss53
Switched to a new branch 'iss53'
```

- Esto es un modo abreviado de:

```txt
$ git branch iss53
$ git checkout iss53
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Trabajamos en el _issue_ ##
<!-- .slide: data-background="#cbe0fc"-->

- Para desarrollar el _issue_ 53 hacemos algunos cambios en el texto
  del artículo y hacemos commit:
  
```txt
# Modificamos el artículo del index.html
$ git commit -am "Completando el artículo [issue 53]"
[iss53 191f0db] Completando el artículo [issue 53]
 1 file changed, 1 insertion(+), 5 deletions(-)
```

- Al hacer esto el puntero de la rama en la que estamos se mueve
  también hacia adelante:
  
<img src="imagenes/ejemplo-issue3.png" width="600px" />


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Cambios sin comitear ##
<!-- .slide: data-background="#cbe0fc"-->

- Ahora llega la petición de realizar un arreglo rápido en la rama de
  producción: tenemos que añadir una dirección de correo en la página
  principal. No hay ningún problema en conservar el trabajo realizado en el
  _issue_, todo lo que tenemos que hacer es cambiarnos a la rama
  `master`.

- Si en el espacio de trabajo o en el área de stage tenemos cambios
  sin comitear que entran en conflicto con la rama a la que nos
  movemos, Git no nos dejará cambiar. Vamos a probarlo.

- Estando en la rama `issue53` hacemos más cambios en el artículo, sin
  hacer commit:
  
```txt
# Hacemos más cambios en el artículo index.html,
# pero no hacemos commit
$ git status
On branch iss53
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
```

- Si ahora intentamos cambiar a `master`:

```txt
$ git checkout master
error: Your local changes to the following files would be overwritten by checkout:
	index.html
Please commit your changes or stash them before you switch branches.
Aborting
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Usamos "git stash" ##
<!-- .slide: data-background="#cbe0fc"-->

- Con `git stash` podemos eliminar los cambios actuales del espacio de
  trabajo y apilarlos en una pila (_stash_) de la que después podremos
  desapilarlos:
  
```txt
$ git stash
Saved working directory and index state WIP on iss53: 191f0db Completando el artículo [issue 53]
$ git status
On branch iss53
nothing to commit, working tree clean
```

- Podemos examinar el contenido de la pila:

```txt
$ git stash list
stash@{0}: WIP on iss53: 191f0db Completando el artículo [issue 53]
```

- El comando `git stash pop` desapila los cambios en el espacio de
  trabajo actual.
  
```txt
$ git stash pop
On branch iss53
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (178d16c6647adc28985253d08ed95de639e6d070)
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Cambiamos de rama y abrimos el hotfix ## 
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

- Volvemos a hacer `git stash` para apilar los cambios y cambiamos a
  `master` para realizar allí el hotfix:

```txt
$ git stash
Saved working directory and index state WIP on iss53: 191f0db Completando el artículo [issue 53]
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
```

- Realizamos el hotfix, creando una rama en la que lo completamos:

<img style="margin-left:40px" src="imagenes/ejemplo-issue4.png" width="500px"/>


```txt
$ git checkout -b hotfix
Switched to a new branch 'hotfix'
# Añadimos el correo electronico acme@gmail.com 
# en el pie de página
$ git commit -am "Añadida la dirección de email"
[hotfix 330b7f8] Añadida la dirección de email
 1 file changed, 1 insertion(+), 1 deletion(-)
```


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Mezclamos el hotfix con master ##
<!-- .slide: data-background="#cbe0fc"-->

- Podemos realizar los tests y asegurarnos de que el hotfix es el que
  queremos (en nuestro caso, bastaría con cargar la página en el
  navegador) y finalmente mezclamos en la rama `master` que es la que
  se despliega en producción:

```txt
$ git checkout master
$ git merge hotfix
Updating fb8f62b..330b7f8
Fast-forward
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

- El término "fast-forward" se refiere a que no se ha tenido que crear
  un commit de merge que combine las dos ramas, dado que no hay
  ninguna historia divergente entre `hotfix` y `master`. Git
  simplemente avanza el puntero de la rama `master`:

<img src="imagenes/ejemplo-issue5.png" width="600px"/>

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Seguimos trabajando el issue 53 ##
<!-- .slide: data-background="#cbe0fc"-->

- Después de haber integrado el hotfix en `master` ya podemos seguir
  trabajando el _issue_ 53.
- Sin embargo, primero borramos la rama `hotfix` porque ya no la
  necesitamos:
  
```txt
$ git branch -d hotfix
Deleted branch hotfix (was 330b7f8).
```

- Comprobamos las ramas que quedan:
  
```txt
$ git branch
  iss53
* master
```

- El asterisco nos indica la rama en la que nos encontramos. 

- Nos movemos a la rama `iss53`, desapilamos el trabajo en proceso y
  terminamos el desarrollo:
  
```txt
$ git checkout iss53
$ git stash pop
# Terminamos el artículo y hacemos commit
$ git commit -am "Terminado el artículo [issue 53]"
[iss53 a5e2c39] Terminado el artículo [issue 53]
 1 file changed, 2 insertions(+)
```


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Actualizamos la rama hotfix ##
<!-- .slide: data-background="#cbe0fc"-->

- Hay que resaltar que el trabajo que hemos realizado en el hotfix no
  está ahora incluido en la rama `iss53`. Si cargas la página en el
  navegador verás que en el pie de página no está la dirección de
  correo.
  
- Puede ser necesario integrar el desarrollo en `master` para probar que
  todo funciona correctamento. Basta con mezclar la rama `master` en
  la rama actual:

```txt
$ git branch
* iss53
  master
$ git merge master
```

- Se abrirá el editor, pidiéndonos que escribamos el mensaje del
  commit de merge. Podemos salvar y dejar el mensaje por defecto.

- Una vez realizado el merge, podemos comprobar que todo funciona
  bien. En nuestro caso, la página contendrá el nuevo artículo y la
  dirección de email en el pié de página.
  
- Si comprobamos que algo no funciona bien, podemos deshacer
  fácilmente el último `merge`:
  
```txt
$ git reset --merge ORIG_HEAD
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Estado del repositorio ##
<!-- .slide: data-background="#cbe0fc"-->

<img src="imagenes/ejemplo-issue6.png" width="900px"/>

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Mezclamos el issue en master ##
<!-- .slide: data-background="#cbe0fc"-->

- Como todo está correcto, mezclamos el issue en la rama master:

```txt
$ git checkout master
$ git merge iss53
Updating 330b7f8..48d7900
Fast-forward
 index.html | 8 +++-----
 1 file changed, 3 insertions(+), 5 deletions(-)
```

- La imagen de la historia de Git resultante:

<img src="imagenes/ejemplo-issue7.png" width="800px" />

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Y subimos los cambios al repositorio remoto ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/ejemplo-issue-historia.png" width="400px"/>

- Subimos `master` al repositorio remoto y borramos la rama `iss53`:
  
```txt
$ git push
$ git branch -d iss53
```

- Todo ha funcionado muy bien: 
    - Hemos realizado un desarrollo independiente de la línea
      principal.
    - Hemos podido introducir en la línea principal un cambio rápido y
      después continuar el desarrollo independiente.
    - Al final hemos mezclado todo y no ha habido ningún problema.

- Examinamos la historia de cambios. ¿Hay algo mejorable?

<!-- Los commits aparecen ordenados sólo por fecha, no hay ninguna -->
<!-- información de la "evolución lógica" del proyecto: cuál ha sido -->
<!-- el hotfix, cuál ha sido el issue, etc.-->

<!-- Tres líneas en blanco para la siguiente transparencia -->



<!-- .slide: data-background-image="imagenes/gafas.gif"  -->
<!-- Tres líneas en blanco para la siguiente transparencia -->



## Resumen de comandos vistos ##

|Comando | Explicación |
|-------|--------------|
| `git branch <rama>` | Crea una rama |
| `git checkout <rama>` | Nos movemos a una rama |
| `git checkout -b <rama>` | Crea una rama y nos movemos a ella |
| `git log --oneline --graph --all ` | Muestra la historia de commits de forma gráfica, incluyendo todas las ramas |
| `git branch` | Muestra todas las ramas | 
| `git branch -d <rama>` | Elimina una rama |
| `git merge <otra-rama> -m "<mensaje>"` | Mezcla la rama `otra-rama` en la rama actual y crea el commit de mezcla con el mensaje indicado|
| `git stash` | Añade los cambios en el espacio de trabajo a la pila stash |
| `git stash list` | Muestras los cambios apilados en la pila stash |
| `git stash pop` | Desapila los cambios del stash y los añade al espacio de trabajo |
| `git reset --merge ORIG_HEAD` | Deshace el último merge realizado |

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Volvemos al estado inicial para empezar de nuevo ##
<!-- .slide: data-background="#cbe0fc"-->

- Vamos a probar otras otros comandos de mezcla, que también se
  utilizan muy a menudo en flujos de trabajo reales: `git merge
  --no-ff` y `git rebase`.
  
- Empezamos volviendo al **commit anterior al ejercicio anterior**, el que
  tiene como descripción `Mezclamos la rama prueba`:

```txt
$ git reset --hard fb8f62b
HEAD is now at fb8f62b Mezclamos la rama prueba
```

- Hacemos un `git push --force` para sobreescribir la historia que hay en
  el repositorio remoto (si intentamos hacer un `push` sin `--force`
  Git no lo dejará, porque el repositorio local tiene el `HEAD` en un
  commit pasado):

```txt
$ git push
To https://github.com/domingogallardo/curso-git-repo1.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/domingogallardo/curso-git-repo1.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
```

```txt
$ git push --force
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/domingogallardo/curso-git-repo1.git
 + 48d7900...fb8f62b master -> master (forced update)
 ```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Creamos las mismas ramas que antes  ##
<!-- .slide: data-background="#cbe0fc"-->

- Creamos las mismas ramas y commits que antes con el objetivo de llegar a la
  situación mostrada en la siguiente imagen:
  
<img src="imagenes/ejemplo-issue8.png" width="800px"/>


<!-- Tres líneas en blanco para la siguiente transparencia -->



## El comando "git merge --no-ff" ##

- Si se hace un _fast forward_ es imposible saber qué commits son los
  que corresponden a la rama y cuáles a la historia previa.
- El comando `git merge --no-ff` previene la realización de un _fast
  forward_ creando un commit de merge artificial.
- Esto permite preservar la historia lógica de una rama, ya que los
  commits de la rama quedan separados de la rama principal y es
  posible examinar los cambios completos que han introducido esos
  commits.

<img src="imagenes/git-merge-vs-no-ff.png" width="1100px" />

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Integramos el hotfix con "merge --no-ff" ##
<!-- .slide: data-background="#cbe0fc"-->

- Mezclamos el hotfix (que tiene un único commit) en master, usando un
  `merge --no-ff`:

```txt
$ git checkout master
$ git merge --no-ff hotfix
# Se abrirá el editor: deja el mensaje de commit por defecto
Merge made by the 'recursive' strategy.
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

- El resultado es el siguiente. A la izquierda lo que muestra el
  comando `git log --oneline --graph --all` y a la derecha la
  representación gráfica. Podemos comprobar que queda claro en la historia el
  commit que hemos realizado en el hotfix:

<img style="vertical-align: middle" src="imagenes/grafo-despues-no-ff.png" width="600px"/> 
<img style="vertical-align: middle; margin-left:40px" src="imagenes/img-grafo-despues-no-ff.png" width="600px"/>

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Incorporamos la rama iss53 ##
<!-- .slide: data-background="#cbe0fc"-->

- Una vez mezclada, eliminamos la rama `hotfix`:

```txt
$ git branch -d hotfix
```

- Y ahora vamos a mezclar la rama `iss53` con `master` ¿Cómo quedaría
  el grafo de commits si hiciéramos un `merge` de `iss53` en `master`? La historia quedaría
  también clara:

<img src="imagenes/git-merge-iss53.png" width="800px"/>

- Pero hay un comando muy útil de Git que deja una historia todavía
  más clara, a costa de cambiar la historia verdadera del proyecto
  introduciendo commits nuevos. Se trata del comando `git rebase`.


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Comando "git rebase" ##

- El comando git rebase realiza un "cambio de base" de una rama,
  haciéndola avanzar al top de la rama sobre la que hacemos el rebase.

<img src="imagenes/antes-despues-rebase.png" width="650px"/>

- La imagen anterior es el resultado de los siguientes comandos:

```txt
$ git checkout iss53
$ git rebase master
```

- Para realizar el rebase Git reproduce los commits `C3` y `C4` en la
  cabeza de la rama `master`, creando los commits `C3'` y
  `C4'`. Después mueve el puntero de la rama `iss53` al último commit añadido.

- El resultado es que la rama `iss53` resultante ha cambiado su commit
  base y se ha colocado a la cabeza de `master`. El contenido de los
  cambios de la rama es el mismo.
  

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Aplicamos "git rebase" al proyecto ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/img-grafo-despues-no-ff3.png" width="600px"/>

- Recordemos el estado actual del proyecto. Tenemos la rama `master`
  en la que se ha integrado el hotfix y la rama con el _issue_ 53 que
  hemos terminado de desarrollar y queremos integrar también:

- Hacemos un rebase de `iss53` sobre `master`:

```txt
$ git checkout iss53
$ git rebase master
First, rewinding head to replay your work ...
Applying: Primer cambio del artículo [iss53]
Applying: Segundo cambio del artículo [iss53]
```

<img src="imagenes/img-grafo-despues-rebase.png" width="800px" />

- El resultado es el siguiente:


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Mezclamos la rama iss53 ##
<!-- .slide: data-background="#cbe0fc"-->

- Y ahora hacemos un `merge --no-ff` para mezclar la rama resultante
  (después del rebase) de `iss53` en `master`, sin hacer _fast
  forward_. Una vez realizada la mezcla, borramos la rama.

```txt
$ git checkout master
$ git merge --no-ff iss53
Merge made by the 'recursive' strategy.
 index.html | 9 ++++-----
 1 file changed, 4 insertions(+), 5 deletions(-)
$ git branch -d iss53
Deleted branch iss53 (was 8b07fdd).
```

- ¿Cuál sería la representación de la historia de los commits? Si
  hacemos un `git log --oneline --graph --all` veremos la
  representación de la derecha:

<img src="imagenes/img-grafo-despues-no-ff2.png" width="700px" /> <img style="margin-left:40px" src="imagenes/grafo-despues-no-ff2.png" width="400px"/>

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Subimos los commits ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/historia-commits-rebase-no-ff.png" width="400px" />

```txt
$ git push
```

- Subimos los commits al repositorio remoto.

- Examinamos los commits en el repositorio GitHub. Podemos comprobar
  que ahora sí que hay información lógica sobre la evolución histórica
  del desarrollo del proyecto: los commits de merge de ramas contienen
  acumulados todos los cambios de todos los commits que se han
  realizado en esa rama.
  
- Para mantener una historia lógica del repositorio es muy útil usar
  los comandos `git merge --no-ff` y `git rebase`.

- En la siguiente clase veremos que esto es también se puede conseguir
  usando _pull requests_.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Problemas del rebase ##
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/prohibido.png" width="150px" />


- Cuando se realiza un rebase se crean commits nuevos (con distintos
  números _hash_, pero el mismo contenido). Los commits nuevos tienen
  la hora y fecha de la realización del rebase. Esto **cambia la
  historia** del proyecto.

- La regla básica se puede resumir en una única frase: 

> **No rebases commits que existan fuera de tu repositorio.**

- Si sigues este consejo, todo irá bien. Si no, serás el culpable de
  muchos males y la gente te odiará.

- Si ya habías subido los commits antiguos y la gente se los ha
  descargado y ha seguido trabajando a partir de ellos, cuando subas
  la nueva historia los compañeros tendrán que re-mezclar sus commits
  y cuando hagas un pull las cosas se pondrán muy complicadas.

- Puedes encontrar en [este
  apartado](https://git-scm.com/book/en/v2/Git-Branching-Rebasing#_pre_merge_rebase_work)
  del libro Pro Git una explicación de qué hacer en este caso.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Comando "git rebase -i" ##
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/git-rebase-i.png" width="800px"/>


- Además de ser útil para clarificar la historia del proyecto, el
  rebase también se puede usar para limpiar los commits de una rama
  antes de subirlos al servidor remoto.

- El comando `git rebase -i` (rebase interactivo) permite modificar
  los mensajes de los commits, mezclar varios commits y/o eliminar
  commits.

- En la figura de la derecha, el rebase interactivo compacta los tres
  commits de la rama `iss53` (`C3`, `C4` y `C5`) en un único commit
  (`C8'`) que incluye todos los cambios.

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Probamos el rebase interactivo ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/antes-rebase-i.png" width="500px"/>

- Crea una rama nueva llamada `iss54` y añade 3 commits en
  ella. Cambia a la rama `master` y añade 2 commits. El resultado
  debería ser el que se ve en la figura:
  
- Vamos ahora a hacer un rebase interactivo en el que nos quedaremos
  con un único commit en el que se incluyan todos los cambios:

```txt
$ git rebase -i master
```


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Edición de las acciones del rebase interactivo ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/rebase-i-opciones.png" width="800px"/>

- Se abrirá un editor en el que deberemos escribir las instrucciones a
  realizar por el rebase. Las instrucciones **se ejecutarán de arriba a
  abajo**. Por defecto aparecen las instrucciones que generarán un 
  rebase normal:
     - aplicar el commit 1
     - aplicar el commit 2
     - aplicar el commit 3


<!-- Tres líneas en blanco para la siguiente transparencia -->



## Opciones del rebase interactivo ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/rebase-i-opciones.png" width="800px"/>

- Sin embargo, podemos cambiar ese comportamiento por defecto,
  modificando esas instrucciones usando los propios comandos que nos
  muestra la página que estamos editando.

- Las opciones que podemos hacer con los commits que rebaseamos
  pueden:
  - **pick**: usar commit tal cual
  - **reword**: modificar el mensaje del commit por el nuevo que
    escribimos a continuación
  - **edit**: usar el commit, pero parar para modificar el mensaje
  - **squash**: mezcla el commit con el previo
  - **fixup**: como "squash", pero descarta el mensaje del commit
  - **drop**: elimina el commit

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Escribimos las acciones del rebase interactivo ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

- Escribimos lo siguiente en el editor (queremos cambiar de nombre el primer
  commit y mezclamos en él los commits 2 y 3):

<img style="margin-left:40px" src="imagenes/git-rebase-reword.png" width="700px"/>

```txt
reword d95b441 Cambios iss54
fixup 2d52f9b Cambio 2 [iss54]
fixup 678856a Cambio 3 [iss54]
```

- Salvamos el fichero de acciones y se ejecutarán una a una.
- Al ejecutar el `reword` del primer commit se abrirá otra vez el
  editor con la información que muestra la imagen de la derecha.
  
- Salvamos sin cambiar nada y automáticamente se realizan los otros
  dos comandos y se termina el rebase.

```txt
[detached HEAD c9b490a] Cambio 1 [iss54]
 1 file changed, 3 insertions(+)
Successfully rebased and updated refs/heads/iss54.
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Comprobamos cómo ha quedado el grafo ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

<img style="margin-left:40px" src="imagenes/despues-rebase-i.png" width="500px"/>

- Mostramos la historia para comprobar cómo ha quedado el grafo de
  commits:
  
```txt
$ git log --oneline --graph --all
```

- Y mergeamos sobre `master` con un `--no-ff`, aceptando el mensaje
  por defecto que nos muestra el editor:

```txt
$ git checkout master
$ git merge --no-ff iss54
```

<img style="margin-left:40px" src="imagenes/despues-rebase-i-merge.png" width="500px"/>

- El grafo debe quedar como muestra la imagen de la derecha.

- Terminamos borrando la rama `iss54` y subiendo todo a GitHub:

```txt
$ git branch -d iss54
$ git push
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Comando "git cherry-pick" ##

<!-- Tres líneas en blanco para la siguiente transparencia -->

<img class="fragment grow" src="imagenes/git-cherry-pick.png" width="600px"/>

- El comando `git cherry-pick` permite duplicar un commit de su rama
  original en la rama actual. La figura anterior muestra el resultado
  de:
  
```txt
$ git checkout master
$ git cherry-pick ec7e05b
```

- Supongamos que en una rama de desarrollo de un _issue_ nos damos
  cuenta de un error importante y lo solucionamos en un commit. Con el
  comando `git cherry-pick` es posible aplicar ese mismo commit a
  `master` para resolver también allí el bug.
- Al igual que el merge y el rebase Git comprueba si es posible
  aplicar el commit en la nueva rama y genera un conflicto en el caso
  en que no lo sea.
  
<!-- Tres líneas en blanco para la siguiente transparencia -->



## Ejemplo de "git cherry-pick" ##
<!-- .slide: data-background="#cbe0fc"-->
<!-- .slide: class="image-right" -->

- Vamos a probar el comando `git cherry-pick`.

- Haz una rama nueva `iss55` y crea un commit cambiando el título
  `<h1>` de la página (ese será el commit que copiaremos en `master`).
- Añade dos o tres commits a la rama.

```txt
$ git checkout -b iss55
# Modificamos el título <h1> de la página
$ git commit -am "Modificado título [iss55]"
# Hacemos varios cambios más y añadimos dos nuevos commits
```

<img style="margin-left:40px" src="imagenes/antes-cherry-pick.png" width="600px"/>

- Vemos el grafo de commits antes de hacer el cherry-pick:

- Cambiamos a `master` y hacemos el cherry-pick, seleccionando el commit en el que hemos
  cambiado el título:

```txt
$ git checkout master
Switched to branch 'master'
$ git cherry-pick 3a586da
[master c5f32a0] Modificado título [iss55]
 Date: Thu Dec 14 12:36:34 2017 +0100
 1 file changed, 1 insertion(+), 1 deletion(-)
```

<!-- Tres líneas en blanco para la siguiente transparencia -->



## Resumen de los últimos commandos ##

|Comando | Explicación |
|-------|--------------|
| `git push --force` | Sube los commits al repositorio remoto sobreescribiendo la historia de commits  |
| `git merge --no-ff <rama>` |  Mezcla la <rama> sobre la rama actual creando un commit de mezcla para prevenir el fast forward |
| `git rebase <rama>` | Mueve la rama actual sobre la rama <rama> creando nuevos commits  |
| `git rebase <rama> -i` | Realiza un rebase interactivo |
| `git cherry-pick <commit>` | Re-aplica el <commit> sobre la rama actual  |

<!-- Tres líneas en blanco para la siguiente transparencia -->



<!-- .slide: data-background-image="imagenes/happy2.gif"  -->
