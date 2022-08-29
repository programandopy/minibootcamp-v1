---
title: Grilla
has_children: false
parent: Conceptos avanzados
nav_order: 2
---

# Grilla o Matriz

En esta sección vamos a introducir un nuevo concepto que es el de creación de grillas mediante CSS.
Una grilla, también llamada matriz, es una colección de líneas horizontales (filas) y líneas verticales (columnas).

Hasta ahora hemos visto lo que es un array, el cual se trata de una estructura unidimencional. Una grilla se trata de una estructura bidimencional; es decir, tiene dos dimensiones.

![matriz](images/matriz.jpeg)


# Grilla en CSS

CSS noss provee de 2 módulos que contienen todas las funciones necesarias para armar grillas, que son [CSS Grid Layout](https://developer.mozilla.org/es/docs/Web/CSS/CSS_Grid_Layout){:target="_blank"} y [CSS Flexbox](https://developer.mozilla.org/es/docs/Web/CSS/CSS_Flexible_Box_Layout){:target="_blank"}.


Nosotros vamos a ver CSS Flexbox. Como siempre, te instamos a que no te limites a la información proveída acá, sino que investigues por tu cuenta y veas cuál módulo que sienta mejor.

# CSS Flexbox

CSS Flexbox es un módulo CSS en el que se define un modelo de caja optimizado para el diseño de interfaces de usuario. Una **interfaz de usuario** es el medio por el cual el usuario interactúa con nuestra página web, aplicación, etc. Por ejemplo, el layout que definimos en clases pasadas es una interfaz de usuario.

En Flexbox (como normalmente se lo conoce) los nodos hijo se pueden distribuir en dirección vertical u horizontal y se puede "flexibilizar" sus tamaños, bien sea rellenando el espacio disponible o encogiéndose para evitar salirse del contorno del nodo padre. También se puede manipular fácilmente tanto la alineación horizontal como la vertical, de los nodos hijo.

Flexbox cuenta con varias propiedades propias que nos ayudan a ubicar los elementos. Veamos un ejemplo sencillo.

## Elementos en una fila

Si por ejemplo tenemos 3 elementos que queremos posicionar uno al lado del otro haríamos lo siguiente. Primero crearíamos nuestro archivo HTML y dento lo siguiente:

```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>
<section class="box">
  <div>Uno</div>
  <div>Dos</div>
  <div>Tres</div>
</section>
</body>
</html>
```

Hasta ahora siempre vimos que el CSS va en un archivo a parte, es posible también incluir CSS directo en el tag `style` de nuestro HTML. Utilizaremos esta aproximación ya que nuestro HTML es pequeño y sencillo.

```html
<style>
.box {
  display: flex;
}
div {
  border: 1px #000 solid;
  width: 200px;
  height: 200px;
}
</style>
```

Si abrimos este html vamos a ver que los elementos se ven como cajas y una al lado de la otra:

![una fila](images/una-fila.png)

Como se puede ser, los elementos se encuentran alineados uno al lado del otro. ¿Qué pasa si no queremos que se apilen todos a la izquierda? Acá entra en juego una propiedad de Flexbox que es `justify-content` que lo vemos a continuación

## Distribución de ítems

La propiedad `justify-content` distribuye el espacio entre y alrededor de los ítems. Puede tener distintos valores:

```css
/* Alinear items flex desde el comienzo */
justify-content: flex-start;

/* Alinear items desde el final */
justify-content: flex-end;

/* Alinear items en el centro */
justify-content: center;

/* Distribuir items uniformemente
El primer item al inicio, el último al final */
justify-content: space-between;

/* Distribuir items uniformemente
Los items tienen el mismo espacio a su alrededor */
justify-content: space-around;
```

✅ Probá cambiar la distribución de los ítems en tu html anterior y ve las diferencias entre todas las opciones.


## Dos dimensiones

Si a nuestro HTML anterior seguimos agregando elementos, éstos se alinean todos en la misma fila. Si queremos que se distribuyan en más de una fila es necesario agregar una nueva propiedad al contenedor de lo divs.

La propiedad `flex-wrap` le indica a los hijos de un nodo si deben permanecer en una misma línea o puede "fluir" en más líneas. Por defecto el valor de esta propiedad es `no-wrap` que es la que hace que se pongan todos los hijos en una misma línea. Para que se alineen en más de una fila el valor debe ser `wrap`.

```css
flex-wrap: wrap;
```

Si cambiás el tamaño de tu navegador vas a notar que la cantidad de hijos por fila se ajusta a medida cambia el tamaño de su contendor. ¿Y si queremos que haya una cantidad fija de ítems por fila? Pues necesitamos de otra propiedad.

## Fijar cantidad de ítems por fila




