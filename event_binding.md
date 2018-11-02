# Enlace de eventos

Queremos que nuestra aplicación reacciones a las acciones de los usuarios. Queremos actualizar el título en cualquier momento que el usuario lo cambie, o que agregue un nuevo elemento cuando el usuario presiones el botón guardar o la tecla Enter.

Todavía no tenemos una lista completa para mostrar, pero en el momento usaremos otra manera para probar la acción. Vamos a cambiar la funcionalidad después.

## La acción

Primer paso, vamos a implementar `changeTitle`. Puedes reemplazar `generateTitle` con este nuevo método. Este recibirá el nuevo título como primer argumento:

```ts
changeTitle(newTitle: string): void {
  this.title = newTitle;
}
```

## Enlazando los eventos

Justo como hicimos con las propiedades de los elementos, podemos enlazar los eventos cuando son emitidos por los elementos. De nuevo, Angular nos da una manera fácil de hacer esto **Solamente debes envolver el nombre de los eventos con un paréntesis, y pasarselo al método que debería ser ejecutado cuando el evento es emitido**.

Vamos a intentar un ejemplo simple, donde el título es cambiado cuando el usuario da click en el botón. Nota los paréntesis al rededor de `click`. (También  enlazaremos el valor del `input` de nuevo a `title`).

```html
template: `
  <input [value]="title">
  <button (click)="changeTitle('Button Clicked!')">
    Save
  </button>
  <p>The title is: {{ title }}</p>
`,
```

El evento llamado es `click` y no `onClick` - en Angular tu eliminas el prefijo `on` de los eventos en los elementos.

Ve al navegador y ve el resultado -  da click en el botón `Save`

## Datos de los eventos

Pasamo una cadena estática a la llamada del método `Button Clicked!` ¡Pero podemos pasarle el valor que el usuario escribió en la caja de texto!

En el siguiente capítulo aprenderemos como usar las propiedades de un elemento en otro elemento en la misma plantilla. Entonces seremos capaces de completar la implementación del evento click en el botón `Save`.

Pero por ahora vamos a enlazar un método al elemento `input`: Cuando el usuario presione Enter, el método `changeTitle` será llamado.

### Evento 'keyup' 

Cuando el usuario escribe, los eventos del teclado son emitidos. Por ejemplo `keyDown` y `keyUp`. Nosotros atraparemos el evento `keyup` (cuando la tecla es solatada) y cambiaremos el título:

```html
<input [value]="title" (keyup)="changeTitle('Button Clicked!')">
```

Este elemento se vuelve grande, entonces para hacerlo mas fácil de leer vamos a partirlo en dos líneas:

```html
<input [value]="title" 
       (keyup)="changeTitle('Button Clicked!')">
```

Ahora cuando el usuario escriba en la caja de texto, el título será cambiado a `Button Clicked!`. Pero todavía será una cadena estática.

### El objeto $event 

Ahora nosotros solo reaccionamos cuando el evento `keyup` ocurre. Angular nos permite obtener el objeto del evento en si mismo. Es pasado al enlace del evento como `$event` - Así que podemos usarlo cuando llamamos a `changeTitle()`

El objeto `event` emitido por `keyup` tiene una referencia al elemento que emitió el evento - el elemento `input`. La referencia es guardada en la propiedad `target`. Como hemos visto antes, el elemento `input` tiene una propiedad `value` la cual tiene el valor actual de la cadena que está en la caja de texto. Podemos pasar `$event.target.value` al método:

```html
<input [value]="title" 
       (keyup)="changeTitle($event.target.value)">
```

Verifica esto en el navegador. Ahora veremos que con cada tecla presionada, puedes ver que el título cambia y refleja el valor del `input`.

### Presionando la tecla Enter

Puedes limitar el cambio unicamente a algunas teclas, en nuestro caso, la tecla Enter. Angular lo hace bastante fácil para nosotros. El evento `keyup` tiene propiedades las cuales son eventos mas específicos. Así que solo agregamos el nombre de la tecla en la que queremos escuchar:

```html
<input [value]="title" 
       (keyup.enter)="changeTitle($event.target.value)">
```

Ahora el título cambia solamente cuando el usuario presiona Enter cuando está escribiendo en el input.

### Consejo: Explora el objeto $event

![](blob:https://www.gitbook.com/909c0ae3-0a60-4870-9a38-6b7588264104) **Zona de Juegos:** Puedes cambiar el método para registrar los cambios del objeto `$event` en la consola, de esta manera puedes explorar y ver que porpiedades tiene.

Cambia el método `changeTitle`:

```ts
changeTitle(event): void {
  console.log(event);
  this.title = event.target.value; // the original functionality still works
}
```


![](blob:https://www.gitbook.com/909c0ae3-0a60-4870-9a38-6b7588264104) **Zona de Juegos:** Ahora cambia el argumento que estás enviando en la plantilla:

```html
<input [value]="title" 
       (keyup.enter)="changeTitle($event)">
```

¡Pruébalo!

No olvides cambiarlo de nuevo para seguir (!).

