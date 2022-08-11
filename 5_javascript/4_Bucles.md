---
title: Vectores y Bucles
has_children: false
parent: Introducción a JavaScript
nav_order: 4
---

# Conceptos básicos de JavaScript: vectores y bucles

En esta lección, aprenderás sobre vectores y bucles, que se utilizan para manipular datos.

# Vectores

Trabajar con datos es una tarea común para cualquier lenguaje y es una tarea mucho más fácil cuando los datos están organizados en un formato estructural, como vectores. Con las vectores (arrays), los datos se almacenan en una estructura similar a una lista. Uno de los principales beneficios de las vectores es que puede almacenar diferentes tipos de datos en un vector.

✅ ¡Las vectores están a nuestro alrededor! ¿Podés pensar en un ejemplo de la vida real de una vector, como una vector de paneles solares?

La sintaxis de una vector es un par de corchetes.

```javascript
let mArray = [];
```

Este es una vector vacío, pero las vectores se pueden declarar ya pobladas con datos. Varios valores en una vector están separados por una coma.

```javascript
let saboresHelado = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
```

A los valores de la vector se les asigna un valor único llamado **índice**, un número entero que se asigna en función de su distancia desde el principio del vector. En el ejemplo anterior, el valor de la cadena "Chocolate" tiene un índice de 0 y el índice de "Rocky Road" es 4. Utilizás el índice entre corchetes para recuperar, cambiar o insertar valores de vector.

✅ ¿Te sorprende que las vectores comiencen en el índice cero? En algunos lenguajes de programación, los índices comienzan en 1. Hay una historia interesante en torno a esto, que podés [leer en Wikipedia](https://hmong.es/wiki/Zero-based_numbering){:target="_blank"}.

```javascript
let saboresHelado = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
saboresHelado[2]; //"Vanilla"
```

Podés aprovechar el índice para cambiar un valor, como este:

```javascript
saboresHelado[4] = "Butter Pecan"; //Se cambió "Rocky Road" a "Butter Pecan"
```

Y podés insertar un nuevo valor en un índice dado como este:

```javascript
saboresHelado[5] = "Cookie Dough"; //Añadida "Cookie Dough"
```

✅ Una forma más común de enviar valores a una vector es mediante el uso de operadores de vector como array.push()

Para saber cuántos elementos hay en una vector, usá la propiedad `length`.

```javascript
let saboresHelado = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];
saboresHelado.length; //5
```

✅ ¡Intentalo vos mismo! Utilizá la consola de tu navegador para crear y manipular una vector de tu propia creación.

# Bucles

Los bucles permiten tareas repetitivas o **iterativas** y pueden ahorrar mucho tiempo y código. Cada iteración puede variar en sus variables, valores y condiciones. Hay diferentes tipos de bucles en JavaScript y tienen pequeñas diferencias, pero esencialmente hacen lo mismo: bucles sobre datos.

### Bucle For

El ciclo `for` requiere 3 partes para iterar:
     - `contador` Una variable que normalmente se inicializa con un número que cuenta el número de iteraciones.
     - `condicion` Expresión que usa operadores de comparación para hacer que el bucle se detenga cuando `true`.
     - `expresion-de-iteracion` Se ejecuta al final de cada iteración, generalmente se usa para cambiar el valor del contador.

  
```javascript
// Contando hasta 10
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

✅ Ejecutá este código en una consola de navegador. ¿Qué sucede cuando realizás pequeños cambios en el contador, la condición o la expresión de iteración? ¿Podés hacer que corra al revés, creando una cuenta regresiva?

### Bucle while

A diferencia de la sintaxis para el ciclo `for`, los ciclos `while` solo requieren una condición que detendrá el ciclo cuando sea `true`. Las condiciones en los bucles suelen depender de otros valores, como contadores, y deben gestionarse durante el bucle. Los valores iniciales para los contadores deben crearse fuera del ciclo, y cualquier expresión que cumpla una condición, incluido el cambio del contador, debe mantenerse dentro del ciclo.

```javascript
//Contando hasta 10
let i = 0;
while (i < 10) {
 console.log(i);
 i++;
}
```

✅ ¿Por qué elegirías un bucle `for` frente a un bucle `while`? 17K espectadores tenían la misma pregunta sobre StackOverflow, y algunas de las opiniones [podrían ser interesantes para vos](https://stackoverflow.com/questions/39969145/while-loops-vs-for-loops-in-javascript){:target="_blank"}.

# Bucles y vectores

Las vectores se utilizan a menudo con bucles porque la mayoría de las condiciones requieren la longitud del vector para detener el bucle, y el índice también puede ser el valor del contador.

```javascript
let saboresHelado = ["Chocolate", "Strawberry", "Vanilla", "Pistachio", "Rocky Road"];

for (let i = 0; i < saboresHelado.length; i++) {
  console.log(saboresHelado[i]);
} //Termina cuando se imprimen todos los sabores
```

✅ Experimentá recorriendo una serie de tu propia creación en la consola de tu navegador.

🚀 Desafío: Hay otras formas de realizar un bucle sobre arreglos además de los bucles for y while. Existen:
 - [forEach](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach){:target="_blank"}.
 - [for-of](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/for...of){:target="_blank"}.
 - [map](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array/map){:target="_blank"}. 
Volvé a escribir tu bucle de vector utilizando una de estas técnicas.


# Revisión y autoestudio

Las vectores en JavaScript tienen muchos métodos adjuntos, extremadamente útiles para la manipulación de datos. [Leé sobre estos métodos](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array){:target="_blank"} y probá algunos de ellos (como push, pop, slice y splice) en una vector de su creación.


## Tarea - Hacer bucle en un vector

### Instrucciones

Creá un programa que enumere cada tercer número entre 1 y 20 y lo imprima en la consola.

> SUGERENCIA: usá un bucle for y modificá la expresión-iteración

### Rúbrica

| Criterios | Ejemplar | Adecuado | Necesita mejorar |
| -------- | --------------------------------------- | ------------------------ | ------------------------------ |
| | El programa se ejecuta correctamente y está comentado | Programa no comentado | El programa está incompleto o con errores |