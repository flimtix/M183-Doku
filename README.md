# M183 - Zusammenfassung

[![ci-mkdocs](https://github.com/21r8390/M183-Doku/actions/workflows/ci-mkdocs.yml/badge.svg)](https://github.com/21r8390/M183-Doku/actions/workflows/ci-mkdocs.yml)

---

> Modul: M183

## How To:

> Doku starten: `docker compose up`

## TODO:

https://docs.google.com/document/d/1G5PQZqtO_Sv-w-VnsT64XWUKr0_YuA0aQ-yUKZAcahg/edit#heading=h.n3f3cuf1ppar

### Theorie

-   OpenSSL
    -   OpenSSL Primzahlen
    -   https://www.cryptool.org/en/cto/openssl/
-   Vertraulichkeit und Integrität
    -   https://docs.google.com/document/d/1aptwCFt1HZGehDyfdj1347u6_0mUR0poIwFWCBIUIK4/edit#heading=h.2ki0wrufwysh
-   Grundlegende Sicherheitsprinzipien
    -   https://docs.google.com/document/d/160llHSFAyvL57Q0sbU5uby6Ng3A7288zjm2EbemgH3o/edit#heading=h.jcfs1mt5gphx
-   Information Disclosure
    -   https://docs.google.com/document/d/1wXridfIGBKOsQsugWz0cocpNrMgrq7iehvLRlH3p93A/edit#heading=h.ed74ctkg9zim
    -   https://portswigger.net/web-security/information-disclosure
-   JWT
-   Verschlüsselung
    -   RSA-Verschlüsselung
        -   https://docs.google.com/document/d/143kpSF6D4UGF13yX7ubqC5HKnQnFIb2sBTf7_x4V3Uo/edit#heading=h.x8iedy5yox8x
    -   Salting
-   Sicherheitslücken
    -   SQL-Injection
        -   https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html
        -   https://portswigger.net/web-security/sql-injection
    -   Command Injection
    -   Business Logic Vulnerabilities
    -   Cross-Site Scripting (XSS)
        -   https://docs.google.com/document/d/1dsY6yo6o5OF7koziCfuGUKM5tguv5fT9va_2R509wG8/edit#heading=h.vxrztom7guhs
-   ORM
    -   Sequelize
-   CSRF, CORS, Cookies, Sessions, SOP, Preflight
    -   https://docs.google.com/document/d/1YztvowA9ToM_Jxmxt7pTjOTjr2e0POOdwdMa66Uc4O4/edit#heading=h.m0jl6t12cyvk

### Praxis

-   Passwort Hashing
    -   bcrypt
    -   https://github.com/kelektiv/node.bcrypt.js#sync
-   JWT
    -   https://docs.google.com/document/d/1tuvMAmY7vvALhTaqmyBRIFDrZ7gI31Uxpoxa-RqUrDI/edit#heading=h.5cqlsyp3uxym
    -   Authentifizierung
    -   Autorisierung
    -   Rollen basierte Zugriffskontrolle
-   Error Handling
-   User-Input-Validierung
    -   https://docs.google.com/document/d/1IjBf3GBy-9k2icUjj_hTiz10LPc9Ad11TqzmXAY0TQE/edit
-   Logging
-   XSS Teilweise erlauben
    -   dompurify
    -   https://docs.google.com/document/d/1dsY6yo6o5OF7koziCfuGUKM5tguv5fT9va_2R509wG8/edit

## Einrichten

-   Docker Datenbank mit MySQL
    -   Leeres Schema
    -   Adminer
-   PortSwigger

## Fragen

-   Packages bereits installiert?
    -   Sequelize ✔
    -   Winston ✔
    -   Muss selbst installiert werden:
        -   bcrypt ❌
        -   validator ❌
        -   dompurify ❌
-   Die Tests werden mit newman durchgeführt
-   Zeit 5 Lektionen

prerequest scripts
requests
test-scripts
