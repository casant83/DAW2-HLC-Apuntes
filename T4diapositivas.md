<!---
Ejemplos de inserción de videos

<video class="stretch" controls><source src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4" type="video/mp4"></video>
<iframe width="560" height="315" src="https://www.youtube.com/embed/3RBq-WlL4cU" frameborder="0" allowfullscreen></iframe>

slide: data-background="#ff0000" 
element: class="fragment" data-fragment-index="1"
-->

## HLC - Fullstack
---
![HLC-Fullstack](http://jamj2000.github.io/hlc-fullstack/hlc-fullstack.png)
<small> 2018-19 - IES Luis Vélez de Guevara - Écija - Spain </small>


## Backend con NodeJS y Express

[![cc-by-sa](http://jamj2000.github.io/hlc-fullstack/cc-by-sa.png)](http://creativecommons.org/licenses/by-sa/4.0/)


## Índice
--- 
- ### Introducción
- ### Node.js
- ### El servidor web
- ### Accediendo a la BD
- ### Ajustes finales
- ### Comprobando la API

<!--- Note: Nota a pie de página. -->



## Introducción


### En esta Unidad aprenderemos a

- Instalar y configurar el entorno de desarrollo.
- Gestionar las dependencias mediante el uso del gestor de paquetes.
- Elaborar una API RESTful.
- Hacer peticiones a la API desde distintos clientes.
- Definir el modelo de datos y acceder a la base de datos desde el código de la aplicación.

_Se envían los datos no la vista, mediante una Api: la más utilizada es la API REST_


### Aplicación de ejemplo

- Existe una aplicación funcional de ejemplo.
- El código está disponible en [`https://github.com/jamj2000/tienda0`](https://github.com/jamj2000/tienda0)
- Los archivos usados para el backend son:
  - **package.json**
  - **server.js**
  - **models.js**
  - **routes.js**
  - **config.js**

_https://github.com/jamj2000/tiendaw_

_package.json equivalente al pom.xml_



## Node.js

![Node](assets/node.png)

_No es un framework, es un entorno de ejecución que se basa en un motor de JS_


### Motor Javascript V8

![v8 engine](assets/v8-engine.png)

Node.js® es un entorno de ejecución para JavaScript construido con el **motor de JavaScript V8 de Chrome**.


### Instalación

**Entorno de ejecución**

```bash
sudo  apt  install  nodejs
```

**Gestor de paquetes**
```bash
sudo  apt  install  npm
```

Note: **npm** =  **N**ode **P**ackage **M**anager

_No nos interesó hacerlo por la versión, lo instalamos desde la página oficial de Node, descomprimirlo 


### Inicio de un proyecto

```bash
mkdir  nombre-proyecto
cd     nombre-proyecto

npm  init  -y 
```

Note: La opción -y (--yes) de `npm init` crea un archivo package.json con opciones por defecto, sin solicitar al usuario.
_npm init crea el archivo package.json_
_npm start: _

### Archivo package.json

```json
{
  "name": "hola",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.16.4"
  },
  "devDependencies": {
    "nodemon": "^1.18.4"
  }
}
```

_ dependencias para utilizarla, devDependencies: nos hacen falta para desarrollarla_


### Instalación de módulos

```bash
     npm  install  express  -S  
     npm  install  nodemon  -D  
sudo npm  install  yarn     -g  
```

o de forma más corta

```bash
     npm  i  express  -S  
     npm  i  nodemon  -D  
sudo npm  i  yarn     -g
```

Note: 
-S: anotar en package.json como dependencia de aplicación.
-D: anotar en package.json como dependencia de desarrollo.
-g: instala en el sistema de forma global.

_no hace falta la -S --save no hace falta en las versiones modernas_
_ -D sí hace falta para instalarla como una dependencia de desarrollo_
_ -g módulos ejecutables, es una forma demasiado larga hay una forma más directa_
_Se puede poner i en vez de install_

### Desinstalación de módulos

```bash
     npm  remove  express  -S 
     npm  remove  nodemon  -D 
sudo npm  remove  yarn     -g 
```   
o de forma más corta

```bash
     npm  r  express  -S  
     npm  r  nodemon  -D  
sudo npm  r  yarn     -g
```

Note: 
-S: anotar en package.json como dependencia de aplicación.
-D: anotar en package.json como dependencia de desarrollo.
-g: instala en el sistema de forma global.

_*Cambio de versión*_

### Instalación de módulos

```bash
     npm  install  express  -S  
     npm  install  nodemon  -D  
sudo npm  install  yarn     -g  
```

o de forma más corta

```bash
     npm  i  express  -S  
     npm  i  nodemon  -D  
sudo npm  i  yarn     -g
```


### Opciones

**-S,  --save**
- dependencia de aplicación. Añade entrada en archivo `package.json`. En las últimas versiones de `npm` no es necesaria esta opción.

**-D,  --save-dev**
- dependencia de desarrollo. Añade entrada en archivo `package.json`.

**-g,  --global**
- instala en el sistema de forma global. Se usa normalmente para paquetes ejecutables.


### Desinstalación de módulos

```bash
     npm  remove  express
     npm  remove  nodemon  -D 
sudo npm  remove  yarn     -g 
```   
o de forma más corta

```bash
     npm  r  express 
     npm  r  nodemon  -D  
sudo npm  r  yarn     -g
```




### npx (I)

- Herramienta de ejecución de paquetes que viene con **npm 5.2+**.
- **Ejecuta** paquetes ejecutables de `node.js` sin necesidad de instalarlos.
- Es más cómodo que usar `sudo npm install -g ...`
- Ejemplo (lanzar servidor web):
  - Usando `sudo npm install -g ...`:
  ```
  sudo npm  install  -g  http-server
  http-server
  ```
  - Usando `npx  ...`:
  ```
  npx  http-server
  ```


### npx (II)

#### Ejemplos

```
npx  serve                                      # Inicia un servidor web
npx  http-server                                # Inicia otro servidor web

npx  @angular/cli  new         nombre-proyecto  # Iniciar proyecto de Angular 
npx  create-react-app          nombre-proyecto  # Iniciar proyecto de React 
npx  @vue/cli  create          nombre-proyecto  # Iniciar proyecto de Vue
npx  degit  sveltejs/template  nombre-proyecto  # Iniciar proyecto de Svelte   
```

_Angular:300megas, React:200megas, Vue:100megas_
_degit descarga un repositorio de github unos 100k_
_npm run dev_


### Módulos incorporados (built-in)

- No es necesario instalarlos.
- Ya vienen con node.js.
- Ejemplos:
  - **fs**:  Sistema de archivos
  - **http**:  Servidor HTTP
  - **https**:  Servidor HTTPS
  - **os**:  Sistema operativo
  - **path**:  Rutas de archivos
  - **process**:  Información y control del proceso actual
  - ...

Mas info: https://www.w3schools.com/nodejs/ref_modules.asp
 _require fs, no hay que instalarlo_
 _process no hay que poner require, se puede acceder con env_


## El servidor web

- Node.js nos permite desarrollar un servidor web desde cero.
- Para ello puede usarse el módulo incorporado `http`.
- Sin embargo es más recomendable, por su sencillez, usar el **framework `express`**.


### Un servidor sencillo

**server1.js**

```javascript
var app  =  require('express')();

app.get ('/', (req, res) => { 
    res.send ('Hola mundo') 
});

app.get ('/hola/:usuario', (req, res) => { 
    res.send (`<h1>Buenos días, ${req.params.usuario}</h1>`); 
});

app.listen (3000);
```
Para ejecutar:

```bash
node  server1
```
_nos conviene tener una variable express para poder acceder a routes, por ejemplo... Está en las capturas_
_Normalmente se hace con un enroutador_
_node  server1: nosotros utilizadmos npm_


### Otro servidor sencillo  

**server2.js**

```javascript
// --- IMPORTACIONES
const path     = require('path');
const express  = require('express');
const morgan   = require('morgan');

const app      = express();

// --- MIDDLEWARE
// Archivos estáticos. Deberás crear un archivo public/index.html para ver el resultado
app.use(express.static(path.join(__dirname , 'public')));
// Soporte de JSON
app.use(express.json());
// Logger
app.use(morgan('dev'));

// --- PUERTO DE ESCUCHA
app.listen (3000, () => console.log('Servidor iniciado en puerto 3000'));
```

Para ejecutar:

```bash
node  server2
```



## Accediendo a la BD


### Conexión a la BD

**server.js**

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/tienda', { useNewUrlParser: true })
  .then(db   => console.log ('Conexión correcta a la BD'))
  .catch(err => console.log ('Error en la conexión a la BD'));
```
_Mongoose se instala como un paquete de aplicación?_

### El modelo de datos
**models.js**

```bash
const mongoose = require('mongoose');

const Cliente  = mongoose.model('Cliente',  { 
                                   nombre: String, 
                                   apellidos: String  });

const Articulo = mongoose.model('Articulo', { 
                                   nombre: String, 
                                   precio: Number });

module.exports =  {
    Cliente,
    Articulo
};
```
_Hay que decir cómo están hechas las colecciones: las tablas_

### Operaciones CRUD

| CRUD     |  HTTP    | MongoDB   | Mongoose                     |
|----------|----------|-----------|------------------------------|
| Create   | POST     | insert    | objeto.save                  |
| Read     | GET      | find      | Modelo.find / Modelo.findOne |
| Update   | PUT      | update    | Modelo.findOneAndUpdate      |
| Delete   | DELETE   | remove    | Modelo.findOneAndRemove      |

_**CAE** Update y Delete hay quien lo hace con get, pero  mejor así._ 
_Crear: Hacer un objeto y guardarlo_
_MongoDB:Operaciones en mongodb, y Mongoose: métodos disponibles_

### Acceso a la BD (I)
**routes.js**
#### Importación de módulos

```javascript
const express = require('express');
const { Cliente, Articulo } = require('./models');

const router = express.Router();
```


### Acceso a la BD (II)
**routes.js**
#### Lectura de datos

```javascript
// ver todos los Clientes
router.get('/clientes', (req, res) => {  
  Cliente.find( ... ver más abajo ... );  
});
```

```javascript
    Cliente.find({}, (err, data) => {
        if (err) res.json({ error: err });
        else     res.json(data);
    });
```


### Acceso a la BD (III)
**routes.js**
#### Lectura de datos

```javascript
// ver un Cliente
router.get('/clientes/:id', (req, res) => {  
  Cliente.findOne( ... ver más abajo ... ); 
});
```

```javascript
    Cliente.findOne({ _id: req.params.id }, (err, data) => {
        if (err) res.json({ error: err });
        else     res.json(data);
    });
```


### Acceso a la BD (IV)
**routes.js**
#### Eliminación de datos

```javascript
// eliminar un Cliente
router.delete('/clientes/:id', (req, res) => { 
  Cliente.findOneAndRemove( ... ver más abajo ... ); 
});
```

```javascript
    Cliente.findOneAndRemove({ _id: req.params.id }, (err, data) => {
        if (err) res.json({ error: err });
        else     res.json(data);
    });
```


### Acceso a la BD (V)
**routes.js**
#### Modificación de datos

```javascript
// actualizar un Cliente
router.put('/clientes/:id', (req, res) => {
  Cliente.findOneAndUpdate( ... ver más abajo ... ); 
});
```

```javascript
    Cliente.findOneAndUpdate (
      {_id: req.params.id}, 
      {$set: { nombre: req.body.nombre, apellidos :req.body.apellidos }}, 
      (err, data) => {
        if (err) res.json({ error: err });
        else     res.json(data);
    });
```


### Acceso a la BD (VI)
**routes.js**
#### Inserción de datos

```javascript
// insertar un Cliente
router.post('/clientes', (req, res) => {
    const cliente = new Cliente({ 
                          nombre: req.body.nombre, 
                          apellidos: req.body.apellidos });
    cliente.save( ... ver más abajo ... );
});
``` 

```javascript
    cliente.save((err, data) => {
        if (err) res.json({ error: err });
        else     res.json(data);
    });
```


### Acceso a la BD (VII)
**routes.js**
#### Exportamos enrutador

```javascript
...  código anterior ... 

module.exports = router;
```



## Ajustes finales


### Estableciendo las rutas 

**server.js**

```javascript
const routes = require('./routes');

// Rutas
app.use ('/api', routes);
```
_Configurar puerto, etc_

### Parámetros de configuración

- Para facilitar el mantenimiento y despliegue de la aplicación, situamos todos los parámetros de configuración en el archivo **`config.js`*

```javascript
// El primer valor es el de PRODUCCIÓN. El valor alternativo es el de DESARROLLO

module.exports = {
  ip         : process.env.HOST   || '0.0.0.0',
  port       : process.env.PORT   || 3000,
  db_uri     : process.env.DB_URI || 'mongodb://localhost:27017/tienda'
};
```


### Uso de parámetros

- En el archivo **`server.js`** utilizamos las variables anteriores en lugar de constantes.
- Si importamos el objeto como config, entonces tenemos:
  - `config.port`
  - `config.db_uri`

```javascript
const config = require('./config');

mongoose.connect(config.db_uri, { useNewUrlParser: true })
  .then(db   => console.log ('Conexión correcta a la BD'))
  .catch(err => console.log ('Error en la conexión a la BD'));

app.listen (config.port, 
            () => console.log(`Servidor iniciado en puerto ${config.port}`));
```



## Comprobando la API

- Para hacer consultas a la API RESTful usaremos 3 métodos:
  - **curl**
  - **DevTools del navegador**
  - **Postman**
_Formas de comprobar las apis, puede caer curl_
_DevTools Consola del navegador_


### curl (I)

Aplicación que nos permite realizar peticiones HTTP de tipo **POST**, **GET**, **PUT**, **DELETE**, y muchas otras, de forma directa desde **terminal de texto**.


### curl (II)

```bash
# GET
curl  http://localhost:3000/api/articulos
curl -H 'Content-Type: application/json' \
     -X GET http://localhost:3000/api/articulos

# POST
curl -H 'Content-Type: application/json' \
     -X POST -d '{"nombre": "Botas de invierno","precio": 99.99}' \
     http://localhost:3000/api/articulos

# PUT
curl -H 'Content-Type: application/json' \
     -X PUT -d '{"nombre": "Paraguas","precio": 100.20}' \
     http://localhost:3000/api/articulos/5b609c52c60bd6656205e3d7

# DELETE
curl -H 'Content-Type: application/json' \
     -X DELETE http://localhost:3000/api/articulos/5b609c52c60bd6656205e3d7
```
_-H cabecera, -X_

### DevTools del navegador (I)

Mediante código javascript podemos realizar peticiones HTTP de tipo **POST**, **GET**, **PUT**, **DELETE**, y alguna otra. Si el servidor no tiene habilitado `CORS`, deberemos tener abierta en el navegador alguna página del dominio para realizar peticiones desde el mismo origen.


### DevTools del navegador (II)

```javascript
fetch('/api/clientes', { method: 'GET' })
  .then ( res => res.json())
  .then ( data => console.log(data) );

fetch('/api/clientes/5b4916cb2100bc25330b6ac9', { method: 'GET' })
  .then ( res => res.json())
  .then ( data => console.log(data) );

fetch('/api/clientes/5b49b5e33808be1b00b982e2', { method: 'DELETE' })
  .then ( res => res.json())
  .then ( data => console.log(data) );
```


### DevTools del navegador (III)

```javascript
var cliente = { nombre: "Isabel", apellidos: "López" };

fetch('/api/clientes', {
  method: 'POST',
  body: JSON.stringify(cliente), 
  headers:{
    'Content-Type': 'application/json'
  }
})
  .then(res => res.json())
  .then(data => console.log(data))
```


### DevTools del navegador (III)

```javascript
var cliente = { nombre: "Pepe", apellidos: "Pérez" };

fetch('/api/clientes/5b4916cb2100bc25330b6ac9', {
  method: 'PUT',
  body: JSON.stringify(cliente), 
  headers:{
    'Content-Type': 'application/json'
  }
})
  .then(res => res.json())
  .then(data => console.log(data));
```


### Postman

Aplicación que nos permite realizar peticiones HTTP de tipo **POST**, **GET**, **PUT**, **DELETE**, y muchas otras, de forma sencilla, cómoda y gráfica.


### Postman: Instalación

- Descargar de la página oficial: https://www.getpostman.com/apps
- Descomprimir
- Ejecutar `Postman/Postman`


###  Postman: Ejecución

![Postman](assets/postman.png)


###  Postman: POST Header

![Postman](assets/postman-post-header.png)


###  Postman: POST Body

![Postman](assets/postman-post-body.png)


###  Postman: PUT Header

![Postman](assets/postman-put-header.png)


###  Postman: PUT Body

![Postman](assets/postman-put-body.png)

