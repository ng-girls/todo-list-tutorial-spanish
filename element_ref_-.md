# Elemento ref

En el capítulo pasado, terminamos con nuestor componente `input` el cual puede reflejar el cambio del valor del título en nuestro elemento. `input.component.ts` debería verse así:

```javascript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'todo-input',
  template: `                           
    <input [value]="title"              
           (keyup.enter)="changeTitle($event.target.value)">
    <button (click)="changeTitle('Button Clicked!')">
      Save
    </button>
    <p>The title is: {{ title }}</p>
  `,  
  styleUrls: ['./input.component.css']  
})    
export class InputComponent implements OnInit {
  title: string = '';           

  constructor() { }                     

  ngOnInit() {
  }

  changeTitle(newTitle: string): void {
    this.title = newTitle;              
  }
}
```

Ahora queremos tomar el valor del `input` (el que el usuario escribió) y cambiar el título cuando presionamos el botón `Save`.

Nosotros ya sabemos como crear un botón y como reaccionar en un click. Ahora necesitamos pasar al método información de un elemento diferente. Queremos usar el valor del   `input` dentro del elemento `button`.

Angular nos ayuda a hacer eso. **Podemos obtener la referencia al objeto que queremos en una variable con el nombre que escojemos, por ejemplo** `inputElement`, usando una notación simple - un numeral. Agrega `#inputElement` al elemento `input`, y luego usalo para pasarlo en el evendo click del botón:

```html
<input [value]="title"              
       (keyup.enter)="changeTitle($event.target.value)"
       #inputElement>

<button (click)="changeTitle(inputElement.value)">
  Save
</button>
```

Ahora podemos usar el valor que el usuario ingresó en el elemento `input` en el llamado del método cuando se hace click en el botón `Save`

¿Qué es el `#` que vemos?

Angular nos deja definir una nueva variable local llamada `inputElement` (o cualquier nombre que escojas), la cual mantiene una referencia al elemento en el que la definimos, y luego la usa en cualquier manera que nosotros queramos. En nuestro caso, para acceder al valor de la propiedad del `input`.

En lugar de cazar los elementos haciendo una consulta al DOM (lo cual es una mala práctica como discutimos), ahora podemos colocar referencias en una plantilla y acceder a cada elemento que queremos declarativamente.
Lo siguiente será construir una lista de elementos para hacer.

### Consejo - explora el elemento referencia

Al igual que hicimos en el capítulo previo, cuando nosotros registramos $event, puedes hacer lo mismo con `#inputElement`. Cambia el método `changeTitle` así puedes recibir el elemento completo e imprimirlo en la consola:

```html
<input [value]="title"              
       (keyup.enter)="changeTitle(inputElement)"
       #inputElement>

<button (click)="changeTitle(inputElement)">
  Save
</button>
```
```ts
changeTitle(inputElementReference): void {
  console.log(inputElementReference);
  this.title = inputElementReference.value;              
}

```

## Recursos

[Angular Template Reference Variables](https://angular.io/docs/ts/latest/guide/template-syntax.html#!#ref-vars)

