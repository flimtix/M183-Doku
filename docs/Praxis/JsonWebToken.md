---
tags:
    - Praxis
---

# JSON Web Token (JWT)

JSON Web Tokens (JWT) werden zur Authentifizierung und Autorisierung in Webanwendungen verwendet. Sie enthalten verschlüsselte Informationen, die verwendet werden können, um Benutzer zu verifizieren und Zugriffskontrollen durchzuführen. [^1]

```js title="Erstellen eines JWT"
const jwt = require("jsonwebtoken");
const secretKey = "yourSecretKey";
const token = jwt.sign({ data: "payloadData" }, secretKey, { expiresIn: "1h" });
console.log(token);
```

```js title="Verifizieren eines JWT"
const decoded = jwt.verify(token, secretKey);
console.log(decoded);
```

## Router Middleware

Um die Authentifizierung und Autorisierung in Express.js zu implementieren, können Sie Middleware verwenden, um den JWT aus dem HTTP-Header zu extrahieren und zu verifizieren.

```js title="Middleware in Router einbinden (api.js)"
api.use(extractApiKey);
api.use(routes);
```

```js title="Middleware in Router einbinden (routes.js)"
router.get(
	"/users/:userid/mnts",
	isOwner,
	isAdmin,
	requireAuth,
	mountainCtrl.getAllUserMountainIds
);
```

```js title="Auslesen des Tokens aus dem Header"
module.exports = (req, res, next) => {
	let isValid = false;

	try {
		// Ist der Value des Feldes Authorization des HTTP-Headers überhaupt vorhanden?
		const authHeader = req.get("Authorization");
		if (authHeader) {
			// Überprüfen, ob der Wert des Feldes Authorization mit dem String "Bearer " beginnt.
			if (authHeader.startsWith(TOKEN_PREFIX)) {
				// Den Bearer-String entfernen.
				const jwtToken = authHeader.substring(TOKEN_PREFIX.length);
				if (jwtToken) {
					// Verifizieren Sie das Token mit der Methode verify().
					const decodedToken = token.verify(jwtToken, JWTSECTRET);
					if (decodedToken) {
						res.locals.authorization = decodedToken;
						isValid = true;
					}
				}
			}
		}
	} catch (err) {
		logger.info(err.message, {
			errno: err.errno,
			error: err,
		});
	}

	res.locals.isAuthorized = isValid;
	next();
};
```

```js title="Überprüfen der Autorisierung"
const {
	HTTP_STATUS_UNAUTHORIZED,
	HTTP_STATUS_FORBIDDEN,
} = require("../util/const");

module.exports = (req, res, next) => {
	if (!res.locals?.isAuthorized) {
		if (res.locals?.authorization) {
			const error = new Error("Forbidden access");
			error.statusCode = HTTP_STATUS_FORBIDDEN;
			throw error;
		}

		const error = new Error("Unauthorized access");
		error.statusCode = HTTP_STATUS_UNAUTHORIZED;
		throw error;
	}
	next();
};
```

```js title="Admin-Rolle überprüfen"
module.exports = (req, res, next) => {
	res.locals.isAuthorized = res.locals?.authorization?.data?.isadmin ?? false;
	next();
};
```

```js title="Benutzer-Rolle überprüfen"
module.exports = (req, res, next) => {
	res.locals.isAuthorized =
		req.params.userId &&
		req.params.userId === res.locals?.authorization?.sub;
	next();
};
```

[^1]: Weitere Informationen: https://docs.google.com/document/d/1tuvMAmY7vvALhTaqmyBRIFDrZ7gI31Uxpoxa-RqUrDI/edit#heading=h.5cqlsyp3uxym
