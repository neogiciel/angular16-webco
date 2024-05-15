## <h1>Application Angular 16 Web Component </h1>
***
<table>
  <tr>
    <td><img src="https://www.mag-corp.com/wp-content/uploads/2021/08/angular.png" alt="drawing" height="260px"/></td>
  </tr>
</table>

## Informations Générales
***
Mise en place d'un WebComponent version 16 <br>
```
Via angular.json
 "scripts": ["./src/assets/webco-widget.js"]
```
puis directement dans le composant
```
<webco-widget></webco-widget>
```
## Technologies
***
Technologies utilisées:
* Angular 16 JS
  
## Instalation
***
Creation du projet
```
$ ng new angular-web-component
$ cd angular-web-component
$ ng add @angular/elements
```
Creation du composant
```
$ ng generate component webco
```
Modifier src/app.module.ts
```
import  { Injector} from '@angular/core';
import  { createCustomElement } from '@angular/elements';

  @NgModule({ 
      declarations: [
        AppComponent,
        WebCoComponent
      ],
      imports: [
        BrowserModule,
        HttpClientModule,
        AppRoutingModule
      ],
      providers: [],
      bootstrap: [AppComponent , NewsComponent]
    })
   export class AppModule {
      constructor(private injector: Injector) {
        const el = createCustomElement(WebCoComponent, { injector });
        customElements.define('webco-widget', el);
      }
      ngDoBootstrap() {}
     }

```
Deployer le composant
```
ng build --prod --output-hashing none
```
## Deploiement
***
Instalation fs-extra
```
npm install --save-dev concat fs-extra
```
Creer un fichier **build-component.js**
```
    const fs = require('fs-extra');
    const concat = require('concat');
    
    build = async () =>{
        const files = [
            './dist/angular-web-component/runtime.js',
            './dist/angular-web-component/polyfills.js',
            './dist/angular-web-component/es2015-polyfills.js',
            './dist/angular-web-component/scripts.js',
            './dist/angular-web-component/main.js'
          ];
        
          await fs.ensureDir('widget');
          await concat(files, 'widget/webco-widget.js');
    }
    build();
```
Modifier le fichier **package.json**
```
"build:component": "ng build --output-hashing none && node build-component.js"
```
Construire le fichier destination
```
$ npm run build:component
```
Creer un fichier index.html dans le dossier widget
```
  <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Testing the News Web Component</title>
      <base href="/">
    </head>
    <body>
      <webco-widget></webco-widget>
      
      <script type="text/javascript" src="webco-widget.js"></script>
    </body>
    </html>
```
Installer le serveur de test et se mettre à la racine du dossier
```
$ npm install -g serve
$ serve
```

## FAQs
***
Quelques lignes de commandes utiles<br>
```
Désinstaller la version courante
npm uninstall -g @angular/cli

Installer la version
npm install -g @angular/cli@17

```

