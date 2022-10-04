---
title: Creemos un juego
has_children: false
parent: Eventos en JavaScript
nav_order: 2
---

# Programemos un juego

Ahora vamos a crear un juego para entender mejor cómo funcionan los eventos en **JavaScript**. El juego a programar se trata de poner a prueba la habilidad de escritura de un jugador, que es una de las habilidades más practicadas por todos los desarrolladores. El flujo general del juego sería así:

- El jugador hace clic en el botón de inicio y se le presenta un texto de ejemplo para escribir.
- El jugador escribe el texto lo más rápido posible en un cuadro de texto.
   - A medida que se completa cada palabra, se resalta la siguiente a escribir.
   - Si el jugador tiene un error de escritura, el cuadro de texto se actualiza resaltándolo en rojo para indicar que algo no va bien.
   - Cuando el jugador completa la totalidad de las palabras del texto, se muestra un mensaje de éxito mostrando también el tiempo total que le tomó el completar el desafío.

**TIP:**
Utilizá las habilidades de JavaScript, HTML y CSS que aprendimos hasta ahora para crear este juego y tené en cuenta los siguientes conceptos:

- Crear entradas de texto y botones.
- CSS y estilos por clases.
- JavaScript básico.
   - Creación de array.
   - Crear números de manera aleatoria (random).
   - Obtener la hora actual.


¡Ahora programemos el juego y aprendamos sobre los eventos!

---

# Nuestros Archivos

Vamos a necesitar crear tres archivos en total: **index.html**, **script.js** y **style.css**. Empecemos por crear y organizar nuestra **estructura de archivos** para que el resto sea un poco más fácil.


- Creamos una nueva carpeta para nuestro proyecto abriendo la consola o la terminal y escribimos el siguiente comando:

```bash
# Linux o macOS
mkdir typingGame && cd typingGame
# Windows
md typingGame && cd typingGame
```


- Abrimos el Visual Studio Code:

```bash
code .
```

- Creamos tres nuevos archivos en la carpeta desde Visual Studio Code con los siguientes nombres:
  - index.html
  - script.js
  - style.css

---

# Creemos la interfaz de usuario
Como ya vimos en los requsitos que definimos para nuestro programa, vamos a necesitar varios componetes para nuestro HTML. A continuación te mostramos una pequeña guía para que lo construyas:

- Un bloque donde mostrar el texto que el usuario debe escribir.
- Un bloque donde mostrar nuestros mensajes de alerta, como los mensajes de error o de éxito.
- Un cuadro de texto para escribir.
- Un botón para iniciar el juego.

Estas secciones necesitarán que les asignemos un "ID" para que podamos trabajar con ellos de forma individual en nuestro JavaScript. También debemos agregar referencias a los archivos CSS y JavaScript que vamos a crear para que nuestro HTML sepa donde encontrarlos.

Ahora creamos un nuevo archivo con el nombre **index.html** y agregamos el siguiente código HTML:

```html
<!-- nuestro index.html -->
<html>
<head>
  <title>Typing game</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Nuestro Typing game!</h1>
  <p>Practique sus habilidades de tipeo con este texto de ejmplo de Sherlock Holmes. Haga Click en  **inicio** para empezar!</p>
  <p id="quote"></p> <!-- En este bloque mostramos el texto de ejemplo -->
  <p id="message"></p> <!-- En este bloque mostramos los mensajes del juego -->
  <div>
    <input type="text" aria-label="palabra actual" id="texto-tipeado" /> <!-- el componente textbox para ingresar el texto -->
    <button type="button" id="inicio">Inicio</button> <!-- Botón para iniciar el juego -->
  </div>
  <script src="script.js"></script>
</body>
</html>
```

---
# Probemos nuestro programa
Es una buena práctica probar nuestro código a medida que lo desarrollamos para ver como van las cosas, entonces iniciemos nuestra aplicación y utilizamos la extensión de Visual Studio Code llamada [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer){:target="_blank"} que alojará la aplicación localmente y actualizará el navegador cada vez que guardemos nuestro código permitiéndonos ver el restultado de nuestros cambios.


- Instalamos, si es que aún no lo tenemos instalado, [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer){:target="_blank"} siguiendo el enlace y haciendo clic en **Instalar**
   - Reiniciá Visual Studio Code si es que así lo solicita.
