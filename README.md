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
let http = require('http');
let fs = require('fs');
let path = require('path');
let port = 3000;

http
  .createServer(function (request, response) {
    console.log('request ', request.url);

    let filePath = '.' + request.url;
    if (filePath == './') {
      filePath = './index.html';
    }

    let extname = String(path.extname(filePath)).toLowerCase();
    let mimeTypes = {
      '.html': 'text/html',
      '.js': 'text/javascript',
      '.css': 'text/css',
      '.json': 'application/json',
      '.png': 'image/png',
      '.jpg': 'image/jpg',
      '.gif': 'image/gif',
      '.svg': 'image/svg+xml',
      '.wav': 'audio/wav',
      '.mp4': 'video/mp4',
      '.woff': 'application/font-woff',
      '.ttf': 'application/font-ttf',
      '.eot': 'application/vnd.ms-fontobject',
      '.otf': 'application/font-otf',
      '.wasm': 'application/wasm',
    };

    let contentType = mimeTypes[extname] || 'application/octet-stream';

    fs.readFile(filePath, function (error, content) {
      if (error) {
        if (error.code == 'ENOENT') {
          fs.readFile('./404.html', function (error, content) {
            response.writeHead(404, { 'Content-Type': 'text/html' });
            response.end('404 Not Found');
          });
        } else {
          response.writeHead(500);
          response.end(
            'Sorry, check with the site admin for error: ' +
              error.code +
              ' ..\n'
          );
        }
      } else {
        response.writeHead(200, { 'Content-Type': contentType });
        response.end(content, 'utf-8');
      }
    });
  })
  .listen(port);
console.log('Server running at http://127.0.0.1:' + port);
```

### Selgitus:

[Selgituse kodu](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Node_server_without_framework)

http serveri loomiseks on meil vaja öelda `require('http')`, mis saab muutuja `let http` väärtuseks.  
`require fs`lubab kasutada failissüsteemi ja `path`radu (või ma ei teagi, kuidas see eesti kelles õige oleks), ehk aadressiriba saaks jälgida.

`https.createServer` loob serveri.

Avame loodud `package.json`i ning lisame server käivitamise käsu `script`jaotuse alla:

```json
"scripts": {
    "start": "node server.js"
},
```

### Testime

Loome kaks faili `index.html`ja mingi muu html file, nt `kontakt.html` ja ava need browseris.

## taaskasutatavad komponendid

[juhend](https://www.freecodecamp.org/news/reusable-html-components-how-to-reuse-a-header-and-footer-on-a-website/)

Siin kasutame kolme tehnoloogiat:

- [HTML templiidid](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_templates_and_slots)
- [Javascripti kohandatud elemendid](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements)
- [Shadow DOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM)
