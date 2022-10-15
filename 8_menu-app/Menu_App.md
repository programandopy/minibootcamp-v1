---
title: Menú App
has_children: false
nav_order: 9
has_toc: true
---
# Desarrollo de un menu virtual

En esta lección crearemos una aplicación para mostrar el menú de nuestro restaurante, tomando los datos de una planilla de Google Sheets, mediante una API. De esta forma si actualizamos los datos de nuestra planilla, también podremos actualizar los datos de nuestro menú.

## API

Una API, interfaz de programación de aplicaciones por sus siglas en inglés, es una forma de comunicar dos o más programas informáticos. Normalmente las API’s web ofrecen un conjunto de *endpoints* a través de los cuales las aplicaciones web pueden interactuar con ella. Se denomina cliente a la aplicación que realiza solicitudes al servidor donde se encuentra la API. El servidor a su vez, envía respuestas a las solicitudes hechas por el cliente.

## Google sheets

Google sheets es una aplicación para manejo de hojas de cálculo (similar a Excel). Una hoja de cálculo es un tipo de documento que permite manipular datos que se encuentran dispuestos en celdas, que se organizan en filas y columnas. Google sheets además nos ofrece una API web para interactuar con los datos de nuestras hojas de cálculo.

### Actividad:
{: .no_toc }

La idea de este proyecto es que nuestra pagina web obtenga los datos a mostrar desde la planilla de google sheets.

Para ello, entra a tu google drive y crea una hoja de calculo nueva llamada `menu-ppy`.

![nueva-planilla](images/nueva-planilla.gif)

Una vez que la planilla este creada, vamos a renombrar la hoja a `almuerzo`.

![renombrar-hoja](images/renombrar-hoja.gif)

Ambos nombres pueden ser cualquier cosa, pero recorda ser consistente y cambiar los nombres en el código mas adelante. También trata de que todos los nombres estén en minúsculas y sin espacios.

Luego, vamos a cargar la planilla con algunos datos de prueba. Podes poner los datos que quieras, pero es importante que las columnas sean el titulo, la descripción y el precio del producto.

Deberias tener algo asi:

![planilla](images/planilla.png)

---

## Configurando la API

Ahora que tenemos la planilla lista, necesitamos configurar el mecanismo que vamos a utilizar para poder conectarnos desde nuestra pagina y extraer datos.

Para ello tendremos que compartir la planilla para que cualquiera con el link la pueda ver, y ademas tendremos que configurar un token de acceso para que google nos deje acceder desde nuestra app.

Un token de acceso es un conjunto de caracteres que nos permiten verificar nuestra identidad ante una API, de forma a verificar que tengamos los permisos correspondientes para realizar las acciones que estamos solicitando.

Las cabeceras o *headers* permiten al cliente y al servidor enviar información adicional con una solicitud o respuesta. Para nuestro ejemplo, enviaremos nuestro token en la cabecera *Authorization*

URL significa Localizador de Recursos Uniforme por sus siglas en inglés, y es una dirección para un recurso único en la Web. Tendremos que especificar el id de la planilla, que se encuentra en la URL de la misma.

### Actividad:
{: .no_toc }

Lo primero que tenemos que hacer es compartir nuestra planilla:

![compartir](images/compartir.gif)

Ahora, si miramos la direccion web de la planilla en el navegador, vamos a ver algo asi: `https://docs.google.com/spreadsheets/d/1rkd10iPZ4S3ijGlVjr1BPeVn3IW63Jn2FM4DyXBjH7k/edit#gid=0`

Tenemos que copiar y guardar el codigo que se encuentra en esta direccion. En el caso del ejemplo, es `1rkd10iPZ4S3ijGlVjr1BPeVn3IW63Jn2FM4DyXBjH7k`. En tu planilla va a ser distinto.

Este codigo es el ID (identificador unico) de tu planilla, y lo vamos a utilizar para pedirle a google los datos. El ID siempre esta entre las barras: `.../ ID /...`:

![id-planilla](images/id-planilla.gif)

Perfecto, ahora tenemos que generar nuestro `token`. Para esto, vamos a utilizar una herramienta de google. Hace click en el botón para ir a la pagina:

