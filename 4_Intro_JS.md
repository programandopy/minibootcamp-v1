---
title: Introducción a JavaScript
has_children: false
nav_order: 5
---

# Introducción:

Manipular el DOM, o el "Modelo de objetos de documento" (Document Object Model en inglés), es un aspecto clave del desarrollo web. Según [MDN](https://developer.mozilla.org/es/docs/Web/API/Document_Object_Model/Introduction){:target="_blank"}, "El modelo de objetos de documento (DOM) es la representación de datos de los objetos que componen la estructura y contenido de un documento en la web ". Los desafíos en torno a la manipulación de DOM en la web a menudo han sido el ímpetu detrás del uso de frameworks de JavaScript en lugar de JavaScript puro para administrar el DOM, ¡pero lo administraremos por nuestra cuenta!

Además, esta lección presentará la idea de un [closure JavaScript](https://developer.mozilla.org/es/docs/Web/JavaScript/Closures){:target="_blank"}, que puedes considerar como una función encerrada por otra función para que la función interna tenga acceso al alcance de la función externa.

Usaremos un closure para manipular el DOM.

Piensa en el DOM como un árbol, que representa todas las formas en que se puede manipular un documento de página web. Se han escrito varias API (interfaces de programas de aplicación) para que los programadores, utilizando el lenguaje de programación de su elección, puedan acceder al DOM y editarlo, cambiarlo, reorganizarlo y administrarlo de otro modo.

![representación de HTML](/assets/images/dom-tree.png)


En esta lección, completaremos nuestro proyecto de plaza interactiva creando el JavaScript que permitirá al usuario manipular los componentes en la página.

# Requisito previo:

Deberías tener el HTML y CSS para tu plaza construido. Al final de esta lección, podrás mover lo componentes dentro y fuera de la plaza arrastrándolos.

# Tarea:

En tu carpeta de la plaza, crea un nuevo archivo llamado `script.js`. Importa ese archivo en la sección `<head>`:


```html
	<script src="./script.js" defer></script>
```

> Nota: usa `defer` cuando importes un archivo JavaScript externo en el archivo html para permitir que JavaScript se ejecute sólo después de que el archivo HTML se haya cargado por completo. También podrías usar el atributo `async`, que permite que el script se ejecute mientras se analiza el archivo HTML, pero en nuestro caso, es importante tener los elementos HTML completamente disponibles para arrastrar antes de permitir que se ejecute el script de arrastre.

---

## 1. Los elementos DOM

Lo primero que debes hacer es crear referencias a los componentes que deseas manipular en el DOM. En nuestro caso, son los 18 elementos o componentes que esperan actualmente en las barras laterales.


# Tarea:

```html
dragElement(document.getElementById('plaza1'));
dragElement(document.getElementById('plaza2'));
dragElement(document.getElementById('plaza3'));
dragElement(document.getElementById('plaza4'));
dragElement(document.getElementById('plaza5'));
dragElement(document.getElementById('plaza6'));
dragElement(document.getElementById('plaza7'));
dragElement(document.getElementById('plaza8'));
dragElement(document.getElementById('plaza9'));
dragElement(document.getElementById('plaza10'));
dragElement(document.getElementById('plaza11'));
dragElement(document.getElementById('plaza12'));
dragElement(document.getElementById('plaza13'));
dragElement(document.getElementById('plaza14'));
dragElement(document.getElementById('plaza15'));
dragElement(document.getElementById('plaza16'));
dragElement(document.getElementById('plaza17'));
dragElement(document.getElementById('plaza18'));
```

¿Que está pasando aquí? Estás haciendo referencia al documento y mirando a través de su DOM para encontrar un elemento con un Id particular. ¿Recuerdas en la primera lección sobre HTML que le diste ID individuales a cada imagen de la plaza (`id = "planza1"`)? Ahora harás uso de eso. Después de identificar cada elemento, pasa ese elemento a una función llamada `dragElement` que crearás en un minuto. Por lo tanto, el elemento en el HTML ahora está habilitado para arrastrar, o lo estará en breve.

✅ ¿Por qué hacemos referencia a elementos por Id? ¿Por qué no por su clase de CSS? Puedes consultar la lección anterior sobre CSS para responder a esta pregunta.

---

## 2. El closure

Ahora estás listo para crear el closure dragElement, que es una función externa que encierra una función o funciones internas (en nuestro caso, tendremos tres).

Los closures son útiles cuando una o más funciones necesitan acceder al alcance de una función externa. He aquí un ejemplo:

```javascript
function mostrarCaramelo(){
	let caramelos = ['jellybeans'];
	function agregarCaramelo(tipoCaramelo) {
		caramelo.push(tipoCaramelo)
	}
	agregarCaramelo('gomitas');
}
mostrarCaramelo();
console.log(caramelos)
```

En este ejemplo, la función mostrarCaramelo rodea una función que inserta un nuevo tipo de caramelo en una lista que ya existe en la función. Si tuvieras que ejecutar este código, la lista `caramelos` no estaría definida, ya que es una variable local (local al closure).

✅ ¿Cómo se puede hacer accesible la lista de `caramelos`? Intenta moverlo fuera del closure. De esta manera, la lista se vuelve global, en lugar de permanecer sólo disponible para el alcance local del closure.

# Tarea:

Debajo de las declaraciones de elementos en `script.js`, crea una función:


```javascript
function dragElement(elementoDePlaza) {
	//establecer 4 posiciones para posicionar en la pantalla
	let pos1 = 0,
		pos2 = 0,
		pos3 = 0,
		pos4 = 0;
	elementoDePlaza.onpointerdown = arrastrarPuntero;
}
```

`dragElement` obtiene su objeto `elementoDePlaza` de las declaraciones en la parte superior del script. Luego, establece algunas posiciones locales en "0" para el objeto pasado a la función. Estas son las variables locales que se manipularán para cada elemento a medida que agregass la funcionalidad de arrastrar y soltar dentro del closure de cada elemento. La plaza estará poblada por estos elementos arrastrados, por lo que la aplicación debe realizar un seguimiento de dónde se colocan.

Además, al elementoDePlaza que se pasa a esta función se le asigna un evento `pointerdown`, que forma parte de las [API web](https://developer.mozilla.org/es/docs/Web/API){:target="_blank"} diseñadas para ayudar con la gestión del DOM. `Onpointerdown` se dispara cuando se presiona un botón, o en nuestro caso, se toca un elemento que se puede arrastrar. Este controlador de eventos funciona tanto en [navegadores web como móviles](https://caniuse.com/?search=onpointerdown){:target="_blank"}, con algunas excepciones.

✅ El [controlador de eventos `onclick`](https://developer.mozilla.org/es/docs/conflicting/Web/API/Element/click_event){:target="_blank"} tiene mucho más soporte entre navegadores; ¿Por qué no lo usarías aquí? Piensa en el tipo exacto de interacción de pantalla que estás intentando crear aquí.

---

## 3. La función arrastrarPuntero

El elementoDePlaza está listo para ser arrastrado; cuando se dispara el evento `onpointerdown`, se invoca la función `arrastrarPuntero`. Agrega esa función justo debajo de esta línea: `elementoDePlaza.onpointerdown = arrastrarPuntero;`:

# Tarea: 

```javascript
function arrastrarPuntero(e) {
	e.preventDefault();
	console.log(e);
	pos3 = e.clientX;
	pos4 = e.clientY;
}
```

Suceden varias cosas. Primero, evita que ocurran los eventos predeterminados que normalmente ocurren en el evento onpointerdown usando `e.preventDefault ();`. De esta manera, tienes más control sobre el comportamiento de la interfaz.

> Regresa a esta línea cuando hayas construido el archivo de script por completo y pruébelo sin `e.preventDefault ()`- ¿qué sucede?

En segundo lugar, abre `index.html` en una ventana del navegador e inspecciona la interfaz. Cuando haces clic en un componente, puedes ver cómo se captura el evento 'e'. ¡Profundiza en el evento para ver cuánta información recopila un evento onpointerdown!

A continuación, observa cómo las variables locales `pos3` y` pos4` se establecen en e.clientX. Puedes encontrar los valores de `e` en el panel de inspección. Estos valores capturan las coordenadas x e y del componente en el momento en que haces clic en él o lo tocas. Necesitarás un control detallado sobre el comportamiento de los componentes al hacer clic en ellos y arrastrarlos, de modo que puedas realizar un seguimiento de sus coordenadas.

✅ ¿Está cada vez más claro por qué toda esta aplicación está construida con un gran closure? Si no fuera así, ¿cómo mantendrías el alcance para cada una de los 18 componentes arrastrables?

Completa la función inicial agregando dos manipulaciones de eventos de puntero más en `pos4 = e.clientY`:

```html
document.onpointermove = arrastrarElemento;
document.onpointerup = detenerArrastreElemento;
```
Ahora estás indicando que deseas que el componente se arrastre junto con el puntero mientras lo mueves, y que el gesto de arrastre se detenga cuando anules la selección del componente. `Onpointermove` y `onpointerup` son partes de la misma API que `onpointerdown`. La interfaz arrojará errores ahora ya que aún no has definido las funciones `arrastrarElemento` y `detenerArrastreElemento`, así que constrúyelas a continuación.

## 4. Las funciones arrastrarElemento y detenerArrastreElemento

Completarás tu closure agregando dos funciones internas más que se encargarán de lo que sucede cuando arrastras un componente y dejas de arrastrarlo. El comportamiento que deseas es que puedas arrastrar cualquier componente en cualquier momento y colocarlo en cualquier lugar de la pantalla. Esta interfaz no tiene opiniones (no hay zona de caída, por ejemplo) para permitirte diseñar tu plaza exactamente como te gusta agregando, quitando y reposicionando componentes.

# Tarea:

Agrega la función `arrastrarElemento` justo después del corchete de cierre de `arrastrarPuntero`:

```javascript
function arrastrarElemento(e) {
	pos1 = pos3 - e.clientX;
	pos2 = pos4 - e.clientY;
	pos3 = e.clientX;
	pos4 = e.clientY;
	console.log(pos1, pos2, pos3, pos4);
	elementoDePlaza.style.top = elementoDePlaza.offsetTop - pos2 + 'px';
	elementoDePlaza.style.left = elementoDePlaza.offsetLeft - pos1 + 'px';
}
```
En esta función, editas mucho las posiciones iniciales 1-4 que estableces como variables locales en la función externa. ¿Que está pasando aquí?

A medida que arrastras, reasignas `pos1` haciéndolo igual a `pos3` (que configuraste anteriormente como `e.clientX`) menos el valor actual de `e.clientX`. Realiza una operación similar a `pos2`. Luego, restablece `pos3` y `pos4` a las nuevas coordenadas X e Y del componente. Puedes ver estos cambios en la consola mientras arrastras. Luego, manipula el estilo CSS del componente para establecer su nueva posición en función de las nuevas posiciones de `pos1` y` pos2`, calculando las coordenadas X e Y superior e izquierda del componente en función de la comparación de su desplazamiento con estas nuevas posiciones.


> `OffsetTop` y `offsetLeft` son propiedades CSS que establecen la posición de un elemento basándose en la de su padre; su padre puede ser cualquier elemento que no esté posicionado como "estático".

Todo este recálculo de posicionamiento te permite afinar el comportamiento de la plaza y sus componentes.

# Tarea:

La tarea final para completar la interfaz es agregar la función `closeElementDrag` después del corchete de cierre de `arrastrarElemento`:

```javascript
function detenerArrastreElemento() {
	document.onpointerup = null;
	document.onpointermove = null;
}
```

Esta pequeña función restablece los eventos `onpointerup` y `onpointermove` para que puedas reiniciar el progreso de tu componente comenzando a arrastrarlo nuevamente, o comenzar a arrastrar un nuevo componente.


✅ ¿Qué sucede si no configura estos eventos como nulos?

¡Ahora has completo tu proyecto!

---

🥇¡Felicitaciones! Has terminado tu hermosa plaza. ![plaza terminada](/assets/images/mi-plaza-final.png)

🚀Desafío: agrega un nuevo controlador de eventos a tu closure para hacer algo más en los componentes; por ejemplo, haz doble clic en un componente para traerlo al frente. ¡Sé creativa!

# Revisión y autoestudio

Si bien arrastrar elementos por la pantalla parece trivial, hay muchas formas de hacerlo y muchas trampas, según el efecto que buscas. De hecho, hay una [API de arrastrar y soltar](https://developer.mozilla.org/es/docs/Web/API/HTML_Drag_and_Drop_API){:target="_blank"} completa que puedes probar. No lo usamos en este módulo porque el efecto que queríamos era algo diferente, pero prueba esta API en tu propio proyecto y ve lo que puedes lograr.

# Tarea - Trabaja un poco más con DOM

Investiga el DOM un poco más 'adoptando' un elemento DOM. Visita la [lista de interfaces DOM de MDN](https://developer.mozilla.org/es/docs/Web/API/Document_Object_Model){:target="_blank"} y elije uno. Encuéntralo en un sitio web en la web y escribe una explicación de cómo se usa.

## Rúbrica

| Criterios | Ejemplar | Adecuado | Necesita mejorar |
| -------- | --------------------------------------------- | ------------------------------------------------ | ----------------------- |
| | Se presenta la redacción del párrafo, con ejemplo | Se presenta la redacción del párrafo, sin ejemplo | No se presenta ninguna reseña |

