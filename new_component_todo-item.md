# Nuevo componente todo-item

Vamos a crear un nuevo componente el cual será usado para cada elemento que será mostrado en la lista. Será un simple componente, al comienzo, pero crecerá después. Lo que es importante es que **tomará el el elemento todo como un input para su componente padre**. De esta manera será un componente reusable, y no dependerá directamente de la información de la aplicación y el estado.

Create un nuevo componente llamado `item`:

```
ng g c item -it
```

Puedes ver que una nueva carpeta ha sido creada con los archivos del componente dentro.

Usa el componente en la plantilla de `appComponent` - dentro del elemento `<li>`:

```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item></todo-item>
  </li>
</ul>
```

Verifica el resultado en el navegador. ¿Qué ves? ¿Por qué?

## @Input()

Queremos mostrar el título de cada elemento en el componente `todo-item`. Necesitamos pasar el título del elemento actual en el ciclo (o el elemento completo) al componente `todo-item`.

De nuevo, Angular lo hace bastante fácil por nosotros, al proveernos el decorador `Input`.

Dentro de la clase generada `itemComponent` agrega la línea.

```ts
@Input() itemTitle: string;
```

Esto le dice al componente que espere una entrada de tipo `string` y la asigne al miembro de la clase `itemtitle`. Asegúrte de que `Input` esté agregada en la sentencia `import` en la primera lína del archivo. ahora podemos usarlo dentro de la plantilla `itemComponent`:

```html
{{ itemTitle }}
```

Puedes agregar otros elementos HTML que quieras aquí.

Ahora vamos a pasarle la cadena, la cual es el título del elemento, la cual usaremos en el componente. Va atrás a `appComponent` y pasa el elemento `title` a `todo-item`:

```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item [itemTitle]="item.title"></todo-item>
  </li>
</ul>
```

El `itemTitle` que aquí está en corchetes, es el mismo declarado en el componente `@Input`.

¡Nosotros usamos enlace de propiedades en un elementoq que creamos nosotros mismos! Y ahora podemos ver y entender en enlace de propiedades a la propiedad del componente.

## Pasando el elemento completo

Vamos a reconstruir nuestro código un poco nuestro código para que podamos implementar mas funcionalidad en el componente `todo-item`, por ejemplo, editando y eliminando el item. En lugar de pasarle solo el título del componente, vamos a pasarle el elemento completo, y vamos a extraer del componente el título cuando lo necesitemos.

En `itemComponent` cambia la interpolación en la plantilla a :

```html
{{ todoItem.title }}
```

Renombra el miembro `Input` y cambia su tipo:

```ts
@Input() todoItem: any;
```

Ahora pasa el objeto completo a la propiedad renombrada en `appComponent` (quita el `.title`):

```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item [todoItem]="item"></todo-item>
  </li>
</ul>
```

Ahora tenemos una lista de componentes, entonces cada componente recibe la información del ciclo en el componente padre. Ahora vamos a er como esta lista puede ser dinámica.
