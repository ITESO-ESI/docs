# Guía de estilo

Esta guía de estilo es esencialmente una traducción de la guía de Harvard con ligeros cambios.

No existe una “única” forma correcta de formatear código. Pero definitivamente existen *varias* formas de hacerlo mal. Durante el curso se pedirá que todos los entregables respeten las reglas de estilo aquí dispuestas (similar a como muchas empresas como AirBnB tienen lineamientos de estilo obligatorios). El objetivo es generar código fuente con estilos consistentes independientemente del programador.

## Longitud de línea

```c
// Notese como esta caja de codigo requiere que el usuario use scroll.

// These next lines of code first prompt the user to give two integer values and then multiplies those two integer values together so they can be used later in the program
int first_collected_integer_value_from_user = get_int("Integer please: ");
int second_collected_integer_value_from_user = get_int("Another integer please: ");
int product_of_the_two_integer_values_from_user = first_collected_integer_value_from_user * second_collected_integer_value_from_user;
```
Por convenciones históricas, la longitud máxima de una línea de código será de 80 caracteres. 

Por decisiones de diseño de IBM, inicialmente los monitores tenían la capacidad de renderizar 24 líneas de texto cada una con hasta 80 caracteres. Ahora es evidentemente obsoleto pero el límite de 80 caracteres es aún una restricción frecuente para evitar `line-wraps` o tener barras de `scroll`.  En cualquier forma, si necesitas más de 80 caracteres para una sola instrucción es posible que necesites pensar en tu esquema de nombres de variables, o reconsiderar el diseño general de tu solución.

En otros lenguajes (javascript en particular) resulta complicado respetar este límite y otras reglas de estilo aplican (i.e segmentar una instrucción con saltos de linea `\n`)

## Comentarios

El objetivo de los comentarios es que el código fuente sea más legible. Es importante recalcar que los comentarios ayudan no solo a otros programadores, ¡ayudan también al autor inicial! Cuando pasan horas, días, semanas o años después de que se implementó algo y se quiere recordar alguna decisión de diseño o detalle importante es más fácil si se deja un **breve** recordatorio en lenguaje natural. Pocos y pobres comentarios no resultan de ayuda, demasiados comentarios caen en la redundancia (o son resultado de implementaciones malas que requieren profundas explicaciones). Cada programador tendrá que decidir cuál es el balance correcto. Un inicio es comentar cada vez que se necesite responder alguna de estas preguntas:

1. ¿Que hace este bloque?
2. ¿Porque implemente este bloque de esta forma?

### en linea

```c
// Convert Fahrenheit to Celsius
float c = 5.0 / 9.0 * (f - 32.0);
```
Para los comentarios dentro de funciones, usa comentarios `inline` y mantenlos **breves** (i.e una sola línea), de otra forma interferirían con la lectura del código fuente. Escribe los comentarios en la línea inmediatamente superior a la pieza de código que se está describiendo. Recuerda dejar un espacio después del inicio del comentario `//`.

<aside class="warning">
  No mezcles codigo y comentario en la misma linea! i.e
 <code>int foo = 12; //asigna un valor al entero </code>
</aside>

### en funciones

```c
// Returns the square of n
int square(int n)
{
    return n * n;
}
```
Las funciones son perfectas candidatas para breves comentarios significativos: resulta util que cada función tenga justo antes de su **implementación** una breve descripción de que hace dicha subrutina. Generalmente no es necesario comentar `main`.

<aside class="notice">
  No es necesario comentar el comportamiento de ciclos de repeticion.
  como <code>for</code> o <code>while</code>
</aside>

### en archivos

```c
//
// Created by Josean Camarena on 07/07/22.
// Implemented by: $STUDENT$ 
// Sorts a given collection with various algorithms.
// 
```
Al principio de cada archivo `.c` o `.h` resulta útil agregar la información de autor y fecha con una breve descripción sobre que hace la librería.

## estructuras condicionales

La guia de estilo pretende resaltar el contenido de los bloques condicionales, y clarificar la expresión de la condicional.

```c
if (x > 0)
{
    printf("x is positive\n");
}
else if (x < 0)
{
    printf("x is negative\n");
}
else
{
    printf("x is zero\n");
}
```
### Las estructuras condicionales tienen que respetar

- las llaves se alinean correctamente, *cada una en su propia linea*, haciendo enfasis en lo que contiene cada bloque de codigo. 
- cada `if` tiene un espacio antes de abrir el parentesis de la expresión condicional.
- cada llamada a `printf` esta correctamente indentada.
- existe un espacio separando `<` y `>` de los valores a comparar.
- No se tiene espacio inmedatamente despues de abrir `(` parentesis o inmediatamente antes de `)` cerrarlo.

<aside class="notice">
 Aunque la indentación tradicional de <code>c</code> son de 4 espacios, se permite tener indentación de 2 espacios siempre y cuando seamos <strong>consistentes</strong>
</aside>

### sobre la apertura de llaves 
```c
if (x < 0) {
    printf("x is negative\n");
} else if (x < 0) {
    printf("x is negative\n");
}
```
Frecuentemente encontraremos llaves en la misma linea que la condición. Esto no es recomendado pero si se desea sera permitido.

