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
Un arreglo es una colección de elementos, todos del mismo tipo, ordenados de forma consecutiva en memoria.
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

### Modificar valores a traves de referencias

consideremos la función `swap` `void swap(int *a, int *b);` que pretende intercambiar los valores de `a` y `b`.

```c
void swap(int *a, int *b)
{
  int temp = *a;
  *a = *b;
  *b = temp;
}
```

En `c` los argumentos a funciones se pasan por **valor** , es decir: cada función tiene su copia de los argumentos que recibe
y los cambios que sufren no se reflejarán en el resto del programa. Si una función recibe apuntadores y modifica los valores 
referenciados usando `*` esos cambios **SI** se mostrarán en todo el programa!

notese que al invocar la función swap, puesto que se modificaron los valores de `a` y `b` esos cambios se reflejarán desde la función "llamadora" (`i.e main`).


### Apuntadores a estructuras

```c
typedef struct {
  float x;
  float y;
}
Vector_2d;
```
Puesto que podemos declarar apuntadores de **cualquier** tipo de dato, declarar un apuntador a estructuras es sencillo.
para comodidad (mas no es mandatorio) usamos `typedef` para definir un alias a nuestra `struct`

ahora es válido declarar `Vector_2d *mi_apuntador_a_vector;`

Para los tipos de datos primitivos `int`, `char`, `float` etc como para estructuras se cumple que si son los argumentos de una función, entonces se pasan por **valor**.
Si una funció recibe un apuntador a estructura y usa `*` para modificar sus miembros, esos cambios se reflejarán también en la función "llamadora" (`i.e main`).

`(*mi_apuntador_a_vector).x = 12.4;` es una instrucción válida asumiento que el apuntador esta referenciando una posición legal de memoria.

### Sintactic sugar - apuntadores a `struct`

`dereferenciar` una estructura es una operación tan común que la notación tradicional de `*` resulta un tanto burda.

```c
void square_vector(Vector_2d *vector)
{
  // equivalente a (*vector).x = (*vector).x * (*vector).x;
  vector->x = vector->x * vector->x;
  // equivalente a (*vector).y = (*vector).y * (*vector).y;
  vector->y = vector->y * vector->y;
}
```

existe entonces el operador "flechita" `->` (es un guión `-` seguido de un "mayor que" `>`) es taquigrafía especial que nos permite
`dereferenciar` rápida y claramente una struct a traves de su apuntador.

## Sesión 4

Sobre arreglos de apuntadores, y diferencias con arreglos de 2 dimensiones.

### Arreglos de apuntadores int*

```c
  int arry_1[] = {12,22,44};
  int some_int = -12;
  int arry_2[] = {20,30,40};

  int *mi_arreglo[3] = { arry_1, &some_int, arry_2 };
```

Si declaramos un arreglo de tipo `int* mi_arreglo[10]` , los elementos de `mi_arreglo` son direcciones de memoria.
Puesto que son referencias, siguen todas las reglas que esperamos, pueden ser `*` de-referenciados y los cambios que sufran sus valores
se reflejarán en todo el programa.

```c
  printf("%d\n", mi_arreglo[0][1]);
  printf("%d\n", *((*mi_arreglo)+1));
```
En este ejemplo en particular, el primer elemento de `mi_arreglo` es una referencia a `arry_1`
por lo tanto: `mi_arreglo[0][1]` es una forma legal de acceder al entero `22` usando notación de corchetes.
Si usaramos únicamente aritmetica de apuntadores `*((*mi_arreglo)+1)` es la expresión equivalente.

```c
  printf("%d\n", mi_arreglo[1][0]);
  printf("%d\n", **(mi_arreglo+1);
```
notece que no es necesario que los miembros de `mi_arreglo` sean tambien arreglos de enteros, es suficiente con que sea una referencia a un entero.
de esta forma, `mi_arreglo[1][0]` es una forma legal de accedera a `-12`. Con aritmetica de apuntadores : `**(mi_arreglo+1)`.

