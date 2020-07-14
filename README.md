# TEST DE INTEGRACIÓN EN NODE

---

Partimos del repositorio del ejercicio de [TDD en NodeJs](https://github.com/ElenaMLopez/TDD_node_example)

## Introducción

Tras realizar los test unitarios, vemos que tan solo testean UNIDADES, y en el anterior ejercicio veíamos que nuestros test pasaban sin embargo el servidor no se levantaba correctamente si dentro del archivo `server.js`, realizábamos la llamada desde una entidad que no existía:

```js
const express = require('express');
const axios = require('axios');
const bodyParser = require('body-parser');
const { posts } = require('./src/endpoints');
const { authentication } = require('./src/middlewares');
console.log(typeof authentication);

const port = 3000;
const app = express();

app.use(bodyParser.urlencoded({ extended: false }));

app.use(bodyParser.json());

const postsHandlers = users({ axios }); // users en ved de posts: Este error no lo tiene localizado nuestros test unitarios

app.post('/', authentication, postsHandlers.post);

app.listen(port, function () {
  console.log(`App listening on port ${port}!`);
});
```

Este tipo de errores son los que los test de integración sacarán a la luz.

Un test de integración prueba el flujo entre las unidades, si es correcto pasará y si no arrojará un error, pudiendo de esta forma confirmar si nuestro flujo es correcto. Para realizar este tipo de test, se va a utilizar otra librería llamada [supertest](https://www.npmjs.com/package/supertest), que utiliza [Mocha](https://mochajs.org/) por debajo. Se instalará como dependencia de desarrollo:

```bash
npm install --save-dev supertest
```

Tras ello, creamos el archivo `index.test.js` en el que vamos a realizar el test de integración. Primero importamos supertest, y creamos la instancia:

```js
```
