---
title: Introducción a HTML
has_children: false
nav_order: 4
has_toc: true
---

# Proyecto Calculadora de hidratación basal - Parte 1: Introducción a HTML
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

# Introducción:

HTML, o HyperText Markup Language, es el "esqueleto" de la web. Si CSS 'viste' tu HTML y JavaScript le da vida, el cuerpo de tu aplicación web es tu HTML. La sintaxis de HTML incluso refleja esa idea, ya que incluye etiquetas "head" (cabeza), "body" (cuerpo) y "footer" (pie).

Para esta lección y las siguientes usaremos como ejemplo el diseño de una calculadora de hidratación basal, acorde a los requerimientos explicados en la [sección anterior](/3_html/Calculadora).

Usaremos HTML para diseñar el 'esqueleto' de la interfaz de nuestra calculadora. Necesitamos un formulario que nos permita cargar el dato de entrada y calcular, y una sección que nos permita explicar como se esta haciendo el calculo.

### Actividad:
{: .no_toc }

En tu computadora, crea una carpeta llamada 'calculadora'.

Una vez creada, abri el Visual Studio Code, y abri la carpeta que creaste. Dentro de ella, crea un archivo llamado 'index.html'. Podés hacer esto en Visual Studio Code después de crear tu carpeta del proyecto abriendo una nueva ventana de VS Code, haciendo clic en 'abrir carpeta' y navegando a tu nueva carpeta. Hacé clic en el botón pequeño 'archivo' en el panel del Explorador y creá el nuevo archivo

<!-- Insertar Gif para abrir la carpeta -->
<!-- Insertar Gif para crear archivo -->

> El archivo index.html indica a un navegador que es el archivo predeterminado en una carpeta; las URL como `https://anysite.com/test` se pueden construir usando una estructura de carpetas que incluya una carpeta llamada `test` con `index.html` dentro; `Index.html` no tiene que aparecer en una URL.

---

# Las etiquetas DocType y html

La primera línea de un archivo HTML es su doctype. Es un poco sorprendente que necesite tener esta línea en la parte superior del archivo, pero le dice a los navegadores más antiguos que el navegador necesita representar la página en un modo estándar, siguiendo la especificación html actual.

> Consejo: en VS Code, puedes colocar el cursor sobre una etiqueta y obtener información sobre su uso en las guías de referencia de MDN.

La segunda línea debe ser la etiqueta de apertura de la etiqueta `<html>`, seguida ahora por su etiqueta de cierre. Estas etiquetas son los elementos raíz de su interfaz.

### Actividad:
{: .no_toc }

Agregá estas líneas en la parte superior de tu archivo `index.html`:


```HTML
<!DOCTYPE html>
<html></html>
```

{: .important }
Es importante que cuando hagamos una pagina web, tengamos en cuenta que no sabemos que navegador utiliza el usuario, utilizamos la etiqueta `<!DOCTYPE html>` para que incluso los usuarios con los navegadores mas viejos puedan ver nuestra web, y de la misma manera tendremos que tener en cuenta otras consideraciones de compatibilidad en adelante.

---

# El 'encabezado' del documento