- Una vez instalado, en Visual Studio Code, hacemos clic en Ctrl+Shift+P (o Cmd+Shift+P en MacOS) para abrir el área de comandos.
- Escribí **Live Server: Abrir con Live Server**
   - Live Server comenzará a alojar su aplicación.
- Abrimos el navegador y escribimos la dirección **https://localhost:5500**
- ¡Ahora ya podemos ver la página que creamos!.

Ahora empieza lo divertivo, vamos a agregar más funcionalidad a nuestro juego.

---
# Agreguemos algo de estilo con CSS
Sobre nuestro HTML creado, ahora agreguemos el CSS para dar el estilo principal a nuestro código. Para que todo sea más claro necesitamos resaltar la palabra que el jugador debe escribir y colorear el cuadro de texto si lo que escribió es incorrecto. Para hacer esto vamos a utilizar dos clases dentro de nuestro CSS.

Empezamos crando un nuevo archivo llamado **style.css** y agregamos el siguiente código:

```css
/* dentro de estilo.css */
.destacar {
   background-color: amarillo;
}
.error {
   background-color: coral claro;
   border-color: rojo;
}
```

✅ **TIP**: Cuando se trata de CSS, podemos diseñar la página como más nos guste. Es aquí donde nos tomamos el tiempo para diseñar lo que querramos mostrar y hacer que la página se vea más atractiva, teniendo en cuenta por ejemplo:

- Eligir un tipo fuente diferente.
- Colores para los encabezados.
- Cambiar el tamaño de los elementos.

---
# Es hora de JavaScript

Con nuestra interfaz de usuario creada, es hora de centrar nuestra atención en el JavaScript para proporcionar la lógica de nuestro juego. Vamos a dividir esto en varios pasos:

