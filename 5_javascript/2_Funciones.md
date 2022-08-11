---
title: Funciones
has_children: false
parent: Introducción a JavaScript
nav_order: 2
---

# Conceptos básicos de JavaScript: funciones

Cuando pensamos en escribir código, siempre queremos asegurarnos que nuestro código sea legible. Si bien esto suena contradictorio, el código se lee muchas más veces de las que se escribe. Una herramienta central en la caja de herramientas de un desarrollador para garantizar que el código se pueda mantener es la función o método.

# Funciones

Una función es un bloque de código destinado a realizar una tarea. Una función se crea usando la palabra clave `function`, un nombre, un conjunto de parámetros y la definición de la función también conocida como _body_.

En esencia, una función es un bloque de código que podemos ejecutar bajo demanda. Esto es perfecto para escenarios en los que necesitamos realizar la misma tarea varias veces; en lugar de duplicar la lógica en varias ubicaciones (lo que dificultaría la actualización cuando llegue el momento), podemos centralizarla en una ubicación y llamarla cuando necesitemos que se realice la operación; ¡incluso podés llamar a funciones desde otras funciones!

Igual de importante es la capacidad de nombrar una función. Si bien esto puede parecer trivial, el nombre proporciona una forma rápida de documentar una sección de código. Podrías pensar en esto como una etiqueta en un botón. Si hago clic en un botón que dice "Cancelar temporizador", sé que dejará de correr el reloj.

# Creando y llamando funciones

La sintaxis de una función se parece a la siguiente:

```javascript
function nombrDeFuncion() { // definición de la funcion
 // (body) cuerpo de la función
}
```

Si quisieras crear una función para mostrar un saludo, podría verse así:

```javascript
function saludar() {
  console.log('¡Hola, mundo!');
}
```

Siempre que queremos llamar (o invocar) nuestra función, usamos el nombre de la función seguido de `()`. Vale la pena señalar el hecho de que nuestra función se puede definir antes o después de que decidamos llamarla; el compilador de JavaScript lo encontrará por vos.

```javascript
// llamando nuestra funcion
saludar();
```

> **NOTA:** Existe un tipo especial de función conocida como **método**, que ya has estado utilizando. De hecho, vimos esto en nuestra demostración anterior cuando usamos `console.log`. Lo que hace que un método sea diferente de una función es que un método está adjunto a un objeto (`console` en nuestro ejemplo), mientras que una función es flotante, libre. Escucharás que muchos desarrolladores usan estos términos indistintamente.

## Mejores prácticas de función

Hay algunas prácticas recomendadas que se deben tener en cuenta al crear funciones:

- Como siempre, usá nombres descriptivos para que sepas lo que hará la función.
- Usá **camelCasing** para combinar palabras.
- Mantené tus funciones enfocadas en una tarea específica.


# Parámetros

Para que una función sea más reutilizable, a menudo querrás pasarle información. Si consideramos nuestro ejemplo de `saludar` anterior, solo mostrará **¡Hola, mundo!**. No es la función más útil que uno podría crear. Si queremos hacerlo un poco más flexible, como permitir que alguien especifique el nombre de la persona a saludar, podemos agregar un **parámetro**. Un parámetro (también llamado a veces **argumento**), es información adicional enviada a una función.

Los parámetros se enumeran en la parte de definición entre paréntesis y están separados por comas así:

```javascript
function nombre(param, param2, param3) {

}
```

Podemos actualizar nuestro `saludar` para aceptar un nombre y mostrarlo.

```javascript
function saludar(nombre) {
  const mensaje = `¡Hola, ${nombre}!`;
  console.log(mensaje);
}
```

Cuando queremos llamar a nuestra función y pasar el parámetro, lo especificamos entre paréntesis.

```javascript
saludar('Alicia');
// dice "¡Hola, Alicia!" cuando ejecutes el comando 
```

## Valores predeterminados

Podemos hacer que nuestra función sea aún más flexible agregando más parámetros. Pero, ¿y si no queremos que se especifiquen todos los valores? Siguiendo con nuestro ejemplo de saludo, podríamos dejar el nombre según sea necesario (necesitamos saber a quién saludamos), pero queremos permitir que el saludo en sí se personalice como se desee. Si alguien no quiere personalizarlo, proporcionamos un valor predeterminado en su lugar. Para proporcionar un valor predeterminado a un parámetro, lo configuramos de la misma manera que configuramos un valor para una variable: `nombreParametro = 'valorPorDefecto'`. Para ver un ejemplo completo:

```javascript
function saludar(nombre, saludo='Hola') {
  console.log(`${saludo}, ${nombre}`);
}
```

Cuando llamamos a la función, podemos decidir si queremos establecer un valor para el "saludo".

```javascript
saludar('Alicia');
// dice "Hola, Alicia"

saludar('Alicia', 'Buenas');
// dice "Buenas, Alicia"
```

Cualquier parámetro con valores predeterminados debe estar al final de la lista de parámetros. La razón es que JavaScript intenta hacer coincidir argumentos con parámetros y los parámetros con valores predeterminados pueden omitirse en la invocación.

# Valores de retorno

