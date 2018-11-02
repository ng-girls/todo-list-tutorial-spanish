# Reconstruir App Component

Vamos a realizar un pequeño cambio. El `app-root` no debería tener una plantilla muy larga y decir toda su lógica. Debería solamente llamar otro componente que maneje eso.

* Crea un nuevo componente llamado `list-manager`:
  `ng g c list-manager -it`
* Mueve todo el código de `appComponent` a `listManager`
* Llama al nuevo compoente desde la plantilla `appComponent`:

```
`
  <todo-list-manager></todo-list-manager>
`
```

Eso es todo, podemos continuar.

