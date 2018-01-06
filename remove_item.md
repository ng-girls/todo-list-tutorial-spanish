# Eliminar elemento

El usuario debería ser capaz de eliminar cualquier elemento, así esté activo o completo. Eliminar un elemento puede ser hecho dand click en un botón llamado "eliminar". En este tutorial, vamos a aprender como añadir esta funcionalidad a nuestro proyecto.

### Archivo: item.component.ts
Primero, necesitamos añadir el botón al elemento, entonces vamos a trabajar en el archivo `item.component.ts`

- Añade un evento **(click)** el botón `remove` en la plantilla:
  ```
  <button (click)="removeItem()">
    remove
  </button>
  ```
- Agrega un nuevo `Output` a la clase `ItemComponent`, el cual se emitirá  a `list-manager` cuando el usuario presione el botón `remove` en un evento específico:
  ```
  @Output() remove:EventEmitter<any> = new EventEmitter();
  ```
  Asegúrate de importar `EventEmitter` y `Output` en tu clase:

  ```
  import { Component, OnInit, Input, EventEmitter, Output } from '@angular/core';
  ```
- Agrega una función a la clase `ItemComponent` la cual emitirá e evento. Esta función será llamada cuando el usuario de click en el botón `remove`:
  ```
  removeItem() {
    this.remove.emit(this.todoItem);
  }
  ```

### Archivo: list-manager.component.ts

Ahora que cada elemento puede emitir su propia eliminación, vamos a asegurarnos de que list manager en realidad elimine el mismo elemento de la lista. Para eso, vamos a trabajar en el archivo `list-manager.component.ts`.

- Necesitamos responder al evento **remove**, vamos a añadir en la plantilla, dentro de la etiqueta `<todo-item>`:
  ```
  (remove)="removeItem($event)"
  ```
- Vamos a necesitar una función llamada `removeItem()` en la clase `ListManagerComponent`:
  ```
  removeItem(item) {
    this.todoList = this.todoListService.removeItem(item);
  }
  ```

### Archivo: todo-list.service.ts

Eliminar el elemento es manejado en el servicio, abre `todo-list.service.ts` y añade una función llamada `removeItem()` a la clase TodoListService:

```
removeItem(item) {
  return this.storage.destroy(item);
}
```

Esta función llama al método `destroy()` que ya creamos en todo-list-storage.service.ts anteriormente.
