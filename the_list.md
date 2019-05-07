# La lista

Ahora vas a agregar la lista en sí al componente  `app-root`. Abre el archivo `src/app/app.component.ts`. Agrega la lista de elementos dentro de la clase `AppComponent` como un areglo de objetos por cada elemento. En este punto, cada elemento solo tendrá un título:

```js
todoList = [
  {title: 'install NodeJS'},
  {title: 'install Angular CLI'},
  {title: 'create new app'},
  {title: 'serve app'},
  {title: 'develop app'},
  {title: 'deploy app'},
];
```

> Colocar información (recursos) dentro del código es llamado `hardcoding` y se considera una mala práctica. Eventualmente, vamos a obtener esta lista de otro recurso, pero incluso esto no es mejor manera de almacenar la información en nuestros propios archivos. Pero vamos a avanzar paso por paso, así que definiremos elementos de esta manamera por ahora.

Ahora debemos decirle al navegador que muestre estos elementos. Para esto, vas a usar la directiva incluida en Angular `*ngFor`. Esto funciona como un ciclo for de Java mejorado. `*` es una notación semántica necesaria la cual hace que Angular use el elemento actual como plantilla cuando renderiza la lista.

Enserta el ciclo justo después de `<todo-input></todo-input>`, de esta manera:

```html
<todo-input></todo-input>
<ul>
  <li *ngFor="let item of todoList">
    {{ item.title }}
  </li>
</ul>
```

Esto significa "recorre todos los elementos del arreglo todoList definido abajo e imprimer una lista sin numeración que contenga los títulos de los elementos". Mientras iteramos sobre `todoList`, cada elemento es asignado a la variable `item`, y podemos usar esta variable dentro del elemento `li` y sus hijos.

### Directivas Angular 

Las directivas son piezas de lógica (escritas como clases) que pueden ser adjuntas a elementos y componentes. Ellas se usan para cambiar la disposición o comportamiento de un elemento. Angular vienen con algunas directivas incluidas.

Como vimos, la directiva `ngFor` modifica la plantilla en tiempo de ejecución repitiendo el elemento que es llamado y su contenido. Otra directiva, por ejemplo es `ngIf`, la cual recive una expresión booleana. Solamente si la expresión es verdadera, se renderiza el elemento y su contenido. Esto también necesita el prefijo `*` porque usa el elemento apuntado como plantilla, similarmente a la directiva `*ngFor`. Por ejemplo:

```html
<h1 *ngIf="userLoggedIn">Welcome!</h1>
```

En este ejemplo, `userLoggedIn` debería ser un miembro del componente, y tener un valor `true` o `false`. Si es `true`, el elemento será mostrado. Si es `false` el elemento no existirá en el DOM.

Hay otras directivas en Angular las cuales no son estructurales (y son usadas sin el `*`). Por ejemplo `ngStyle` y `ngClass`, las cuales pueden aplicar estilos y clases dinámicamente al elemento. 
