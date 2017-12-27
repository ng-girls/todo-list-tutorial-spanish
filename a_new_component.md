# Un nuevo componente

En este capítulo vamos a escribir un nuevo componente completo. Esto nos va a permitir agregar nuevos elementos  ala lista de tareas. Estará compuesto de elementos HTML `input` y `button`.

Nosotros usaremos Angular CLI para generar todos los archivos necesarios y que comience por nosotros. En un terminal ejecuta:

```cmd
ng g c input -it
```

> Nota que tu necesitas abrir un nuevo terminal (ventana o pestaña) para poder ejecutar un nuevo comando. Inser el comando en la terminalsuperior donde está ejecutando el comando `ng serve` no tendrá ningún efecto.

Como podemos ver anteriormente, `ng` es el comando para usar Angular CLI `g` es una abreviatura para `generate`. `c` es una abreviatura para `component`. `input` es el nombre que le daremos al componente, `it` es una abreviatura para `inline-template`.

Así que la versión de larga del comando es:

```
ng generate component input --inline-template
```

> Puedes evitaru usar el `it` cada vez que generes un componente definiendo plantillas en linea como por defecto en la configuración del archivo `angular-cli.json`.
> No te preocupes sobre el nombre del componente `input`. No reemplazará el elemento HTML `input`. Eso es gracias al prefijo que Angular CLi le da a nuestros componentes. El prefijo por defecto es `app`, así que el selector del componente será `app-input`. Si tu has creado el proyecto con un prefijo de tu preferencia o has cambiado en el archivo `angular-cli.json`, este será el prefijo del selector. Cuando nosotros creamos el proyecto, definimos el prefijo a "todo", así que el selector será `todo-input`. 

Vamos a mirar lo que Angular CLI ha creado por nosotros.

Creó una carpeta llamada `src/app/input`. Aquí hay tres archivos:

* `input.component.css` - Aquí es donde estilizamos el componente específico que colocaremos.
* `input.component.spec.ts` - Este e sun archivo para probar el componente. Nosotros no trataremos esto en este tutorial.
* `input.component.ts` - Este es el archivo del componente el cual definiremos su plantilla y lógica.

Abre el arhcivo `input.component.ts`. Puedes ver que Angular CLI ha generado una plantilla por defecto para nosotros:

```js
template: `
    <p>
      input Works!
    </p>
  `,
```

También ha agregado el selector de acuerdo al nombre de nuestro componente, con el prefijo que configuramos:

```js
selector: 'todo-input',
```

Podemos usar este componente como es y ver el resultado:

Abramos el componente raiz `app.component.ts` y agreguemos la etiqueta `todo-input` en cualquier lugar dentro de la plantilla:

```js
template: `
  <h1>
    {{title}}
  </h1>

  <todo-input></todo-input>
`,
```

¡Verifiquemos que hay de nuevo en el navegador!

Volvamos a nuestro `input.component.ts` y agreguemos algún contenido. Primero, agrega un miembro `title` el cual nos dirá cual es el título del elemento para agregar:

```ts
export class InputComponent implements OnInit {
  title: string = '';
  ...
```

Esto no interferirá con el `title` del componente `todo-root`, desde que cada componente está encapsulado.

Puedes darle una cadena inicial al títutlo, como lo hicimos con el componente `todo-root`.

A continuación, agrega un elemento, un botón y una unión del título a la plantilla: 

```html
<input>
<button>Save</button>
<p>The title is: {{ title }}</p>
```

¡Verifica el resultado!

Este componente no hace mucho en este punto. En los siguientes capítulos aprenderemos sobre la clase componente, y luego implementaremos la lógica del componente.