- [Crear las constantes](../5_javascript/1_DataTypes.html#constantes)
- [Event Listener para iniciar el juego](#como-iniciar-el-juego)
- [Event Listener para escribir](#control-del-juego)

Pero primero, creemos un nuevo archivo llamado **script.js**.

---
# Agreguemos las constantes

Vamos a necesitar algunos elementos para hacernos la vida un poco más fácil para la programación. Nuevamente, similar a una receta, esto es lo que necesitaremos:

- Matriz con la lista de todas los textos de ejemplo a tipear.
- Matriz vacía para almacenar todas las palabras del texto actual.
- Espacio para almacenar el índice de la palabra que el jugador está escribiendo actualmente.
- El momento en que el jugador hizo clic en iniciar.

También vamos a querer referencias a los elementos de la interfaz de usuario:

- El cuadro de texto (**valor escrito**)
- La pantalla de cotización (**texto de ejemplo**)
- El mensaje (**mensaje**)


```javascript
// dentro del script.js
// todas nuestros textos de ejemplo
const textos = [
    'When you have eliminated the impossible, whatever remains, however improbable, must be the truth.',
    'There is nothing more deceptive than an obvious fact.',
    'I ought to know by this time that when a fact appears to be opposed to a long train of deductions it invariably proves to be capable of bearing some other interpretation.',
    'I never make exceptions. An exception disproves the rule.',
    'What one man can invent another can discover.',
    'Nothing clears up a case so much as stating it to another person.',
    'Education never ends, Watson. It is a series of lessons, with the greatest for the last.',
];
// almacena la lista de palabras y el índice de la palabra que el jugador está escribiendo actualmente
let palabras = [];
let palabraIndice = 0;
// la hora de inicio
let startTime = Date.now();
// elementos de la pagina
const textoElemento = document.getElementById('textos');
const mensajeElemento = document.getElementById('mensaje');
const typedValorElemento = document.getElementById('typed-value');
```

✅ Continúa y agrega más textos a tu juego

> **NOTA:** Podemos recuperar los elementos cuando queramos en el código usando `document.getElementById`. Debido al hecho de que nos referiremos a estos elementos de manera regular, evitaremos errores tipográficos con cadenas literales mediante el uso de constantes. Los marcos como [Vue.js](https://vuejs.org/){:target="_blank"} o [React](https://reactjs.org/){:target="_blank"} pueden ayudarlo a administrar mejor la centralización de su código.
Tómese un minuto para ver un video sobre el uso de `const`, `let` y `var`


---
# Agreguemos la lógica del juego
## Como iniciar el juego
Para comenzar el juego, el jugador hará clic en el inicio. Por supuesto, no sabemos cuándo van a hacer clic en Inicio. Aquí es donde entra en juego un Event Listener, ya que nos permitirá escuchar algo que ocurra (un evento) y ejecutar código como respuesta. En nuestro caso, queremos ejecutar código cuando el usuario haga clic en Inicio.

Cuando el usuario hace clic en Inicio, necesitamos elegir un texto de ejemplo para mostrar, configurar la interfaz de usuario y configurar el seguimiento de la palabra y el tiempo actuales para saber la duración del juego. A continuación te mostramos el JavaScript que necesitás agregar.

```javascript

// en el final de nuestro archivo script.js
document.getElementById('start').addEventListener('click', () => {
  // elegimos el texto de ejemplo a mostrar
  const textoIndice = Math.floor(Math.random() * quotes.length);
  const texto = texto[textoIndice];
  // separamos el texto en un array de palabras
  palabras = texto.split(' ');
  // reestablemos el idice de palabras para el seguimiento
  palabraIndice = 0;

  // Actualizamos la interfaz de usuario
  // Creamos una matriz con los elementos span de nuestro HTML para poder definirles una class
  const spanPalabras = palabras.map(function(palabra) { return `<span>${palabra} </span>`});
  // Convertimos a string y lo definimos como innerHTML en el texto de ejemplo a mostrar
  textoElement.innerHTML = spanPalabras.join('');
  // Resaltamos la primer palabra
  textoElement.childNodes[0].className = 'highlight';
  // Borramos los mensajes previos
  messageElement.innerText = '';

  // Definimos el elemento textbox
  // Vaciamos el elemento textbox
  typedValueElement.value = '';
  // Definimos el foco en el elemento
  typedValueElement.focus();
  // Establecemos el manejador de eventos

  // Iniciamos el contador de tiempo
  startTime = new Date().getTime();
});
```

¡Analicemos el código!

- Configurar el seguimiento de las palabras
  - Usando [Math.floor](https://developer.mozilla.org/docs/web/javascript/reference/global_objects/math/floor){:target="_blank"} y [math.random](https://developer.mozilla.org/docs /Web/javascript/reference/global_objects/math/random){:target="_blank"} nos permite seleccionar aleatoriamente una cotización de la matriz "texto"
  - Convertimos el "texto" en una matriz de "palabras" para que podamos rastrear la palabra que el reproductor está escribiendo actualmente
  - "palabraIndice" se establece en 0, ya que el reproductor comenzará con la primera palabra
- Configurar la interfaz de usuario
  - Cree una matriz de "spanwords", que contiene cada palabra dentro de un elemento "span"
    - Esto nos permitirá resaltar la palabra en la pantalla
  - "join" la matriz para crear una cadena que podemos usar para actualizar el "innerhtml" en "textoElement"
    - Esto mostrará la cita al jugador
  - Establezca el "className" del primer elemento "span" en "highlight" para resaltarlo como amarillo
  - Limpie el "MessageElement" configurando "inteText" a '"'
- Configurar el cuadro de texto
  - Borre el "valor" actual en "typedValueElement"
  - Establezca el "Focus" en "typedValueElement"
- Comience el temporizador llamando a "gettime"

## Control del juego
A medida que el jugador escribe, se estará realizando un evento de entrada. Entonces nuestro Event Listener verificará este evento para asegurarse de que el se esté escribiendo la palabra correctamente y manejar el estado actual del juego. Volviendo a script.js, agregamos el siguiente código al final.

```javascript
// al final de nuestro archivo script.js
typedValueElement.addEventListener('input', () => {
  // tomamos la palabra actual
  const currentWord = words[wordIndex];
  // tomamos el valor actual
  const typedValue = typedValueElement.value;
  if (typedValue === currentWord && wordIndex === words.length - 1) {
    // fin de la sentencia
    // Definimos el mensaje de éxito
    const elapsedTime = new Date().getTime() - startTime;
    const message = `FELICITACIONES! Finalizaste en ${elapsedTime / 1000} segundos.`;
    messageElement.innerText = message;
  } else if (typedValue.endsWith(' ') && typedValue.trim() === currentWord) {
    // fin de la palabra
    // vaciamos el valor typedValueElement para la siguiente palabra
    typedValueElement.value = '';
    // movemos a la palabra siguiente
    palabraIndicea++;
    // reiniciamos el estado de todas las clases para los textos
    for (const palabraElement of textoElement.childNodes) {
      palabraElement.className = '';
    }
    // resaltamos la palabra actual
    quoteElement.childNodes[wordIndex].className = 'highlight';
  } else if (currentWord.startsWith(typedValue)) {
    // correcta actual
    // resaltar la siguiente palabra
    typedValueElement.className = '';
  } else {
    // estado error
    typedValueElement.className = 'error';
  }
});
```

¡Analicemos el código! Comenzamos agarrando la palabra actual y el valor que el jugador ha escrito hasta ahora. Luego tenemos una lógica de cascada, donde verificamos si la cotización está completa, la palabra está completa, la palabra es correcta o (finalmente), si hay un error.

- La cita se completa, indicada por "typedValue" igual a "currentword", y "wordIndex" es igual a uno menos que la "length" de "palabras"
  - Calcule "elapsedTime" restando "starttime" desde la hora actual
  - Divide "elapsedTime" por 1,000 para convertir de milisegundos a segundos
  - Muestra un mensaje de éxito
- La palabra se completa, indicada por "typedvalue" que termina con un espacio (el final de una palabra) y "typedvalue" igual a "currentword"
  - Establecer "value" en "typedElement" para ser '""' para permitir que se escriba la siguiente palabra
  - Incrementar "WordIndex" para moverse a la siguiente palabra
  - Reunir todos los "bidnodes" de "quoteElement" para establecer "classname" a '""' para volver a la pantalla predeterminada
  - Establecer "className" de la palabra actual en "highlight" para marcarlo como la siguiente palabra para escribir
- La palabra se escribe correctamente (pero no completa), indicado por "currentword" iniciado con "typedValue"
  - Asegúrese de que "typedValueElement" se muestre como predeterminado al borrar "className"
- Si llegamos tan lejos, tenemos un error
  - Establecer "classname" en "typedValueElement" en "error".


## Probemos el código
¡Lo logramos! El último paso es garantizar que nuestra aplicación funcione es ejecutar y probarlo. A jugar y a no preocuparse si hay errores; **Todos los desarrolladores** tienen errores. Examinemos los mensajes y la depuración según sea necesario.

Hagamos clic en **Iniciar** y comienza a escribir! Debería parecerse un poco a la animación que se muestra a continuación.

![Animación del juego en acción](images/demo-typing-game.gif)

🚀 Desafío: agregar más funcionalidad

- Deshabilitá el "Input" Event Listener al finalizar y vuelva a habilitarlo cuando se haga clic en el botón
- Deshabilitá el cuadro de texto cuando el reproductor complete el texto de ejemplo
- Mostrá un cuadro de diálogo modal con el mensaje de éxito
- Almacená puntajes altos usando [LocalStorage](https://developer.mozilla.org/docs/web/api/window/localstorage){:target="_blank"}

# Revisión y autoestudio

También podés leer [todos los eventos disponibles](https://developer.mozilla.org/docs/web/events){:target="_blank"} para que como desarrollador puedas usar a través del navegador web, e imaginá los escenarios en los que usarías cada uno.

## Tarea - Creá un nuevo juego con los eventos de teclado reusando lo aprendido

### Instrucciones
Creá un juego pequeño que use eventos de teclado similar al que acabamos de realizar, para esta ocación el desafío es dearrollar el juego conocido como "ahorcado" donde el participante debe adivinar una palabra determinda contando con tan solo 5 oportunidades más que la cantidad de letras que contenga la palabra. ¡Sé creativo!
Para más referencias respecto a la lógica del juego podés consultar en el siguiente [link](https://es.wikipedia.org/wiki/Ahorcado_(juego)){:target="_blank"}.

### Rúbrica

| Criterios | Ejemplar | Adecuado | Necesita mejorar |
| -------- | -------------------------------------------------- ------------------------------------ | -------------------------------------------------- -------------- | ----------------- |
| | La solución presentada es completa y funciona correctamente | La solución presentada es mínimo y funciona correctamente | La solución tiene errores |


