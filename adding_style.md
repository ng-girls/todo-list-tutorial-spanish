# Agregar estilos

Con Angular podemos darle estilo a los componentes, en una maera que no afecte el resto de la aplicación. Es una buena práctica encapsular los estilos relativos al componente de esta manera.

También podemos definir estilos generales que se usarán en toda la aplicación. Esto es bueno para crear el mismo `look-and-feel` para todos nuestros componentes. Por ejemplo, podemos decirid que palata de colores vamos a usar como tema para nuestra app. Entonces, si queremos cambiar los colores o ofrecer distintos temas, podemos cambiarlos en un solo lugar en vez de en cada componente.

Angular nos da distintos métodos de encapsulado de estilos, pero vamos a quedarnos en lo genérico.

Angular CLO ha generado una hoja de estilos general por nosotros en `src/style.css`. Copia el siguiente código en ese archivo:

```css
html, body, div, span,
h1, p, ul, li {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}

body {
  line-height: 1;
  background: #f1f1f1;
  font-size: 16px;
  line-height: 22px;
  color: #404040;
  font-family: 'Lucida Grande', Verdana, sans-serif;
}

ol, ul {
  list-style: none;
}

.btn {
  background: lightseagreen;
  color: #fff;
  padding: 3px 10px;
  margin: 0 0 0 3px;
  border: none;
  border-radius: 5px;
  font-size: 12px;
  line-height: 24px;
  cursor: pointer;
  vertical-align: bottom;
}

.btn:hover {
  background: lightslategrey;
}

```

> ¿Cómo el proyecto sabe como ver a este archivo? En el archivo de configuración `.angular-cli.json` bajo `apps[0].styles` puedes ver los archivos que la herramienta de construcción añade al proyecto. Puedes abrir las herramienta de desarrollo del navegador y ver los estilos dentro del elemento:

```html
<html>
  ...
  <head>
    ...
    <style type="text/css">
    ...Your style is here
    </style>
    ...
  </head>
  ...
</html> 
```

Ahora vamos a agregar estilos específicamente al compoentne `list-manager`.

Abre el archivo `list-manager.component.css` y pega el siguiente estilo dentro:

```css
.todo-app {
  position: relative;
  width: 400px;
  padding: 30px 30px 15px;
  background: white;
  border: 1px solid;
  border-color: #dfdcdc #d9d6d6 #ccc;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  margin: 20px auto;
}

.todo-app:before, .todo-app:after {
  content: '';
  position: absolute;
  z-index: -1;
  height: 4px;
  background: white;
  border: 1px solid #ccc;
  border-radius: 2px;
}

.todo-app:after {
  bottom: -3px;
  left: 0;
  right: 0;
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}

.todo-app:before {
  bottom: -5px;
  left: 2px;
  right: 2px;
  border-color: #c4c4c4;
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.15);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.15);
}

.todo-app h1 {
  font-size: 52px;
  line-height: 52px;
  margin-bottom: 30px;
  font-weight: bold;
  text-align: center;
  letter-spacing: -0.8px;
}

.todo-add {
  margin-bottom: 20px;
}
```

Como este estilos es adjunto al componente `list-manager`?

Mira dentro del archivo `list-manager.component.ts`. Una de las propiedades pasadas al decorador `@Component` es `styleUrls`. Este es una lista de hojas de estilo que pueden ser usadas por Angular, el cual encapsula es estilo con el componente.

Agrega el siguiente estilo a `input.component.css`:

```css
.todo-input {
  padding: 4px 10px 4px;
  font-size: 16px;
  font-family: 'Lucida Grande', Verdana, sans-serif;
  line-height: 20px;
  border: solid 1px #dddddd;
  border-radius: 5px;
  flex-grow: 1;
}

:host(:not([hidden])) {
  display: flex;
  justify-content: space-between;
  flex-grow: 1;
}
```

Agrega el siguiente estilo a `input.component.css`:

```css
.todo-item {
  padding: 10px 0;
  border-top: solid 1px #ddd;
  min-height: 30px;
  line-height: 30px;
  display: flex;
  justify-content: space-between;
}

.todo-checkbox {
  flex-shrink: 0;
  margin: auto 1ex auto 0;
}

.todo-title {
  flex-grow: 1;
  padding-left: 11px;
}

.btn-red {
  background: red;
}

.btn-red:hover {
  background: darkred;
}

```

Nota: No olvides colocar  las clases CSS al código de la plantilla de tu componente especificado, mas o menos así:

```ts
 @Component({
    ...
    template: `
          <button class="btn btn-red" (click)="removeItem()">
          `,
```

Puedes cambiar el estilo como desees, el tamaño de los elementos, los colores, ¡lo que tu quieras!

Nota: Tu puedes usar archivos SCSS en el proyecto, lo que es una buena manera de escribir estilos. Tiene grandes características que puede ayudar al desarrollador. Los archivos SCSS son compilados a CSS cuando el proyecto es construido.
