---
tags:
    - Theorie
---

# OpenSSL

[Konsole](https://www.cryptool.org/en/cto/openssl/)
[Zusammenfassung](https://docs.google.com/document/d/1Yfb73i1p9VX0_3EsxnjohPKpb73Bvi7wYucgtmInYr8/edit#heading=h.m0mwp3rswb8o)

OpenSSL ist eine leistungsstarke Open-Source-Implementierung von SSL (Secure Sockets Layer) und TLS (Transport Layer Security) Protokollen. Es enthält eine Vielzahl von Werkzeugen zum Erzeugen und Verwalten von Schlüsseln und Zertifikaten. [^1]

#### Befehle zur Schlüssel- und Zertifikatserzeugung:

-   **Private Key generieren**: `openssl genpkey -algorithm RSA -out private_key.pem -aes256`
-   **Öffentlichen Schlüssel extrahieren**: `openssl rsa -pubout -in private_key.pem -out public_key.pem`
-   **Zertifikatsignierungsanforderung (CSR) erstellen**: `openssl req -new -key private_key.pem -out request.csr`
-   **Selbstsigniertes Zertifikat erstellen**: `openssl req -x509 -key private_key.pem -in request.csr -out certificate.pem -days 365`

??? info "Weitere Befehle für OpenSSL"

    **Schlüsselgenerierung**

    ```sh title="Generieren eines RSA-Privatschlüssels:"
    openssl genpkey -algorithm RSA -out private_key.pem -aes256
    ```

    -   `-aes256`: Verschlüsselt den privaten Schlüssel mit AES-256.

    ```sh title="Generieren eines RSA-Privatschlüssels mit spezifischer Schlüssellänge:"
    openssl genpkey -algorithm RSA -out private_key.pem -pkeyopt rsa_keygen_bits:4096
    ```

    -   `-pkeyopt rsa_keygen_bits:4096`: Setzt die Schlüssellänge auf 4096 Bits.

    ---

    **Zertifikate**

    ```sh title="Erstellen einer Zertifikatsignierungsanforderung (CSR):"
    openssl req -new -key private_key.pem -out request.csr
    ```

    ```sh title="Erstellen eines selbstsignierten Zertifikats:"
    openssl req -x509 -key private_key.pem -in request.csr -out certificate.pem -days 365
    ```

    ---

    **Verschlüsselung und Entschlüsselung**

    ```sh title="Verschlüsseln einer Datei:"
    openssl enc -aes-256-cbc -salt -in plaintext.txt -out encrypted.txt
    ```

    ```sh title="Entschlüsseln einer Datei:"
    openssl enc -aes-256-cbc -d -in encrypted.txt -out decrypted.txt
    ```

    ---

    **Hashing**

    ```sh title="Berechnen des SHA256-Hashes einer Datei:"
    openssl dgst -sha256 file.txt
    ```

    ---

    **OpenSSL-Befehlsoptionen**

    Hier sind einige allgemeine Optionen, die häufig verwendet werden:

    -   `-in`: Gibt die Eingabedatei an.
    -   `-out`: Gibt die Ausgabedatei an.
    -   `-aes256`, `-aes-128-cbc`, `-des3`: Gibt den Verschlüsselungsalgorithmus an.
    -   `-salt`: Fügt Salz zu einer Verschlüsselung hinzu, um die Sicherheit zu erhöhen.
    -   `-d`: Dekodiert oder entschlüsselt Daten.

### Primzahlen

Primzahlen sind natürliche Zahlen größer als 1, die nur durch 1 und sich selbst teilbar sind. Sie spielen eine zentrale Rolle in der Kryptographie, insbesondere bei der Generierung von Schlüsselpaaren für Algorithmen wie RSA.

#### Befehle zur Primzahlgenerierung mit OpenSSL:

-   **Primzahl generieren**: `openssl prime -generate -bits 2048`
    -   Dieser Befehl erzeugt eine 2048-Bit-Primzahl.
-   **Testen, ob eine Zahl prim ist**: `openssl prime -hex 0xD3A8D3B1`
    -   Dieser Befehl überprüft, ob die angegebene hexadezimale Zahl eine Primzahl ist.

??? info "Weitere Befehle für Primzahlen"

    **Generieren von Primzahlen**

    ```sh title="Generiere eine Primzahl mit einer bestimmten Länge in Bits:"
    openssl prime -generate -bits 2048
    ```

    ```sh title="Generiere eine Primzahl mit zusätzlichen Optionen:"
    openssl prime -generate -bits 2048 -hex -safe
    ```

    - `hex`: Gibt die Primzahl im hexadezimalen Format aus.
    - `safe`: Generiert eine "sichere" Primzahl, d.h. 𝑝 p ist prim und ( 𝑝 − 1 ) / 2 (p−1)/2 ist ebenfalls prim.

    ---

    **Testen von Zahlen auf Primzahl-Eigenschaft**

    ```sh title="Testen, ob eine Zahl prim ist:"
    openssl prime 1234567891
    ```

    ```sh title="Testen einer hexadezimalen Zahl:"
    openssl prime -hex 0xD3A8D3B1
    ```

## RSA-Verschlüsselung

RSA das verbreitetste asymmetrische Verschlüsselungsverfahren (public-key cryptography). Es bildet die Grundlage für die Gewährleistung der Vertraulichkeit und Integrität von digitalen Daten. Die Entwicklung geht zurück in die 70er-Jahre auf die drei Mathematiker Ronald **R** ivest, Adi **S** hamir und Leonard **A** dleman.[^2]

RSA bildet zusammen mit ECC (elliptic-curve cryptography) die beiden wichtigsten [asymmetrischen Verschlüsselungsverfahren](Verschluesselung.md#asymmetrische-verschlüsselung).

RSA (Rivest-Shamir-Adleman) ist ein asymmetrisches Kryptosystem, das weit verbreitet für sichere Datenübertragung eingesetzt wird. Es basiert auf der mathematischen Schwierigkeit, große Primzahlen zu faktorisieren.

-   **Schlüsselgenerierung**: Zwei große Primzahlen (`p`) und (`q`) werden gewählt. Das Produkt (`n = p * q`) bildet den Modul. Der öffentliche Schlüssel besteht aus (`n`) und einem Exponenten (`e`) (_typischerweise 65537_), während der private Schlüssel aus (`n`) und einem Exponenten (`d`) besteht, der die Umkehrung von (`e`) modulo (`(p-1)*(q-1)`) ist.
-   **Verschlüsselung**: Eine Nachricht (`m`) wird mit dem öffentlichen Schlüssel verschlüsselt: `c = m^e mod n`.
-   **Entschlüsselung**: Der verschlüsselte Text (`c`) wird mit dem privaten Schlüssel entschlüsselt: `m = c^d mod n`.

### Kongruenz - Bedeutung

Zwei natürliche Zahlen a und b sind zueinander kongruent, wenn diese bei der Division durch eine natürliche Zahl N den gleichen Rest (remainder) liefern. Man sagt dann "a und b sind kongruent modulo n" oder "a und b sind kongruent nach dem Modulus n". Die formale Schreibweise dazu:

```txt
a = b (mod n) oder a =n b
```

### Kongruenz in RSA

Kongruenz mit der dahinterliegenden Zahlentheorie ist der grundlegende Baustein des RSA-Verfahrens.
Nachrichten werden normalerweise als Strings angesehen, die ver- und entschlüsselt werden. Jeder String ist aber letztendlich eine Folge von Bits, eine solche Folge von Bits kann aber ebenso gut als Integer bzw, natürliche Zahl interpretiert werden. Es besteht also prinzipiell eine eineindeutige (sogenannte bijektive) Beziehung zwischen einem String und einem Integer. RSA wendet ausschliesslich Integer-Operationen an. Eine Nachricht wird in RSA als Integer/natürliche Zahl repräsentiert.

| Symbol | Bedeutung                                                                                                                |
| ------ | ------------------------------------------------------------------------------------------------------------------------ |
| m      | unverschlüsselter Wert                                                                                                   |
| c      | verschlüsselter Wert                                                                                                     |
| n      | Modulus. Entspricht zusammen mit e den öffentlichen Schlüssel.                                                           |
| e      | Exponent für Verschlüsselung (encrypt). Entspricht (zusammen mit dem Modulus n) dem öffentlichen Schlüssel (public key). |
| d      | Exponent für Entschlüsselung (decrypt). Entspricht dem privaten Schlüssel (private key).                                 |

### Wahl von n, e und d

Für die Wahl von n, e und d gibt es zahlentheoretische Grundlagen, die auf das 17. und 18. Jahrhundert zurückgehen, zum Beispiel

-   [ Kleiner fermatsche Satz](https://de.wikipedia.org/wiki/Kleiner_fermatscher_Satz)
-   [Satz von Euler](https://de.wikipedia.org/wiki/Satz_von_Euler) (Verallgemeinerung des kleinen fermatschen Satzes)

#### n (Modulus)

Im Unterschied zum obigen Beispiel sind die effektiv verwendeten Zahlen um Dimensionen grösser. Der Modulus n hat in RSA typischerweise eine Länge von 2048 oder gar 4096 Bits. Diese entspricht einer natürlichen Zahlen mit etwa 600 bis 1200 Stellen.
Der gewählte Modulus n hat eine fundamentale Eigenschaft, die RSA letztendlich eine hohe Sicherheit verleiht: n ist das Produkt zweier sehr grossen Primzahlen (bis zu einige hundert Stellen lang) p und q

```txt
n = p * q
```

#### e (public key)

e (bildet zusammen mit n den public key) wird prinzipiell auch aus n abgeleitet. Heutzutage wird meistens der universelle Wert 65637 gewählt.

#### d (private key)

d (private key) wird aus e sowie p und q abgeleitet. Vor allem aber: Es gibt bis heute keine Algorithmen, die den Modulus n in vernünftiger Zeit in die beiden Primfaktoren p und q zerlegen könnten. Dies ist aber Voraussetzung, um diesen geheimen Schlüssel berechnen zu können. p und q werden nur bei der Erzeugung von n und d benötigt, danach werden diese beiden Primzahlen nicht mehr gebraucht und weggeworfen. Das macht die Stärke des RSA-Verfahrens aus.

Die Primfaktorzerlegung als "pièce de résistance" des Verfahrens steht im Kontrast zur Tatsache, dass eine grosse Zahl äusserst effizient auf prim getestet werden kann. Grosse Primzahlen können mit den heutigen Algorithmen einfach gefunden werden, was letztendlich die Grundlage zur Verbreitung von RSA beitrug.

| Operationen mit sehr grossen natürlichen Zahlen | Laufzeit     |
| ----------------------------------------------- | ------------ |
| Test auf Primzahl                               | schnell      |
| Finden einer Primzahl                           | schnell      |
| Division, Berechnung Restbetrag (mod)           | schnell      |
| Multiplikation, Potenzen                        | schnell      |
| Primfaktorzerlegung                             | sehr langsam |

[^2]: Weitere Informationen: https://www.golinuxcloud.com/openssl-cheatsheet/
[^1]: Quelle: https://docs.google.com/document/d/143kpSF6D4UGF13yX7ubqC5HKnQnFIb2sBTf7_x4V3Uo/edit
