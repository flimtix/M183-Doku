Um dir für die bevorstehende Prüfung im Modul 183 über Sicherheit im Internet eine umfassende Zusammenfassung zu bieten, gehen wir systematisch durch die Theorie- und Praxisteile deines Kurses:

### Theorie

**1. OpenSSL und Primzahlen**

-   OpenSSL wird häufig zur Implementierung von SSL/TLS-Protokollen verwendet. Primzahlen spielen eine wichtige Rolle in der Kryptographie, insbesondere bei der Erzeugung von Schlüsseln für Verfahren wie RSA.

**2. Vertraulichkeit und Integrität**

-   Diese Prinzipien sind zentral für die Informationssicherheit. Vertraulichkeit schützt Daten vor unbefugtem Zugriff, während Integrität die Korrektheit und Vollständigkeit der Daten sicherstellt.

**3. Grundlegende Sicherheitsprinzipien**

-   Dazu zählen Aspekte wie die Minimierung der Angriffsfläche, das Prinzip des geringsten Privilegs und die Notwendigkeit, Sicherheit von Anfang an in Systeme zu integrieren.

**4. Information Disclosure**

-   Unbeabsichtigte Offenlegung von Informationen kann durch Konfigurationsfehler oder unsichere Software entstehen. Tools wie Portswigger bieten Techniken, um solche Schwachstellen zu identifizieren.

**5. JWT (JSON Web Tokens)**

-   JWTs sind ein kompaktes, URL-sicheres Mittel, um Informationen zwischen zwei Parteien zu übermitteln. Sie werden häufig in der Authentifizierung und Autorisierung verwendet.

**6. Verschlüsselung**

-   RSA-Verschlüsselung ist ein asymmetrisches Verschlüsselungsverfahren, das auf zwei Schlüsseln basiert: einem öffentlichen und einem privaten. Salting verbessert die Sicherheit von Passwörtern durch Hinzufügen zufälliger Daten vor dem Hashing.

**7. Sicherheitslücken**

-   Wichtige Sicherheitslücken sind SQL-Injection, Command Injection, Business Logic Vulnerabilities und Cross-Site Scripting (XSS). Jede dieser Lücken kann schwerwiegende Sicherheitsverletzungen zur Folge haben.

**8. ORM und Sequelize**

-   ORM (Object-Relational Mapping) hilft bei der Interaktion mit Datenbanken durch Objekte statt SQL-Code. Sequelize ist ein beliebtes ORM für Node.js.

**9. CSRF, CORS, Cookies, Sessions, SOP, Preflight**

-   Dies sind wesentliche Konzepte zur Verwaltung von Webanwendungen und zur Kontrolle der Sicherheit im Umgang mit cross-origin Anfragen und Benutzersitzungen.

### Praxis

**1. Passwort Hashing**

-   bcrypt ist eine Methode zum sicheren Hashing von Passwörtern, um sie vor Diebstahl zu schützen.

**2. JWT in der Praxis**

-   Verwendung von JWTs für Authentifizierung, Autorisierung und rollenbasierte Zugriffskontrolle.

**3. Error Handling und User-Input-Validierung**

-   Wichtig für die Sicherstellung der Robustheit von Anwendungen, um sie vor fehlerhaften oder böswilligen Eingaben zu schützen.

**4. Logging**

-   Protokollierung von Vorgängen in einer Anwendung zur Fehlerdiagnose und zur Überwachung von Sicherheitsereignissen.

**5. XSS teilweise erlauben**

-   DomPurify ermöglicht das Säubern von HTML-Content zur sicheren Einbettung von Benutzerinhalten, ohne XSS-Angriffe zu ermöglichen.

### Packages

-   **Sequelize, Winston, bcrypt, validator, dompurify**
    -   Diese Tools und Libraries unterstützen verschiedene Sicherheits- und Funktionalitätsaspekte in Webanwendungen.

Diese Zusammenfassung deckt die wesentlichen Inhalte deines Kurses ab. Es wäre gut, die verlinkten Dokumente und Ressourcen nochmals gründlich zu überprüfen, um ein tiefes Verständnis der Themen zu erreichen, besonders im Hinblick auf die anstehende Prüfung.