{: .fs-6 .fw-300 }
[OAuth 2.0 Playground](https://developers.google.com/oauthplayground/){: .btn .btn-blue-cird .fs-5 .mb-4 .mb-md-0 .mr-2 }

Una vez ahi, la herramienta nos pide que sigamos tres pasos.

Primero, le vamos a decir que es lo que queremos hacer. En la lista de opciones que vemos, vamos a buscar y seleccionar `Google Sheets API v4`. Al seleccionar se abren una lista de opciones, y debemos hacer clic en la opción que termina en `auth/spreadsheets`. Hacemos click en `Authorize APIs` y le damos permiso:

![step1](images/step1.gif)

En el siguiente paso, tenemos que hacer clic en el botón `Exchange authorization code for tokens`. Esto nos genera un `Access token` en el campo de abajo. Este código también debemos copiarlo y guardarlo en algún lado, ya que sera necesario para conectarnos.

Finalmente, podemos pasar al paso 3 (Step 3). En este paso, solo queda probar la conexión y ver si todo esta funcionando.

Aca nos interesan dos campos que deberías estar viendo en la pantalla. El campo HTTP Method debe estar en GET, este es el tipo de petición que vamos a hacer, y al usar GET, estamos diciendo que queremos obtener datos de algún lugar.

Por ultimo, en el campo Request URI tenemos que pegar lo siguiente: `https://sheets.googleapis.com/v4/spreadsheets/${SHEET_ID}/values/almuerzo!A2:C`, pero en vez de `${SHEET_ID}`, tenes que poner el ID de tu planilla (lo vimos mas arriba).

El deberías pegar algo asi: `https://sheets.googleapis.com/v4/spreadsheets/1rkd10iPZ4S3ijGlVjr1BPeVn3IW63Jn2FM4DyXBjH7k/values/almuerzo!A2:C`

Presiona el boton azul que dice `Send the request`.

Si hiciste todo bien, deberias ver algo asi en la seccion que dice **Request / Response**:

```js
GET /v4/spreadsheets/1rkd10iPZ4S3ijGlVjr1BPeVn3IW63Jn2FM4DyXBjH7k/values/almuerzo!A2:C HTTP/1.1
Host: sheets.googleapis.com
Content-length: 0
Authorization: Bearer ya29.a0Aa4xrXPHhHKqIh4yQDevr8TwspPZ4UnhooYiPAdr41d1cL1lbDqJxps-q3OkJP7pHanFvwfew-erYRG_8avRyIrMhJ_8X5nZMqKuPo0-CtrDSIhDfKB96Bsg4R0hpjQW5FhiHeLm8-WRfNF61djDGQTMgXHnaCgYKATASARASFQEjDvL9pgfmTXav6PptYf7Eob6T6w0163

HTTP/1.1 200 OK
Content-length: 384
X-xss-protection: 0
Content-location: https://sheets.googleapis.com/v4/spreadsheets/1rkd10iPZ4S3ijGlVjr1BPeVn3IW63Jn2FM4DyXBjH7k/values/almuerzo!A2:C
X-content-type-options: nosniff
Transfer-encoding: chunked
Vary: Origin, X-Origin, Referer
Server: ESF
-content-encoding: gzip
Cache-control: private
Date: Sat, 15 Oct 2022 04:03:19 GMT
X-frame-options: SAMEORIGIN
Alt-svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000,h3-Q050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"
Content-type: application/json; charset=UTF-8
{
  "range": "almuerzo!A2:C1000", 
  "values": [
    [
      "Pollo al horno", 
      "Texto descriptivo", 
      "20000"
    ], 
    [
      "Tallarines", 
      "Texto descriptivo", 
      "15000"
    ], 
    [
      "Hamburguesa", 
      "Texto descriptivo", 
      "15000"
    ], 
    [
      "Pizza Grande", 
      "Texto descriptivo", 
      "40000"
    ]
  ], 
  "majorDimension": "ROWS"
}
```

Funciona! ya tenemos lo que se llama "una API expuesta", a la que cualquier persona le puede pedir datos.

El resumen que ves en la parte derecha de la pantalla tiene dos partes.

La primera sección, la que empieza con **GET**, es la petición. Es lo que le enviamos a google para pedirle los datos, y básicamente le dice que estamos pidiendo y quienes somos.

La segunda sección, que empieza con **HTTP/1.1**, es la respuesta. Es todo lo que nos responde la API, y al final podemos ver que nos devuelve los datos que solicitamos.

Ahora que nuestra API ya funciona, podemos tratar de obtener los datos usando javascript.

## Estructura de archivos

Necesitaremos crear tres archivos: uno para nuestro markup: `index.html`, uno para nuestros estilos: `style.css`, y uno para nuestros scripts: `scripts.js`.

Primero vamos a crear la carpeta `menu-app` que contendrá estos archivos.

Abrimos el Visual Studio Code, y luego la carpeta `menu-app`.

Creamos los tres archivos mencionados dentro de la carpeta `menu-app`.

* index.html
* style.css
* scripts.js

## HTML

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

## CSS

En el archivo styles.css podemos incluirlo, por ejemplo así:

```css
body { /* Aplica a todo el body*/
    background-color: #ffe6d1;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    color: #3D3C42;
}

h1 {
    text-align: center;
    margin-top: 2rem;
}

.menu-item {
    margin-top: 1%;
    height: 2rem;
    border-radius: 10px;
    max-width: 100%;
    background-image: none;
}

.menu-item:hover {
    color: #3D3C42;
    background-color: #c19a79a5;
}

.precio {
    float: right;
    margin-right: 3%;
    }

.producto {
    float: left;
    margin-left: 3%;
}

/*
Esta clase permite centrar verticalmente los items en el div, tener en cuenta que si aumenta el alto del div contenedor,
el line-height acá también debería aumentar al mismo valor.
*/
.item {
    vertical-align: middle;
    line-height: 2rem; 
}

#lista-menu {
    margin: auto; /* con esto se logra que este centrado horizontalmente */
    width: 70%;
    font-size: 17px;
    font-weight: 600;
}
```

Notemos que tenemos algunas clases que todavía no están siendo usadas. Las usaremos en nuestro script.

## Javascript

A continuación escribiremos nuestro script para obtener los datos de la API y mostrarlos correctamente. Debemos tener en cuenta que traeremos los datos de una planilla electrónica de Google (Google sheets) y para esto debemos autenticarnos mediante un token de acceso.

Un token de acceso es un conjunto de caracteres que nos permiten verificar nuestra identidad ante una API, de forma a verificar que tengamos los permisos correspondientes para realizar las acciones que estamos solicitando.

Las cabeceras o *headers* permiten al cliente y al servidor enviar información adicional con una solicitud o respuesta. Para nuestro ejemplo, enviaremos nuestro token en la cabecera *Authorization*

URL significa Localizador de Recursos Uniforme por sus siglas en inglés, y es una direccion para un recurso único en la Web. Tendremos que especificar el id de la planilla, que se encuentra en la URL de la misma.

Para poder obtener los datos de nuestra hoja de cálculo, utilizaremos la función `fetch` que nos provee javascript. Fetch es una función que nos ofrece una forma sencilla de realizar solicitudes de forma asíncrona.

```javascript
const SHEET_ID = "1rkd10iPZ4S3ijGlVjr1BPeVn3IW63Jn2FM4DyXBjH7k";

const ACCESS_TOKEN =
  "ya29.A0AVA9y1s92zHK1z5VDfnNOniFq9l-O7zXjcnqjy41IY_SpXw8oI-IBbj8AoD23_n5zZM16R77VtgMQpdD3ypsbIuwzDgWH_l_ZbLNeOtTKX5iHCq2cuh7V-gPC09fV-hAZlJxXUk3Zs2CxGTQuohqWfn6Urj6aCgYKATASATASFQE65dr8y7vf7mUfgGE5UgzcQD8URA0163";

fetch(
  // Obtenemos los datos de la planilla, de la hoja hojaMenu, columnas A y B desde la segunda fila
  `https://sheets.googleapis.com/v4/spreadsheets/${SHEET_ID}/values/almuerzo!A2:C`,
  {
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${ACCESS_TOKEN}`,
    },
  }
//esperamos el response
)
```

Ahora necesitaremos mostrar los datos que obtuvimos de la API. Notemos que la respuesta se encuentra en formato JSON. JSON (acrónimo de JavaScript Object Notation, 'notación de objeto de JavaScript') es un formato de texto sencillo para el intercambio de datos. Normalmente en este el formato que se utiliza para comunicar datos entre el cliente y el servidor.

Finalmente agregaremos el siguiente código para mostrar los datos obtenidos de la API:

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

        // Nombre del producto
        const itemProducto = document.createElement("span");
        itemProducto.className = "item producto";
        itemProducto.innerHTML = values[i][0]; 

        // Precio
        const itemPrecio = document.createElement("span");
        itemPrecio.className = "item precio";
        itemPrecio.innerHTML = values[i][2];

        // Agregamos todos los elementos al div de producto
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
            "Texto descriptivo",
            "25000"
        ],
        [
            "Pizza muzzarella",
            "Texto descriptivo",
            "40000"
        ],
        [
            "Coca cola zero",
            "Texto descriptivo",
            "8000"
        ],
        [
            "Sprite zero",
            "Texto descriptivo",
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

---

# Desafío

Reemplazar los elementos del menú por los personajes de star wars de obtenidos de la API, mediante la url (https://swapi.dev/api/people/) sin autenticación. Mostrar nombre (atributo name) y estatura (atributo height).

---

# Lectura complementaria

Si querés saber más sobre API's REST, te recomendamos [esta lectura](https://docs.microsoft.com/es-es/azure/architecture/best-practices/api-design){:target="_blank"}

---

# Tarea

Agregar una columna al sheet del cual se obtienen los datos (por ejemplo si es dulce o salado) y mostrarla en la interfaz gráfica.

## Rúbrica

| Criterios | Ejemplar | Adecuado | Necesita mejorar |
| -------- | --------------------------------------------- | ------------------------------------------------ | ----------------------- |
| | Se muestra el dato nuevo correctamente | Se obtiene correctamente el nuevo dato pero no se muestra | No se muestra el nuevo dato|
