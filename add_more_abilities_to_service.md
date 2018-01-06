# Agrega mas características al servicio

En esta capítulo vamos a mejorar nuestro servicio agregando nuevas características.

Primero, vamos a abrir nuestro archivo de servicio, el cual está en `app/todo-list.service.ts`

Aquí vamos a agregar una nueva función al servicio llamada `addItem`, así:

```javascript
addItem(item): void { 
    this.todoList.push(item); 
} 
```

Esto nos permitirá llamar a la misma función desde cualquier lugar en la aplicación, además de hacerlo mas fácil de mantener.

Y ahora vamos a cambiar nuestro código en `app/list-manager/list-manager.component.ts` para llamar la función `addItem` directamente desde el servicio así:

```javascript
addItem(item): void { 
    this.todoListService.addItem(item); 
} 
```

- Puede haber lógica adiciona cuando llamamos a estos métodos, por ejemplo, guardando los cambios en la base de datos (lo implementaremos después)
- Una mejor manera de manejar la información es usando objetos inmutables, entonces no hay enlace - las referencias cambiarán (pero no vamos a implementar redux en este tutorial por el momento).
