# Despliega tus aplicaciones a Github Pages

Para desplegar nuestros cambios a Github pages, vamos a utilizar el paquete [angular-cli-ghpages](https://github.com/angular-buch/angular-cli-ghpages)

* Necesitas tener un usuario Github
* Necesitas crear un repositorio para tu proyecto.
* Necesitas guardar todos los cambios que haces en el proyecto en git
* Necesitas instalar `angular-cli-ghpages`  

## Crear un usuario Github
> Si tu ya tienes un usuario Github puedes saltar este paso.

Para crear un usuario en Github ve a:  https://github.com/
Llena el formulario de registro y asegúrate de validar tu dirección de correo electrónico.

## Crea un repositorio para tu proyecto.
Después de acceder a Github.

Da click en `Iniciar un proyecto` y nombra el repositorio `ng-girls-todo` o cualquier nombre que quieras.

## Conectando tu repositorio

Guarda todos los cambios en git ejecutando este comando en tu directorio de proyecto.

```
git add -A && git commit -m "Your Message"
```

Ejecuta el siguiente comando para conectar tu código al repositorio.
Asegúrate de reemplazar {YOUR_USERNAME} y {YOUR_REPO} con tu nombre de usuario y nombre de repositorio.

```
git remote add origin https://github.com/{YOUR_USERNAME}/{YOUR_REPO}.git
git push -u origin master
```

## Desplegar a Github pages
Primero instala `angular-cli-ghpages`

```
npm i -g angular-cli-ghpages
```

Luego solo ejecuta:

```
ng build --prod --base-href="/[your-repo-name]/"
angular-cli-ghpages
```

Tu página debería estar disponible en https://{YOUR_USERNAME}.github.io/{YOUR_REPO}

Para mas información mira [https://github.com/angular-buch/angular-cli-ghpages.]https://github.com/angular-buch/angular-cli-ghpages.() 
