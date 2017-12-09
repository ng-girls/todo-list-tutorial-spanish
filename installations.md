# Instalación

Cada desarrollador necesita un conjunto de herramientas y librerías para comenzar a trabajar. En nuestro caso, vamos a instalar todas las herramientas necesarias, y una vez tengamos nuestro Angular CLI instaladovamos a tomar en cuenta librerías adicionales que necesitaremos para futuros proyectos.

## Herramientas

### Navegador

Nuestra primera herramienta va a ser el **navegador**. Veremos el resultado de nuestro trabajo y lo depuraremos. Nosotros recomendamos [Google Chrome](https://www.google.com/chrome/browser/desktop/) - tiene herramientas de desarrollo muy buenas. [Firefox](https://www.mozilla.org/en-US/firefox/new/) también es increible. Si no tienes alguno de estos, solo da click en el vínculo y sigue las instrucciones para descargar e instalar el navegador de tu elección.

### IDE

Nuestra siguiente herramienta es el **IDE** (Ambiente Integrado de Desarrollo (en Inglés)). Es un software que nos ayuda a escribir código. los IDEs puede hacer muchas cosas maravillosas como:

* Pintar el código, así es fácil identificar expresiones.
* Sugerir código así es más fácil identificar expresiones.
* Ayudar a navegar fácilmente a través de archivos en tus proyectos.
* Y mucho más ...

JetBrains [Webstorm](https://www.jetbrains.com/webstorm/download/) es uno de los IDEs mas fuertes en el mercado, Puedes conseguir el primer mes gratis y una licencia totalmente gratis si eres estudiante.

Microsoft [Visual Studio Code](https://code.visualstudio.com/) es también una gran elección que ha ganado popularidad últimamente. Es completamente gratis para individuos.

Escoge un IDE con el que te guste trabajar y sigue las instrucciones de instalación en su sitio web.

**Visual Studio Code**

Si escoget VSCode, te recomendamos instalar los siguientes plugins para angular:

- [Angular.ng-template](https://marketplace.visualstudio.com/items?itemName=Angular.ng-template)
- [natewallace.angular2-inline](https://marketplace.visualstudio.com/items?itemName=natewallace.angular2-inline)

![image](https://user-images.githubusercontent.com/1223799/30781828-88bf447c-a126-11e7-9128-4c1cdec4002c.png)

### Git

Git es una herramienta que te ayuda a manejar las versiones de tu código y trabajar en colaboración con miembros del equipo. Hay mucho que aprender sobre el, pero en este tutorial vamos a cubrir únicamente lo básico.

Puedes descargar y seguir las instrucciones de instalación [aquí](https://git-scm.com/).
Cuando te pregunten si instalar **git bash**, di si.

### Github
[Github](https://github.com/) es un sitio web de repositorios de código, el cual se integra con Git. Te permite publicar tu proyecto en la web, copiar otros proyectos de código abierto y colaborar. Para poder publicar tu proyecto, asegúrate de tener una cuenta en el sitio web de Github (Es gratuito, obviamente).

### NodeJS y NPM

**Por favor revisa la [documentación de Angular CLI](https://github.com/angular/angular-cli#prerequisites) para tener los prerequerisitos actualizados**

Otra gran herramienta que muchos desarrolladores web están usando en **NodeJS**. Una vez instalado, viene con una herramienta llamada **NPM** (Node Package Manager).

NodeJS te permite ejecutar código JavaScript en tu computador. Es usado para ejecutar servidores locales que sirven los archivos del proyecto en el navegador y simula un sitio web real ejecutándose.

NPM te permite fácilmente descargar e instalar diferentes librerías de internet y manejar sus versiones.

Descarga NodeJS [aquí](https://nodejs.org/en/).

Si tu ya tienes NodeJS instalado, asegúrate que tengas la versión 6.9.0 o superior ejecutando el siguiente comando en tu terminal:

```
node -v
```
\('-v' significa 'version'.\)  

Si la versión es inferior a la requerida, descarga la nueva versión del sitio web para instalarla.

Una vez instalada, puedes verificar que NPM está instalado. Verifica esto escribiendo:

```
npm -v
```


### Angular-CLI

[Angular-CLI](https://github.com/angular/angular-cli) es una herramienta poderosa que simplifica mucho el proceso de desarrollo. También instala librerías que tu usarás en tu proyecto actual y también en futuros. Instalalo ejecutando:

```
npm i -g @angular/cli
```

Este comando ejecuta NOM que recientemente instalamos aquí - el sabe encontrar el paquete (angular-cli) que estás buscando por el nombre que tu proveas.
El parámetro 'i' es una abreviación para 'install'
El parámetro '-g', significa 'global' - nos gustaría tener esta herramienta instalada globalmente en el computador, así que la podremos usar desde cualquier carpeta para crear futuros proyectos.

Lee mas sobre Angular-CLI en la siguiente sección.

### Crear un proyecto

Primero, creemos una carpeta para almacenar todos tus proyectos, por ejemplo _misProyectos_, y luego ve a esa carpeta usando una terminal (ventana de línea de comandos):

```
cd ruta-a-tu-carpeta/misProyectos
```

Ahora creemos un nuevo proyecto llamado _lista-de-tareas_ dentro de la carpeta del proyectos, usando Angular-CLI, ejecutando el siguiente comando:
```
ng new lista-de-tareas --prefix=todo
```
Esto puede tomar un poco de tiempo, desde que muchos paquetes están siendo descargados e instalados.
El prefijo 'todo' será usado en cada componente que creemos. El prefijo por defecto (si no utilizas la bandera `--prefix`) es 'app'.

Ahora entremos a la nueva carpeta que Angular-CLI ha creado para este proyecto

```
cd todo-list
```
Una vez dentro de esta carpeta de aplicacieon, ejecuta la aplicación usando los siguientes comandos:
```
ng serve -o
```
La bandera `-o` es una abreviatura de `--open`, la cual abrirá tu navegador en la URL correcta: [`localhost:4200`](http://localhost:4200)

Deberías ver algo como esto:

![image](https://github.com/bluebirrrrd/todo-list-tutorial/blob/master/assets/installation-result.png)

### ¡Felicitaciones!

¡Tienes una aplicación de Angular! **Siempre que tengas una aplicación ejecutándose, deberías tener el terminal donde la abriste abierto**. Cualquier cambio que realices en el proyecto, será reflejado inmediatamente en el navegador web.

Puedes abrir otra terminal para ejecutar tareas en paralelo.

Puedes terminar la aplicación, presionando `Ctrl+C` en el terminal, o cerrar el terminal.

¡Ahora estamos listos para comenzar a desarrollar!.
