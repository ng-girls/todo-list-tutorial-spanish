# Agregar Elementos

Queremos agregar elementos a nuestra lista. Con Angular podemos hacer esto facilmente, y ver el elemento agregado inmediatamente. Haremos esto desd el componente `inputComponent` que creamos antes. Vamos a cambiarlo, así que cuando se presione Enter o cuando se de click en el botón, el valor del `input` se volverá el título de un nuevo elemeto. Y el nuevo elemento será agregado a la lista.

Pero nosotros no queremos que el componente `todo-input` sea el responsable de enviar el nuevo elemento a la lista. Queremos que este tenga la mínima responsabilidad, y **delegue la acción a su componente padre**. Una de las ventajas de esta aproximación es que el componente será reusable, y puede ser adjunto a diferentes acciones en diferentes situaciones.

Por ejemplo, en nuestro caso, seremos capaces de usar el `inputComponent` dentro de `itemComponent`. Entonces vamos a tener una caja de texto por cada elemento y vamos a poder editar el título del elemento. En este caso, presionando la tecla Enter o el botón Guardar tendrá un efecto diferente.

Entonces lo que queremos actualmente es **emitir un evento** desde el componente `todo-input` cuandl el título ha sido cambiado. ¡Con Angular podemos fácilmente emitir eventos desde nuestros componentes!

## @Output()

Dentro de la clase `inputComponent` añadiremos la siguiente línea, la cual define un `output` para el componente.

```ts
@Output() submit: EventEmitter<string> = new EventEmitter();
```

La propiedad `output` es llamada `submit` Asegúrate de que `Output` and `EventEmitter` estén agregados en las sentencias de `import` en las primeras líneas del archivo:

```ts
import { Component, OnInit, Output, EventEmitter } from '@angular/core';
```

Ahora, cuando llamemos `this.submit.emit()` un evento será emitido al componente padre. Vamos a llamarlo en el método `changeTitle`:

```ts
changeTitle(newTitle: string): void {
  this.submit.emit(newTitle);
}
```

Delegamos todo al componente padre - incluso actualmente cambiar el título del elemento si es necesitado. (El nombre del método puede parecer irrelevante ahora. Si quieres puedes cambiarlo a algo mas apropiado como `submitValue`. Recuerda cambiarlo en la plantilla también).

Pasamos `newtitle` cundo emitimos el evento. Lo que sea que pasemos en `emit()` estará disponible por el padre como `$event`.

Nada mas necesita ser cambiado en el componente `todo-input`. Los eventos emitidos por `keyup.enter` y `click` seguirán en el mismo método, pero el método en si ha cambiado.

Ahora necesitamos atrapar el evento en el componente padre y añadirle lógica a él. Ve al componente `app-root` y enlaza el evento `submit` en el componente `<todo-input>`:

```html
<todo-input (submit)="addItem($event)"></todo-input>
```

Ahora todo lo que falta implmenentar es el método `addItem`, el cual recive una cadena y la añade a la lista:

```ts
addItem(title: string): void {    
  this.todoList.push({ title });
}
```

¡Pruébalo!

