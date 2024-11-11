# Creacion-de-un-Proyecto-Angular

## Paso 1: Instalar la última versión de Angular CLI
Para asegurarte de tener la última versión de Angular que soporta componentes standalone y las nuevas directivas:

## Paso 2: Crear el Proyecto Angular
Ejecuta el siguiente comando en la terminal para crear un nuevo proyecto standalone:

## Creación del Proyecto
1. Instalamos la última versión de Angular CLI con `npm install -g @angular/cli@latest`.
2. Creamos el proyecto con `ng new nombre-proyecto --standalone`.
   - La opción `--standalone` permite utilizar componentes independientes, eliminando la necesidad de módulos.

## Configuración de Componentes Standalone
- Usamos `ng generate component HomeComponent --standalone` para crear componentes independientes.
- Los componentes standalone simplifican la arquitectura, eliminando la necesidad de módulos para cada componente.

## Uso de `@if` y `@for`
Angular permite manejar condicionales y bucles de forma eficiente:
- `*ngIf`: para mostrar contenido basado en una condición.
- `*ngFor`: para iterar sobre una lista y mostrar sus elementos en pantalla.

Ejemplo:
```html
<section *ngIf="mostrarContenido">
  <p>Este contenido se muestra bajo una condición.</p>
</section>
por un 
@if (mostrar contenido) {
  <p>Este contenido se muestra bajo una condición.</p>
}

<section *ngFor="let item of listaElementos">
  <p>{{ item }}</p>
</section>
por un 
@for (item of listaElementos; track item.name) {
<li>{{ item.name }}</li>
} @empty {
<li>There are no items.</li>
}
```

### 2. Estructura del Directorio
Aquí tienes una estructura recomendada para un proyecto Angular SPA con componentes standalone:

```bash
angular-spa/
├── src/
│   ├── app/
│   │   ├── components/          # Componentes compartidos
│   │   │   └── header/          # Ejemplo de componente header compartido
│   │   │       ├── header.component.ts
│   │   │       ├── header.component.html
│   │   │       └── header.component.scss
│   │   │   └── footer/          # Ejemplo de componente footer compartido
│   │   │       ├── footer.component.ts
│   │   │       ├── footer.component.html
│   │   │       └── footer.component.scss
│   │   ├── pages/               # Páginas principales de la aplicación
│   │   │   ├── home/            # Página Home
│   │   │   │   ├── home.component.ts
│   │   │   │   ├── home.component.html
│   │   │   │   └── home.component.scss
│   │   │   ├── about/           # Página About
│   │   │   │   ├── about.component.ts
│   │   │   │   ├── about.component.html
│   │   │   │   └── about.component.scss
│   │   │   └── contact/         # Página Contact
│   │   │       ├── contact.component.ts
│   │   │       ├── contact.component.html
│   │   │       └── contact.component.scss
│   │   ├── app.component.ts     # Componente raíz de la aplicación
│   │   ├── app.component.html
│   │   ├── app.component.scss
│   │   ├── app.routes.ts        # Definición de rutas de la aplicación
│   │   └── main.ts              # Punto de entrada de la aplicación
│   ├── assets/                  # Recursos estáticos (imágenes, etc.)
│   └── styles.scss              # Estilos globales
```

### 3. Configuración de Rutas
Configura las rutas de la aplicación en el archivo app.routes.ts para crear una SPA con navegación entre componentes.

```html
// src/app/app.routes.ts
import { Routes } from '@angular/router';
import { HomeComponent } from './pages/home/home.component';
import { AboutComponent } from './pages/about/about.component';
import { ContactComponent } from './pages/contact/contact.component';

export const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: 'contact', component: ContactComponent },
  { path: '**', redirectTo: '' }  // Redirige a Home si la ruta no existe
];
```

### 4. Configurar el Routing en main.ts
En el archivo main.ts, configura el router para que reconozca el archivo app.routes.ts.

```html
// src/main.ts
import { bootstrapApplication } from '@angular/platform-browser';
import { provideRouter } from '@angular/router';
import { AppComponent } from './app/app.component';
import { routes } from './app/app.routes';

bootstrapApplication(AppComponent, {
  providers: [
    provideRouter(routes)
  ]
});
```

### 5. Configuración del AppComponent
En el archivo app.component.html, puedes agregar el router outlet para cargar los componentes según la ruta:

```html
<!-- src/app/app.component.html -->
<app-header></app-header>
<main>
  <router-outlet></router-outlet>
</main>
<app-footer></app-footer>
```

### 6. Crear el Contenido de Cada Componente
Agrega el contenido en cada uno de los componentes (Home, About, Contact) en sus respectivos archivos .html.

ng g c components/pages/HomeComponent

Ejemplo para home.component.html:
```html
<!-- src/app/pages/home/home.component.html -->
<h1>Bienvenido a la Página Principal</h1>
<p>Esta es una SPA en Angular con componentes standalone.</p>
```

ng g c components/pages/AboutComponent

Ejemplo para about.component.html:
```html
<!-- src/app/pages/about/about.component.html -->
<h1>Sobre Nosotros</h1>
<p>Información sobre la empresa.</p>
```

Ejemplo para contact.component.html:
```html
<!-- src/app/pages/contact/contact.component.html -->
<h1>Contacto</h1>
<p>Datos de contacto de la empresa.</p>
```

Ejemplo para header.component.html:
```html
<!-- src/app/components/header/header.component.html -->
<header>
  <nav>
    <a routerLink="/">Inicio</a>
    <a routerLink="/about">Sobre Nosotros</a>
    <a routerLink="/contact">Contacto</a>
  </nav>
</header>
```

Ejemplo para footer.component.html:

```html
<!-- src/app/components/footer/footer.component.html -->
<footer>
  <p>&copy; 2024 Tu Empresa</p>
</footer>
```

8. Agregar Estilos Globales en styles.scss
Define estilos globales en src/styles.scss para aplicar un diseño consistente en toda la aplicación.
```html
/* src/styles.scss */
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

header, footer {
  background-color: #333;
  color: #fff;
  padding: 1rem;
  text-align: center;
}

nav a {
  color: white;
  margin: 0 1rem;
  text-decoration: none;
}

main {
  padding: 2rem;
}
```
