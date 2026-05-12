# Arbeitsbericht

- Datum: 12.5.2026
- Thema: [Download mit automatisierter Hash/Checksum Überprüfung](https://www.franzmatejka.at/htl/doc/SYTB_3/17_if_putty_ue.html)
- Name: Alexander Schauer
- Klasse: 3AHITS
- Fach: SYTB

# Übersicht

- Übung (Secure Download)

# Übung (Maximum)

### Angabe:

PuTTY ist als SSH Client für Windows sehr beliebt. Genauso beliebt ist aber auch einen Trojaner in einem PuTTY Download zu verstecken. Um das zu verhindern werden Downloads gerne mit einem Hashwert (in diesem Zusammenhang auch **Checksum** genannt) abgesichert.

- Schreibe ein Script das einen Download der ```64-bit x86``` Variante von ```putty.zip``` durchführt. [Webseite von PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

![alt text](image1.png)

- Gleichzeitig soll die Datei mit den SHA-512 checksums geladen werden. Diese sind ganz am Ende der Seite. Die passende Zeile im File ```sha512sums``` ist mit ```w64/putty.zip``` am Ende gekennzeichnet.

![alt text](image2.png)

Im Script soll automatisiert geprüft werden ob die Checksum (=SHA-512 Hash) des geladenen Files mit der Checksum aus dem Checksumfile übereinstimmt. Also zum Beispiel eine Ausgabe kommen: ```HASH OK```.

- Das Script erwartet lediglich ```putty.zip``` im gleichen Directory
- Das checksum file soll das Script live von der PuTTY Seite laden und im ```/tmp``` Directory ablegen. Das Script erzeugt dafür mit ```mktemp``` ein Unterverzeichnis. Alle Zwischenergebnisse sollen ebenfalls in diesem temp directory abgelegt werden.

Eine Liste aller u.U. brauchbarer Tools:

- ```curl -O``` – zum Download
- ```grep``` – um die passende Zeile aus dem Checksum-File zu filtern
- ```cut``` – um den SHA-512 aus der Zeile zu extrahieren
- ```openssl``` – um den SHA-512 Hash von putty.zip zu rechnen
- ```xxd``` – ist nicht für das Script notwendig sondern fürs debugging der Zwischenergebnisse
- ```tr``` – ```tr -d [:space:]``` entfernt evtl. enthalten Leerzeichen und Zeilenumbrüche
- ```cmp``` – zum Vergleich der Hashwerte
- ```if``` – das Ergebnis von cmp auswerten


### Lösung:

### Erklärung

### Output:
