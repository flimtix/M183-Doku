---
tags:
    - Praxis
---

# Error Handling

Effektives Error Handling ist entscheidend für die Sicherheit und Zuverlässigkeit von Anwendungen. Es schützt vor unvorhergesehenen Abstürzen und verhindert, dass sensible Informationen an Benutzer weitergegeben werden. ([Information Disclosure](../Theorie/Sicherheitsprinzipien.md#information-disclosure))

```js title="Error Handling Middleware"
api.use((err, req, res, next) => {
	console.error(err.message);
	res.status(err.statusCode || 500).json({ errorMessage: err.message });
});
```

```js title="Error Handling mit Information Disclosure"
api.use((err, req, res, next) => {
	logger.error(err.message, {
		errno: err.errno,
		error: err,
	});
	err.statusCode ??= HTTP_STATUS_INETERNAL_SERVER_ERROR;
	if (err.statusCode === HTTP_STATUS_INETERNAL_SERVER_ERROR) {
		err.message = "Internal Server Error";
	}
	res.status(err.statusCode).json({
		errorMessage: err.message,
	});
});
```