```c
  printf("%d\n", mi_arreglo[2][2]);
  printf("%d\n", *(*(mi_arreglo+2)+2);
```
Como último ejemplo, consideremos el caso en que queramos obtener el entero `40`, usando corchetes es trivial: `mi_arreglo[2][2]`
usando aritmetica de apuntadores: `*(*(mi_arreglo+2)+2)`. 

### en general sobre arreglos de apuntadores.

Para entender mejor la notación de aritmetica de apuntadores:

<aside class="notice">
  de forma general: <code>*(*(mi_arreglo+i)+j)</code> resolverá el mismo elemento que <code>mi_arreglo[i][j]</code> si y solo
  si son arreglos con tipos completos (i.e NO <code>void*</code>).
</aside>

### Arreglos de apuntadores char*

consideremos el siguiente programa:

```c
int main(void)
{
  char *many_strings[] = {
          "hola!",
          "este arreglo tiene muchas frases",
          "todas se pueden acceder",
          "de forma sencilla!"
  };

  printf("%s", many_strings[0]);

  for(int i = 1; i < 4; i++)
    printf(" %s", many_strings[i]);
}
```

resulta practico que sea un arreglo de apuntadores `char*` puesto que el contenido del mensaje es constante.
si usaramos un arreglo de tipo `char[][]`, estariamos obligados a determinar la longitud máxima de nuestros mensajes en tiempo de compilación!

Considera porque un arreglo tipo `char*[]` no requiere dicha definición? (Aprovecha los conocimientos de la sesión 7 - Organización de memoria)

## Sesión 5
Sobre apuntadores sin tipo, o `void*`.

### Sobre void*

```c
  int mi_entero = 12;
  void *mi_ptr = &mi_entero;

  printf("%p\n", &mi_entero);
  printf("%p\n", mi_ptr);
```
Cuando ignoramos (o no nos interesa) el tipo de dato concreto al que estamos apuntando, pero SI deseamos guardar una referencia para futuros usos
utilizamos apuntadores tipo `void*`.

En este ejemplo, la dirección de `mi_entero` y el valor de `mi_ptr` serán iguales.

<aside class="warning">
  Es ilegal el uso del operador de dereferencia <code>*</code> en apuntadores <code>void*</code>.
</aside>


```c
  // ilegal, esto no compila.
  printf("%d\n", *mi_ptr);
```

La razón tendria que ser evidente: al no conocer el tipo de dato concreto al que estamos apuntando, es imposible que sepamos cuantas direcciones de memoria
tenemos que leer para construir el dato concreto.

```c
  // esto si es legal
  int *mi_helper = mi_ptr;
  printf("%d\n", *mi_helper);
```

Para obtener el valor de un apuntador `void*` es necesario especificar el tipo de dato concreto al que estamos apuntando, y posteriormente dereferenciarlo.
Esta operación se conoce como `typecasting` o sencillamente `casting`.

es posible realizar el `cast` en una sola linea, i.e: `printf("%d\n", *(int*)mi_ptr);`

### Sobre aritmetica de apuntadores

```c
  int *mi_int_ptr = &mi_entero;
  void *mi_ptr = &mi_entero;

  mi_ptr++;
  mi_int_ptr++;

  printf("%p != %p", mi_ptr, mi_int_ptr);
```
Como vimos en **arimetica de apuntadores** cuando tenemos un apuntador de tipo concreto, lo podemos manipular tal que si se le suma o resta algun número entero,
se calculará la siguiente dirección de memoria valida para ese tipo concreto en particular. Puesto que `void*` desconoce el tipo, en su lugar se toma el tipo de 
dato mas pequeño que se soporte (i.e `char`) para completar la operación, generalmente esto significa que si aumentamos en `1` el valor de un apuntador `void*` este
apuntará al siguiente `byte`. **

Considerando el ejemplo, `mi_ptr` apuntará a una dirección `3` bytes antes que `mi_int_ptr`. **

** Nota: Esto puede variar dependiendo de su arquitectura, pero para efectos de esta clase siempre será cierto.

## Sesión 6

