---
tags:
    - Theorie
---

# Verschlüsselung

Dieses Dokument behandelt [Vertraulichkeit](Sicherheitsprinzipien.md#vertraulichkeit-confidentiality) und [Integrität](Sicherheitsprinzipien.md#integrität-integrity) in der Informationsverarbeitung. [^1]

## Symmetrische Verschlüsselung

Bei symmetrischen Verschlüsselungsverfahren erfolgt die Ver- und Entschlüsselung mit **dem selben Schlüssel**. [^2]

**Vorteile:**

-   Schnell
-   Einfach zu implementieren
-   Beim vergrössern des Schlüssels wird die Verschlüsselung sicherer

**Nachteile:**

-   Schlüssel muss vorher ausgetauscht werden
-   Jeder, der den Schlüssel kennt, kann die Nachricht entschlüsseln
    -   Für jeden Empfänger muss ein neuer Schlüssel generiert werden

## Asymmetrische Verschlüsselung

Bei der asymmetrischen Verschlüsselung kommt ein **Schlüsselpaar** zum Einsatz. Nachrichten, die mit dem einen Schlüssel verschlüsselt werden, können nur mit dem anderen Schlüssel entschlüsselt werden. Bei diesem Verfahren wird ein Schlüssel immer geheim gehalten (_geheimer Schlüssel, private key, secret key_), der andere ist öffentlich (_öffentlicher Schlüssel, public key_). [^3]

**Vorteile**

-   Kein Schlüsselaustausch nötig
-   Authentifizierung von digitalen Signaturen
-   Öffentlicher Schlüssel kann von mehreren Personen verwendet werden

**Nachteile**

-   Langsam
-   Sicherheit basiert auf der Annahme, dass der Algorithmus sicher ist

## Hashing

Hashing ist ein Verfahren, bei dem eine Eingabe in eine Zeichenkette mit einer festen Länge von Buchstaben und Nummern umgewandelt wird. Der daraus resultierende Hashwert ist einzigartig und kann nicht zurück in die ursprüngliche Eingabe umgewandelt werden. [^4]

**Dieses Verfahren hat folgende wichtige Eigenschaften:**

-   Ein unveränderte Nachricht M berechnet immer den selben Wert H, eine veränderte Nachricht ∆M berechnet einen ganz anderen Wert H.
-   Der Aufwand, um aus einer Nachricht M den Wert H zu berechnen, ist sehr gering.
-   Der Aufwand, aus dem Wert H die ursprüngliche Nachricht M zu berechnen, ist äusserst hoch bzw praktisch unmöglich.
-   Die Wahrscheinlichkeit, dass zwei verschiedene Nachrichten M1 und M2 zum gleichen Wert H führen ist äusserst gering (Kollisionswahrscheinlichkeit). Praktisch führen unterschiedliche Nachrichten immer zu unterschiedlichen Hashwerten.
-   Der Hashwert hat immer die gleich Länge (zum Beispiel 256 Bits).

### Anwendungsbeispiel

Passwörter sollten niemals persistent abgespeichert werden, stattdessen wird der Hashwert eines Passwort abgelegt. Bei einer Authentifizierung wird der Hashwert des vom Benutzer eingegeben Passwortes erzeugt und mit dem abgelegten Hashwert in der Datenbank verglichen. [^5]

**Vorteil:** Bei einem Diebstahl von Nutzerdaten (Username und Passwort-Hash) kann aus dem Passwort-Hash nicht auf das Passwort geschlossen werden.

### Salting

Beim Salted Hash wird der Nachricht ein zusätzlicher (zufälliger) String hinzugefügt, dem sogenannten Salt. Damit wird mit extrem hoher Wahrscheinlichkeit sichergestellt, dass gleiche Nachrichten unterschiedliche Hashwerte produzieren. Der Salt muss nicht geheim bleiben, wichtig ist die zufällige Erzeugung. Der für die Erzeugung des Hashes verwendete Salt wird zusammen mit dem Hashwert abgelegt.

Mit der Verwendung von Salted-Hashfunktionen werden vorgefertigte Tabellen unbrauchbar. Die einzige Möglichkeit einen Hashwert zu knacken sind sogenannte Brute-Force oder Dictionary-Angriffe.

## Digitales Zertifikat

Ein digitales Zertifikat ist eine Beglaubigung eines [öffentlichen Schlüssels](#asymmetrische-verschlüsselung).

Ein digitales Zertifikat ist ein elektronischer Ausweis, mit dem man die **vorgegebene Identität überprüfen** kann. Mit einem digitalen Zertifikat kann man prüfen, ob der öffentliche Schlüssel der vorgegebenen Identität gehört. In diese Kategorie gehören auch SSL/TLS-Zertifikate.

Eine Zertifizierungsstelle (certificate authority / CA) ist eine Organisation, die einen öffentlichen Schlüssel mit einer Identität verknüpft und diese Beziehung beglaubigt. Dies geschieht über einen Zertifizierungsantrag (certificate signing request / CSR). Die CA prüft die Identität und stellt dann das Zertifikat aus.

Manchmal wird zwischen Zertifizierungsstellen (certificate authority / CA) und Registrierungsstellen unterschieden. Die Registrierungsstelle (registration authority / RA) ist die Organisation, die eine Identität überprüft und einen Zertifizierungsantrag genehmigt, währende Zertifizierungsstelle auf der Basis eines genehmigten Antrages ein Zertifikat ausstellt. Oft handelt es sich aber um dieselben Organisationen (QuoVaids, Godaddy etc.)

### Chain of Trust - Zertifikatskette

Weltweit gibt es eine Vielzahl von CAs (Certificate Authorities). Im OS oder Browser sind die vertrauenswürdigen CAs hinterlegt.

Vertrauenswürdig heisst in diesem Kontext: Eine anerkannte Organisation, die Identitäten nach vorgegebenen Standards prüft.

Apple-Geräte zum Beispiel vertrauen grundsätzlich allen Zertifikaten, die von diesen CAs ausgestellt worden sind. Diese aufgelisteten CAs nennt man root certificate authorities oder Stammzertifizierungsstellen. In den meisten Fällen wird aber eine Zertifikat nicht von Stammzertifizierungsstellen ausgestellt. Vielmehr gibt es darunter liegende intermediäre CAs, die zur Stammzertifizierungsstelle eine Vertrauensstellung haben. Solche vertrauenswürdige intermediäre CAs können sich über mehrere Hierarchiestufen erstrecken und bilden eine sogenannte chain of trust oder Zertifikatskette. Zertifikatsketten sind im Zertifikat selbst vorhanden und können (zum Beispiel von einem Browser) auf Gültigkeit geprüft werden. Ein Zertifikat gilt als gültig, wenn alle Zertifikate dieser Zertifikatskette gültig sind und das Stammzertifikat von einer Stammzertifizierungsstelle stammt.

Zum Beispiel wurde das TLS-Zertifikat für sbb.ch nicht direkt von der Stammzertifizierungsstelle _SwissSign Gold CA - G2_ ausgestellt, sondern von einer Sub-Zertifizierungsstelle. Diese Zertifikatskette kann angezeigt werden:

### Signaturen

Eine Signatur (oder elektronische Unterschrift) ist ein Zusatz zu einer Nachricht oder Datei. Die Signatur beweist, wer der Erzeuger oder Sender einer Nachricht ist, ebenso kann die Signatur auch beweisen, dass eine Nachricht nicht durch Dritte abgeändert wurde. Die Signatur ist ein zentrales Element, um die Integrität einer Nachricht zu gewährleisten.

## JTW

Ein JWT besteht aus drei Abschnitten: einem Header, einer Nutzlast und einer Signatur. Jeder Abschnitt ist eine Base64-kodierte Zeichenfolge, und die Abschnitte werden durch Punkte getrennt. Ein typisches JWT sieht wie folgt aus, wobei die X's für den Header, die Y's für die Payload und die Z's für die Signatur stehen: [^6]

```txt
xxxxxx.yyyyyy.zzzzzz
```

Ein explizit geschriebenes JWT würde etwa so aussehen:

```txt
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkphbmUgRG9lIiwiaWF0IjoxNjk3MjM5MDIyfQ.5CerSPBCrO_3WdiyPjR7HoWBOeXsuq2AcfplJeG7erc
```

JWT ist ein offener Standard (RFC 7519) für die sichere Übertragung von Informationen zwischen Parteien als JSON-Objekt. Diese Informationen können überprüft und vertrauenswürdig sein, da sie digital signiert sind.

-   **Struktur**: Ein JWT besteht aus drei Teilen: Header, Payload und Signature, die durch Punkte getrennt sind (`header.payload.signature`).
-   **Header**: Typ der Token und das verwendete Signaturalgorithmus.
-   **Payload**: Enthält die Claims (z.B. Benutzerinformationen, Berechtigungen).
-   **Signature**: Wird mit einem geheimen Schlüssel oder einem RSA-Schlüsselpaar erstellt.

### Header

Der Header enthält Informationen über das gesamte JWT, wie z. B. den Hauptalgorithmus (`alg`), der für die Signierung und Verschlüsselung (required) verwendet wird, den Medientyp des JWT (`typ`) und seinen Inhaltstyp (`cty`). Ein entschlüsselter JWT-Header könnte wie folgt aussehen:

```json
{
	"alg": "HS256",
	"typ": "JWT"
}
```

### Payload

The payload consists of all of the data that’s being transmitted. This data is optional, and it is added as claims. There are three primary types of claims: registered claims, private claims, and public claims.

### Registered claims

Dabei handelt es sich um optionale, aber vorab festgelegte Ansprüche, die in der JWT-Spezifikation definiert sind und die Interoperabilität unterstützen. Es gibt sieben Arten von registrierten Claims:

-   Issuer (`iss`): Die Partei, die das JWT ausgestellt hat.
-   Subject (`sub`): Das Subjekt des JWT oder die Entität, über die dieses JWT Informationen enthält.
-   Audience (`aud`): Der Empfänger des JWT.
-   Expiration time (`exp`): Der Zeitpunkt, zu dem das JWT abläuft.
-   Not before(`nbf`): Der Zeitpunkt, vor dem das JWT ungültig ist.
-   Issued at (`iat`): Der Zeitpunkt, zu dem das JWT ausgestellt wurde.
-   JTW ID (`jti`): Eine Zeichenfolge, die als eindeutiger Bezeichner für dieses JWT dient.

### Was sind die Anwendungsfälle von JWT?

JWT wird häufig zur Verwaltung der Benutzerauthentifizierung und -autorisierung in Webanwendungen verwendet. Wenn sich ein Benutzer bei einer Anwendung anmeldet, stellt der Server ein JWT aus und sendet es an den Client zurück. Dieses JWT kann grundlegende Informationen über den Benutzer sowie die Rollen und Berechtigungen des Benutzers enthalten. Das JWT wird dann auf der Client-Seite gespeichert und bei nachfolgenden Anfragen zur Überprüfung mitgesendet. Dies ist eine zustandslose Form der Authentifizierung und Autorisierung, da der Server den Sitzungsstatus nicht für jeden Benutzer aufrechterhalten muss.

JWT wird auch für den sicheren Austausch von Daten zwischen Anwendungen und Microservices verwendet. Die in einem JWT übertragenen Daten können verschlüsselt werden, um zu verhindern, dass Dritte sie lesen, und sie können signiert werden, um ihre Authentizität zu beweisen. Dies macht es zu einem sehr effizienten Mechanismus für den sicheren Austausch von Daten bei gleichzeitiger Wahrung des Vertrauens.

[^1]: Quelle: https://docs.google.com/document/d/1aptwCFt1HZGehDyfdj1347u6_0mUR0poIwFWCBIUIK4/edit#heading=h.2ki0wrufwysh
[^2]: Quelle: https://studyflix.de/informatik/symmetrische-verschlusselung-1610
[^3]: Quelle: https://studyflix.de/informatik/asymmetrische-verschlusselung-1609
[^4]: Quelle: https://www.codecademy.com/resources/blog/what-is-hashing/
[^5]: Quelle: https://github.com/21r8390/m214
[^6]: Quelle: https://blog.postman.com/what-is-jwt/
