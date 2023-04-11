---
title: Creemos un juego
has_children: false
parent: Eventos en JavaScript
nav_order: 2
---

# Programemos un juego

Ahora vamos a crear un juego para entender mejor cómo funcionan los eventos en **JavaScript**. Y para eso vamos a basarnos en el clásico juego del "TA TE TI" (conocido en inglés como Tic Tac Toe), donde nuestro mayor desafío es el manejar las interaccioens de los jugadores con el tablero. El flujo general del juego sería así:

- El jugador hace clic en el botón de inicio y se carga el tablero de tres casillas por tres casillas vacío.
- El primer juegador inicia seleccionando una casilla para poner su ficha, en este caso representada por una X.
- El segundo jugador continúa la partida colocando su ficha en el tablero, en este caso representada por un O.
   - A medida que se completa el tablero cada jugador debe buscar formar una línea de tres de sus fichas alineadas de forma vertical, horizonta o diagonal.
   - Si algún jugador jugador logra alinear sus fichas se declara ganador y finaliza el juego.
   - En caso que ninguno de los jugadores logre alinear sus fichas y todas las posiciones del tablero sean ocupadas el juego se declara en empate.

**TIP:**
Utilizá las habilidades de JavaScript, HTML y CSS que aprendimos hasta ahora para crear este juego y tené en cuenta los siguientes conceptos:

- Crear botones y sus acciones.
- CSS y estilos por clases.
- JavaScript básico.
   - Creación de array.
   - Obtener el resultado actual.


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
Como ya vimos en los requsitos que definimos para nuestro programa, vamos nuestro HTML para dar forma a nuestro tablero conformando de esta manera nuestra interfaz de usuario. Para este caso nuestra interfaz es muy sencilla y se compone de un tablero de 3 celdas por 3 celdas que podemos resumir de la siguiente manera :

- Un bloque donde mostrar un títutlo para el juego.
- Un bloque donde dibujar nuestro tablero.
    - Una celda para cada posición del tablero.
- Un botón para iniciar el juego.

Estas secciones necesitarán que les asignemos tanto un identificador único como uno de clase para que podamos trabajar luego con ellos de forma en nuestro JavaScript y también poder manipular sus propiedades desde nuestro CSS. También es aquí dónde debemos agregar las referencias a los archivos CSS y JavaScript que vamos a crear para que nuestro HTML sepa donde encontrarlos.

Ahora creamos un nuevo archivo con el nombre **index.html** y agregamos el siguiente código HTML:

```html
<!-- nuestro index.html -->
<!DOCTYPE html>
<html>
  <head>
    <title>Ta Te Ti</title>
    <link rel="stylesheet" href="./style.css">
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css2?family=Itim&display=swap" rel="stylesheet">
  </head>
  <body>
    <h1>Juguemos Ta Te Ti</h1>
    <div id="board">
      <div class="cells"></div>
      <div class="cells"></div>
      <div class="cells"></div>
      <div class="cells"></div>
      <div class="cells"></div>
      <div class="cells"></div>
      <div class="cells"></div>
      <div class="cells"></div>
      <div class="cells"></div>
    </div>
    <script src="./script.js"></script>
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

Ahora seguimos con nuetro juego, vamos a agregar más funcionalidad a nuestro juego.

---
# Agreguemos algo de estilo con CSS
Sobre nuestro HTML creado, ahora agreguemos el CSS para dar el estilo principal a nuestro código. 
Como ya mencionamos todo nuestro juego se basa en posicionar fichas en nuestro tablero, por eso es aquí donde vamos a dar forma a nuestro espacio de juego resaltando nuestro tablero a través de nuestro CSS. Para que todo sea más claro categorizamos nuestro código HTML dividiéndolo en dos partes, por un laod el board (tablero en inglés), que identidicamos con un ID y por otro las celdas (cells en inglés) que identificamos con una clase cada uno con sus respectivas propiedades.

Empezamos crando un nuevo archivo llamado **style.css** y agregamos el siguiente código:

```css
/* dentro de estilo.css */
#board {
  display: flex;
  flex-wrap: wrap;
  width: 300px;
  height: 300px;
}

