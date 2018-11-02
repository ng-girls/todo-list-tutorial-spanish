# Agregar un checkbox

Ahora podemos interactuar con nuestra lista de tareas al eliminar elementos. Pero si nosostros queremos completar elementos, y todavía tenerlos en nuestra lista, por ejemplo, tener una linea tachando el título? ¡Agregamos un checkkbox!

Vamos a:

* Agregar un checkbox
* Agregar la funcionalidad de que al clickear el checkbox agregaremos una clase CSS, la cual agregará el estilo de tachar el título de nuestros elementos
* Editar el título para que responda al checkbox
* Agregar una nueva clase CSS

Comencemos agregando un checkbox en nuestro archivo `item.component.ts`. Coloca el siguiente código después de la etiqueta `<p>` que contiene el ` {{todoItem.title}}`:

```html
  <input type="checkbox"/>
```

Ahora, para que el checkbox haga algo, necesitamos agregar un evento de click el cual llamará la función `completeItem()`:

```html
  <input type="checkbox" (click)="completeItem()"/>
```

Cuando hacemos click en el checkbox se ejecutará la función `completeItem()`. Vamos a hablar sobre lo que esta función debe hacer. Queremos ser capaces de cambiar el estilo del título del CSS cuando el checkbox esté marcado colocando una línea atravesándolo, y sin la línea cuando no estee marcado. Para lograr esto vamos a colocar una variable alternada para que sea `true` o `false` que represente los estados de marcado/no-marcado. Agrega el siguiente código a la clase `ItemComponent`:

```js
isComplete: boolean = false;

completeItem() {
  this.isComplete = !this.isComplete;
}
```

¡Pero espera! ¿Cómo va a hacer esto efecto al título cuando solamente estamos tocando el checkbox? Bueno, Angular tiene esta maravillosa directiva llamada ngClass. Esta directiva aplica o elimina una clase CSS en función de un valor booleano (`true`/`false`). Aquí hay muchas maneras de usar esta directiva (Mira la documentación [aquí](https://angular.io/docs/ts/latest/api/common/index/NgClass-directive.html)) Pero  nos enfocaremos en usarla así:

```html
<some-element [ngClass]="{'first': true, 'second': true, 'third': false}">...</some-element>
```

Las clases 'first' y 'second' serán aplicadas al elemento porque se les dió el valor `true`, mientras que la clase 'third' no será aplicada porque se le dió el valor `false`. Aquí es donde el código viene a jugar. Nuestra función `completeItem()` alternará entre `true` y `false`, esto nos dirá si la clase debe ser colocada o eliminada.

Vamos a añadir la directiva `ngClass` a nuestro títlo ahora:

```html
<p class="todo-title" [ngClass]="{'todo-complete': isComplete}">
  {{ todoItem.title }}
</p>
```

Y finalmente, agregaremos el css a nuestro archivo `item.component.css`

```css
  .todo-complete {
    text-decoration: line-through;
  }
```

¡Et Voila! Verifica que el checkbox aplique la línea através del título cuando se marque y la elimine cuando se desmarque.
