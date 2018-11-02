# Local Storage

## ¿Qué es Local Storage?

Local Storage, como su nombre inplica, es una herramienta para almacenar información localmente.
Similar a las cookies, local storage almacena información en el computador del usuario, y con eso, nos permite a nosotros como desarrolladores, una manera fácil de acceder a la información para leer y escribir.

## Soporte de navegadores

Como local storage fue introducido a nosotros ocn HTML5, todos los navegadores que soporta en estándar HTML5 también soporta local storage.
Básicamente es soportado por todos los navegadores modernos, incluyendo IE 8.

## ¡Queremos código!

Primero, para usar local storage, necesitamos acceder la instancia localStorage, la cual estea expuesta para nosotros globalmente.
Esto significa que podemos llamar a los métodos disponibles con esta interface usando esta instancia.

Local storage almacena información en una forma de llave-valor, entonces la interfaz es bastante simple y tiene dos métodos principales: `getItem` y `setItem`

Un ejemplo de uso:

```
localStorage.setItem('name','Mor');

let name = localStorage.getItem('name'); 
alert('Hello '+name+'!');
```

Otro método muy util es `clear` y es usado para limpiar toda la información de local storage:

```
localStorage.clear();
```

Existen otros métodos maravillosos que están descritos [aquí](https://developer.mozilla.org/en-US/docs/Web/API/Storage).

## Hora de Angular (de vuelta a nuestra aplicación)

En la siguiente sección vamos a construir nuestro servicio de almacenamiento local, el cual luego será usado para almacenar nuestra lista de elementos.
Como describimos anteriormente, vamos a generar el servicio usando Angular CLI:

```
ng g s todo-list-storage
```

El nuevo archivo `todo-list-storage.service.ts` debería ser creado con el siguiente código:

```
import { Injectable } from '@angular/core';

@Injectable()
export class TodoListStorageService {

  constructor() { }

}
```

**Si algo parece no-familiar/raro a ti, por favor, ve al [tutorial de Servicios](service.html) para información mas detallada sobre servicios**.

Necesitamos proveer el servicio en nuestro `ngModule`. Abre `app.module.ts` y en la lista de `providers` añade la nueva clase:

```ts
providers: [TodoListService, TodoListStorageService],
```

Asegúrate que la clase también esté importada en el archivo:

```ts
import { TodoListStorageService } from './todo-list-storage.service';
```

Vamos a comenzar agregando una propiedad privada a nuestro servicio llamada `todoList` la cual contendrá los elementos.

```
private todoList;
```

Adicionalmente, vamos a añadir una constante que almacene el nombre de la llave con la que queremos usar nuestro local storage, agregala justo después d elos imports:

```
const storageName = 'aah_todo_list';
```

Ahora vamos a inicializar esta propiedad con datos, al obtenerlos de localStorage, entonces en el constructor agrega:

```ts
constructor() {  
    this.todoList = JSON.parse(localStorage.getItem(storageName));  
}
```

¡Espera! ¿por qué `JSON.parse`? La respuesta es simple:

Como describimos anteriormente en este tutorial, local storage almacena información en forma llave-valor, lo que significa que los valores son almacenados como **cadenas**. Entonces si quieres tener un verdadero objeto para manejar, necesitas transformar la cadena en un objeto real.

Ahora comencemos a hacer cosas reales, pero primero vamos a declarar todos los métodos públicos que queremos exponer en este servicio, los cuale son **get, post, put** y **destroy**

Nuestro servicio debería verse similar a:

```typescript
import { Injectable } from '@angular/core';

const storageName = 'aah_todo_list';

@Injectable()
export class TodoListStorageService {

  private todoList;

  constructor() {
    this.todoList = JSON.parse(localStorage.getItem(storageName));
  }

  // get items
  get() {}

  // add a new item
  post(item) {}

  // update an item
  put(item, changes) {}

  // remove an item
  destroy(item) {}

}
```

Vamos a implementarlos uno por uno

### get

Este método simplemente retornarea el estado acutal de los elementos almacenados en el servicio:

```ts
/**
   * get items
   * @returns {any[]}
   */
  get() {
    return [...this.todoList];
  }
```

Si no estás familiarizado con el operador `...` por favor ve a [esta documentación](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Spread_operator) para mas información.

### post

Este método será responsable por agregar nuevos elementos, y retornar una nueva lista.

Acepta un parámetro, `item` el cual será el elemento a agregar:

```ts
/**
   * Add a new todo item
   * @param item
   * @returns {any[]}
   */
  post(item) {
    this.todoList.push(item);
    return this.get();
  }
```

Algo que debes haber notado es que nosotros solamente insertamos un elemento al arreglo. Pero ¿qué pasa con localStorage? ¡Necesitamos sincronizarlo con el nuevo arreglo!

Vamos a agregar un nuevo método **privado** a nuestro servicio, el cual será usado internamente para actualizar la lista almacenada:

```ts
/**
   * Syncronize the local storage with the current list
   * @returns {any[]}
   */
  private update() {
    localStorage.setItem(storageName, JSON.stringify(this.todoList));

    return this.get();
  }
```

Vamos a explicar:

Aquí usamos el método `setItem`, el cual toma una llave (primer elemento) y un valor (segundo argumento) y lo almacena en `localStorage`. Después que actualizamos el valor, simplemente retornamos la nueva lista usando el método `get` que implementamos antes.

Ahora vamos a modificar nuestra función `post` para que use `update` y todo esté sincronizado en armonía:

```ts
/**
   * Add a new todo item
   * @param item
   * @returns {any[]}
   */
  post(item) {
    this.todoList.push(item);
    return this.update();
  }
```

### put

Aquí nosotros queremos actualizar un elemento existente. Antes de eso, vamos a crear un método privado `findItemIndex` el cual simplemente retornará el índice de un elemento en la lista:

```ts
/**
   * find the index of an item in the array
   * @param item
   * @returns {number}
   */
  private findItemIndex(item) {
    return this.todoList.indexOf(item);
  }
```

Ahora podemos usar `Object.assign` para actualizar el elemento existente:

```ts
/**
   * Update an existing item
   * @param item
   * @param changes
   * @returns {any[]}
   */
  put(item, changes) {
    Object.assign(this.todoList[this.findItemIndex(item)], changes);
    return this.update();
  }
```

¿Qué está pasando aquí?

`Object.assign` toma el objeto destino (primer argument) y objetos recursos (todos los demás argumentos), y los copia al objeto destino.
Si una propiedad existe en ambos, el recurso y el destino, este método reemplazará con la nueva. Aquí queremos actualizar un elemento en la lista, entonces primero necesitamos encontrar el índice en el arreglo, y luego aplicar los cambios a el. Al final, queremos sincronizar el almacenamiento local (`this.update`) y retornar la nueva lista.

### destroy

Este método eliminará un elemento de la lista y luego sincronizará con el almacenamiento local:

```ts
/**
   * Remove an item from the list
   * @param item
   * @returns {any[]}
   */
  destroy(item) {
    this.todoList.splice(this.findItemIndex(item), 1);
    return this.update();
  }
```

El código anterior es muy simple. `splice(i, n)` elimina `n` elementos comenzando desde el índice `i`. En nuestro código, primero encontramos el índice el índice a eliminar, y luego lo elimina solo a el (por eso usamos 1 como segundo parámetro).

## Agregar alguna información por defecto

Vamos a asumir que queremos que nuestra lista de tareas siempre tenga información para comenzar. Entonces vamos a modificar nuestro servicio, al agregar en la sección de constantes (después de las importaciones):

```ts
const defaultList = [
  { title: 'install NodeJS' },
  { title: 'install Angular CLI' },
  { title: 'create new app' },
  { title: 'serve app' },
  { title: 'develop app' },
  { title: 'deploy app' },
];
```

Y luego modificar nuestro constructor:

```ts
constructor() {
    this.todoList = JSON.parse(localStorage.getItem(storageName)) || defaultList;
  }
```

El código anterior se asegura de que si no hay información definida en `localStorage`, nuestro servicio todavía tendrá información para devolver.

## ¡Casi terminamos!

Nuestor servicio está ahora listo para el trabajo. Pero espera, necesitamos proveerlo para poder usarlo.

Abre `app.module.ts` y luego agrega `TodoListStorageService` a la lista de `providers`.

¡Ahora verdaderamente podemos usar nuestro servicio!

Ahora para que nuestra aplicación use nuestro nuevo servicio, vamos a abrir `todo-list.service.ts` y modificarla.

Primero necesitamos importar el nuevo servicio:

```ts
import { TodoListStorageService } from './todo-list-storage.service';
```

Luego, vamos a inyectarlo en el contructor, entonces vamos a tener una instancia para trabajar:

```ts
constructor(private storage:TodoListStorageService) {
}
```

Esto nos deja usar `this.storage` en todo el servicio todo-list.

Vamos a modificar los métodos actuales:

**Antes**

```ts
getTodoList() {
    return this.todoList;
}

addItem(item) {
    this.todoList.push(item);
}
```

**Después**

```ts
getTodoList() {
    return this.storage.get();
}

addItem(item) {
    return this.storage.post(item);
}
```

Ahora vamos a realizar una última modificación. Abre `list-manager.component.ts`, y vamos a modificar  el método `addItem` de esta manera:

```ts
addItem(title:string) {
    this.todoList = this.todoListService.addItem({ item:title });
}
```

El cambio anterior nos asegura que cuando agreguemos un elemento, nuestra lista también se actualizará visualmente.

## Resumen

En este tutorial hemos aprendido que es `localStorage` y como usarlo. Vimos como `localStorage` es una herramienta genial y sencilla para almacenar información localmente  en los dispositivos del usuario. También hemos implementado un nuevo servicio que utiliza `localStorage` para almacenar nuestros elementos `todo`, y actualizamos el resto de los componentes para soportar este nuevo servicio.

¡Disfruta el resto del tutorial!
