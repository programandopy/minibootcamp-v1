---
title: Dinamismo
has_children: false
parent: Conceptos avanzados
nav_order: 1
---

# Dinamismo

Hasta ahora hemos creado todos los elementos HTML directo en el HTML, pero ¿qué pasa si no sabemos cuántos elementos vamos a tener, o si queremos cambiar la cantidad de elementos haciendo la menor cantidad posible de cambios en el código? Para estos casos utilizaremos el concepto de creación dinámica de elementos.

Crear los elementos mediante JavaScript puede ser más complejo pero es mucho más **potente, dinámico y flexible**.

---

# Crear elementos HTML

Para crear elementos HTML, JavaScript proporciona una serie de métodos; el que vamos a utilizar es el [createElement](https://developer.mozilla.org/es/docs/Web/API/Document/createElement){:target="_blank"}. Recibe como primer parámetro el tipo del elemento o nodo a crear, y como segundo parámetro (el cual es opcional) un objeto; este segundo parámetro se utiliza para cuando queremos definir elementos personalizados. En esta clase y en las siguientes no vamos a hacer uso de este segundo parámetro.

Algunos ejemplos sencillos:

```javascript
const div = document.createElement("div"); // Retorna <div></div>
const img = document.createElement("img"); // Retorna <img />
const span = document.createElement("span"); // Retorna <span></span>
```

## Elementos en memoria

Hay que tener en cuenta que al momento de crear estos elementos no los vas a poder ver aún en tu HTML, esto es debido a que todavía no fueron insertados en ninguna posición en el DOM. Es decir, estos elementos solamente son accesibles mediante las variables que las contienen, viven en memoria, **todavía**.

---

# Insertar un elemento en el DOM

Una vez creado un elemento, es necesario posicionarlo en algún lugar del DOM, para ello nos valemos del método [appendChild](https://developer.mozilla.org/es/docs/Web/API/Node/appendChild){:target="_blank"}.

Por ejemplo, si tenemos un `div` con ID `div1` ya existente en nuestro HTML al que deseamos agregar el `<img />` creado en el ejemplo anterior lo haríamos de la siguiente manera:

```javascript
const div = document.getElementById("div1");
div.appendChild(img);
```

✅ Probá en la consola de tu navegador crear varios elementos y agregarlos. Si tu elemento padre ya tiene "hijos", ¿dónde se agregan lo nuevos recién creados?

## Ventajas por sobre HTML estático

Como mencionamos en la introducción, esta manera de crear los elementos HTML nos proporciona dinamismo por sobre los elementos estáticos directo en el HTML. Esto es importante porque nos permmite modificar fácilmente la cantidad de elementos a ser mostrados sin necesidad el tocar el código HTML.

Cuando veamos la clase de [API](https://aws.amazon.com/es/what-is/api/){:target="_blank"}, en la cual vamos a tener un pequeño servidor que nos provea de información, se nos va a hacer más evidente la ventaja de tener de esta manera nuestro código.