```c
  int un_numero = 12;
  char *mi_frase = "hola mundo!";
  int mi_arry[] = {22, 34, 45};
  Vector2d mis_vectores[] = {
          {.x = 12, .y = 12},
          {.x = 5.3,.y = 0.2}
  };

  void *mis_refs[] = {&un_numero, mi_frase, mi_arry, mis_vectores};
```
Sobre arreglos de apuntadores sin tipo, o `void*[]`.

### direcciones sin restricciones

Puesto que un arreglo de apuntadores `void*` es un arreglo de referencias sin tipo, no existen restricciones de los apuntadores que puede contener.
En el ejemplo, `mis_refs` contiene referencias a una gran variedad de tipos! desde un sencillo entero (`un_numero`) hasta un arreglo de vectores.

aunque un apuntador sin tipo no se puede dereferenciar, este no es el caso para `void*[]`, puesto que el tipo de dato es `void*` es posible obtener direcciones
individuales del arreglo!

### Obteniendo miembros individuales

```c
  printf("la direccion de mi frase %p\n", mis_refs[1]);
  printf("la direccion de mis vectores %p\n", *(mis_refs+3));
```
Los arreglos de direcciones `void*` siguen las mismas reglas que cualquier otro arreglo de apuntadores. Es posible obtener los valores que contiene usando tanto 
corchetes, como aritmetica de apuntadores.

### Imprimiendo valores

```c
  printf("%d\n", *(int*)mis_refs[0]);
  printf("%s\n", (char*)mis_refs[1]);
  printf("%d\n", *((int*)*(mis_refs+2)+2));
```

Puesto que las referencias que contiene `mis_refs` no tienen tipo, se siguen las mismas reglas que los apuntadores `void*` para poder dereferenciarlos!
Notese el último cast (para imprimir `45`), puesto que la dirección de memoria que corresponde a `mis_refs+2` ya es un `int*` podemos volver a aprovechar la aritmetica
de apuntadores para imprimir el tercer elemento del arreglo!

### Sobre casts en una sola linea

Notesé que realizar varias operaciones de aritmetica de apuntadores y `casts` en una sola linea rápidamente se vuelve confuso y ofuscado.

```c
  printf("vector 1, x: %f\n", ((Vector2d*)*(mis_refs+3))->x);
  printf("vector 2, x: %f\n", ((Vector2d*)*(mis_refs+3)+1)->x);
```

En general, cuando manipulamos referencias complejas (como es este caso) es mejor crear las variables intermedias necesarias para clarificar la intención del codigo
tal que, podemos refactorizar los `printfs` a:

```c
  // refactorizando codigo confuso
  
  Vector2d *vector_ptr = *(mis_refs+3);
  Vector2d first = *vector_ptr;
  Vector2d second = *(vector_ptr+1);

  printf("vector 1, x: %f\n", first.x);
  printf("vector 2, x: %f\n", second.x);
```

De esta forma, resulta evidente en que nivel de indirección nos encontramos en cada paso del programa.

## Sesión 7

Sobre la organización de la memoria.

### Las áreas lógicas

Para "ejecutar" un programa, el sistema operativo inica un `proceso`. Este proceso tiene acceso a memoria, misma que se divide en:

1. Texto
2. Datos
3. BSS
4. Pila o `stack`
5. Zona libre o `heap`

### Sobre texto, datos, bss
```c
  void foo()
  {
    static int count = 0;
    count++;
  }


  int main(void)
  {
    foo(); // count será 1 al terminar la invocación
    foo(); // count será 2 al terminar la invocación
    foo(); // count será 3 al terminar la invocación
    // etc
  }
```

Las instrucciones ejecutables que conforman su programa se guardaran en `texto`.
las variables globales (inicializadas o no) y constantes literales pertenecen a `Datos` / `BSS`
para efectos de esta materia, podremos encapsular estas tres secciones en una sola (`Texto/Datos/BSS`) que llamaremos
`Static Storage`, o Memoria estática.

### Static

A recordar que la palabra reservada `static` modifica el tiempo de vida de una variable, tal que ya no se guarda en
el `stack`. `count` vivirá en la sección de `Datos` (parte de `Static Storage`).


## Sesión 8

