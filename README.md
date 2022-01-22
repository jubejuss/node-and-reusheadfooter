# Node server, taaskasutatavad komponendid – päis ja jalus

## Node install

Node installiks külasta [Node kodulehte](https://nodejs.org/en/) lae Node alla ja installi.
Sellega installeeritakse Node ja Node Package Manager ehk NPM.

## `package.json`

Node kasutamiseks loome `package.json`, milles on kirjas projektis kasutatavad vidinad.  
Selleks käivitame terminalis käsu:

```bash
npm init
```

Selle käigus küsitakse meilt, mis panna projektile nimeks, kes on autor jne.  
Seejärel: `npm install`

## Node server

Loome projekti juurkataloogi faili `server.js` ja kirjutame sinna sisse:

```javascript
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer(function (req, res) {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, function () {
  console.log('Server running at http://' + hostname + ':' + port + '/');
});
```

### Selgitus:

[Selgituse kodu](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Node_server_without_framework)
http serveri loomiseks on meil vaja öelda `require('http')`, mis saab muutuja `const http` väärtuseks.  
Kuna me kasutame localhosti anname muutujale `hostname`väärtuseks `127.0.0.1`.  
Valime meelepärase pordi numbri.  
Seejärel loome serveri, kasutades `createServer`meetodit.

Avame loodud `package.json`i ning lisame server käivitamise käsu `script`jaotuse alla:

```json
"scripts": {
    "start": "node server.js"
},
```

Samuti loome
