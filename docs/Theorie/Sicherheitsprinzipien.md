---
tags:
    - Theorie
---

# Grundlegende Sicherheitsprinzipien

Die grundlegenden Sicherheitsprinzipien sind in vier Kategorien unterteilt, welche die Sicherheit von Informationen gewährleisten sollen. [^1]

| Kategorie             | Prinzipien                                          |
| --------------------- | --------------------------------------------------- |
| Vertraulichkeit       | Information vor unberechtigten Dritten verschlossen |
| Integrität            | Information nicht durch Dritte abgeändert           |
| Verfügbarkeit         | Information bleibt verfügbar                        |
| Nicht-Abstreitbarkeit | Information kann nicht abgestritten werden          |

## Vertraulichkeit (confidentiality)

Sicherstellung, dass eine Information vor unberechtigten Dritten **verschlossen** bleibt.

## Integrität (integrity)

Sicherstellung, dass eine Information authentisch bleibt. Dazu gehört, dass kein falsche Identität vorgetäuscht werden kann, dass keine Information durch unberechtigte Dritte (unbemerkt) **abgeändert** werden kann.

## Verfügbarkeit (availability)

Sicherstellung, dass eine Information **verfügbar** bleibt.

## Nicht-Abstreitbarkeit / Unleugbarkeit (non-repudiation)

Sicherstellung, dass das Versenden oder der Empfang einer Information **nicht abgestreitet** werden kann. Dies ist von Bedeutung bei Informationen, die Teil einer vertraglichen Transaktion sind (zum Beispiel Versenden einer Bestellung oder der Empfang einer Rechnung).

## Information Disclosure

Die Offenlegung von Informationen, auch bekannt als Informationsleck, liegt vor, wenn eine Website unbeabsichtigt sensible Informationen an ihre Nutzer weitergibt. Je nach Kontext können Websites alle Arten von Informationen an einen potenziellen Angreifer weitergeben, darunter: [^2]

-   Daten über andere Nutzer, wie z. B. Benutzernamen oder finanzielle Informationen
-   Sensible kommerzielle oder geschäftliche Daten
-   Technische Details über die Website und ihre Infrastruktur

Die Gefahren, die mit der Weitergabe sensibler Benutzer- oder Geschäftsdaten verbunden sind, liegen auf der Hand, aber die Offenlegung technischer Informationen kann manchmal ebenso schwerwiegend sein. Auch wenn einige dieser Informationen nur von begrenztem Nutzen sind, können sie ein Ausgangspunkt für die Aufdeckung einer zusätzlichen Angriffsfläche sein, die weitere interessante Schwachstellen enthalten kann. Das Wissen, das Sie sammeln können, könnte sogar das fehlende Puzzlestück liefern, wenn Sie versuchen, komplexe, hochgradig gefährliche Angriffe zu konstruieren.

Gelegentlich kann es vorkommen, dass sensible Informationen unvorsichtigerweise an Benutzer weitergegeben werden, die ganz normal auf der Website surfen. In den meisten Fällen muss ein Angreifer jedoch die Offenlegung von Informationen durch unerwartete oder böswillige Interaktion mit der Website herbeiführen. Er wird dann die Antworten der Website sorgfältig studieren, um ein interessantes Verhalten zu erkennen.

### Beispiele für die Offenlegung von Informationen

Nachfolgend einige grundlegende Beispiele für die Offenlegung von Informationen:

-   Offenlegung der Namen von versteckten Verzeichnissen, ihrer Struktur und ihres Inhalts über eine robots.txt-Datei oder eine Verzeichnisliste
-   Zugang zu Quellcodedateien über temporäre Backups gewähren
-   Explizite Nennung von Datenbanktabellen oder Spaltennamen in Fehlermeldungen
-   Unnötige Offenlegung hochsensibler Informationen, wie z. B. Kreditkartendaten
-   Festcodierung von API-Schlüsseln, IP-Adressen, Datenbankanmeldeinformationen usw. im Quellcode
-   Andeutungen über das Vorhandensein oder Fehlen von Ressourcen, Benutzernamen usw. durch subtile Unterschiede im Anwendungsverhalten

[^1]: Quelle: https://docs.google.com/document/d/160llHSFAyvL57Q0sbU5uby6Ng3A7288zjm2EbemgH3o/edit#heading=h.jcfs1mt5gphx
[^2]: Quelle: https://portswigger.net/web-security/information-disclosure
