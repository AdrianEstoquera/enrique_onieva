# Página personal en github pages:
# Table of Contents

- [Página personal en github pages:](#página-personal-en-github-pages)
  - [Estructura del proyecto](#estructura-del-proyecto)
  - [Características de la página web](#características-de-la-página-web)
    - [Actualizar información de mis publicaciones y index.html](#actualizar-información-de-mis-publicaciones-y-indexhtml)
    - [Añadir posts](#añadir-posts)
    - [Otros cambios:](#otros-cambios)
    - [Actualizar los cambios](#actualizar-los-cambios)
- [Github pages y github actions](#github-pages-y-github-actions)
  - [¿Que es github pages?](#qué-es-github-pages)
  - [Limitaciones de github pages](#limitaciones-de-github-pages)
  - [Publicar en github pages mediante github actions](#publicar-en-github-pages-mediante-github-actions)
  - [Entendiendo el archivo deploy.yml](#entendiendo-el-archivo-deployyml)
- [Servir esta pagina web en local](#servir-esta-pagina-web-en-local)
- [Cómo hacer que este sitio web se sirva desde tu propio perfil de github (y no el mio)](#cómo-hacer-que-este-sitio-web-se-sirva-desde-tu-propio-perfil-de-github-y-no-el-mio)
## Estructura del proyecto
```
/_includes
  - Plantillas HTML que suelen heredarse frecuentemente (header + footer).

/_layouts
  - Plantillas HTML que heredan y reciben el texto y estructura del Markdown para crear las páginas HTML que se muestran en la web personal.
  - Los markdowns con el contenido hacen referencia a alguna de estas plantillas

/_posts
  - Compilación de posts personales escritos en Markdown. Los títulos deben ser `[aaaa-mm-dd]-[titulo_de_post].md`.

/_site
  - Jekyll compilará en esta carpeta lo necesario para hacer la página web:
    - Creará páginas HTML que combinan la herencia de las distintas plantillas y el texto en Markdown.
    - Copiará los recursos (CSS, imágenes, etc.) que necesite.
    - Organizará las páginas HTML en carpetas para lograr la estructura de proyecto deseada.

/.github
  - /workflows: Workflow necesario para publicar la página en GitHub Pages.

/assets
  - /css: Archivos CSS.
  - /images: Imágenes.
  - /pdf: PDFs y documentos para descargar en la página de "publicaciones".

/_config.yml
  - Necesario para que Jekyll pueda gestionar las URLs.

/favicon.png
  - Icono de las pestañas del navegador.

/Gemfile
  - Dependencias (gems) de Ruby.

/index.md
  - Contenido de la página de inicio (index). Usa la plantilla "default".

/posts.html
  - Página HTML que busca los posts en la carpeta correspondiente y crea una página HTML con ellos.

/publicaciones.md
  - Contenido de la página de publicaciones. Enlaces a internet y documentos de la carpeta `/assets/pdfs/` para poder descargarlos.
```
## Características de la página web
Gracias a que la página web se compila con Jekyll, se logra separar el contenido de las páginas del HTML que le da estructura. Esto hace que actualizar la información sea muy sencillo. Se puede actualizar la informacion de 2 maneras:
### Actualizar información de mis publicaciones y index.html
Para hacer esto habría que cambiar el contenido de publicaciones.md y index.md respectivamente. Al actualizar los cambios en github, el contenido de la página se actualizará.
### Añadir posts
Para añadir un nuevo post, se debe añadir un nuevo documento markdown a la carpeta de posts y la plantilla HTML posts.html se encargará de buscarlo y añadir su contenido a una página HTML.
**Cada página .md puede tener embedidas imágenes, tablas, listas, etc. No es necesarias añadirlas como recursos en assests. Ahí solo van imagenes que usen las plantillas HTML. Como la que aparece en index.html de Enrique**
### Otros cambios:
También puede cambiarse la estructura HTML o el CSS
### Actualizar los cambios 
Una vez se han llevado a cabo los cambios deseados, es necesario subir el trabajo realizado a github. Pasados unos minutos la página personal se actualizará


## Github pages y github actions
### ¿Que es github pages?
GitHub Pages es un servicio gratuito proporcionado por GitHub para alojar sitios web estáticos directamente desde un repositorio. Al subir los archivos necesarios (HTML, CSS, JS o contenido generado por herramientas como Jekyll) a una rama específica, GitHub se encarga de servirlos públicamente como un sitio web. Es especialmente útil para portafolios, documentación o blogs estáticos.
### Limitaciones de github pages
GitHub Pages está diseñado exclusivamente para servir sitios estáticos, lo que significa que tiene limitaciones inherentes en comparación con servidores que ejecutan aplicaciones dinámicas. Aquí se detalla qué cosas puede hacer y qué cosas no puede hacer:
Qué puede hacer GitHub Pages
   1.  Servir contenido estático:
        Archivos HTML, CSS, JavaScript.
        Imágenes, documentos PDF, fuentes, y otros recursos estáticos.

   2.  Generar sitios estáticos con Jekyll:
        GitHub Pages puede compilar sitios escritos en Markdown o Liquid usando Jekyll, siempre que no utilicen plugins personalizados (solo los aprobados por GitHub).

  3. Redirecciones básicas:
        A través de archivos .html o configuraciones como meta refresh.

  4.   Hosting gratuito con HTTPS:
        Ofrece un certificado SSL automático para proteger las conexiones a tu sitio.

  5.   Optimización y caching:
        GitHub Pages optimiza automáticamente los archivos para que se carguen rápidamente y aplica caching para mejorar el rendimiento.

  6.  Integración con GitHub Actions:
        Puedes usar GitHub Actions para automatizar la compilación y despliegue del sitio.

Qué NO puede hacer GitHub Pages:
    Ejecutar código del lado del servidor:

1. No puede procesar lenguajes como:
            - PHP (por ejemplo, para generar contenido dinámico en el servidor).
            - Python (para aplicaciones como Flask o Django).
            - Node.js (para ejecutar JavaScript en el servidor).
            - Ruby (más allá de Jekyll, que se ejecuta antes del despliegue).
            - Ejemplo: No puedes realizar operaciones como consultar una base de datos en el servidor o procesar formularios directamente en GitHub Pages.

2. Interacción con bases de datos:
        No se puede conectar a bases de datos como MySQL, PostgreSQL, o MongoDB porque no hay un backend en ejecución.

3. Procesar formularios dinámicamente:
        Aunque puedes mostrar formularios HTML, no puedes procesarlos en el servidor. Para ello, necesitas servicios externos como:
            - Formspree.
            - Netlify Forms.

4. Autenticación de usuarios:
        No puedes manejar inicio de sesión, registro o autenticación de usuarios directamente, ya que requiere lógica del lado del servidor.

5. Realizar cálculos complejos en tiempo real:
        Sin un backend, no puedes realizar operaciones como cálculos matemáticos o generación de informes en tiempo real.

6. Streaming de datos:
        No es posible realizar tareas como transmisión de video/audio en tiempo real o WebSocket para aplicaciones en tiempo real.

7. Acceso a APIs privadas:
        Aunque puedes consumir APIs públicas desde JavaScript del lado del cliente, no puedes acceder a APIs privadas que requieren un token seguro sin exponerlo en el cliente.
### Publicar en github pages mediante github actions
GitHub Actions es el servicio de computacion que ofrece github. Este servicio recive archivos .yml con instrucciones y configuraciones que se ejecutarán en un servidor de github. En nuestro caso, nos va a permitir automatizar flujos de trabajo como la construcción y publicación de sitios web. En lugar de confiar en la rama gh-pages de manera manual, GitHub Actions permite compilar automáticamente el sitio (por ejemplo, usando Jekyll) y publicarlo en GitHub Pages cada vez que haya cambios en el repositorio.
Ventajas de usar GitHub Actions con GitHub Pages:
    - Automatización completa del flujo de trabajo.
    - Mayor flexibilidad, como usar versiones específicas de Ruby o personalizar el proceso de compilación.
    - Compatibilidad con plugins de Jekyll no permitidos en GitHub Pages, ya que la compilación ocurre en la acción, no en los servidores de GitHub Pages.
### Entendiendo el archivo deploy.ymlname: Deploy to GitHub Pages  # Nombre del flujo de trabajo que aparecerá en GitHub Actions
```
on:
  push:
    branches:
      - main  # Este flujo se ejecutará cada vez que haya un push en la rama principal (main)

jobs:
  deploy:  # Nombre del trabajo principal
    runs-on: ubuntu-latest  # Define el entorno en el que se ejecutarán las acciones (Ubuntu)

    steps:
    - name: Checkout code  # Paso 1: Descargar el código del repositorio
      uses: actions/checkout@v3  # Usa la acción oficial de GitHub para clonar el repositorio

    - name: Set up Ruby  # Paso 2: Configurar Ruby, necesario para ejecutar Jekyll
      uses: ruby/setup-ruby@v1  # Acción para instalar y configurar Ruby
      with:
        ruby-version: '3.3.6'  # Especifica la versión de Ruby que se utilizará

    - name: Install dependencies  # Paso 3: Instalar las dependencias de Jekyll
      run: |  # Ejecuta comandos en la terminal
        gem install bundler  # Instala Bundler, una herramienta para gestionar gemas
        bundle install  # Instala las dependencias especificadas en el archivo Gemfile

    - name: Build the site  # Paso 4: Construir el sitio con Jekyll
      run: |
        bundle exec jekyll build  # Usa Jekyll para generar los archivos estáticos en la carpeta `_site`

    - name: Deploy to GitHub Pages  # Paso 5: Publicar los archivos generados en GitHub Pages
      uses: peaceiris/actions-gh-pages@v3  # Acción para desplegar en GitHub Pages
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}  # Token de autenticación generado automáticamente por GitHub
        publish_dir: ./_site  # Especifica la carpeta que contiene los archivos estáticos generados por Jekyll
```
# Servir esta pagina web en local
Es muy útil visualizar esta página web de manera local para observar los cambios que se van realizando y cómo estos afectan a la apariencia o funcionalidad del sitio. Para hacerlo, debes seguir estos pasos:
## Instalar Ruby
1. Descargar e instalar Ruby:

    Ve a la página oficial de Ruby: https://rubyinstaller.org/.
    Descarga el instalador para Windows (la versión recomendada).
    Sigue las instrucciones del instalador. Asegúrate de marcar la opción "Add Ruby to PATH".

2. Verificar la instalación:

    Abre la terminal de comandos (cmd o PowerShell) y escribe:
   *ruby -v*
## Instalar Bundler:
Instalar Bundler: Bundler es una herramienta para gestionar las dependencias de Ruby. Para instalarlo, ejecuta el siguiente comando en tu terminal:
```
gem install bundler
bundler -v
```
## Instalar Jekyll
```
gem install jekyll
jekyll -v
```
## Clonar el repo.
## Instalar las dependencias del proyecto
Ejecuta el siguiente comando para instalar todas las dependencias necesarias:
```bundle install```
## Servir el sitio web de forma local
Una vez que todas las dependencias estén instaladas, ejecuta el siguiente comando para iniciar el servidor local de Jekyll:
```bundle exec jekyll serve```
**Esto compilará el sitio y lo servirá en un servidor local en la dirección http://localhost:4000.**

**Si nos fijamos en el deply.yml**, esto es más o menos lo que ese archivo de configuracion está haciendo del paso 2 al 4

# Cómo hacer que este sitio web se sirva desde tu propio perfil de github (y no el mio)

De esta forma se puede clonar un repositorio de GitHub y subirlo a tu propio perfil, cambiando la URL de `https://adrianestoquera.github.io/enrique_onieva/` a `https://enrique_onieva.github.io/enrique_onieva/` o similar.

## Paso 1: Clonar el repositorio

1. **Clonar el repositorio original**:
  Hay distintas formas pero una es esta (También se puede descargar en zip)
   ```bash
   git clone https://github.com/adrianestoquera/enrique_onieva.git
   ```

2. **Acceder a la carpeta del repositorio**:
   Después de clonar el repositorio, navega dentro de la carpeta del proyecto:
   ```bash
   cd enrique_onieva
   ```

---

## Paso 2: Crear un nuevo repositorio en tu cuenta de GitHub

1. **Iniciar sesión en GitHub**:
   Inicia sesión en tu cuenta de GitHub.

2. **Crear un nuevo repositorio**:
   - Ve a [GitHub](https://github.com/) y haz clic en el botón **New** (Nuevo) en la parte superior derecha.
   - Asigna el nombre `enrique_onieva` al nuevo repositorio.
   - **No inicialices el repositorio** con README ni con ningún archivo `.gitignore` ni licencia (esto es importante para evitar conflictos con el repositorio clonado).
   - Haz clic en **Create repository** (Crear repositorio).

---




## Paso 3: Configurar GitHub Actions para la publicación

Tu archivo `deploy.yml` está configurado para publicar el sitio automáticamente mediante **GitHub Actions**. Asegúrate de que este archivo esté ubicado en la carpeta `.github/workflows/` en tu repositorio.
Este flujo de trabajo de **GitHub Actions** se ejecutará cada vez que haya un cambio en la rama principal (`main`), construirá el sitio web con **Jekyll** y lo publicará automáticamente en **GitHub Pages**.

## Paso 4: Subir los archivos a tu repositorio


---

## Paso 5: Habilitar GitHub Pages

1. **Ir a la configuración del repositorio**:
   - Ve a tu repositorio en GitHub: `https://github.com/enrique_onieva/enrique_onieva`.
   - Haz clic en la pestaña **Settings** (Configuración).

2. **Habilitar GitHub Pages**:
   - En la barra lateral, busca la sección **Pages**.
   - En **Source**, selecciona la rama `main` y la carpeta `/ (root)` si no está seleccionada por defecto.
   - Haz clic en **Save** (Guardar).

3. **Esperar la publicación**:
   GitHub comenzará a procesar el sitio. Este proceso puede tomar unos minutos. Una vez que esté listo, verás un enlace a tu página en la misma sección de **Pages**.

---

## Paso 7: Acceder a tu página web

Una vez que GitHub termine de procesar el sitio, podrás acceder a tu página en la siguiente URL:
```
https://enrique_onieva.github.io/enrique_onieva/
```
