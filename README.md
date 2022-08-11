# MiniBootcamps
## Minibootcamp de Programación Web
Capacitación intensiva con foco en:
- Git
- Github y Github Pages
- HTML
- CSS
- JavaScript

## Levantar el proyecto localmente
### RVM
Instalar [RVM](https://nrogap.medium.com/install-rvm-in-macos-step-by-step-d3b3c236953b) y setear la version de Ruby a 3.1.2 con
```sh
$ rvm install 3.1.2 
$ rvm alias create default 3.1.2 
```

### Theme: Just the Docs
Instalar `just-the-docs` con: 
```sh
$ gem install just-the-docs
```

### Eventmachine
Instalar `eventmachine` con: 
```sh
$ gem install eventmachine -- --with-cppflags=-I/usr/local/opt/openssl/include
```

### Dependencias 
Instalar depedencias con: 
```sh
$ bundle install
```
Levantar el proyecton con: 
```sh
$ bundle exec jekyll serve
``` 
Se levanta localmente en `localhost:4000`

## Directrices de colaboración
### Convención de nombres
El contenido de cada clase (.md e imágenes necesarias) se agrupan por directorios.
El nombre de cada directorio debe empezar con el orden del contenido seguido de un _ (guión bajo) y el nombre de la clase. Ejemplo:
```html
4_css
```

Las clases dentro de un mismo directorio siguen la misma convención, donde el orden en el nombre se debe corresponder con el `nav_order` del archivo.

### Tono de voz de las clases
Para el tono se utiliza el [voseo](https://www.rae.es/dpd/voseo).

### Branch
Para la inclusión de una nueva clase crear un branch que represente a la clase que se quiere incluir siguiendo la siguiente convención para el nombre:
`clase_[nombre-clase]`
Donde `nombre-clase` representa a la clase (en camelCase) que se desea incluir, por ejemplo: `clase_speedTyping`.

### Commits
Los commits puede estar en español.

### Deploy
El deploy en Github Pages se hace únicamente a partir de la rama `main` por lo que cualquier clase nueva debe ir al main mediante un Pull Request.

### Pull Request
#### Nombre
La convención es similar a la del branch
`Clase [nombre-clase]`

#### Revisión
Si luego de hacer el PR un branch necesita nuevamente un cambio, una vez terminado el cambio realizar otro PR siguiendo la misma convención de nombre pero con un sufijo que indique el número del cambio. Ejemplo:
```html
Clase SpeedTyping
. . . 
Clase SpeedTyping [2]
```

