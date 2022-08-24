---
title: Menú App
has_children: false
nav_order: 8
has_toc: false
---
# Creación de aplicación menú

En esta lección crearemos una aplicación para mostrar el menú de nuestro restaurante, tomando los datos de una planilla de Google Sheets, mediante una API. De esta forma si actualizamos los datos de nuestra planilla, también podremos actualizar los datos de nuestro menú.

Necesitaremos crear tres archivos: uno para nuestro markup: `index.html`, uno para nuestros estilos: `style.css`, y uno para nuestros scripts: `scripts.js`.

```bash
# Linux o macOS
mkdir menu-app && cd menu-app
# Windows
md menu-app && cd menu-app
```

Abrimos el Visual Studio Code, y luego la carpeta menu-app.

Creamos los tres archivos mencionados dentro de la carpeta menu-app.

* index.html
* style.css
* scripts.js

En nuestro html tendremos un título para nuestro menú, y abajo tendremos un div que contendrá todos los productos de nuestro menú. A este div le pondremos el id `lista-menu` de forma a poder utilizarlo luego desde nuestro javascript.

```html
<html>
  <meta charset="UTF-8">
  <head>
    <title>Menú</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <h1>Menú de mi restaurante</h1>
    <div id="lista-menu"></div> <!-- Aquí pondremos nuestros productos -->
    <script src="scripts.js"></script>
  </body>
</html>
```

Podemos observar lo que hemos hecho hasta ahora, abriendo el archivo `index.html` en nuestro navegador. Falta estilo, ¿verdad?

En el archivo styles.css podemos incluirlo, por ejemplo así:

```css
body { /* Aplica a todo el body*/
  background-color: #A6D1E6;
  font-family: 'Roboto', sans-serif;
  color: #3D3C42;
}

h1 {
  text-align: center;
  margin-top: 2rem;
}

.menu-item {
  background-color: #7F5283;
  color: #FEFBF6;
  margin-top: 1rem;
  min-height: 5rem;
  border-radius: 10px;
  max-width: 100%;
  line-height: 3rem;
  border: 1px solid #3D3C42;
  background-image: none; /* esto es necesario para que cuando no se haga hover se vuelva al fondo purpura sólido */
}

.menu-item:hover {
  color: #3D3C42;
  background-image: linear-gradient(90deg, #FBC5C5, #FEFBF6); /* esto es para generar el degradado desde el rosa al blanco,
  el angulo es de 90 grados porque de otro modo el degradado seria de arriba a abajo */
}

.precio {
  float: right;
  margin-right: 1rem;
}

/*
Es importante que esta clase esté después del menu-item por el orden de prioridad de las clases aplicadas
*/
.index-item {
  width: 80px;
  height: 5rem;
  position: relative;
  float: left;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
  background-color: #FBC5C5;
  color: #3D3C42;
}

.producto {
  float: left;
  margin-left: 1rem;
}

/*
Esta clase permite centrar verticalmente los items en el div, tener en cuenta que si aumenta el alto del div contenedor,
el line-height acá también debería aumentar al mismo valor.
*/
.item {
  vertical-align: middle;
  line-height: 5rem; 
}

.indice {
  margin-left: 40px;
}

#lista-menu {
  margin: auto; /* con esto se logra que este centrado horizontalmente */
  width: 60%;
}
```

Notemos que tenemos algunas clases que todavía no están siendo usadas. Las usaremos en nuestro script.

A continuación escribiremos nuestro script para obtener los datos de la API y mostrarlos correctamente. Debemos tener en cuenta que traeremos los datos de una planilla electrónica de Google (Google sheets) y para esto debemos autenticarnos mediante un token de acceso. Este token de acceso se envía en la cabecera `Authorization`. También tendremos que especificar el id de la planilla, que se encuentra en la url de la misma. Esto lo realizamos de la siguiente manera:

