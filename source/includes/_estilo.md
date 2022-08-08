# Guía de estilo

Esta guía de estilo es esencialmente una traducción de la [guía de Harvard](https://cs50.readthedocs.io/style/c/) con ligeros cambios.

No existe una “única” forma correcta de formatear código. Pero definitivamente existen *varias* formas de hacerlo mal. Durante el curso se pedirá que todos los entregables respeten las reglas de estilo aquí dispuestas (similar a como muchas empresas tienen lineamientos de estilo obligatorios). El objetivo es generar código fuente con estilos consistentes independientemente del programador.

## Longitud de línea

```c
// Nótese como esta caja de código requiere que el usuario use scroll.

// These next lines of code first prompt the user to give two integer values and then multiplies those two integer values together so they can be used later in the program
int first_collected_integer_value_from_user = get_int("Integer please: ");
int second_collected_integer_value_from_user = get_int("Another integer please: ");
int product_of_the_two_integer_values_from_user = first_collected_integer_value_from_user * second_collected_integer_value_from_user;
```
Por convenciones históricas, la longitud máxima de una línea de código será de 80 caracteres. 

Por decisiones de diseño de IBM, inicialmente los monitores tenían la capacidad de renderizar 24 líneas de texto cada una con hasta 80 caracteres. Ahora es evidentemente obsoleto pero el límite de 80 caracteres es aún una restricción frecuente para evitar `line-wraps` o tener barras de `scroll`.  En cualquier forma, si requieres más de 80 caracteres para una sola instrucción es posible que necesites pensar en tu esquema de nombres de variables, o reconsiderar el diseño general de tu solución.

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
  No mezcles código y comentario en la misma linea! i.e
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
Las funciones son perfectas candidatas para breves comentarios significativos: resulta útil que cada función tenga justo antes de su **implementación** una breve descripción de que hace dicha subrutina. Generalmente no es necesario comentar `main`.

<aside class="notice">
  No es necesario comentar el comportamiento de ciclos de repetición.
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

La guía de estilo pretende resaltar el contenido de los bloques condicionales, y clarificar la expresión de la condicional.

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

- las llaves se alinean correctamente, *cada una en su propia linea*, haciendo énfasis en lo que contiene cada bloque de código. 
- cada `if` tiene un espacio antes de abrir el paréntesis de la expresión condicional.
- cada llamada a `printf` esta correctamente indentada.
- existe un espacio separando `<` y `>` de los valores a comparar.
- No se tiene espacio inmediatamente después de abrir `(` paréntesis o inmediatamente antes de `)` cerrarlo.

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
// esto es terrible y no será aceptado.
if (x < 0)
    {
    printf("x is negative\n");
    }
else
    {
    printf("x is negative\n");
    }
```
Estos estilos no serán aceptados independientemente de si la solución es programaticamente correcta. 
## Switches

Para la sentencia `switch` 

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

es necesario que:

- cada llave se encuentra en su propia linea;
- existe un espacio entre la palabra reservada `switch` y la expresión a evaluar;
- no se tiene espacio inmediatamente después de abrir `(` paréntesis o inmediatamente antes de `)` cerrarlo.
- las condiciones de cada caso se encuentran correctamente indentadas en relación al inicio de la expresión. 
- el bloque de código correspondiente a cada caso se encuentra correctamente indentado en relación a la expresión de ese caso; y
- todos los `case` (incluyendo `default`) termina con `break`.

Sobre el ultimo punto, es importante recalcar que aunque `c` permite `fallthrough` en los casos (i.e no terminar explícitamente un caso) esto no será permitido. 

## Funciones

### Sobre <code>main</code>

Para declarar `main`

```c
// ✓ correcto
int main(void)
{

}
```
de acuerdo con el estándar [C99](http://en.wikipedia.org/wiki/C99), la declaración de la función `main` será tan explicita como sea posible, en su version mas simple regresando un `int` y descartando `argc` y `argv` de forma explicita con `void`.

```c
// ✓ correcto
int main(int argc, char *argv[])
{
}
```

de otra forma, si se requieren `argc` y `argv` estos pueden ser declarados como un arreglo de `char`.


```c
// ✓ correcto
int main(int argc, char **argv)
{
}
```
O si se prefiere, como un `char**`.

recuerda no dejar vacíos los argumentos de `main`

```c
// ✗ incorrecto
int main()
{
}
```

o declarar `main` tal que regrese un tipo de dato diferente de `int`.

```c
// ✗ incorrecto
void main()
{
}
```

o dejar implícito el tipo de dato de retorno. 

```c
// ✗ incorrecto
main()
{
}
```

<aside class="notice">
Para nuestras propias funciones, se seguirá el mismo estilo, con las llaves de apertura y cierre cada una en su propia linea y el tipo de dato que regresa la función en la misma linea que el identificador. 
</aside>

## Indentación

Decide si tu estilo de indentación sera de 2 espacios por `\t`  o 4 espacios y mantén el estilo **consistente**. Indenta los bloques de código de tu programa para que sea evidente que subrutinas están dentro de otras rutinas. Si usas la tecla de tabulador, asegúrate que tu editor de texto este configurado para sustituir `\t` por espacios. Esto es porque el carácter tabulador `\t` se renderiza de forma ligeramente distinta en cada editor.

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

considera este programa, nótese que:

- Es evidente que subrutina corresponde a cada ciclo de repetición `for`.
- Cada llave tanto de apertura como de cierre se encuentra en su propia linea.
- La expresión de condición e incremento se encuentran en la misma linea.

## Ciclos de repetición

### for

para ciclos de repetición `for` 

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

Cuando necesites variables temporales de iteración, usa en primera instancia `i`, después `j`, y por ultimo `k`, a menos que el ciclo tenga algún significado semántico que sea util usar nombres mas específicos (i.e `row` y `col` para iterar sobre arreglos de dos dimensiones que representan una matriz).

Si en algún momento consideras que necesitas mas de 3 ciclos anidados, es muy probable que necesites reconsiderar el diseño de tu solución. 

### while

Los ciclos `while` se declararán como sigue: 

```c
while (condition)
{
    // Do something
}
```

nótese que:

- cada llave se encuentra en su propia linea;
- existe un espacio justo después de la palabra reservada `while`;
- no se tiene espacio inmediatamente después de abrir `(` paréntesis o inmediatamente antes de `)` cerrarlo; y
- el cuerpo del ciclo (en este caso un comentario) esta correctamente indentado.

### do ... while

Los ciclos `do..while` se declararán como sigue: 

```c
do
{
    // Do something
}
while (condition);
```

Nótese que:

- cada llave se encuentra en su propia linea;
- la palabra reservada `do` se encuentra en su propia linea.
- existe un espacio justo después de la palabra reservada `while`;
- la condición se encuentra en la misma linea que la palabra reservada `while`;
- no se tiene espacio inmediatamente después de abrir `(` paréntesis o inmediatamente antes de `)` cerrarlo; y
- el cuerpo del ciclo (en este caso un comentario) esta correctamente indentado.

## Apuntadores

Los apuntadores seguirán las siguiente reglas de estilo: 

```c
int *p; // ✓ correcto
```
cuando declaramos un apuntador, el símbolo `*` se encuentra de forma adyacente al identificador de la variable. 


```c
int* p; // ✗ incorrecto
```
No de forma adyacente al tipo de dato.

## Variables

### Sobre nombres

Puesto que usaremos el estándar [C99](http://en.wikipedia.org/wiki/C99), no definan todas las variables de un bloque en la parte superior del bloque.

```c
for (int i = 0; i < LIMIT; i++)
{
    printf("%i\n", i);
}
```
declaren las variables tan cerca a su primer uso como sea posible,asimismo las variables tendrán el alcance (`scope`) mínimo indispensable. por ejemplo, si la variable `i` solo se necesita para la iteración de un ciclo, declara la variable en la cabecera del ciclo. 

Para variables cuya única funcionalidad es iteración, los nombres `i`, `j` y `k` son suficiente, para otras variables sera util encontrar nombres semánticamente relevantes que describan de forma **concisa** cual es su uso. Por ejemplo, `sum` si la variable es el resultado de una expresión de adición. Si la variable requiere de dos o mas palabras (i.e `is_ready`), usa un guion bajo `_` para separarlas. Esta es una convención popular en lenguajes como `C` y `ruby` . otro lenguajes prefieren `camelCase` i.e `isReady`.

### sobre declaraciones


Si declaramos multiples variables del mismo tipo, es correcto declararlas en la misma linea, o una por linea.

```c
// ✓ correcto
int quarters, dimes, nickels, pennies;
```

Si se decide declararlas en la misma linea, esta prohibido inicializar solamente algunas variables. 

```c
// ✗ incorrecto
int quarters, dimes = 0, nickels = 0 , pennies;
```

Es importante declarar apuntadores y tipos primitivos por su cuenta, cada uno en su linea.

```c
// ✓ correcto
int *p;
int n;
```

No declares apuntadores, y tipos de datos primitivos en la misma linea. 

```c
// ✗ incorrecto
int *p, n;
```

## Tipos estructurados

Para declarar un tipo `struct` compuesto:

```c
typedef struct
{
    string name;
    string dorm;
}
student;
```

nótese que:

- las palabras reservadas `typedef` y `struct` se encuentran en la misma linea, en su propia linea;
- las llaves de apertura y cierre se encuentran en su propia linea;
- los miembros de la estructura se encuentran correctamente indentados, uno por linea; y
- el identificador del tipo de dato compuesto `student` se encuentra en su propia linea.
