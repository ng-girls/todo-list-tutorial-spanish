# Generando un nuevo proyecto

En cada proyecto existen diferentes maneras de comenzar, la mayoría de ellas incluyen asistentes como Yeoman o Slush. Estas herramientas generan un proyecto inicial, ayudándonos con los archivos necesarios, y se ocupan de la compilación y ejecución del proyecto.

Otras maneras de comenzar es usando kits de inicio, también llamados proyectos semilla, los cuales contienen todo lo que tu puedas necesitar para comenzar un proyecto. A diferencia de los asistentes, los kits de inicio son relevantes únicamente para proyectos iniciales. Despuś de a instalación posiblemente no vuelvas a usar el kit de nuevo (si es un buen kit de inicio, posiblemente vuelvas a la documentación).

La mejor manera de comenzar con Angular es utilizar Angular CLI, el cual es un asistente. Nosotros lo usaremos en este tutorial.

En este capítulo nosotros veremos todos los archivos y las carpetas que son creadas por Angular CLI cuando creas un nuevo proyecto. Comenzaremos con una cción importante: cambiar el prefijo de la aplicación.

### Prefijo de aplicación

El prefijo de aplicación es usado para diferenciar los componentes que tu creas en tu aplicación de los componentes que usas de otras fuentes, y de los componentes HTML. Puedes dar tus iniciales como prefijo si es un proyecto principal. Si estás colaborando o trabajando para un cliente, puedes tener las iniciales del proyecto como prefijo. En este tutorial usaremos simplemente el prefijo `todo`.

Angular CLI genera un archivo de configuración para su propio uso: `angular-cli.json`. Abre este archivo, encuentra la propiedad `prefix` y cambia su valor de `app` a `todo`. De ahora en adelante, cada componente y directiva que crees usando Angular CLI tendrá su propio prefijo en su selector.

Nosotros podemos definir el prefijo cuando creamos el proyecto, agregando `--prefix <prefix>`. Incluso el componente raiz es generado usando este prefijo. Pero nosotros estamos bien con el selector actual `app-root`, y no lo vamos a cambiar en el momento.

### Estructura de la aplicación

El primer paso para comenzar cuando trabajas con Angular es crear el proyecto inicial. Para hacer esto, simplemente crea una carpeta y escribe `ng init`. Desde este punto Angular CLI descargará las dependencias y las intalará. Otra manera de iniciar el proyecto es escribiendo `ng new <nombre_del_proyecto>` y Angular CLI creará la carpeta por ti y hará `ng init` en esa carpeta.

Después de haber creado el proyecto, vamos a tener esta estructura de archivos:

```
├── angular-cli.json // angular cli configuration
├── e2e // end to end testing
├── karma.conf.js // testing configuration file
├── package.json // package configuration file
├── protractor.conf.js // testing configuration file
├── README.md // your readme
├── src // your code in here
│   ├── app
│   │   ├── app.component.css
│   │   ├── app.component.html
│   │   ├── app.component.spec.ts
│   │   ├── app.component.ts
│   │   ├── app.module.ts
│   │   └── index.ts
│   ├── assets // pictures etc
│   ├── environments // environments variables
│   │   ├── environment.prod.ts
│   │   └── environment.ts
│   ├── favicon.ico // the browser icon
│   ├── index.html
│   ├── main.ts
│   ├── polyfills.ts
│   ├── styles.css
│   ├── test.ts
│   ├── tsconfig.json // typescript configuration
│   └── typings.d.ts
└── tslint.json // linting configuration
```

Vamos a saltarnos todos los archivos de configuración por ahora y enfocarnos en la estructura de carpetas. 

App es el componente principal de la aplicación, desde este punto iniciaremos nuestra aplicación. cubriremos los componentes mas profundamente después en este tutorial, pero la idea principal de un proyecto es que construyas componentes y los conectes entre ellos hasta tener una aplicación.

Con Angular CLI podemos generar componentes y algunos otros archivos que pueden ayudarnos en el futuro. para hacer eso deberíamos escribir  `ng generate component <nombre_del_componente>` y `ng generate route <ruta>` para las rutas y muchas cosas mas que pueden ser revisadas en [la documentación oficial](https://github.com/angular/angular-cli#generating-components-directives-pipes-and-services)

Ahora probablemente te estés preguntando ¿cómo ver y revisar tu aplicación? Tu comando serán `ng serve` y tendrás acceso a la aplicación e `http://localhost:4200`  y lo último, pero no menos importante, si quieres construir tu aplicación para producción es que deberías escribir `ng build` y ya lo tendrás, un asistente completo para tu aplicación
and last but not least if you want to build your application for production you should write `ng build` and there you have it, easy way to scaffold you Angular application

