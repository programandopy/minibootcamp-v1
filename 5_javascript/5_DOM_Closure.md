---
title: Manipulación del DOM
has_children: false
parent: Introducción a JavaScript
nav_order: 5
---

# Proyecto de Diseño Parte 3: Introducción a Manipulación del DOM y Closure
{: .no_toc }

Ahora que tenemos algunos fundamentos de Javascript, podemos aprender los nuevos conceptos mientras retomamos nuestro proyecto del diseñador de tarjetas de producto.

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

Manipular el DOM, o el "Modelo de objetos de documento", es un aspecto clave del desarrollo web. Según [MDN](https://developer.mozilla.org/es/docs/Web/API/Document_Object_Model/Introduction){:target="_blank"}:

> "El modelo de objeto de documento (DOM) es una interfaz de programación para los documentos HTML y XML. Facilita una representación estructurada del documento y define de qué manera los programas pueden acceder, al fin de modificar, tanto su estructura, estilo y contenido. El DOM da una representación del documento como un grupo de nodos y objetos estructurados que tienen propiedades y métodos. Esencialmente, conecta las páginas web a scripts o lenguajes de programación. ". 

Además, esta lección presentará la idea de un [closure de JavaScript](https://developer.mozilla.org/es/docs/Web/JavaScript/Closures){:target="_blank"}, que podés considerar como una función encerrada por otra función para que la función interna tenga acceso a los datos de la función externa.

Usaremos un closure para manipular el DOM.

> Pensá en el DOM como un árbol, que representa todas las formas en que se puede manipular un documento de página web. Se han escrito varias API (interfaces de programas de aplicación) para que los programadores, utilizando el lenguaje de programación de su elección, puedan acceder al DOM y editarlo, cambiarlo, reorganizarlo y administrarlo de otro modo.

![representacion DOM](images/dom-tree.png){: width="650" }{: .center-image}

En esta lección, completaremos nuestro proyecto de diseño interactivo creando el JavaScript que permitirá al usuario manipular los elementos en la página.

## Requisito previo:

{: .important }
Deberías tener el HTML y CSS para tu layout construido. Al final de esta lección, podrás mover los elementos dentro y fuera del layout arrastrándolos.

### Actividad:
{: .no_toc }

En tu carpeta de layout, creá un nuevo archivo llamado `script.js`. 

Ahora tenemos que pedirle al navegador que incluya nuestro archivo. Como siempre, hacemos esto en la sección `<head>`:

```html
	<script src="./script.js" defer></script>
```

{: .note }
Usá `defer` cuando importes un archivo JavaScript externo en el archivo html para permitir que el JavaScript se ejecute sólo después de que el archivo HTML se haya cargado por completo. También podría usar el atributo `async`, que permite que el script se ejecute mientras se analiza el archivo HTML, pero en nuestro caso, es importante tener los elementos HTML completamente disponibles para arrastrar antes de permitir que se ejecute el script de arrastre.

Para probar que todo esta funcionando, podemos imprimir un mensaje en la consola:

```javascript
	console.log('hola mundo')
```

✅ ¿Donde escribimos esta instrucción de javascript? si no esta funcionando podes volver a mirar las lecciones anteriores.

---

# Los elementos DOM

Lo primero que debemos hacer es crear referencias a los elementos que queremos manipular en el DOM. En nuestro caso, son los componentes y productos que esperan actualmente en las barras laterales.

Te invitamos a leer mas sobre como funciona el DOM en esta página: [MDN](https://developer.mozilla.org/es/docs/Web/API/Document_Object_Model/Introduction){:target="_blank"}.

Con cada etiqueta HTML que escribimos en nuestro código, el navegador crea un **ELEMENTO**, con un montón de funcionalidad que nos permite trabajar con el usando javascript.

Hagamos un experimento para entender mejor.

### Actividad:
{: .no_toc }

Vamos a tratar de modificar el color de fondo del tablero derecho, donde están las imágenes de productos.

Como sabemos, esto lo podemos hacer editando el CSS, pero si lo hacemos asi, el cambio será estático. Se aplica el color que especificamos y esto queda escrito en piedra.

Para tener un comportamiento mas dinámico hagamos lo siguiente:

```javascript
	let tableroDerecho = document.getElementById('tablero-derecho');
```

Lo que hacemos con esto es guardar en la variable `tableroDerecho` el elemento que tenga el id `tablero-derecho`, en este caso el `div` que contiene todas las imagenes de productos.

Desglosemos esta linea de código:
* `document` hace referencia al DOM (modelo de objeto de documento), y con el `.`, podemos pedir algo que se encuentre dentro de ese *objeto*
* `getElementById()`, es un **método** o función que nos devuelve un elemento. Tal como dice el nombre (obtener elemento por id), busca un elemento en el DOM por el ID que especificamos en el HTML.
* `let tableroDerecho =`: Creamos una variable llamada tableroDerecho, y la inicializamos con un valor. Hasta ahora vimos solo algunos tipos de dato que podemos asignar a una variable, en este caso, la variable `tableroDerecho`, tiene un ELEMENTO, que es un tipo de dato llamado **OBJETO**

{: .important }
El **método** `getElementById`, recibe como **argumento** el ID del elemento que queremos obtener.

Ahora podemos manipular el elemento seleccionado como queramos. En este caso queremos cambiar el color, asi que vamos a acceder a un objeto llamado **style** que se encuentra dentro del elemento, allí encontraremos todas las propiedades de estilo que podemos cambiar.

```javascript
	tableroDerecho.style.backgroundColor = 'blue';
```

Guarda los cambios y actualiza la pagina para ver lo que pasa.

De esta misma forma, interactuar con la pagina para cambiar cosas en cualquier momento y de forma dinámica con JavaScript, gracias a estas herramientas que nos da el DOM para manipular los elementos.

---

### Actividad:
{: .no_toc }

Ahora, lo que necesitamos hacer es que el usuario pueda arrastrar las imágenes, asi que vamos a hacer lo siguiente:

```html
arrastrarElemento(document.getElementById('componente1'));
arrastrarElemento(document.getElementById('componente2'));
arrastrarElemento(document.getElementById('componente3'));
arrastrarElemento(document.getElementById('componente4'));
arrastrarElemento(document.getElementById('componente5'));
arrastrarElemento(document.getElementById('componente6'));
arrastrarElemento(document.getElementById('componente7'));
arrastrarElemento(document.getElementById('componente8'));
arrastrarElemento(document.getElementById('componente9'));
arrastrarElemento(document.getElementById('componente10'));
arrastrarElemento(document.getElementById('componente11'));
arrastrarElemento(document.getElementById('componente12'));
arrastrarElemento(document.getElementById('componente13'));
arrastrarElemento(document.getElementById('componente14'));
arrastrarElemento(document.getElementById('componente15'));
arrastrarElemento(document.getElementById('componente16'));
arrastrarElemento(document.getElementById('producto1'));
arrastrarElemento(document.getElementById('producto2'));
arrastrarElemento(document.getElementById('producto3'));
arrastrarElemento(document.getElementById('producto4'));
```

✅ ¿Cual es el argumento de la función `arrastrarElemento()`?

¿Que está pasando acá? Estamos haciendo referencia al documento y mirando a través de su DOM para encontrar un elemento con un Id particular. ¿Recordás en la primera lección sobre HTML que le diste ID individuales a cada imagen (`id = "componente1"`)? Ahora vas a hacer uso de ese esfuerzo. Una vez identificado, se pasa el elemento a una función llamada `arrastrarElemento()`. Con esto, seleccionamos los elementos y podemos empezar a manipularlos.

Esto todavía no funciona, y si probas el código guardando y actualizando la página, vamos a ver un error en la consola. Esto es porque el navegador no sabe que significa `arrastrarElemento()`, nos falta definir la función.

✅ ¿Por qué hacemos referencia a elementos por Id? ¿Por qué no por su clase de CSS? Podés consultar la lección anterior sobre CSS para responder a esta pregunta.

---

# El closure

Ahora estás listo para crear el closure `arrastrarElemento`, que es una función externa que encierra una función o funciones internas (en nuestro caso, tendremos tres).

Los closures son útiles cuando una o más funciones necesitan acceder al alcance de una función externa. He aquí unos ejemplos que podes probar (pero recorda que nuestro proyecto esta dando un error, asi que lo tenes que hacer en otro lado):

```javascript
function init(){
    let mensaje = 'Aprendiendo Javascript'
}

function mostrarMensaje(){
    console.log(mensaje)
}

mostrarMensaje()
```

Este ejemplo va a dar un error, porque estamos declarando la variable `mensaje` dentro de la función `init()`, y estamos tratando de acceder a la variable en la función `mostrarMensaje()`. La variable `mensaje` *vive* unicamente dentro de `init()`, y no existe en ningún otro lado, solo se puede acceder desde la función en la que fue declarada.

Sin embargo, si hacemos lo siguiente:

```javascript
function init(){
    let mensaje = 'Aprendiendo Javascript'
    
    function mostrarMensaje(){
        console.log(mensaje)
    }

    mostrarMensaje()
}

init()
```

La función `mostrarMensaje()` puede acceder a la variable `mensaje`, porque ambos *viven* dentro de la misma funcion `init()`

✅ Podes probar de modificar este código cambiando de lugar las cosas y agregando mas funciones y variables para entender mejor que está pasando.

### Actividad:
{: .no_toc }

Debajo de las declaraciones de elementos en `script.js`, vamos a definir la función `arrastrarElemento`:

```javascript
function arrastrarElemento(element) {
    //Declaramos 4 variables para manejar la posición de cada elemento en la pantalla.
    let pos1 = 0,
        pos2 = 0,
        pos3 = 0,
        pos4 = 0;
    element.onpointerdown = arrastrarPuntero;
}
```

`arrastrarElemento` recibe un objeto `element` de las declaraciones en la parte superior del script. Luego, establece algunas posiciones locales en "0" para el objeto pasado a la función. Estas son las variables locales que se manipularán para cada elemento a medida que agregás la funcionalidad de arrastrar y soltar dentro del closure de cada elemento. El layout estará poblado por estos elementos arrastrados, por lo que la aplicación debe hacer seguimiento de dónde se colocan.

Además, al `element` que se pasa a esta función se le asigna un evento `onpointerdown`, que forma parte de las [API web](https://developer.mozilla.org/es/docs/Web/API){:target="_blank"} diseñadas para ayudar con la gestión del DOM. `onpointerdown` se dispara cuando se presiona un botón, o en nuestro caso, se toca un elemento que se puede arrastrar. Este controlador de eventos funciona tanto en [navegadores web como móviles](https://caniuse.com/?search=pointerdown){:target="_blank"}, con algunas excepciones.

✅ El [controlador de eventos `onclick`](https://developer.mozilla.org/es/docs/conflicting/Web/API/Element/click_event){:target="_blank"} tiene mucho más soporte entre navegadores; ¿Por qué no lo usarías acá? Pensá en el tipo exacto de interacción de pantalla que estás intentando crear acá.

---

# La función arrastrarPuntero

El element está listo para ser arrastrado; cuando se dispara el evento `onpointerdown`, se invoca la función `arrastrarPuntero`. Agregá esa función justo debajo de esta línea: `element.onpointerdown = arrastrarPuntero;`:

### Actividad:
{: .no_toc }

```javascript
function arrastrarPuntero(e) {
    e.preventDefault();
    console.log(e);
    pos3 = e.clientX;
    pos4 = e.clientY;
}
```

Suceden varias cosas. Primero, evitamos que ocurran los eventos predeterminados que normalmente ocurren cuando se presiona el puntero usando `e.preventDefault ();`. De esta manera, tenés más control sobre el comportamiento de la interfaz.

✅ Regresá a esta línea cuando hayas construido el archivo de script por completo y pruébelo sin `e.preventDefault ()`- ¿qué sucede?

En segundo lugar, abrí `index.html` en una ventana del navegador e inspeccioná la interfaz. Cuando hacés clic en un elemento, podés ver cómo se captura el evento 'e'. ¡Profundizá en el evento para ver cuánta información recopila un evento de puntero hacia abajo!

A continuación, observá cómo las variables locales `pos3` y` pos4` se establecen en `e.clientX`. Podés encontrar los valores de `e` en el panel de inspección. Estos valores capturan las coordenadas x e y del elemento en el momento en que hacés clic en él o lo tocás. Necesitarás un control detallado sobre el comportamiento de los elementos al hacer clic en ellos y arrastrarlos, de modo que puedas realizar un seguimiento de sus coordenadas.

✅ ¿Está cada vez más claro por qué toda esta aplicación está construida con un gran closure? Si no fuera así, ¿cómo mantendrías el alcance para cada uno de los elementos arrastrables?

Completá la función inicial agregando dos manipulaciones de eventos de puntero más despues de `pos4 = e.clientY`:

```javascript
document.onpointermove = iniciarArrastreElemento;
document.onpointerup = pararArrastreElemento;
```

Ahora estás indicando que deseás que el elemento se arrastre junto con el puntero mientras lo movés, y que el gesto de arrastre se detenga cuando anulás la selección del elemento. `onpointermove` y `onpointerup` son partes de la misma API que `onpointerdown`. En este punto la interfaz arrojará errores ya que aún no definiste las funciones `iniciarArrastreElemento` y `pararArrastreElemento`.

Hasta este punto, el archivo script.js debería estar quedando asi:

```javascript
arrastrarElemento(document.getElementById('componente1'));
arrastrarElemento(document.getElementById('componente2'));
arrastrarElemento(document.getElementById('componente3'));
arrastrarElemento(document.getElementById('componente4'));
arrastrarElemento(document.getElementById('componente5'));
arrastrarElemento(document.getElementById('componente6'));
arrastrarElemento(document.getElementById('componente7'));
arrastrarElemento(document.getElementById('componente8'));
arrastrarElemento(document.getElementById('componente9'));
arrastrarElemento(document.getElementById('componente10'));
arrastrarElemento(document.getElementById('componente11'));
arrastrarElemento(document.getElementById('componente12'));
arrastrarElemento(document.getElementById('componente13'));
arrastrarElemento(document.getElementById('componente14'));
arrastrarElemento(document.getElementById('componente15'));
arrastrarElemento(document.getElementById('componente16'));
arrastrarElemento(document.getElementById('producto1'));
arrastrarElemento(document.getElementById('producto2'));
arrastrarElemento(document.getElementById('producto3'));
arrastrarElemento(document.getElementById('producto4'));

function arrastrarElemento(element) {
    //Declaramos 4 variables para manejar la posición de cada elemento en la pantalla.
    let pos1 = 0,
        pos2 = 0,
        pos3 = 0,
        pos4 = 0;
    element.onpointerdown = arrastrarPuntero

    function arrastrarPuntero(e) {
        e.preventDefault();
        console.log(e);
        pos3 = e.clientX;
        pos4 = e.clientY;
        document.onpointermove = iniciarArrastreElemento;
        document.onpointerup = pararArrastreElemento;
    }
}
```

# Las funciones iniciarArrastreElemento y pararArrastreElemento

Completarás tu closure agregando dos funciones internas más que se encargarán de lo que sucede cuando arrastrás un elemento y dejás de arrastrarlo. El comportamiento que deseamos es que puedas arrastrar cualquier elemento en cualquier momento y colocarlo en cualquier lugar de la pantalla. Esta interfaz no tiene opiniones (no hay restricciones sobre donde se pueden colocar las imágenes) para permitirte diseñar tu layout exactamente como quieras agregando, quitando y reposicionando elementos.

### Actividad:
{: .no_toc }

Agregá la función `iniciarArrastreElemento` justo después de la llave de closure de `arrastrarPuntero`:

```javascript
function iniciarArrastreElemento(e) {
    pos1 = pos3 - e.clientX;
    pos2 = pos4 - e.clientY;
    pos3 = e.clientX;
    pos4 = e.clientY;
    console.log(pos1, pos2, pos3, pos4);
    element.style.top = element.offsetTop - pos2 + 'px';
    element.style.left = element.offsetLeft - pos1 + 'px';
}
```

En esta función estamos editando las posiciones iniciales 1-4 que estableciste como variables locales en la función externa `arrastrarElemento()`. ¿Que está pasando acá?

A medida que arrastrás el elemento, reasignás `pos1` haciéndola igual a `pos3` (que configuraste anteriormente como `e.clientX`) menos el valor actual de `e.clientX`. Realizás una operación similar a `pos2`. Luego, restablecés `pos3` y `pos4` a las nuevas coordenadas X e Y del elemento. Podés ver estos cambios en la consola mientras arrastrás. Luego, manipulás el estilo CSS del elemento para establecer su nueva posición en función de las nuevas posiciones de `pos1` y `pos2`, calculando las coordenadas X e Y superior e izquierda del elemento en función de la comparación de su desplazamiento con estas nuevas posiciones.

> `OffsetTop` y `offsetLeft` son propiedades CSS que establecen la posición de un elemento basándose en la de su padre; su padre puede ser cualquier elemento que no esté posicionado como "estático". Para esto necesitábamos que las imágenes estén en un `div` con posición relativa.

Todo este recálculo de posicionamiento te permite afinar el comportamiento del layout y sus elementos.

### Actividad:
{: .no_toc }

Finalmente, para completar la interfaz debemos agregar la función `pararArrastreElemento` después de la llave de closure de `iniciarArrastreElemento`:

```javascript
function pararArrastreElemento() {
    document.onpointerup = null;
    document.onpointermove = null;
}
```

Esta pequeña función restablece los eventos `onpointerup` y `onpointermove` para que puedas reiniciar el progreso de tu elemento comenzando a arrastrarlo nuevamente, o comenzar a arrastrar un nuevo elemento.

✅ ¿Qué sucede si no configurás estos eventos como nulos?

¡Ahora completaste tu proyecto!

El código completo debería quedar asi:

```javascript
arrastrarElemento(document.getElementById('componente1'));
arrastrarElemento(document.getElementById('componente2'));
arrastrarElemento(document.getElementById('componente3'));
arrastrarElemento(document.getElementById('componente4'));
arrastrarElemento(document.getElementById('componente5'));
arrastrarElemento(document.getElementById('componente6'));
arrastrarElemento(document.getElementById('componente7'));
arrastrarElemento(document.getElementById('componente8'));
arrastrarElemento(document.getElementById('componente9'));
arrastrarElemento(document.getElementById('componente10'));
arrastrarElemento(document.getElementById('componente11'));
arrastrarElemento(document.getElementById('componente12'));
arrastrarElemento(document.getElementById('componente13'));
arrastrarElemento(document.getElementById('componente14'));
arrastrarElemento(document.getElementById('componente15'));
arrastrarElemento(document.getElementById('componente16'));
arrastrarElemento(document.getElementById('producto1'));
arrastrarElemento(document.getElementById('producto2'));
arrastrarElemento(document.getElementById('producto3'));
arrastrarElemento(document.getElementById('producto4'));

function arrastrarElemento(element) {
    //Declaramos 4 variables para manejar la posición de cada elemento en la pantalla.
    let pos1 = 0,
        pos2 = 0,
        pos3 = 0,
        pos4 = 0;
    element.onpointerdown = arrastrarPuntero

    function arrastrarPuntero(e) {
        e.preventDefault();
        console.log(e);
        pos3 = e.clientX;
        pos4 = e.clientY;
        document.onpointermove = iniciarArrastreElemento;
        document.onpointerup = pararArrastreElemento;
    }

    function iniciarArrastreElemento(e) {
        pos1 = pos3 - e.clientX;
        pos2 = pos4 - e.clientY;
        pos3 = e.clientX;
        pos4 = e.clientY;
        console.log(pos1, pos2, pos3, pos4);
        element.style.top = element.offsetTop - pos2 + 'px';
        element.style.left = element.offsetLeft - pos1 + 'px';
    }

    function pararArrastreElemento() {
        document.onpointerup = null;
        document.onpointermove = null;
    }
}
```

---

🥇¡Felicitaciones! Terminaste tu interfaz. 

![interfaz terminada](images/interfaz-terminada.png){: width="650" }{: .center-image}


🚀 Desafío: agregá un nuevo controlador de eventos a tu closure para hacer algo más en los elementos; por ejemplo, hacer doble clic en un elementos para traerlo al frente. ¡Sé creativo!


# Revisión y autoestudio

Si bien arrastrar elementos por la pantalla parece trivial, hay muchas formas de hacerlo y muchas trampas, según el efecto que busques. De hecho, hay una [API de arrastrar y soltar](https://developer.mozilla.org/es/docs/Web/API/HTML_Drag_and_Drop_API){:target="_blank"} completa que podés probar. No la usamos en este módulo porque el efecto que queríamos era algo diferente, pero probá esta API en tu propio proyecto y ve lo que podés lograr.


