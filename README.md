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

## Live server

Pisikeste projektide tarbeks on mõistlik kasutada kas VS Code livererverit või nt [web Dev Serverit](https://modern-web.dev/docs/dev-server/overview/)

Suuremate asjade jaoks vast Webpack, Parcel vms
