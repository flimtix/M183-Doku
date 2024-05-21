---
tags:
    - Praxis
---

# XSS (Cross-Site Scripting)

Cross-Site Scripting (XSS) ist eine Sicherheitslücke, bei der Angreifer bösartigen Code in Webseiten einschleusen, um sensible Informationen zu stehlen oder Benutzer zu täuschen. XSS-Angriffe können in drei Kategorien unterteilt werden: Reflected XSS, Stored XSS und DOM-based XSS. Um XSS-Angriffe zu verhindern, sollten Entwickler Benutzereingaben validieren und sicherstellen, dass sie nicht direkt in HTML eingefügt werden. [^1]

XSS-Angriffe erfolgen durch das Einfügen von schädlichem Skript in Webanwendungen. `dompurify` ist ein Werkzeug zur Bereinigung von HTML, um XSS-Angriffe zu verhindern.[^2]

```js title="Installation von dompurify"
npm install dompurify
```

```js title="Verwendung von dompurify"
const DOMPurify = require("dompurify");
const cleanHTML = DOMPurify.sanitize('<script>alert("XSS")</script>');
console.log(cleanHTML); // ''
```

[^1]: Quelle: https://docs.google.com/document/d/1dsY6yo6o5OF7koziCfuGUKM5tguv5fT9va_2R509wG8/edit#heading=h.vxrztom7guhs
[^2]: Quelle: https://www.npmjs.com/package/dompurify