El área 'encabezado' del documento HTML incluye información crucial sobre tu página web, también conocida como [metadatos](https://developer.mozilla.org/es/docs/Web/HTML/Element/meta){:target="_blank"}. En nuestro caso, solo le vamos a poner un titulo a nuestra pagina web

### Actividad:
{: .no_toc }

Agregá un bloque de 'encabezado' a tu documento entre las etiquetas de apertura y cierre `<html>`.

```html
<head>
	<title>Calculadora de hidratación</title>
</head>
```

{: .concept }
El encabezado debe incluir la información que necesita el navegador para saber como interpretar el código HTML.

---

# El `cuerpo` del documento

En HTML, agregamos etiquetas al archivo .html para crear elementos de una página web. Cada etiqueta generalmente tiene una etiqueta de apertura y cierre, como esta: `<p>hola</p>` para indicar un párrafo.

Todo este contenido va a en el `cuerpo` del documento HTML, para lo que se usa la etiqueta `<body>`.

### Actividad:
{: .no_toc }

Lo primero que vamos a hacer es construir el formulario que vamos a usar para la calculadora.

Agrega a tu HTML el cuerpo del documento y empecemos cargando el primer elemento de nuestra web, el titulo del formulario.

```html
<!DOCTYPE html>
<html>
	<head>
        <title>Calculadora de hidratación</title>
    </head>
	<body>
        <h1>Hidratación Basal</h1>
    </body>
</html>
```

{: .concept }
Las etiquetas que encapsulan algún contenido le dicen a navegador de que tipo de contenido se trata. La etiqueta `h1` dice que su contenido es un titulo, y de la misma manera hay etiquetas para todo tipo de contenido, texto normal, botones, etc.

La mayoría de las etiquetas encapsulan contenido mediante etiquetas de apertura y etiquetas de cierre, de esta manera: `<apertura> contenido encapsulado </cierre>`


## Atributos

Ahora que tenemos la estructura de la web, terminemos de crear el formulario agregando un elemento `input` y el `botón` para calcular.

### Actividad:
{: .no_toc }

Agrega los elementos `<input>` y `<button>`:

```html
<!DOCTYPE html>
<html>
	<head>
        <title>Calculadora de hidratación</title>
    </head>
	<body>
        <h1>Hidratación Basal</h1>
        <input type="number" placeholder="Peso en kg" />
        <button>Calcular</button>
    </body>
</html>
```

El elemento `<input>` se utiliza para cargar información, en este caso lo vamos a utilizar para cargar el peso del paciente, pero recién vamos a aprender a utilizar este dato en la introducción a JavaScript.

Ya mencionamos que las etiquetas tienen una apertura y un cierre, pero ademas de eso pueden tener **atributos**, que nos permiten agregar información adicional que el navegador sabe interpretar.

Si miramos la etiqueta `<input>`, vemos que utilizamos los siguientes atributos:
* `type`: define el tipo de dato que el elemento acepta. Si el valor del atributo des `"number"`, entonces solo se pueden ingresar números.
* `placeholder`: define un texto que se muestra en el elemento antes de que el usuario ingrese algún valor, esto se puede usar para transmitir información al usuario. En este caso aprovechamos el placeholder para decirle al usuario que debe ingresar el peso en kilogramos.

{: .concept }
Todos los elementos HTML pueden tener atributos que proveen información adicional sobre los elementos.
Los atributos siempre van en la etiqueta de apertura y tienen un nombre y un valor, que se escriben así: **nombre="valor"**

---

## Division del documento en secciones - Elementos <div>

Con lo que hicimos hasta ahora, nuestro formulario ya esta listo, pero los requerimientos también nos piden que en la pagina se explique el método utilizado para calcular. Por ahora, podemos agregar la siguiente descripción:

* De 0kg a 10kg, se calcula 100cc por cada kilo.
* Se suman 50cc por cada kilo de peso por arriba de 10kg, hasta 20kg.
* De 20kg para arriba, se suman 20cc por cada kilo adicional

Además, podemos agregarle un título usando otro elemento `<h1>`.

### Actividad:
{: .no_toc }

Agregá al documento el titulo y la descripción:

```html
<h1>¿Como se calcula?</h1>
<ul>
    <li>De 0kg a 10kg, se calcula 100cc por cada kilo.</li>
    <li>Se suman 50cc por cada kilo de peso por arriba de 10kg, hasta 20kg</li>
    <li>De 20kg para arriba, se suman 20cc por cada kilo adicional</li>
</ul>
```

Utilizamos la etiqueta <ul> (de un-ordered list) y <li> (de list item) para hacer una lista con viñetas.

Hasta ahora, el codigo completo te deberia estar quedando asi:

```html
<!DOCTYPE html>
<html>
	<head>
        <title>Calculadora de hidratación</title>
    </head>
	<body>
        <h1>Hidratación Basal</h1>
        <input type="number" placeholder="Peso en kg" />
        <button>Calcular</button>
        <h1>¿Como se calcula?</h1>
        <ul>
            <li>De 0kg a 10kg, se calcula 100cc por cada kilo.</li>
            <li>Se suman 50cc por cada kilo de peso por arriba de 10kg, hasta 20kg</li>
            <li>De 20kg para arriba, se suman 20cc por cada kilo adicional</li>
        </ul>
    </body>
</html>
```

Ahora que tenemos todo el contenido que necesitamos, tenemos que organizar la pagina web de mejor manera.

Necesitamos dividir el contenido en secciones que nos permitan ordenar la pagina como queremos. En nuestro caso, si queremos seguir el diseño propuesto en los requerimientos, necesitamos posicionar todo el contenido en el centro de la pagina, centrar y alinear el formulario a la izquierda y la explicación a la derecha.

Para hacer todo esto utilizamos etiquetas `<div>`, que después nos van a ayudar a posicionar las cosas mediante CSS.

Si necesitamos posicionar todo el contenido en el centro de la pagina, vamos a necesitar que todo lo que este dentro del cuerpo este encapsulado en un `<div>`:

```html
<!DOCTYPE html>
<html>
	<head>
        <title>Calculadora de hidratación</title>
    </head>
	<body>
        <div>
            <h1>Hidratación Basal</h1>
            <input type="number" placeholder="Peso en kg" />
            <button>Calcular</button>
            <h1>¿Como se calcula?</h1>
            <ul>
                <li>De 0kg a 10kg, se calcula 100cc por cada kilo.</li>
                <li>Se suman 50cc por cada kilo de peso por arriba de 10kg, hasta 20kg</li>
                <li>De 20kg para arriba, se suman 20cc por cada kilo adicional</li>
            </ul>
        </div>
    </body>
</html>
```

Por otro lado, necesitamos separar el formulario de la calculadora de la explicación. Necesitamos encapsular ambas cosas con mas etiquetas `<div>`:

```html
<!DOCTYPE html>
<html>
	<head>
        <title>Calculadora de hidratación</title>
    </head>
	<body>
        <div>
            <div>
                <h1>Hidratación Basal</h1>
                <input type="number" placeholder="Peso en kg" />
                <button>Calcular</button>
            </div>
            <div>
                <h1>¿Como se calcula?</h1>
                <ul>
                    <li>De 0kg a 10kg, se calcula 100cc por cada kilo.</li>
                    <li>Se suman 50cc por cada kilo de peso por arriba de 10kg, hasta 20kg</li>
                    <li>De 20kg para arriba, se suman 20cc por cada kilo adicional</li>
                </ul>
            </div>
        </div>
    </body>
</html>
```

## Preparando los mensajes de error y resultados

Con esto tenemos todo el HTML preparado, y solo queda agregarle estilos. Pero también tenemos que pensar como vamos a mostrar los mensajes o cualquier otro elemento que el usuario necesite ver, como los resultados de la calculadora!.

Hay muchas formas de crear elementos HTML de forma dinamica, pero para simplificar este proyecto, vamos a hacerlo directamente en el HTML.

Sabemos que los requerimientos nos piden que calculemos dos resultados:
* El Flujo o mantenimiento (en cc/hr): Este es el calculo principal.
* El valor m+m/2, que es en mantenimiento: Es un valor secundario.

Agreguemos estos elementos debajo del boton:

```html
...
<div>
    <h1>Hidratación Basal</h1>
    <input type="number" placeholder="Peso en kg" />
    <button>Calcular</button>
    <p>71cc/h</p>
    <p>m+m/2 : 105cc/h</p>
</div>
...
```

Lo que hicimos fue agregar los resultados al formulario, pero son valores de prueba, solo para ver como quedaría finalmente. Mas adelante vamos a aprender a ocultar o mostrar los resultados y a cambiar los valores valiéndonos de JavaScript.

Una cosa mas que nos esta faltando es un mensaje de error para cuando el usuario quiere hacer el calculo sin haber ingresado ningún valor:

```html
...
<div>
    <h1>Hidratación Basal</h1>
    <input type="number" placeholder="Peso en kg" />
    <p>* Debe completar todos los datos</p>
    <button>Calcular</button>
    <p>71cc/h</p>
    <p>m+m/2 : 105cc/h</p>
</div>
...
```

{: .concept }
La etiqueta `<p>` se usa para agregar `párrafos`, o en otras palabras, texto que ocupe toda una linea. Esto significa que el elemento va a ocupar toda una linea.

# Marcado semántico

En general, es preferible usar ‘semántica’ significativa al escribir HTML. Qué significa eso? Significa que tenemos que utilizar las etiquetas HTML de la forma en que fueron diseñadas. Por ejemplo, el título principal en una página debería usar siempre una etiqueta <h1>.

Agregá la siguiente línea justo debajo de tu etiqueta de apertura <body>:

```html
<h1>Detalle de Producto</h1>
```

El uso de marcado semántico, como que los encabezados sean `<h1>` y las listas no ordenadas se representen como `<ul>`, ayuda a los lectores de pantalla a navegar por una página. En general, los botones deben escribirse como `<button>` y las listas deben ser `<li>`. Si bien es posible usar elementos `<span>` de estilo especial con controladores de clic para simular botones, es mejor para los usuarios con capacidades diferentes usar tecnologías para determinar en qué parte de una página reside un botón e interactuar con él. Por esta razón, intenta utilizar el marcado semántico tanto como sea posible.