```javascript
const SHEET_ID = "1SY8CrCyX_yNpdURlXxWup_pQWJ59X9vnOGlN0yE2aow";

const ACCESS_TOKEN =
  "ya29.A0AVA9y1s92zHK1z5VDfnNOniFq9l-O7zXjcnqjy41IY_SpXw8oI-IBbj8AoD23_n5zZM16R77VtgMQpdD3ypsbIuwzDgWH_l_ZbLNeOtTKX5iHCq2cuh7V-gPC09fV-hAZlJxXUk3Zs2CxGTQuohqWfn6Urj6aCgYKATASATASFQE65dr8y7vf7mUfgGE5UgzcQD8URA0163";

fetch(
  // Obtenemos los datos de la planilla, de la hoja hojaMenu, columnas A y B desde la segunda fila
  `https://sheets.googleapis.com/v4/spreadsheets/${SHEET_ID}/values/hojaMenu!A2:B`,
  {
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${ACCESS_TOKEN}`,
    },
  }
//esperamos el response
)
```

Ahora necesitaremos mostrar los datos que obtuvimos de la API. Para esto agregaremos el siguiente código:

```javascript
.then(function (response) {
  //esperamos el json del response para poder utilizarlo
  response.json().then(function (data) {
    const values = data.values;

    // Obtenemos el elemento del dom
    const lista = document.getElementById("lista-menu");

    for (var i = 0; i < values.length; i++) {

        // Div que va a contener los datos del producto
        const producto = document.createElement("div");
        producto.className =  "menu-item";

        // El número de producto
        const itemIndice = document.createElement("span");
        itemIndice.className = "item indice";
        itemIndice.innerHTML = i + 1;

        // Nombre del producto
        const itemProducto = document.createElement("span");
        itemProducto.className = "item producto";
        itemProducto.innerHTML = values[i][0]; 

        // Precio
        const itemPrecio = document.createElement("span");
        itemPrecio.className = "item precio";
        itemPrecio.innerHTML = values[i][1];

        // Div que contiene el número de producto (itemIndex)
        const divIndice = document.createElement("div");
        divIndice.className = "index-item";
        divIndice.appendChild(itemIndice);

        // Agregamos todos los elementos al div de producto
        producto.appendChild(divIndice);
        producto.appendChild(itemProducto);
        producto.appendChild(itemPrecio);

        // Agregamos el producto a la lista
        lista.appendChild(producto);
     }
  });
});
```

Ahora analicemos la solución:

* Primero esperamos por la respuesta al request hecho mediante fetch.

* Luego esperamos por el JSON que se encuentra en el response. Este JSON tiene la siguiente estructura:

```javascript
{
    "range": "hojaMenu!A2:B1000",
    "majorDimension": "ROWS",
    "values": [
        [
            "Hamburguesa con queso",
            "25000"
        ],
        [
            "Pizza muzzarella",
            "40000"
        ],
        [
            "Coca cola zero",
            "8000"
        ],
        [
            "Sprite zero",
            "8000"
        ]
    ]
}
```

* Creamos una variable llamada `values` a la cual le asignaremos el array contenido en el JSON del response.

* Obtenemos el elemento cuyo id es `lista-menu` en la variable `lista`, dentro del cual pondremos los demás elementos que corresponden a los productos del menú.

* Mediante el `for`, iteramos sobre los valores de la variable `values`.

* Para cada uno de estos productos, creamos un elemento div con el className `menu-item` en la variable `producto`. Este div contendrá todos los datos del producto en cuestión.

* Usamos la variable `itemIndice` para crear un elemento span con las clases `item` e `indice` que contiene el número de producto del menú.

* Usamos la variable `itemProducto` para crear un elemento span con las clases `item` y `producto` que contiene el nombre del producto.

* La variable `itemPrecio` con las clases `item` y `precio` para crear otro elemento span que contiene el precio del producto.

* La variable `divIndice` con la clase `index-item` que contendrá el elemento `itemIndice` que creamos previamente.

* Luego agregaremos estos elementos a nuestro elemento `producto` que creamos inicialmente.

* Y por último, agregamos el producto en cuestión a nuestro elemento lista.

# Desafío

Reemplazar los elementos del menú por los personajes de star wars de obtenidos de la API, mediante la url (https://swapi.dev/api/people/) sin autenticación. Mostrar nombre (atributo name) y estatura (atributo height).

# Lectura complementaria

Si querés saber más sobre API's REST, te recomendamos [esta lectura](https://docs.microsoft.com/es-es/azure/architecture/best-practices/api-design){:target="_blank"}

# Tarea

Citar y describir brevemente cuáles son los métodos HTTP más utilizados en API’s REST.

## Rúbrica

| Criterios | Ejemplar | Adecuado | Necesita mejorar |
| -------- | --------------------------------------------- | ------------------------------------------------ | ----------------------- |
| | Se citan y explican los métodos correctamente | Se citan los métodos pero no se explican | No se presentan los métodos |