Como continuación del tema `organización de memoria`, consideramos `stack` vs `heap`.

### Sobre el stack
```c
  int foo(int a, int b)
  {
    return a + b;
  }

  int main(void)
  {
    int suma_1 = foo(1, 1);
    int suma_2 = foo(12, 12);
    int suma_3 = foo(21, 21);
  }
```

Las variables declaradas en funciones, o sus argumentos se guardan en el stack conforme se necesiten.
Es decir, cuando invocamos una función, se reserva el espacio de memoria suficiente para representar su contenido y sus miembros
y al finalizar la ejecución esta memoria se libera.

Esta también se llama `memoria automática` puesto que se reserva y libera de forma implicita durante la ejecución

en el ejemplo, los argumentos de `foo` (`a` y `b`) viven de forma efímera en el `stack` mientras la función se ejecuta.
mismo caso con `suma_1`, `suma_2` y `suma_3` que residen en el `stack` mientras main exista en la pila de llamadas (o `callstack`).

### Sobre el heap

```c
  #include <stdlib.h>

  void* foo()
  {
    void* mi_blocke_de_memoria = malloc(100);
    return mi_blocke_de_memoria;
  }

  int main(void)
  {
    void* suma = foo();
  }
```

aquellos bloques de memoria que se reserven explicitamente con `malloc` vivirán en el `heap` mientras no 
se liberen explicitamente, como son direcciones válidas a travez de todo el programa, es legal regresar dicha referencia
de una función (no así cuando se traten de referencias al `stack`).

## Sesión 9

Sobre malloc, y arreglos en memoria dinámica. `free` y otros detalles

### Sobre malloc

```c
int main(int argc, char *argv[])
{
  char *mi_string = malloc(sizeof(char) * 10);
  mi_string[0] = 'h';
  mi_string[1] = 'o';
  mi_string[2] = 'l';
  mi_string[3] = 'a';
  mi_string[4] = '\0';
  
  printf("%s", mi_string);
}
```

`malloc(size)` ( "Memory Allocation" ) reserva un bloque de memoria de al menos un tamaño `size` y regresa un apuntador `void*` a este
nuevo bloque reservado.

Dicho bloque de memoria puede ser usado como un arreglo si conocemos el tipo concreto de lo que guardaremos.
en el ejemplo `mi_string` puede ser de-referenciado usando notación de corchetes para escribir la palabra `hola`
a notar que es necesario agregar el caracter terminador.

aunque al terminar la ejecución del programa, los recursos reservados son recuperados por el sistema operativo, es recomendable
que una vez que terminemos de usar el bloque de memoria reservado este se "libere" para evitar `memoryLeaks`

Siguiendo el ejemplo, seria suficiente usar `free(mi_string)` para liberar los 10 bytes de memoria reservados.

notese que como cualquier apuntador, es posible manipularo usando aritmetica (i.e `*(mi_string + 3)` será la letra `a` )

### Sobre free

Cuando se implementen `TDA`s que reserven memoria de forma dinamica, es fundamental que al eliminar objectos de nuestra colección,
los bloques de memoria asociados se liberen.

## Sesión 10

Evaluación síncrona I

## Sesión 11

Sobre argumentos de main `argc` `argv` y 
Sobre archivos de texto, `fopen` `fgets` `rewind` y `fclose`

### Sobre `argc` y `argv`

```c
int main(int argc, char *argv[])
{
  // recordamos que el primer argumento es la ejecución del programa
  printf("EJECUTAMOS: %s\n", argv[0]);
  
  // despues, de 1..n los argumentos adicionales del usuario
  for(int i = 1; i < argc; i++)
    printf("argumento #%d: %s\n", i, argv[i]);
}
```

es posible alimentar un programa con información al ejecutarse, con los `program arguments` mismos
que se agregan despues de invocar el ejecutable, separados por espacios.

En `C`, dichos argumentos se capturan usando `argc` -> "Argument Count" y `argv` -> "Argument Vector"

Siempre el primer argumento es la ruta de ejecución del programa, seguido por un arreglo de `strings` con cada
uno de los argumentos que envió el usuario.

