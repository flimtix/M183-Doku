---
tags:
    - Praxis
---

# Logging

Logging ist essenziell für die Überwachung und Fehlerdiagnose in Anwendungen. Die Bibliothek `winston` ist ein leistungsfähiges Logging-Tool in Node.js.

```js title="Initialisierung des Loggers"
const winston = require("winston");
const logger = winston.createLogger({
	level: "info",
	format: winston.format.json(),
	transports: [
		new winston.transports.File({ filename: "error.log", level: "error" }),
		new winston.transports.File({ filename: "combined.log" }),
	],
});
```

```js title="Logging von Informationen"
logger.info("This is an informational message");
```

```js title="Logging von Fehlern"
logger.error("This is an error message");
```

```js title="Logging von Fehlern mit Metadaten"
try {
	throw new Error("This is an error message");
} catch (err) {
	logger.error(err.message, {
		errno: err.errno,
		error: err,
	});
}
```

```js title="Logging von Fehlern in Express"
app.use((err, req, res, next) => {
	logger.error(err.message, {
		errno: err.errno,
		error: err,
	});
	res.status(err.statusCode || 500).json({ errorMessage: err.message });
});
```
