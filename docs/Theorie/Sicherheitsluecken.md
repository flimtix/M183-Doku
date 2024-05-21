---
tags:
    - Theorie
---

# Sicherheitslücken

Sicherheitslücken sind Schwachstellen in einer Software, die es Angreifern ermöglichen, unerlaubten Zugriff auf Systeme oder Daten zu erhalten. Die folgenden Sicherheitslücken sind besonders relevant für Webanwendungen[^1]:

### SQL-Injection

SQL-Injection ist eine Technik, bei der Angreifer schädlichen SQL-Code in eine Abfrage einfügen, um auf die Datenbank zuzugreifen oder sie zu manipulieren.

-   **ORM (Object-Relational Mapping)**: ORMs abstrahieren die Datenbankinteraktionen und können helfen, SQL-Injections zu vermeiden, indem sie vorbereitete Anweisungen und Parameterbindungen verwenden.

### Command-Injection

Bei einer Command-Injection kann ein Angreifer beliebige Betriebssystembefehle auf einem Server ausführen. Dies geschieht oft durch unsichere Handhabung von Benutzereingaben.

### Cross-Site Scripting (XSS)

XSS ermöglicht es Angreifern, schädliches JavaScript in Webseiten einzubetten, das im Browser anderer Benutzer ausgeführt wird.

-   **Typen**:
    -   **Reflected XSS**: Der schädliche Code wird im HTTP-Request übergeben und sofort im Response ausgeführt.
    -   **Stored XSS**: Der schädliche Code wird in der Datenbank gespeichert und bei späteren Anfragen ausgeführt.
    -   **DOM-based XSS**: Der Angriff erfolgt durch Manipulation der clientseitigen Scripts.

### Business Logic Vulnerabilities

Diese Schwachstellen entstehen durch Fehler in der Geschäftslogik einer Anwendung, die es Angreifern ermöglichen, unerwartete oder unberechtigte Aktionen durchzuführen.

### CSRF (Cross-Site Request Forgery)

CSRF zwingt einen angemeldeten Benutzer dazu, unerwünschte Aktionen in einer Webanwendung durchzuführen. Ein Angreifer nutzt die Authentifizierung des Benutzers aus, um schädliche Aktionen durchzuführen.

### CORS (Cross-Origin Resource Sharing)

CORS ist ein Mechanismus, der den Zugriff auf Ressourcen von einer anderen Domain kontrolliert. Unsachgemäße CORS-Konfigurationen können zu Sicherheitslücken führen.

### Cookies, Sessions, SOP und Preflight

-   **Cookies**: Werden zur Sitzungsverwaltung verwendet und sollten sicher konfiguriert sein (z.B. HttpOnly, Secure).
-   **Sessions**: Verwalten Benutzersitzungen und sollten sicher gegen Session-Hijacking und Fixation sein.
-   **SOP (Same-Origin Policy)**: Beschränkt, wie Dokumente oder Skripte von verschiedenen Ursprüngen miteinander interagieren können.
-   **Preflight**: Eine CORS-Option, bei der der Browser eine OPTIONS-Anfrage sendet, bevor die eigentliche Anfrage gestellt wird, um zu überprüfen, ob die Anfrage zulässig ist.

[^1]: Quelle: https://docs.google.com/document/d/1YztvowA9ToM_Jxmxt7pTjOTjr2e0POOdwdMa66Uc4O4/edit#heading=h.m0jl6t12cyvk
[^2]: Quelle: https://portswigger.net/web-security/cross-site-scripting#what-is-cross-site-scripting-xss