### Sobre archivos de texto

```c
int main(void)
{
  FILE *my_file = fopen("../myfile", "r");
  char buffer[255];
  fgets(buffer, 255, my_file);
  fgets(buffer, 255, my_file);
  printf("%s", buffer);

  fclose(my_file);
}
```

Consideremos las siguientes funciones:

| función  | descripción                                                                      |
|:--------:|:---------------------------------------------------------------------------------|
| `fopen`  | recibe de argumentos un `path` y un `modo`, abre el archivo y regresa un `file*` |
| `fgets`  | lee y guarda en un `buffer` una linea de un `stream` (comunmente un archivo)     |
| `rewind` | regresa el cursor del archivo al inicio (para leer de nuevo)                     |
| `fclose` | Cierra un `stream`                                                               |


```console
[my_file]

This is a line
this is also a line
the last line

```
nuestro programa imprimirá  `this is also a line`.

## Sesión 12

Sobre archivos binarios, modificadores de fopen `r`, `w`, `a` y `+`

### Modificadores o modos de fopen

```c
int main(void)
{
  FILE *my_file = fopen("../myfile", "a");
  char buffer[255];
  fputs("Esta es una nueva linea\n", my_file);
  fclose(my_file);
}
```

| función | descripción                                                                       |
|:-------:|:----------------------------------------------------------------------------------|
|   `r`   | `readonly` el archivo se abre para solo lectura, error si no existe.              |
|   `w`   | `write` el archivo se crea si no existe, si existe se sobreescribe.               |
|   `a`   | `append` el archivo se abre con el cursor al final para agregar datos.            |
|   `+`   | `r+`, `w+`, `a+` permite lectura y escritura de archivos, y se crea si no existe. |

Dependiendo del `modo` de apertura, se limitan las operaciones que se pueden realizar sobre los archivos.

En el primer ejemplo, abrimos un archivo para agregar información - `Esta es una nueva linea\n` aparecerá
al final del archivo despues de cerrar `fclose` el stream.

Consideremos las siguientes funciones.

```c
int main(void)
{
  FILE *my_file = fopen("../myfile", "w");
  Una_struct_equis foo = {'a', 1, {5,6,7}};
  fwrite(&foo, sizeof(Una_struct_equis), 1, my_file);
  fclose(my_file);
}
```

| función  | descripción                         |
|:--------:|:------------------------------------|
| `fputs`  | agrega lineas de texto a un archivo |
| `fread`  | lee de un archivo binario           |
| `fwrite` | escribe a un archivo binario        |

la diferencia principal entre un archivo de texto (`fgets`, `fputs`) y un archivo binario (`fread`, `fwrite`) es importante.

Cuando usamos `fgets` , `fputs` trabajamos sobre lineas de texto en el archivo, tanto al leer como al escribir.
frecuentemente usamos `buffers` de tipo `char` i.e `char buffer[255]` para leer/escribir lineas de hasta `255` caracteres.

Cuando usamos `fread`, `fwrite` trabajamos a nivel de bits sobre el archivo, y tenemos libertad de escribir `t_size` bytes de memoria
o leer `t_size` bytes de memoria, es decir, no se trata de caracteres ASCII, guardamos en el archivo cualquier bloque de memoria.

notese que en el segundo ejemplo, estamos guardando al archivo los bytes que le corresponden a `foo`, que es de tipo `Una_Struct_equis`.

## Sesión 13

sobre estructuras autoreferenciales (`cadenitas`)

### Structs mágicos

```c
typedef struct node
{
  int value;
  struct node *next;
}
Node;
```

Puesto que `node` es una estructura autoreferencial, es necesario asignarle un nombre antes que el `typedef`.
`node` ahora contiene un apuntador a su mismo tipo.

La estructuras autoreferenciales resultan útiles cuando deseamos implementar `Contenedores` y el número de elementos que
el usuario desee agregar nos es desconocido. 

```c
  Node n = {.value = -13, .next = NULL };
  Node n2 = {.value = 70, .next = NULL };
  Node n3 = {.value = 12, .next = NULL };
  Node n4 = {.value = 13, .next = NULL };
  n.next = &n2;
  n2.next = &n3;
  n3.next = &n4;
```

