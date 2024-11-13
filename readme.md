# Tutorial: Configuración de Proyecto Frontend con Vite, Bootstrap 5 y SASS

En este tutorial, configuraremos un entorno de desarrollo frontend utilizando **Vite**, **Bootstrap 5** y **SASS**, con la estructura de archivos en la carpeta `src`. Te guiaré desde la instalación inicial hasta el despliegue.

## Paso 1: Configurar el Proyecto en Node.js

1. **Crea una carpeta para el proyecto**  
   Abre la terminal y crea una carpeta para el proyecto. Luego, navega dentro de ella:
   ```bash
   mkdir proyecto-bootstrap
   cd proyecto-bootstrap
   ```

2. **Inicializa el proyecto Node.js**  
   Esto generará un archivo `package.json` para gestionar las dependencias:
   ```bash
   npm init -y
   ```

3. **Instala Vite, Bootstrap y SASS**  
   Vite actuará como servidor de desarrollo y empaquetador, mientras que Bootstrap y SASS permitirán personalizar los estilos:
   ```bash
   npm install vite bootstrap
   npm install -D sass
   ```

## Paso 2: Organiza la Estructura de Carpetas

Configura una estructura de carpetas básica para organizar el proyecto:
```
proyecto-bootstrap
├── public
│   ├── imagen.png
│   └── favicon.ico
├── src
│   ├── index.html
│   ├── styles
│   │   ├── custom.scss
│   │   └── bootstrap.scss
│   └── main.js
├── package.json
└── vite.config.js
```

- **public**: Carpeta para archivos públicos como imágenes e íconos.
- **index.html**: Página principal.
- **styles/custom.scss**: Archivo donde puedes definir tus estilos personalizados.
- **styles/bootstrap.scss**: Archivo donde importarás Bootstrap y sobrescribirás variables.
- **main.js**: Archivo JavaScript principal.
- **vite.config.js**: Archivo para configuración de Vite.

## Paso 3: Configura los Archivos

1. **index.html**  
   En `src/index.html`, enlaza los archivos CSS y JavaScript que serán procesados por Vite:
   ```html
   <!DOCTYPE html>
   <html lang="es">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Página con Bootstrap 5 y SASS</title>
       <link rel="stylesheet" href="/styles/bootstrap.css">
   </head>
   <body>
       <div class="container">
           <img src="imagen.png" alt="Imagen desde public" class="img-fluid">
           <h1 class="text-primary">Hola, Bootstrap 5!</h1>
           <p>Esta es una página de ejemplo con estilos personalizados.</p>
       </div>
       <script type="module" src="/main.js"></script>
   </body>
   </html>
   ```

2. **bootstrap.scss**  
   En este archivo, importa Bootstrap directamente desde `node_modules` y sobrescribe variables si lo deseas:
   ```scss
   // src/styles/bootstrap.scss

   // Sobrescribe variables de Bootstrap
   $primary: #3498db;

   // Importa Bootstrap desde node_modules
   @import "bootstrap/scss/bootstrap";
   ```

3. **custom.scss**  
   Añade tus propios estilos personalizados aquí para definir ajustes adicionales:
   ```scss
   // src/styles/custom.scss

   body {
       font-family: Arial, sans-serif;
   }

   .container {
       margin-top: 20px;
   }
   ```

4. **main.js**  
   Importa los archivos de estilo en `main.js` para que Vite los procese y genere el CSS:
   ```javascript
   // src/main.js

   import './styles/bootstrap.scss';
   import './styles/custom.scss';
   ```

5. **vite.config.js**  
   Para indicarle a Vite que la carpeta de origen de los archivos es `src`, crea el archivo `vite.config.js` en la raíz del proyecto con el siguiente contenido:
   ```javascript
   import { defineConfig } from 'vite';
   import path from 'path';

   export default defineConfig({
    root: path.resolve(__dirname, 'src'),
    publicDir: path.resolve(__dirname, 'public'),
       resolve: {
           alias: {
               '@': path.resolve(__dirname, 'src'),
           },
       },
   });
   ```

## Paso 4: Ejecuta el Servidor de Desarrollo

1. **Agrega un Script para Vite en `package.json`**  
   Añade un script en el archivo `package.json` para ejecutar el servidor de desarrollo:
   ```json
   "scripts": {
       "dev": "vite",
       "build": "vite build"
   }
   ```

