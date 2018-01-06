# Servicios

## ¿Qué y por qué?

Los servicios son funciones de Javascript que responden a una específica tarea solamente. Los servicios de Angular son inyectatos a través del mecanismo de Inyección de dependencias e incluyen valor, funcieon o característica requerida por la aplicación. En nuestra aplicación, vamos a necesitar un servicio que guarde las tareas y lo usaremos para inyectarlas en los componentes.

### Creación

Para crear un nuevo servicio con Angular CLI, necesitamos escribir el siguiente comando:

```bash
ng g s todoList
```

Este comando generará el servicio y lo colocará en `src/app/todo-list.service.ts`

Proveerlo en ngModule

Ahora, para usar el servicio, necesitamos proveerlo en el componenten `NgModule`.

En `src/app/app.module.ts`, agrega el código de importación:

```javascript
import { TodoListService } from './todo-list.service';
```

Ahora agrega el servicio al arreglo de `providers`, ese componente `ngModule` se verá así:

```javascript
@NgModule({
  declarations: [
    AppComponent,
    InputComponent,
    ItemComponent,
    ListManagerComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [TodoListService],
  bootstrap: [AppComponent]
})
```

Esto nos permitirá crear la instancia del servicio y usarla en cualquier lugar de nuestra app.

### Mover la lista del componente al servicio:

Ahora vamos a mover el arreglo `todoList` del componente a nuestro servicio. El servicio ahora tendrá:

```javascript
private todoList = [
    { title: 'install NodeJS' },
    { title: 'install Angular CLI' },
    { title: 'create new app' },
    { title: 'serve app' },
    { title: 'develop app' },
    { title: 'deploy app' },
  ];
```


### Crear un método en el servicio para retornar la lista

Ahora ve al archivo generado del servicio, encontrado en `src/app/todo-list.service.ts`, y agrega una función `getTodoList` que retorna el arreglo `todoList`. El servicio se verá así:

```javascript
import { Injectable } from '@angular/core';

@Injectable()
export class TodoListService {

  private todoList = [
    { title: 'install NodeJS' },
    { title: 'install Angular CLI' },
    { title: 'create new app' },
    { title: 'serve app' },
    { title: 'develop app' },
    { title: 'deploy app' },
  ];

  constructor() {
  }

  getTodoList() {
    return this.todoList;
  }
}
```

### Inyectar el servicio al componente `list-manager`

Después de crear la instancia del servicio, podemos inyectarlo a nuestro componente `list-manager`. Ve al archivo `src/app/list-manager/list-manager.component.ts` y agrega el siguiente código:

```javascript
import { TodoListService } from '../todo-list.service'; 
```

Y ahora úsalo en la clase `ListManagerComponent: Elimina el arreglo `todoList` pero guarda el miembro `todoList` y cambia el contructor a:

```javascript
constructor(private todoListService:TodoListService) { }
```

Y ahora `todoList` usará el servicio que creamos en la función **ngOnInit**:

```javascript
ngOnInit() {
    this.todoList = this.todoListService.getTodoList();
}
```