consideremos la "cadenita" formada, tal que `n` tiene una referencia a `n2`. `n2` tiene una referencia a `n3` etc.
A notarse que `NO` existe forma de regresar, i.e `n2` NO tiene una referencia a `n1`.

## Sesión 14

Sobre `TDA`s (Tipo de dato abstracto) - ( `ADS` en ingles ) y `Contenedores`

### definiciones

**definición**
<aside class="success">
Un tipo de dato abstracto es un "Objeto" definido por su comportamiento, no por su implementación.
</aside>

**definición**
<aside class="success">
Un contenedor es un TDA que agrupa elementos y restringe su acceso con verbos semanticamente significativos.
</aside>

Es importante conocer la diferencia entre: `QUE` hace el contenedor, y `COMO` logra realizar estas acciones (la `implementación`).

```c
#include "my_list.h"

int main(int argc, char *argv[])
{
  List foo = new_list();
  add(foo, 2);
  add(foo, 6);

  if(contains(foo, 2))
    printf("It works!");
}
```

A considerar un contenedor tipo `List`:

- `Add` agrega un elemento al final de la lista
- `Remove (i)` elimina un elemento de la lista
- `Find (val)` encuentra y regresa el elemento con valor `val`
- `Contains (val)` determina si existe el elemento `val`.

Notese que NO se describe la implementación concreta de las funciones, unicamente define su comportamiento,
la lista podria estar implementada usando estructuras autoreferenciales, arreglos, archivos etc. etc.

En `C` es común al definir nuevos `contenedores` que los verbos y datos relevantes sean "publicos" en un 
archivo de cabecera "`.h`" mientras que las implementaciones concretas se encapsulen en su propio archivo fuente `.c`.

## Sesión 15

Sobre `contenedor` - Stack

### definiciones

Un stack es un contenedor que sigue el comportamiento `LIFO`

**definición**
<aside class="notice">
<code>LIFO</code> es "Last in, First Out"
</aside>

que indica el orden en que obtendremos los elementos que se agreguen al contenedor, en el caso del stack
el último elemento que se agrego (`push`) , será el elemento a obtener (`pop`)

### API

```c

typedef struct stack Stack; // Para apuntadores tipo Stack*

Stack *stack_new();
void stack_push(Stack *s, void *val);
void* stack_peek(Stack *s);
void* stack_pop(Stack *s);
int stack_empty(Stack *s);

```

las operaciones relevantes son:

- `push` para agregar elementos
- `peek` para obtener un elemento del stack **sin retirarlo**
- `pop` para obtener un elemento del stack, retirandolo en el proceso

adicional a esto, tenemos ciertas funciones apropiadas para todo tipo de contenedores:

- `new` para obtener un stack nuevo
- `empty` que regresa `true` si el stack esta vacio, `false` caso contrario.

## Sesión 16

Sobre `contenedor` - Queue

### definiciones

Un queue es un contenedor que sigue el comportamiento `FIFO`

**definición**
<aside class="notice">
<code>FIFO</code> es "First in, First Out"
</aside>

para una queue: el primer elemento que se agrego (`append`) , será el elemento a obtener (`remove`)
se puede visualizar como una fila común, el orden en que se forman las personas indica el orden en que serán atendidas.
donde el primero que se formó, será el primero en ser atendido.

### API

```c

typedef struct queue Queue;

Queue *queue_new();
void queue_append(Queue *s, void *val);
void* queue_peek(Queue *s);
void* queue_remove(Queue *s);
int queue_empty(Queue *s);

```

las operaciones relevantes son:

- `append` para agregar elementos
- `peek` para obtener un elemento del queue **sin retirarlo**
- `remove` para obtener un elemento del queue, retirandolo en el proceso

adicional a esto, tenemos ciertas funciones apropiadas para todo tipo de contenedores:

- `new` para obtener un queue nuevo
- `empty` que regresa `true` si el queue esta vacio, `false` caso contrario.
