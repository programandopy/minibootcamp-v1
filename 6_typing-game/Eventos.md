---
title: Eventos en JavaScript
has_children: true
nav_order: 7
has_toc: true
---

Usualmente cuando creamos una aplicación para nuestro navegador creamos lo que se conoce como una "Interfaz Gráfica de Usuario" (GUI por sus siglas en inglés, Graphic User Interface) para interactuar con el usuario. De esta manera el usuario puede comunicarse con nuestro programa a través de "clicks" en diferentes elementos de nuestro programa o ingresando texto, por ejemplo.

Es así que nuestro principal desafío al programar es controlar esas acciones que realiza el usuario, y poder planear una respuesta para ellas, sin poder saber cuando van a suceder. Como aprendimos en lecciones anteriores, nuestra manera de crear respuesta por parte de nuestro programa es utilizando funciones pero para que nuestras funciones estén relacionadas a una acción determinada del usuario (click en un botón, escribir texto, etc.) necesitamos un nuevo componente que se conoce como "event listeners" que no son otra cosa que funciones que se dedican a escuchar las acciones posibles y una vez que estas ocurren ejecutar una respuesta. Podemos agregar un event listener usando el código **addEventListener** y asignando una función a ejecutarse.

**TIP:** Vale la pena señalar que hay varias formas de crear detectores de eventos. Se puede usar funciones anónimas o crear funciones con nombre, también se puede configurar la propiedad "clic" o usar "addEventListener". En esta lección vamos a manejar "addEventLister" y funciones anónimas, ya que es probablemente la técnica más común utilizada por los desarrolladores web. También es el método más flexible porque "addEventListener" funciona para todos los eventos y el nombre del evento se puede agregar como parámetro.
