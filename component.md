# Componentes

Una aproximación en desarrollo web (y desarrollo de software generalmente) es la arquitectura basada en componentes. En los años pasados ganó mucha popularidad. ¿Qué es un componente?

Helmut Petritsch lo define es [Arquitectura basada en servicios vs Arquitectura basada en Componentes](http://petritsch.co.at/download/SOA_vs_component_based.pdf):

> Un componente es un objeto de software, definido para interactuar con otros componentes, encapsulando cierta funcionalidad o conjunto de funcionalidades. Un componente tiene una interfaz claramente definida y conforma un componertamiento preescrito común a todos los componentes en la arquitectura.

En aplicaciones web, **un componente controla un segmento de pantalla llamado vista**. Es una parte de lo que eventualmente veremos en la pantalla. Tiene su plantilla, la cual define la estructura visual. También tiene lógica que define el comportamiento y los valores dinámicos. La parte lógica es código Javascript y es llamado el controlador.

Aquí hay un diagrama de un componente en Angular, con el resultado abajo.
![Angular 2 Component](Angular Component.001.jpeg)

Las directivas, flujos y servicios son otros bloques de construcción en Angular, lo cual discutiremos mas tarde en el tutorial.

Miremos el componente que fue creado por Angular CLI. Todos los archivos relevantes existen en la carpeta `src/app`. Abre el archivo `app.component.ts`.

Al igual que los módulos que vimos en el capítulo previo, un componente también está definido por un decorador de clase. Este es la definición de clase:

```js
export class AppComponent {
  title = 'todo works!';
}
```

Tiene un miembro llamado "title". Es una variable a la que le puedes asignar un valor. El valor asignado aquí es la cadena "todo works!".

Angular se encarga de sincronizar los miembros del componente con los componentes de la plantilla, así que podemos fácilmente usar el miembro `title` en la plantilla. Mira la plantilla adjuntada al componente en el:

```html
<h1>
  {{ title }}
</h1>
```

Las llaves dobles y su contenido son llamadas **Interpolación**. Esta es una forma de **data binding** en Angular. Como mencionamos anteriormente, el código en este archivo no es usado cuando el cnavegador renderiza el componente. Angular compila a código Javascript. En una paso de la compilación, se buscan las interpolaciones dentro de la plantilla. **El contenido de la Interpolación es una expresión escrita en Javascript**. En tiempo de ejecución, la expresión es evaluadam y puedes ver el resultado.

Interpolación es una las características mas poderosas y básicas en Angular. Existe desde el comienzo de Angular -  en la primera versión. Hace uso insertar datos dinámicos a la vista.

En este componente, la expresión es simplemente el miembro de la casle componente `title`. **Vamos a cambiarlo**. Trata de seguir y ver el resultado en el navegador. (¡Con cada cambio que hagas en el archivo, el navegador se refrescará automáticamente!).

* Elimina el contenido de las llaves y manten solo el contenido de `title`
* Coloca de nuevo las llaves y reemplaza el contenido con alguna expresión matemática, por ejemplo: `{% raw %}{{ 2 + 2 }}{% endraw %}`. (Estos espacios no son obligatorios, solo hacen el código mas legible).
* Escribe una expresión matemática combinada con el miembro `title`: `{% raw %}{{ title + 10 }}{% endraw %}` 
* Pasa una variable no definida a la expresión - una variable la cual no ha sido declarada en la clase componente. Por ejemplo: `{% raw %}{{ x }}{% endraw %}¡ 
* Intenta lo que quieras. No te preocupes, ¡no puedes hacerle ningún daño al navegador o al computador! En el peor de los casso, el navegador se quedará sin memoria y se atascará (¡Pero tendrás que escribir algo realmente complicado para hacer que es pase!).

Esta es una manera en la que puedes enlazar miembros del componente a su plantilla. ¿Cómo Angular sabe cual es la plantilla del componente App?

Vamos atrás al archivo `app.component.ts` y mira la metadata definida en el decorador `@Component` justo debajo de la definición de clase:

```js
@Component({
  selector: 'todo-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
```
Le pasamos un objeto de definiciones al decorador, como vimos en el capítulo anterior con ngModule. La segunda propiedad, `templateUrl` le dice a Angular donde buscar por la plantilla adjunta al componente. Aquí hay otra opción para apuntar a la plantilla, la cual es una mejor práctica: escribir toda la plantilla en el mismo archivo aquí, en la definición de componente. Discutiremos esto después.

La tercera propiedad, `styleUrls` le dice a Angular donde buscar por archivos CSS que definen el estilo del componente. Este puede tener múltiples archivos CSS. Esta es la razón por la que `styleUrls` es un arreglo. Puedes ver al archivo `app.component.css`, verás que está vacío. Puede agregar algún estilo CSS aquí, por ejemplo:

```css
h1 {
  color: red;
}
```

Añadiremos mas estilos luego.

La primera propiedad, `selector` le dice a Angular cual va a ser el nombre de la etiqueta que usaremos para llamar al componente. Como vemos en el archivo `src/index.html`, usaremos el compoente todo-root dentro del cuerpo:

```html
<body>
  <todo-root>Loading...</todo-root>
</body>
```

El elemento `todo-root` no es un elemento HTML. Es un componente que creamos con el selector `todo-root`. Trata de cambiar el selector. Verás que si tu cambias solamente  uno de los archivos, "Loading..." aparecerá. Este es el contenido que colocamos dentro del elemento `index.html`, y es renderizado mientras no lo reemplacemos con el componente de Angular. Puedes ver en la consola del navegador un código de error.

Una última cosa, la primera línea del componente importa el ceodigo que define el decorador `@Component`. Esto es necesario para usar el decorador, el cual es definido en el archivo importado (o actualmente, en uno de sus propias importaciones). Trata de eliminar esta línea y verás el error.

#### Plantillas en línea

Vamos a mover la plantilla para que esté en línea con la definición del componente. Esto nos puede ayudar a manejar la plantilla viendo su propia funcionalidad.

En el archivo `app.component.ts` reemplaza la línea

```js
templateUrl: './app.component.html',
```

con

```js
template: ``,
```

Nota las **comillas inclinadas** - Ellas son usadas para definir Plantillas Literales, con son nuevas en JAvascript (ES6). De esta manera puedes definir cadenas de múltiples líneas. Estas pueden tener otra habilidad: Facilmente usar variables de Javascript y expresiones en a cadena (sin relaciones a expresiones enlazadas  de Angular en la plantilla). Lee mas sobre esto en la [documentación MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Template_literals).

Asegúrate de reemplazar `templateURL` con `template` y no olvides la coma al final de la línea.

Ahora copia la plantilla completa desde `app.component.html` y pégala entre las comillas inclinadas. Verás que re formatear el código es muy fácil con la visión:

```js
template: `
  <h1>
    {{ title }}
  </h1>  
`,
```

Es fácil manejar la plantilla cuando puedes ver el controlador al mismo tiempo. Esto es verdad mientras la plantilla no se agrande y el contorlador se vuelva complicado. Si esto es así, deberías reconstruir tu código partiendo el componente en varios mas pequeños.

En este punto puedes eliminar el archivo `app.component.html`.

> Cuando generamos un nuevo proyecto podemos definir que te gustaría usar una plantilla en lína para el componente principal con la bandera `-it` (o `--inline-template`). ¡Ten esto en mente para tu próximo proyecto!

De la misma manera en que usamos la plantilla en línea podemos usar los estilos en línea. Pero por ahora está bien mantener los estilos en un archivo separado.

### Resumen

Hemos explorado el componente raiz que fue generado por Angular CLI, e incluso lo hemos reconstruido. En el siguiente capítulo crearemos un nuevo componente. Comenzaremos a comenzar a construir árboles de componentes, los cuales definen la estructura de la aplicación.