Hasta ahora, la función que construimos siempre saldrá a la [consola](https://developer.mozilla.org/es/docs/Web/API/console){:target="_blank"}. A veces, esto puede ser exactamente lo que estamos buscando, especialmente cuando creamos funciones que llamarán a otros servicios. Pero, ¿qué pasa si quiero crear una función auxiliar para realizar un cálculo y devolver el valor para poder usarlo en otro lugar?

Podemos hacer esto usando un **valor de retorno**. La función devuelve un valor de retorno y se puede almacenar en una variable de la misma manera que podríamos almacenar un valor literal como una cadena o un número.

Una función puede devolver algo o no. Si una función devuelve algo, entonces se usa la palabra clave `return`. La palabra clave `return` espera un valor o referencia de lo que se devuelve así:


```javascript
return miVariable;
```  

Un ejemplo más completo puede verse así:

```javascript
function sumar(primerValor, segundoValor) {
  let suma = primerValor + segundoValor;
  return suma;
}
```

En el código anterior, se devuelve la variable `suma`.

# Invocación

Cuando _invocas_ una función, la llamas con 0...N conjuntos de argumentos. Los valores de los argumentos se vinculan a los parámetros correspondientes a su posición. La función `sumar()` introducido se puede invocar de la siguiente manera:


```javascript
let resultado = sumar(1, 3);
console.log(resultado); // imprime 4
```

Los argumentos `1` y `3` están vinculados a los parámetros `primerValor` y `segundoValor` debido al orden en el que se definen los parámetros.

JavaScript es bastante flexible cuando se trata de invocaciones. No estás obligado a proporcionar argumentos para todos los parámetros, el código se ejecutará de todos modos. Sin embargo, dependiendo de lo que le pases, es posible que el código no se comporte como se esperaba.

🚀 Desafío, intentá llamar al función `sumar()` así `sumar(1)` y ve qué sucede.



# Funciones como parámetros de funciones

A medida que progreses en ru carrera de programación, te encontrarás con funciones que aceptan funciones como parámetros. Este ingenioso truco se usa comúnmente cuando no sabemos cuándo ocurrirá o se completará algo, pero sabemos que debemos realizar una operación en respuesta.

Como ejemplo, considera [setTimeout](https://developer.mozilla.org/es/docs/Web/API/setTimeout){:target="_blank"}, que inicia un temporizador y ejecuta el código cuando se completa. Necesitamos decirle qué código queremos ejecutar. ¡Suena como un trabajo perfecto para una función!

Si ejecutas el código a continuación, después de 3 segundos verás el mensaje **Han transcurrido 3 segundos**.

```javascript
function mostrarCuandoEsteListo() {
  console.log('Han transcurrido 3 segundos');
}
//el valor del temporizador está en milisegundos
setTimeout(mostrarCuandoEsteListo, 3000);
```

# Funciones anónimas

Revisemos lo que hemos construido. Estamos creando una función con un nombre que se usará una vez. A medida que nuestra aplicación se vuelve más compleja, podemos vernos creando muchas funciones que sólo se llamarán una vez. Esto no es ideal. ¡Resulta que no siempre necesitamos proporcionar un nombre!

Cuando estamos pasando una función como parámetro, podemos omitir la creación de una por adelantado y, en su lugar, construir una como parte del parámetro. Usamos la misma palabra clave `función`, pero en su lugar la construimos como un parámetro.

Reescribamos el código anterior para usar una función anónima:

```javascript
setTimeout(function() {
  console.log('Han transcurrido 3 segundos');
}, 3000);
```

Si ejecutás este nuevo código, notarás que obtenemos los mismos resultados. ¡Hemos creado una función, pero no teníamos que darle un nombre!


# Funciones de fecha ancha (Fat arrow functions)

Un atajo común en muchos lenguajes de programación (incluido JavaScript) es la capacidad de usar lo que se llama una función de **flecha** o **flecha ancha**. Utiliza un indicador especial de `=>`, que parece una flecha, ¡de ahí el nombre! Al usar `=>`, podemos omitir la palabra clave `función`.

Reescribamos nuestro código una vez más para usar una función de flecha ancha:
```javascript
setTimeout(() => {
  console.log('Han transcurrido 3 segundos');
}, 3000);
```

## Cuándo usar cada estrategia

Ahora viste que tenemos tres formas de pasar una función como parámetro y puede que te preguntes cuándo usar cada una. Si sabés que usarás la función más de una vez, creala normalmente. Si lo usarás solo para una ubicación, generalmente es mejor usar una función anónima. Depende de vos si usás o no una función de flecha ancha o la sintaxis de `función` más tradicional, pero notarás que la mayoría de los desarrolladores modernos prefieren `=>`.


# Revisión y autoestudio

Vale la pena [leer un poco más sobre las funciones de flecha](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Functions/Arrow_functions){:target="_blank"}, ya que se utilizan cada vez más en bases de código. Practicá escribir una función y luego reescribirla con esta sintaxis.


## Tarea - Diversión con funciones

### Instrucciones

Creá diferentes funciones, tanto funciones que devuelvan algo como funciones que no devuelvan nada.

Ve si podés crear una función que tenga una combinación de parámetros y parámetros con valores predeterminados.

### Rúbrica

| Criterios | Ejemplar | Adecuado | Necesita mejorar |
| -------- | -------------------------------------------------- ------------------------------------ | -------------------------------------------------- -------------- | ----------------- |
| | La solución se ofrece con dos o más funciones de buen rendimiento con diversos parámetros | La solución de trabajo se ofrece con una función y pocos parámetros | La solución tiene errores |


