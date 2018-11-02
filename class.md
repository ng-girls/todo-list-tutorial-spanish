# Clases

## Definiciones de Clases

Una Clase es una estructura de programación. Se define con **miembros** que pueden ser **propiedades** (variables) y **métodos** (funciones). Las instancias de la clase son creadas, usualmente llamando al operador `new` de la clase: `let myInstance = new myClass;`. La instancia es creada como un objeto en el cual puedes llamar métodos de la clase y definir los valores de sus propiedades. Múltiples copias pueden ser creadas de una clase.

### En Angular...

Angular se encarga de crear instancias de las clases que tu definas - si ellas son reconocidas como bloques de construcción de Angular. Los decoradores harán la decoración con Angular.

Cada vez que usas un componente en una plantilla, una nueva instancia de esta es creada. Por ejemplo, aquí tenemos tres instancias de la clase `inputComponent` que has creado:

```html
template: `
  <todo-input></todo-input>
  <todo-input></todo-input>
  <todo-input></todo-input>
`
```

Veamos  la clase `inputComponent`.

### implementando OnInit

Primero vereas que algo agregado en la declaración de clase:

```ts
export class InputComponent implements OnInit {
  ...
}
```

`OnInit` es una **interface** - una estructura definida pero no implementada como una clase. Esta define las propiedades y/o métodos que deberían existir en la clase que lo implementa. En este caso `OnInit` es una interface para los componentes d eAngular los cuales implementan el método `ngOnInit`. Este médito es un **compomente los métodos del ciclo de vida**. Angular llamará a este método después que una instancia ha sido creada.

Angular CLI agrega su propia sentencia para recordarnos que es mejor inicializar cosas en un componente a través del método `ngOnInit`.

Puedes ver también el método agregado en el cuerpo de la clase:

```ts
ngOnInit() {
}
```

Puedes usar este método sin indicar explícitamente que la clase implementa la interface `OnInit`.. Pero es útil usar la sentencia de implementación. Para ver como, elimina el método `ngOnInit`. El IDE te dirá que hay un error - debes implementar `ngOnInit`. ¿Cómo sabe esto? por el `implements OnInit`.

### constructor

Otro método que no hemos vist en el componente `todo-root` es el constructor. Es un método llamado por JavaScript cuando una instancia de la clase es creada. Lo que sea que se encuentre en este método es usado para crear la instancia. Entonces es llamado antes de `ngOnInit`.

> Una poderosa caracterísitica en Angular es que el constructor usa inyección de dependencias. Veremos esto después, cuando comencemos a usar servicios.

### Propiedades

La propiedad `titl` fue agregada para guardar un valor, en nuestro caso, de tipo cadena. Cada instancia de la clase tendrá su propia variable `title`m lo que significa que puedes cambiar el valor `title` de una instancia, pero permanecerá igual en otras instancias.

En TypeScript, debemos declarar miembros de la clase en la clase, en cualquier parte del cuerpo de la clase fuera de cualquier método o pasarlos en el constructor, como veremos cuando usemos los servicios.

Puedes declara la propiedad sin inicializarla:

```ts
title: string;
```

Entonces puedes asignar un valor en una etapa posterior, por ejemplo en el constructor o en el método `ngOnInit`. Cuando referencias un miembro de la clase en algún lugar dentro de la clase, debes usar el prefijo con un `this`. Esta es una propiedad especial que apunta a la instancia actual.

Trata definir un valor diferente para `title` fuera del constructor. Verás el resultado en el navegador:

```ts
title: string = 'my title';

constructor() { 
  this.title = 'Hello World';
}
```

Trata cambiando el valor de `title` dentro del método `ngOnInit`. ¿Qué valor será mostrado en la pantalla?

### Métodos

Vamos a agregar un método que cambie el valor de `title` de acuedo al argumento que le pasemos. El método tendrá un parametro de tipo `string`. Agrega dentro del cuerpo de la clase (pero no dentro de otro método):

```ts
changeTitle(newTitle: string): void {
  this.title = newTitle;
}
```

Este método es llamad `changeTitle`. Y no tiene ninguna sentencia de retorno, entonces notamos que "retorna void" Nosotros podemos cambiar eso si queremos que retorne un valor actual. Por ejemplo:

```ts
changeTitle(newTitle: string): string {
  this.title = newTitle;
  return this.title;
}
```

Este método no es usado en cualquier lugar. Nosotros podemos llamarlo desde otro método de nuestra plantilla (lo cual veremos en los siguientes capítulos). Vamos a llamarlo en el constructor.

```ts
constructor() { 
  this.changeTitle('I love Angular');
}
```

![](/assets/lab.jpg) **Zona de Juego**: Puedes tratar de llamar al método con distintos argumentos (la cadena que pasamos dentro de las llaves) de `ngOnInit`. Trata de llamarla antes o después de asignar el valor directamente a `title`. Trata de llamarla varias veces desde el mismo método. Veras el resultado en el navegador.

### Tip de depuración

Siempre puedes usar `console.log(algunValor)` dentro de los métodos de clase. Entonces el valor que le pasas como argumento será impreso en la consola del navegador. de esta manera puedes saber el orden de ejecución de los métodos y el valor de los argumentos que pasas (si son una variable). Por ejemplo:

```ts
constructor() { 
  console.log('in constructor');
  this.changeTitle('I love Angular');
  console.log(this.title);
}
```

La consola del navegador hace parte de las Opciones de Desarrollador. Mira las diferentes maneras de abrir la consola de tu navegador[https://webmasters.stackexchange.com/questions/8525/how-do-i-open-the-javascript-console-in-different-browsers](https://webmasters.stackexchange.com/questions/8525/how-do-i-open-the-javascript-console-in-different-browsers)

