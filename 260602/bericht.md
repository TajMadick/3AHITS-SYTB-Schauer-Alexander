# Arbeitsbericht

- Datum: 2.6.2026
- Thema: [Regex](https://www.franzmatejka.at/htl/doc/SYTB_3/20_regex_ue.html)
- Name: Alexander Schauer
- Klasse: 3AHITS
- Fach: SYTB

# Übersicht

- Erklärung Regex
- Übung (Subdir Count)
- Übung (REs)
- Übung (sed)
- Übung (Datum)
- Übung (Logfile)

# Erklärung Regex

- Regex wird hergenommen nach gewissen Regeln nach Ausdrücken zu suchen oder Ausdrücke zu prüfen
- Ein Beispiel: wenn man einen nummerischen Ausdruck will sagt man [0-9]+ was so viel heißt wie: 1-unendlich Ziffern
- Erklärung verschiedener Regex Ausdrücke:
- ```.``` steht für einen Beliebigen Charakter
- genauso kann man zB. schreiben: ```a``` und dann muss ein ```a``` drinnen vorkommen
- mit ```*``` kann man sagen den vorgehenden Charakter 0-unendlich mal
- mit ```+``` kann man den vorhergehenden Charakter 1-unendlich mal
- ```\d``` steht für 0-9 und ```\w``` steht für A-Z, a-z und 0-9
- man kann mit [A-Za-z0-9] das gleiche bewirken wie mit ```\w``` also man kann die Ranges selber festlegen
- mit [^0-9] kann man alle Charaktere von 0-9 ausschließen
- wenn man Charaktere escapen will schreibt man ```\``` davor wie bei zB. ```\*```
- mit ```?``` nach dem Zeichen ist das Zeichen entweder 0 oder 1 mal
- Man kann auch conditionals machen also wenns entweder eins oder zwei sein soll schreibt man ```(eins|zwei)```
- Mit ```()``` kann man Syntaktische Gruppen bilden also wenn man schreib: ```(a?b+)``` kann man mit ```\1```  die erste Syntaktische Gruppe sehen
- damit man diese Sachen hernehmen kann muss man bei ```sed``` und ```grep``` ```-E``` schreiben da viele der Sachen Expanded Regex Expressions sind

# Übung (Subdir Count)