### definitivamente así no

```c
if (x < 0)
    {
    printf("x is negative\n");
    }
else
    {
    printf("x is negative\n");
    }
```
Esto es terrible.

## Switches

Declare a `switch` as follows:

```c
switch (n)
{
    case -1:
        printf("n is -1\n");
        break;

    case 1:
        printf("n is 1\n");
        break;

    default:
        printf("n is neither -1 nor 1\n");
        break;
}
```

Notice how:

- each curly brace is on its own line;
- there's a single space after `switch`;
- there isn't any space immediately after each `(` or immediately before each `)`;
- the switch's cases are indented with 4 spaces;
- the cases' bodies are indented further with 4 spaces; and
- each `case` (including `default`) ends with a `break`.

## Functions

In accordance with [C99](http://en.wikipedia.org/wiki/C99), be sure to declare `main` with:

```c
int main(void)
{

}
```

or, if using the CS50 Library, with:

```c
#include <cs50.h>

int main(int argc, string argv[])
{

}
```

or with:

```c
int main(int argc, char *argv[])
{

}
```

or even with:

```c
int main(int argc, char **argv)
{

}
```

Do not declare `main` with:

```c
int main()
{

}
```

or with:

```c
void main()
{

}
```

or with:

```c
main()
{

}
```

As for your own functions, be sure to define them similiarly, with each curly brace on its own line and with the return type on the same line as the function's name, just as we've done with `main`.

## Indentation

Indent your code four spaces at a time to make clear which blocks of code are inside of others. If you use your keyboard's Tab key to do so, be sure that your text editor's configured to convert tabs (`\t`) to four spaces, else your code may not print or display properly on someone else's computer, since `\t` renders differently in different editors. (If using [CS50 IDE](https://ide.cs50.io/), it's fine to use Tab for indentation, rather than hitting your keyboard's space bar repeatedly, since we've preconfigured it to convert `\t` to four spaces.)

Here's some nicely indented code:

```c
// Print command-line arguments one per line
printf("\n");
for (int i = 0; i < argc; i++)
{
    for (int j = 0, n = strlen(argv[i]); j < n; j++)
    {
        printf("%c\n", argv[i][j]);
    }
    printf("\n");
}
```

## Loops

### for

Whenever you need temporary variables for iteration, use `i`, then `j`, then `k`, unless more specific names would make your code more readable:

```c
for (int i = 0; i < LIMIT; i++)
{
    for (int j = 0; j < LIMIT; j++)
    {
        for (int k = 0; k < LIMIT; k++)
        {
            // Do something
        }
    }
}
```

If you need more than three variables for iteration, it might be time to rethink your design!

### while

Declare `while` loops as follows:

```c
while (condition)
{
    // Do something
}
```

Notice how:

- each curly brace is on its own line;
- there's a single space after `while`;
- there isn't any space immediately after the `(` or immediately before the `)`; and
- the loop's body (a comment in this case) is indented with 4 spaces.

### do ... while

Declare `do ... while` loops as follows:

```c
do
{
    // Do something
}
while (condition);
```

Notice how:

- each curly brace is on its own line;
- there's a single space after `while`;
- there isn't any space immediately after the `(` or immediately before the `)`; and
- the loop's body (a comment in this case) is indented with 4 spaces.

## Pointers

When declaring a pointer, write the `*` next to the variable, as in:

```c
int *p;
```

Don't write it next to the type, as in:

```c
int* p;
```

## Variables

Because CS50 uses [C99](http://en.wikipedia.org/wiki/C99), do not define all of your variables at the very top of your functions but, rather, when and where you actually need them. Moreover, scope your variables as tightly as possible. For instance, if `i` is only needed for the sake of a loop, declare `i` within the loop itself:

```c
for (int i = 0; i < LIMIT; i++)
{
    printf("%i\n", i);
}
```

Though it's fine to use variables like `i`, `j`, and `k` for iteration, most of your variables should be more specifically named. If you're summing some values, for instance, call your variable `sum`. If your variable's name warrants two words (e.g., `is_ready`), put an underscore between them, a convention popular in C though less so in other languages.

If declaring multiple variables of the same type at once, it's fine to declare them together, as in:

```c
int quarters, dimes, nickels, pennies;
```

Just don't initialize some but not others, as in:

```c
int quarters, dimes = 0, nickels = 0 , pennies;
```

Also take care to declare pointers separately from non-pointers, as in:

```c
int *p;
int n;
```

Don't declare pointers on the same line as non-pointers, as in:

```c
int *p, n;
```

## Structures

Declare a `struct` as a type as follows, with each curly brace on its own line and members indented therein, with the type's name also on its own line:

```c
typedef struct
{
    string name;
    string dorm;
}
student;
```

If the `struct` contains as a member a pointer to another such `struct`, declare the `struct` as having a name identical to the type, without using underscores:

```c
typedef struct node
{
    int n;
    struct node *next;
}
node;
```

