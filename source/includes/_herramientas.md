# Herramientas
## Editores & IDEs

[CLion](https://www.jetbrains.com/clion/) es el IDE oficial del curso. Unicamente se proporcionara soporte institucional a CLion.
<aside class="notice"> Recuerden solicitar su licencia gratuita por estudiantes usando su correo institucional.</aside>

[Vs-Code](https://code.visualstudio.com/) es una opción alternativa para aquellos **hackers** que no tengan miedo de configurar su propio toolchain.

[SpaceVim](https://spacevim.org/) para aquellos que quieran pasar mas tiempo configurando su IDE que programando.

## VCS

Usaremos Git como nuestro **V**ersion **C**ontrol **S**ystem para todos los entregables y ejercicios.
Aunque si lo desean pueden usar una GUI - **G**raphic **U**ser **I**nterface, es **altamente recomendado** que usen la CLI - **C**ommand **L**ine **I**nterface.

Pueden obtener [Git aquí](https://git-scm.com/downloads)

| Herramienta | Version |
| :----- | :--------- |
| git | `>= 2.3` |

## Toolchain

CLion tiene `out-of-the-box` configurado correctamente el toolchain necesario, si se desea usar otro IDE (i.e `vs-code`) es necesario instalar de forma independiente:

| Herramienta | Version |
| :----- | :--------- |
| CMake | `>= 3.33` |
| clang, gcc | `>= 12.0`, ` >= 4.5`|
| Microsoft™ Visual™ Studio™ C++™ | ` >= ???` |

Para los mortales de Microsoft™ Windows™ 10™ CLion usa una version empaquetada de MinGW. Esta es suficiente siempre y cuando NO usemos librerías externas (i.e `raylib` o `Criterion`).

Opcionalmente pero **altamente recomendado**, si desean ejecutar las pruebas unitarias de forma local se requiere [Criterion](https://github.com/Snaipe/Criterion).

Para los mortales de Microsoft™ Windows™ 10™ es necesario instalar Microsoft™ Visual™ Studio™ C++™ y Meson de forma independiente, compilar e instalar la librería.

<aside class="success">Se recomienda desinstalar windows y sustituirlo por Ubuntu</aside>

Adicional a esto, yo uso:

| Herramienta | Version |
| ----- | --------- |
| vim | `>= 8.2` |
| iTerm | `>= 3` |
| Homebrew | `>= 3.5` |

Si algún hacker usa MacOS es **altamente** recomendado que usen [Homebrew](https://brew.sh/) como su administrador de paquetes.