2. **Ejecuta el Servidor de Desarrollo**  
   Ahora, ejecuta el servidor de desarrollo con el siguiente comando. Esto abrirá la página en tu navegador y se recargará automáticamente con cada cambio:
   ```bash
   npm run dev
   ```

   La página se abrirá automáticamente en `http://localhost:3000`, y verás el mensaje "Hola, Bootstrap 5!" con los estilos personalizados.

## Paso 5: Compilación para Producción

Cuando hayas terminado el desarrollo, genera los archivos optimizados para producción con el siguiente comando:
```bash
npm run build
```
Esto generará una carpeta `dist` con todos los archivos listos para su despliegue.

---

## ¿Qué es SASS y Cuáles son sus Características Más Relevantes?

**SASS (Syntactically Awesome Stylesheets)** es un preprocesador de CSS que permite escribir estilos de manera más eficiente y organizada. Algunas de sus características más relevantes son:

1. **Variables**: Puedes definir variables para almacenar colores, fuentes, tamaños, etc., lo cual facilita la reutilización y mantenimiento de los estilos.
   ```scss
   $primary-color: #3498db;
   body {
       color: $primary-color;
   }
   ```

2. **Anidamiento**: Permite anidar selectores, haciendo que el código sea más legible y refleje mejor la estructura HTML.
   ```scss
   .container {
       .header {
           color: #333;
       }
   }
   ```

3. **Mixin**: Los mixins permiten reutilizar bloques de código, lo cual es muy útil para evitar la repetición.
   ```scss
   @mixin flex-center {
       display: flex;
       justify-content: center;
       align-items: center;
   }
   .box {
       @include flex-center;
   }
   ```

4. **Extends**: Puedes extender un selector para reutilizar sus estilos en otro. A diferencia de los mixins, `@extend` permite compartir estilos sin necesidad de repetir el código, pero tiene limitaciones cuando se usa en contextos complejos. Mientras que los mixins permiten incluir bloques de código reutilizable con mayor flexibilidad, `@extend` es útil para heredar estilos de un selector base sin aumentar el tamaño del archivo CSS.
   ```scss
   %button-style {
       padding: 10px;
       border-radius: 5px;
   }
   .btn-primary {
       @extend %button-style;
       background-color: $primary-color;
   }
   ```

5. **Funciones**: SASS incluye funciones integradas y también permite definir funciones personalizadas para manipular valores como colores y tamaños. Por ejemplo, se puede utilizar la función `lighten()` para aclarar un color:
   ```scss
   $primary-color: #3498db;
   .box {
       background-color: lighten($primary-color, 20%);
   }
   ```
   También se pueden crear funciones propias para realizar cálculos específicos:
   ```scss
   @function double($number) {
       @return $number * 2;
   }
   .container {
       width: double(10px);
   }
   ```

Estas características permiten escribir CSS más modular, mantenible y eficiente, mejorando la productividad y organización del código.

## ¿Qué es Vite y Cuáles son sus Ventajas?

**Vite** es una herramienta de desarrollo rápida y moderna que actúa como servidor de desarrollo y empaquetador. Fue creada por el autor de Vue.js y está diseñada para proporcionar una mejor experiencia en el desarrollo frontend. Algunas de las ventajas de trabajar con Vite son:

1. **Inicio de Desarrollo Súper Rápido**: Vite aprovecha módulos ES nativos del navegador, lo que hace que el tiempo de arranque sea casi instantáneo, incluso en proyectos grandes.

2. **Recarga en Caliente (HMR)**: Vite tiene un sistema de recarga en caliente extremadamente rápido, lo que significa que los cambios en el código se reflejan inmediatamente en el navegador sin necesidad de recargar toda la página.

3. **Compatibilidad con Múltiples Frameworks**: Vite es compatible con Vue, React, Svelte, y también con proyectos sin framework específico.

4. **Empaquetado para Producción Optimizado**: Utiliza **esbuild** y **Rollup** para empaquetar los archivos para producción de manera rápida y eficiente, generando un código optimizado.

## ¿Cómo Maneja las Rutas Vite?

Vite tiene una manera específica de manejar las rutas que facilita la importación de módulos y archivos:

1. **Importación desde `node_modules`**: Si importas un módulo sin prefijo (`@import "bootstrap/scss/bootstrap"`), Vite lo buscará automáticamente en `node_modules`.

