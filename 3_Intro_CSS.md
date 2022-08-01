---
title: Introducción a CSS
has_children: false
nav_order: 4
---
# Introducción:

CSS, o Cascading Style Sheets, resuelve un problema importante del desarrollo web: cómo hacer que tu sitio web se vea bien. Diseñar tus aplicaciones las hace más útiles y atractivas. También puedes usar CSS para crear un diseño web receptivo (RWD), lo que permite que tus aplicaciones se vean bien sin importar en qué tamaño de pantalla se muestren. CSS no se trata sólo de hacer que tu aplicación se vea bien; su especificación incluye animaciones y transformaciones que pueden permitir interacciones sofisticadas para tus aplicaciones. El grupo de trabajo CSS ayuda a mantener las especificaciones CSS actuales; puedes seguir su trabajo en el [sitio del World Wide Web Consortium](http://es.tz8.de/style-css-members.html){:target="_blank"}.

> Ten en cuenta que CSS es un lenguaje que evoluciona, como todo en la web, y no todos los navegadores admiten partes más nuevas de la especificación. Siempre verifica tus implementaciones consultando [CanIUse.com](https://caniuse.com){:target="_blank"}.

En esta lección, agregaremos estilos a nuestra plaza en línea y aprenderemos más sobre varios conceptos de CSS: la cascada, la herencia y el uso de selectores, posicionamiento y uso de CSS para crear diseños. En el proceso, diseñaremos la plaza y crearemos la plaza en sí.

# Requisito previo:

Deberías tener el HTML para tu plaza construido y listo para darle estilo.

# Tarea:

En tu carpeta de plaza, crea un nuevo archivo llamado `style.css`. Importa ese archivo en la sección `<head>`:

```
<link rel="stylesheet" href="./style.css" />
```

---

## 1. La cascada

Las hojas de estilo en cascada incorporan la idea de que los estilos 'se mueven en cascada' de manera que la aplicación de un estilo está guiada por su prioridad. Los estilos establecidos por el autor de un sitio web tienen prioridad sobre los establecidos por un navegador. Los estilos configurados 'en línea' tienen prioridad sobre los configurados en una hoja de estilo externa.

# Tarea:

Agrega el estilo en línea "color: red" a tu etiqueta `<h1>`:

```HTML
<h1 style="color: red">Mi plaza</h1>
```

Luego, agrega el siguiente código a tu archivo `style.css`:

```CSS
h1 {
 color: blue;
}
```

✅ ¿Qué color se muestra en tu aplicación web? ¿Por qué? ¿Puedes encontrar una forma de anular estilos? ¿Cuándo querrías hacer esto o por qué no?

---

## 2. Herencia

Los estilos se heredan de un estilo antepasado a un estilo descendiente, de modo que los elementos anidados heredan los estilos de sus padres.

# Tarea:

Establece la fuente del cuerpo en una fuente determinada y verifica para ver la fuente de un elemento anidado:

```
body {
	font-family: helvetica, arial, sans-serif;
}
```

Abre la consola de tu navegador en la pestaña 'Elementos' y observa la fuente H1. Hereda su fuente del cuerpo, como se indica en el navegador:

![fuente heredada](/assets/images/body-font.png){:target="_blank"}

✅ ¿Puedes hacer que un estilo anidado herede una propiedad diferente?

---

## 3. Selectores CSS

# Etiquetas

Hasta ahora, tu archivo `style.css` tiene solo algunas etiquetas con estilo, y la aplicación se ve bastante extraña:

```
body {
	font-family: helvetica, arial, sans-serif;
}

h1 {
	color: #3a241d;
	text-align: center;
}
```

Esta forma de diseñar una etiqueta te da control sobre elementos únicos, pero necesitas controlar los estilos de muchos elementos en tu plaza. Para hacer eso, necesitas aprovechar los selectores de CSS.

# ID

Agrega un poco de estilo para diseñar los contenedores izquierdo y derecho. Dado que solo hay un contenedor izquierdo y solo un contenedor derecho, se les dan identificadores en el marcado. Para diseñarlos, usa `#`:

```
#contenedor-izquierdo {
	background-color: #eee;
	width: 15%;
	left: 0px;
	top: 0px;
	position: absolute;
	padding: 10px;
}

#contenedor-derecho {
	background-color: #eee;
	width: 15%;
	right: 0px;
	top: 0px;
	position: absolute;
	padding: 10px;
}
```

Aquí, has colocado estos contenedores con posicionamiento absoluto en el extremo izquierdo y derecho de la pantalla, y has utilizado porcentajes para su ancho para que puedan escalar para pantallas móviles pequeñas.

✅ Este código se repite bastante, por lo tanto, no "DRY" (Don't Repeat yourself: No se repita); ¿Puede encontrar una mejor manera de diseñar estos identificadores, tal vez con un id y una clase? Necesitarías cambiar el marcado y refactorizar el CSS:

```html
<div id="contenedor-izquierdo" class="contenedor"></div>
```

# Clases

En el ejemplo anterior, diseñaste dos elementos únicos en la pantalla. Si deseas que los estilos se apliquen a muchos elementos en la pantalla, puedes usar clases CSS. Has esto para colocar los elementos en los contenedores izquierdo y derecho.

Observa que cada elemento en el marcado HTML tiene una combinación de identificadores y clases. Los identificadores aquí son utilizados por JavaScript que agregarás más adelante para manipular la ubicación de los elementos en la plaza. Las clases, sin embargo, dan a todos lo elementos un estilo determinado.

```html
<div class="contenedor-componente">
	<img class="componente" alt="componente" id="plaza1" src="./images/plaza_1.png" />
</div>
```

Agrega lo siguiente a tu archivo `style.css`:

```css
.contenedor-componente {
	position: relative;
	height: 10.5%;
	left: 20%;
}

.componente {
	position: absolute;
	max-width: 150%;
	max-height: 150%;
	z-index: 2;
}
```

Echa un vistazo a la forma en que se manejan las alturas por porcentajes:

Establece la altura del contenedor-componente en 10.5%, un buen número para garantizar que todos los elementos de la plaza se muestren en cada contenedor vertical sin necesidad de desplazarse.

Configura el contenedor-componente para que se mueva hacia la derecha para permitir que los elementos estén más centrados dentro de su contenedor. Esto se logra con `left`, acá lo que hacemos es agregar un espacio del 20% dele ancho del contenedor a la izquierda, esto hace los elementos se desplacen más al centro de sus contenedores.	

Luego, al componente en sí se le asigna un ancho máximo del 150%. Esto permite que se reduzca a medida que el navegador se reduce. Intenta cambiar el tamaño de tu navegador; los elementos permanecen en sus contenedores pero se reducen para adaptarse.

También es notable el uso del índice z, que controla la altitud relativa de un elemento (de modo que los elementos se sientan en la parte superior del contenedor y parezcan "sentarse" dentro de la plaza).

✅ ¿Por qué se necesita tanto un contenedor-componente para los elementos como un selector CSS de componentes?

## 4. Posicionamiento CSS

Mezclar propiedades de posición (hay posiciones estáticas, relativas, fijas, absolutas y pegajosas) puede ser un poco complicado, pero cuando se hace correctamente, te da un buen control sobre los elementos de tus páginas.

Los elementos de posición absoluta se colocan en relación con sus antepasados ​​colocados más cercanos y, si no hay ninguno, se colocan de acuerdo con el cuerpo del documento.

Los elementos de posición relativa se colocan según las direcciones del CSS para ajustar su ubicación lejos de su posición inicial.

En nuestra muestra, el "contenedor-componente" es un elemento de posición relativa que se coloca dentro de un contenedor de posición absoluta. El comportamiento resultante es que los contenedores de las barras laterales se sujetan a izquierda y derecha, y el contenedor de elementos se encaja, ajustándose dentro de las barras laterales, dando espacio para que los elementos de la plaza se coloquen en una fila vertical.

> El `componente` en sí también tiene un posicionamiento absoluto, necesario para que sea arrastrable, como descubrirás en la siguiente lección.

✅ Experimenta cambiando los tipos de colocación de los contenedores laterales y el portaplantas. ¿Qué pasa?

## 5. Diseños CSS

Ahora usarás lo que aprendiste para construir el espacio para la plaza en sí, ¡todo usando CSS!

Primero, diseña los elementos secundarios `.plazita` div como un rectángulo redondeado usando CSS:

```css
.cielo {
	height: 80%;
	width: 60%;
	background: #BDE6F1;
	border-radius: 1rem;
	position: absolute;
	bottom: 0.5%;
	left: 20%;
	opacity: 0.5;
	z-index: 1;
}

.suelo {
	width: 60%;
	height: 45%;
	background: #C9E4C5;
	position: absolute;
	border-radius: 0 0 1rem 1rem;
	bottom: 1%;
	left: 20%;
	opacity: 0.7;
	z-index: -1;
}
```

Ten en cuenta el uso de porcentajes aquí. Si reduces la escala de tu navegador, también puedes ver cómo se escalan las esquinas de la plaza. Observa también los porcentajes de ancho y alto del cielo y el suelo, y como están absolutamente posicionados en el centro, fijado a la parte inferior de la ventana gráfica (viewport).

✅ Intenta cambiar los colores y la opacidad. ¿Qué pasa?

---

![plaza terminada](/assets/images/mi-plaza-terminada.png){:target="_blank"}


# Revisión y autoestudio

CSS parece engañosamente sencillo, pero existen muchos desafíos cuando se trata de diseñar una aplicación perfectamente para todos los navegadores y todos los tamaños de pantalla. CSS-Grid y Flexbox son herramientas que se han desarrollado para hacer el trabajo un poco más estructurado y más confiable. Aprende sobre estas herramientas jugando a [Flexbox Froggy](https://flexboxfroggy.com/#es){:target="_blank"} y [Grid Garden](https://codepip.com/games/grid-garden/){:target="_blank"}.

Lectura adicional: [Diseña tu aplicación HTML con CSS](https://docs.microsoft.com/es-mx/learn/modules/build-simple-website/4-css-basics?WT.mc_id=academic-13441-cxa){:target="_blank"}

## Tarea - Refactorización CSS
Cambia el estilo de la plaza usando Flexbox o CSS Grid, y toma capturas de pantalla para mostrar que lo probaste en varios navegadores. Es posible que debas cambiar el marcado, así que crea una nueva versión de la aplicación para su refactorización. No te preocupes por hacer que los elementos se puedan arrastrar; solo refactoriza el HTML y CSS por ahora.

### Rúbrica

| Criterios | Ejemplar                                                         | Adecuada                      | Necesita mejorar                    |
| -------- | ----------------------------------------------------------------- | ----------------------------- | ------------------------------------ |
|          | Presenta una plaza completamente rediseñada usando Flexbox o CSS Grid | Modificó algunos de los elementos | No cambió el estilo de la plaza en absoluto |




