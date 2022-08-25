# Conferencias
## Sesión 0

* Introducción al curso.
* Revisamos puntos importantes de la guía de aprendizaje.
  * Metodos y notas importantes sobre el esquema de calificaciones y evaluaciones.
  * Donde encontrar los recursos del curso, como `docs`, `github` etc.
  * Se presento la metodologia de clase.

## Sesión 1

### prefacio
se asume una cierta familiaridad con una `cli`, si este no es el caso, podemos estudiar como funcionan.

a recordar los comandos que vimos:

| commando |                       descripción                       |
|:--------:|:-------------------------------------------------------:|
|  `cls`   |            limpiar la pantalla de la consola            |
|  `pwd`   | responde a `donde estoy?`, imprime el directorio actual |
|   `ls`   |        lista los archivos del directorio actual         |
|   `cd`   |              para cambiarnos de directorio              |


### repositorio local

es un directorio con git inicializado. (i.e `git init`), por lo tanto, el folder `.git` existe.
para "desinstalar" `git`, es suficiente borrar el folder `/.git`.
Tradicionalmente contiene codigo, instrucciones de compilacion, y un archivo `.gitignore`.

### repositorio remoto

Es una copia de un `repo` local, pero en un servidor remoto. (i.e `github`, `gitlab` etc.)

### comandos notables

|       commando        |               descripción                |
|:---------------------:|:----------------------------------------:|
|      `git init`       |        inicializa un repo de git         |
|     `git status`      | obtiene el estado actual del repositorio |
|   `git add %ARGS%`    |      agrega archivos al `tracking`       |
|     `git commit`      |  "comete" (o guarda) los cambios a git   |
|     `git branch`      |     muestra todas las ramas del repo     |
| `git checkout %ARGS%` |         cambia a la rama deseada         |
|      `git merge`      |              une dos ramas               |


### Single-player git

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

### tldr
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


## sesión 2

sobre apuntadores, aritmetica de apuntadores, operadores de `dereferencia` y `direccion de`.

```c
int main(void)
{
  int mi_entero = 12;
  int *mi_apuntador = 0; // aun no apuntamos a nada
  mi_apuntador = &mi_entero;
  return 0;
}
```
**definición**
<aside class="success">
un apuntador es una <code>variable</code> cuyo valor es una <code>dirección de memoria</code>.
</aside>

de forma general, declaramos un apuntador con la forma `tipo_de_dato *identificador;` es legal declarar 
apuntadores para cualquier tipo de dato.

### sobre `*` y `&`


las direcciones de memoria se representan numericamente, frecuentemente usando el sistema hexadecimal.
para declarar apuntadores, usamos asteriscos `*` despues del tipo de dato al que queremos referenciar.

notesé que al declarar `mi_apuntador` el valor `0` denota `NULL` o una dirección INVALIDA
posteriormente, se asigna a `mi_apuntador` la dirección de memoria de `mi_entero` usando el operador 
`direccion de` representado con `&`.

```c
int mi_entero = 12;
int* apuntador_a_entero = &mi_entero;

printf("VALORES:\n");
printf("<mi_entero:> %d\n", mi_entero); // usando el identificador de la variable "tradicional"
printf("<VALOR> <apuntador_a_entero> %d\n", *apuntador_a_entero); // usando operador '*' "de dereferencia" para obtener valor.

printf("DIRECCIONES DE MEMORIA:\n");
printf("<DIRECCION> <mi_entero> %p\n", &mi_entero); // usando el operador '&'  "direccion de" para obtener direccion de memoria
printf("<apuntador_a_entero> %p\n", apuntador_a_entero); // el valor de apuntador_a_entero es una direccion de memoria!

```

### la desafortunada vida de `*`
recordemos que el simbolo `*`, `asterisco` "trabaja tiempo extra":

1. Es el operador de multiplicación.
2. Es el simbolo que denota que el tipo de dato de nuestra variable es apuntador (`int *mi_apuntador`)
3. Es el operador de `dereferencia`. se usa para obtener el **VALOR** de una dirección de memoria.

### la afortunada vida de `&`
aunque podriamos argumentar que `&`, `ampercent` tambien tiene multiples usos:

1. Se usa para declarar que multiples condiciones logicas tienen que ser verdaderas (`&&`)
2. Como operador `AND` a nivel de bits (`baz = foo & bar;`)
3. Como operador `dirección de`.

por los diferentes contextos donde aparece, suele no causar el mismo nivel de confusión que `*`

### los apuntadores también son variables!

```c
int mi_arreglo[5] = {-1, 0, 5, 123, 2782};
int *mi_apuntador = mi_arreglo;

for(int i = 0; i < 5; i++)
{
  printf(" %d ", *mi_apuntador);
  mi_apuntador = mi_apuntador + 1; // o mi_apuntador++; !
}
```

recordando la definición de arreglo
**definición**
<aside class="success">
Un arreglo es una colección de elementos, todos del mismo tiempo, ordenados de forma consecutiva en memoria.
</aside>

por lo tanto, si "aumentamos" el valor de un apuntador, efectivamente estamos cambiando la referencia al dato siguiente consecutivo!
podemos aprovechar eso para visitar cada elemento de un arreglo usando el operador de `*`.

como nota, al finalizar el ciclo `for`, el valor de `mi_apuntador` es una dirección invalida, y por lo tanto
`dereferenciarla` podria causar comportamiento indeterminado!.

<aside class="notice">
Si en lugar de imprimir los valores del arreglo nos interesaran las direcciones de memoria, 
como cambiaria el cuerpo del ciclo <code>for</code>?
</aside>

### Notas importantes

manipular la dirección que guarda un apuntador es generalmente una operación sin riesgo, `i.e` si un apuntador guarda una
dirección de memoria inválida el programa se comportará correctamente, el riesgo existe al `dereferenciar` (con `*`) una referencia ilegal!


## Sesión 3

Sobre apuntadores a estructuras, apuntadores como argumentos a funciones.


