# Conferencias
## Sesión 0

Introduccion al curso! Revisamos la guia de aprendizaje. 

## Sesión 1

prefacio
---
se asume una cierta familiaridad con una `cli`, si este no es el caso, podemos estudiar como funcionan.

a recordar los comandos que vimos:

|       commando        |               descripción                |
|:---------------------:|:----------------------------------------:|
|      `cls`       | limpiar la pantalla de la consola |
|     `pwd`      | responde a `donde estoy?`, imprime el directorio actual |
|   `ls`    |      lista los archivos del directorio actual      |
|     `cd`      |   para cambiarnos de directorio |


repositorio local
---
es un directorio con git inicializado. (i.e `git init`), por lo tanto, el folder `.git` existe.
para "desinstalar" `git`, es suficiente borrar el folder `/.git`.
Tradicionalmente contiene codigo, instrucciones de compilacion, y un archivo `.gitignore`.

repositorio remoto
---
Es una copia de un `repo` local, pero en un servidor remoto. (i.e `github`, `gitlab` etc.)

comandos notables
---

|       commando        |               descripción                |
|:---------------------:|:----------------------------------------:|
|      `git init`       |        inicializa un repo de git         |
|     `git status`      | obtiene el estado actual del repositorio |
|   `git add %ARGS%`    |      agrega archivos al `tracking`       |
|     `git commit`      |  "comete" (o guarda) los cambios a git   |
|     `git branch`      |     muestra todas las ramas del repo     |
| `git checkout %ARGS%` |         cambia a la rama deseada         |
|      `git merge`      |              une dos ramas               |


## Single-player git

durante el curso (quizá a excepcion del proyecto) jugaremos **single-player** git. por lo tanto, las poderosas
funciones de colaboración usualmente no las usaremos. el *"flow"* de trabajo que se recomienda es el siguiente:

1. `git init` en el repo local deseado.
2. crear archivo `.gitignore` siguiendo el `boilerplate` del curso.
3. `git add .` para agregar todos los archivos al `branch` por defecto ( i.e `main` ).
4. `git commit -m "First commit"` para crear un punto inicial del historial.
5. `git checkout -b "feat/mi-nuevo-feature"` para crear y cambiarnos a un branch nuevo.
6. programar el feature necesario hasta estar satisfechos con los cambios.
7. cada cierto tiempo guardar los cambios a git (`git add .` si creamos archivos, `git commit -m "descripcion de mi cambio"`)
8. una vez terminado el feature, `git checkout main` para regresar a nuestra `branch` principal.
9. `git merge feat/mi-nuevo-feature` para unir las dos ramas, e inmediatamente despues borrar `git branch -d feat/mi-nuevo-feature` la branch vieja.
10. regresar al paso 5 si existen features por implementar.

opcionalmente, si queremos publicar nuestro trabajo a github, desde la branch deseada `git push`.

si el repo que queremos manipular esta en un repositorio remoto, es suficiente `git clone %URL%` para crear el repo local, regresar al paso 1.

si tenemos un `repo` local que desconoce de la existencia de un `repo` remoto, es necesario usar `git remote add` para registrarlo.

tldr
---
`git` es un **VCS**. Es útil para desarrollar secciones de nuestros programas con cambios discretos.

Los archivos que nos interesa agregar al `tracking` se tienen que `add`ear. (i.e `git add .`)

Cuando queremos guardar los cambios, es suficiente con `commite`earlos.

Estos cambios pueden ser consultados(`git log`) y podemos revertirlos de ser necesario (`git reset`).

Es útil al jugar single player `git` que cada cambio sea un `feat/feature-name`.
Cuando estemos satisfechos con los cambios, realizamos un `merge` al branch principal (`main`, o `master`)

**IMPORTANTE** En todo momento solo tendremos dos (2) branches, nuestra rama principal que contiene una version estable del programa
y nuestra rama donde estemos desarrollando `features` nuevas. de otra forma, es posible que nos enfrentemos a `merge conflicts`.

Si queremos compartir los cambios a un repositorio remoto (i.e en `github`) es suficiente con `push`ear los cambios.

Si queremos obtener cambios de un repositorio remoto, es suficiente con `pull`earlos (o `clone`earlos si no tenemos el repo local.)
