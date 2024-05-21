---
tags:
    - Praxis
---

# Passwort Hashing

Passwort-Hashing ist eine grundlegende Sicherheitsmaßnahme, um sensible Informationen wie Passwörter zu schützen. Anstatt Passwörter im Klartext zu speichern, werden diese mithilfe von Hashing-Algorithmen in eine nicht umkehrbare Form umgewandelt. Die Bibliothek `bcrypt` ist in Node.js weit verbreitet, um Passwörter zu hashen und zu verifizieren. [^1]

```js title="Installation von bcrypt"
npm install bcrypt
```

```js title="Hashing eines Passworts"
const bcrypt = require("bcrypt");
const saltRounds = 10;
const plainPassword = "yourPassword";

const hashedPassword = bcrypt.hashSync(plainPassword, saltRounds);
console.log(hashedPassword);
```

```js title="Verifizieren eines Passworts"
const isMatch = bcrypt.compareSync(plainPassword, hashedPassword);
console.log(isMatch); // true oder false
```

[^1]: bcrypt: https://github.com/kelektiv/node.bcrypt.js#sync
