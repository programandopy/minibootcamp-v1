---
title: Qué es Programación
has_children: false
parent: Introduccion a la programación
---

# ¿Qué es programación?

La programación (también conocida como codificación) es el proceso de escribir instrucciones para un dispositivo, como una computadora o un dispositivo móvil. Escribimos estas instrucciones con un lenguaje de programación, que luego es interpretado por el dispositivo. Estos conjuntos de instrucciones pueden recibir varios nombres:  programa, programa de computadora, aplicación (app) y ejecutable son algunos nombres populares.

Un programa puede ser cualquier cosa que esté escrita con código; Los sitios web, los juegos y las aplicaciones para teléfonos son programas. Si bien es posible crear un programa sin escribir código, el dispositivo interpreta la lógica subyacente y lo más probable es que esa lógica se haya escrito con código. Un programa que está ejecutando o ejecutando código está realizando instrucciones. El dispositivo con el que está leyendo esta lección está ejecutando un programa para imprimirlo en su pantalla.

✅ Busca en google: ¿quién fue el primer programador/a informático del mundo?


# ¿Qué es lenguaje de programación?

Los lenguajes de programación permiten a los desarrolladores escribir instrucciones para una computadora. Las computadoras solo pueden entender binarios (1 y 0) y, para la mayoría de los desarrolladores, esa no es una forma muy eficiente de comunicarse. Los lenguajes de programación son el vehículo para la comunicación entre humanos y computadoras.

Los lenguajes de programación vienen en diferentes formatos y pueden servir para diferentes propósitos. Por ejemplo, JavaScript se usa principalmente para aplicaciones web, mientras que Bash se usa principalmente para sistemas operativos.

Los idiomas de bajo nivel generalmente requieren menos pasos que los idiomas de alto nivel para que un dispositivo interprete las instrucciones. Sin embargo, lo que hace que los lenguajes de alto nivel sean populares es su legibilidad y compatibilidad. JavaScript se considera un lenguaje de alto nivel.

El siguiente código ilustra la diferencia entre un lenguaje de alto nivel con JavaScript y un lenguaje de bajo nivel con código ensamblador ARM.

```javascript
let number = 10
let n1 = 0, n2 = 1, nextTerm;

for (let i = 1; i <= number; i++) {
    console.log(n1);
    nextTerm = n1 + n2;
    n1 = n2;
    n2 = nextTerm;
}
```

```c
 area ascen,code,readonly
 entry
 code32
 adr r0,thumb+1
 bx r0
 code16
thumb
 mov r0,#00
 sub r0,r0,#01
 mov r1,#01
 mov r4,#10
 ldr r2,=0x40000000
back add r0,r1
 str r0,[r2]
 add r2,#04
 mov r3,r0
 mov r0,r1
 mov r1,r3
 sub r4,#01
 cmp r4,#00
 bne back
 end
```

## Elementos de un programa

Una sola instrucción en un programa se denomina *declaración* y generalmente tendrá un carácter o espacio entre líneas que marca dónde termina la instrucción. La forma en que termina un programa varía con cada lenguaje. Una declaración puede ser algo como una oración:  *mover__pasos*

Las declaraciones dentro de un programa pueden basarse en los datos proporcionados por un usuario o en otro lugar para llevar a cabo las instrucciones. Los datos pueden cambiar el comportamiento de un programa, por lo que los lenguajes de programación vienen con una forma de almacenar datos temporalmente para que puedan usarse más tarde. Estas se llaman *variables*. Las variables son declaraciones que le indican a un dispositivo que guarde datos en su memoria. Las variables en los programas son similares a las variables en álgebra, donde tienen un nombre único y su valor puede cambiar con el tiempo. Ejemplo *mover_10_pasos*, el valor *10* puede ser considerado una variable.

Existe la posibilidad de que un dispositivo no ejecute algunas declaraciones. Esto suele ser por diseño cuando lo escribe el desarrollador o por accidente cuando se produce un error inesperado. Este tipo de control sobre una aplicación la hace más robusta y fácil de mantener. Por lo general, estos cambios en el control ocurren cuando se cumplen ciertas condiciones. Una declaración común utilizada en la programación moderna para controlar cómo se ejecuta un programa es la declaración `if..else` que significa `si...entonces`. Un ejemplo puede ser `si llegó al final entonces saltar`

✅ Aprenderás más sobre este tipo de declaraciones en lecciones posteriores.