.cells {
  width: 30%;
  height: 100px;
  border: 1px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 60px;
  cursor: pointer;
}
```

✅ **TIP**: Cuando se trata de CSS, podemos diseñar la página como más nos guste. Es aquí donde nos tomamos el tiempo para diseñar lo que querramos mostrar y hacer que la página se vea más atractiva, teniendo en cuenta por ejemplo:

- Eligir un tipo fuente diferente.
- Colores para los encabezados.
- Cambiar el tamaño de los elementos.
- Poner color a los bordes o fondos del tablero.

---
# Es hora de JavaScript

Con nuestra interfaz de usuario creada, es hora de centrar nuestra atención en el JavaScript para proporcionar la lógica de nuestro juego. Vamos a dividir esto en varios pasos:

- [Crear nuestra constante](../5_javascript/1_DataTypes.html#constantes)
- [Event Listener para iniciar el juego](#como-iniciar-el-juego)
- [Event Listener para jugar](#control-del-juego)

Pero primero, creemos un nuevo archivo llamado **script.js**.

---
# Agreguemos las constantes

Vamos a necesitar algunos elementos para hacernos la vida un poco más fácil para la programación. Nuevamente, similar a una receta, esto es lo que necesitaremos:

- Matriz con las celdas que conforman nuestro tablero.
- Espacio para almacenar las combinaciones de posiciones ganadoras en nuestro tablero.

Con eso podemos iniciar nuestro código JavaScript.


```javascript
// dentro del script.js
const cells = document.querySelectorAll(".cells");
const winConditions = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ];
```


> **NOTA:** Podemos recuperar los elementos cuando queramos en el código usando `document.getElementById`, o con `document.querySelectorAll` para referir a un grupo de elementos tratados como objetos. Debido al hecho de que nos referiremos a estos elementos de manera regular, evitaremos errores tipográficos con cadenas literales mediante el uso de constantes. Los marcos como [Vue.js](https://vuejs.org/){:target="_blank"} o [React](https://reactjs.org/){:target="_blank"} pueden ayudarlo a administrar mejor la centralización de su código.
Tómese un minuto para ver un video sobre el uso de `const`, `let` y `var`


---
# Agreguemos la lógica del juego
## Control del juego
A medida que el jugador posiciona una de sus fichas, se estará realizando un evento de entrada. Entonces nuestro Event Listener verificará este evento para asegurarse de que movimiento no signifique una victoria o empate y así manejar el estado actual del juego pasando el turno al siguiente jugador. Volviendo a script.js, agregamos el siguiente código al final.

```javascript
// al final de nuestro archivo script.js
let currentPlayer = "X";
let gameEnd = false;

cells.forEach(cell => {
  cell.addEventListener("click", () => {
    if (gameEnd) {
      return;
    }
    if (cell.textContent === "") {
      cell.textContent = currentPlayer;
      if (checkWin()) {
        gameEnd = true;
        alert(`${currentPlayer} es el ganador!`);
      } else if (checkTie()) {
        gameEnd = true;
        alert("Excelente juego, es un empate!");
      } else {
        currentPlayer = currentPlayer === "X" ? "O" : "X";
      }
    }
  });
});

function checkWin() {
//en base a nuestra constante winConditions verificamos si la posición del tablero muestra alguna victoria.
  return winConditions.some(condition => {
    return condition.every(index => {
      return cells[index].textContent === currentPlayer;
    });
  });
}

function checkTie() {
//en base a nuestras celdas del tablero verificamos que todas las celdas estén ocupadas por alguna ficha.
  return Array.from(cells).every(cell => {
    return cell.textContent !== "";
  });
}
```

¡Analicemos el código! Comenzamos definiendo como jugador actual a las fichas representadas por "X" y definimos la variable de fin de juego como false. Luego recorremos nuestro tablero agregando nuestro EventListener y preguntando si aún no finalizó el juego; si no lo hizo verificamos en una lógica de cascada si la celda está vacía asignamos el jugador actual a la ficha correspondiente, si la jugada representa una victoria finalizamos el juego sino verificamos si es un empate y finalmente sino es ninguno de los casos anteriores cambiamos el turno del jugador actual a la próxima ficha.

En todos los casos de fin de juego usamos alert() para mostrar los mensajes correspondientes.

## Probemos el código
¡Lo logramos! El último paso es garantizar que nuestra aplicación funcione es ejecutar y probarlo. A jugar y a no preocuparse si hay errores; **Todos los desarrolladores** tienen errores. Examinemos los mensajes y la depuración según sea necesario.

Hagamos clic en **Iniciar** y comienza a escribir! Debería parecerse un poco a la animación que se muestra a continuación.

![Animación del juego en acción](images/tateti.gif)

🚀 Desafío: agregar más funcionalidad

- Agregar un "Inicio" y "Reincio" que vacie el tablero cuando se haga clic en el.
- Permitir el ingreso de Nombres para cada jugador.
- Almacená puntajes altos usando [LocalStorage](https://developer.mozilla.org/docs/web/api/window/localstorage){:target="_blank"}

# Revisión y autoestudio

También podés leer [todos los eventos disponibles](https://developer.mozilla.org/docs/web/events){:target="_blank"} para que como desarrollador puedas usar a través del navegador web, e imaginá los escenarios en los que usarías cada uno.


### Rúbrica

| Criterios | Ejemplar | Adecuado | Necesita mejorar |
| -------- | -------------------------------------------------- ------------------------------------ | -------------------------------------------------- -------------- | ----------------- |
| | La solución presentada es completa y funciona correctamente | La solución presentada es mínimo y funciona correctamente | La solución tiene errores |
