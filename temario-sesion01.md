# Temario #


Día 1: Git para el desarrollo en solitario
   - Introducción a Git, instalación y configuración
   - Comandos básicos
      - add, commit, diffs, tags, amend, reset, push, pull
      - Búsqueda en el historial de cambios: checkouts a commits anteriores, blame, bisect
   - Ramas
      - Creación de ramas, checkout entre ramas, merge, cherry-pick, rebase, stash, borrado
      - Solución de conflictos en merge y rebase
      - Trabajo con el repositorio remoto: fetch, referencias y tracking de ramas remotas
   - Trabajo con git en entornos de desarrollo y GUIs
   - Práctica: trabajo con un repositorio git para el desarrollo de un sencillo sitio web

Temario extendido:

  Sesión 1 (2,5 h.)
     - Introducción
     - Configuración de Git: instalación, configuración de cliente,
       servidor de git
     - Configuración de GitHub: creación y configuración de cuenta
     - Creación de repositorios
     - Trabajo en una rama
         Commit, diffs, tags, checkout a commits anteriores, reset, amend, recuperar
         ficheros de commits anteriores
     - Subida al repositorio remoto

  Sesión 2 (2,5 h.)
      - Trabajo con ramas: introducción, ramas long-lived vs. ramas short-lived
      - Creación de ramas, checkout entre ramas, merge, cherry-pick,
        rebase
      - Solución de conflictos
      - Stash para guardar los cambios no commiteados

Sesión 3:

   - Subida de ramas al repositorio remoto

Ideas: 

- ¿Usar GitHub Pages como sitio para subir el sitio web?

**************************


## Desarrollo del curso ##
### Temario ###
### Metodología ###
### Práctica: Alta en GitHub ###

## Introducción a Git ##

### Sistemas de control de versiones ###

- Permiten mantener un histórico de:
  - Quién ha hecho los cambios
  - Qué cambios se han hecho en cada fichero
  - Volver a algún momento del pasado para comprobar allí el estado
    del proyecto o recuperar algún fichero que se ha cambiado
    posteriormente
    
- Permiten desarrollo en ramas independientes, de forma que los
  cambios en una rama no afectan a otras
  - Útil para probar características que desarrollamos en paralelo


### Práctica: Examinar proyecto Git en GitHub ###

Podemos ver que cada commit contiene información relevante:

- Correo electrónico y nombre del responsable del commit
- Fecha en la que se realizó el commit
- Cambios introducidos por el commit
   - Ficheros modificados: líneas cambiadas, añadidas, borradas
   - Ficheros añadidos
   - Ficheros borrados

### Práctica: Crear un repositorio Git ###

Configuramos los variables globales de git `user.name` y `user.email`:

```
$ git config --global user.name “Pilar Hernández”
$ git config --global user.email pilar.hernandez@ua.es
```


Creamos el directorio que va a contener el repositorio y nos movemos a él:

```
$ mkdir turismo-alicante
$ cd turismo-alicante
```

Inicializamos git:

```
$ git init
$ git add .
```