2. **Rutas Relativas (`./`)**: Cuando usas `./` al inicio de una ruta, Vite busca el archivo relativo a la ubicación del archivo actual. Por ejemplo, `@import "./custom.scss"` buscará `custom.scss` en la misma carpeta que el archivo que lo importa.

3. **Rutas Absolutas (`/`)**: Las rutas que comienzan con `/` son relativas a la raíz del proyecto. Esto es útil para organizar las importaciones de una manera más clara y evitar problemas con rutas complicadas.

Estas características hacen que trabajar con Vite sea muy conveniente, ya que simplifica la configuración y mejora la velocidad y eficiencia del desarrollo.

## Gestión de Archivos Públicos

Para gestionar los archivos públicos en un proyecto con Vite, deberías incluir una carpeta llamada `public` en la raíz del proyecto. Todos los archivos en esta carpeta se copiarán tal cual a la carpeta de compilación (`dist`) y estarán disponibles en la URL raíz.

1. **Crea la Carpeta `public`**  
   En la raíz de tu proyecto, crea una carpeta llamada `public`:
   ```
   proyecto-bootstrap
   ├── public
   │   ├── imagen.png
   │   └── favicon.ico
   ├── src
   ├── package.json
   └── vite.config.js
   ```

2. **Accede a los Archivos Públicos**  
   Puedes acceder a los archivos dentro de la carpeta `public` directamente desde el HTML o el JavaScript sin necesidad de importar o especificar rutas complejas:
   ```html
   <img src="/imagen.png" alt="Imagen desde public">
   ```

3. **Propósito**  
   La carpeta `public` es ideal para archivos estáticos que no necesitan ser procesados ni empaquetados, como imágenes, íconos, o cualquier otro recurso que desees mantener accesible y sin cambios durante la fase de construcción.

Esto hace que la gestión de archivos públicos con Vite sea fácil y conveniente, manteniendo todos los recursos estáticos bien organizados y accesibles.

## Diferencia entre Dependencias de Desarrollo y Producción

En un proyecto Node.js, las dependencias se dividen en dos categorías principales: **dependencias de producción** y **dependencias de desarrollo**. Esta distinción es importante para gestionar qué paquetes son necesarios durante el desarrollo y cuáles lo son en producción.

1. **Dependencias de Producción** (`dependencies`)  
   Estas son las dependencias necesarias para que la aplicación funcione en producción. Incluyen paquetes que se utilizan directamente en el código de la aplicación, como frameworks (por ejemplo, React, Express) y bibliotecas de utilidad. Cuando despliegas tu aplicación, solo las dependencias de producción se instalan para reducir el tamaño del proyecto.

2. **Dependencias de Desarrollo** (`devDependencies`)  
   Estas son las dependencias que solo se necesitan durante el proceso de desarrollo, pruebas y construcción del proyecto. Incluyen herramientas como Vite, linters (ESLint), transpiladores (Babel), y otros paquetes utilizados para compilar o empaquetar el código. No son necesarias para que la aplicación funcione en producción, por lo que se excluyen en el despliegue.

Por ejemplo, **SASS** y **Vite** se instalan como dependencias de desarrollo porque solo son necesarias para compilar y construir el proyecto antes de su despliegue, mientras que **Bootstrap** se instala como dependencia de producción ya que es parte del estilo final de la aplicación.

## Extensiones Recomendadas para Visual Studio Code

Para mejorar la productividad, estas extensiones son muy útiles en **VSCode**:

1. **Live Sass Compiler**  
   Aunque Vite ya compila SASS, esta extensión es útil para ver errores y realizar compilaciones de prueba.

2. **Prettier**  
   Para mantener el código limpio y consistente, esta extensión formatea el código automáticamente.

3. **ESLint**  
   Ayuda a detectar errores en el JavaScript y garantiza que sigas buenas prácticas de codificación.

4. **VSC Bootstrap 5 Snippets**  
   Proporciona fragmentos de código rápidos de Bootstrap 5, facilitando el desarrollo con los componentes de Bootstrap.

5. **Auto Rename Tag y CSS Peek**  
   - **Auto Rename Tag**: Cambia las etiquetas HTML de apertura y cierre de manera sincronizada.
   - **CSS Peek**: Permite ver definiciones CSS y SASS directamente desde el HTML.

6. **Path Intellisense**  
   Autocompleta rutas de archivos, útil para evitar errores al escribir rutas relativas.

