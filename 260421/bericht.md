# Arbeitsbericht

- Datum: 21.4.2026
- Thema: [Arithmetik](https://www.franzmatejka.at/htl/doc/SYTB_3/10_arithmetic_ue.html)
- Name: Alexander Schauer
- Klasse: 3AHITS
- Fach: SYTB

# Übersicht

- Erklärung Arithmetik
- Übung (Multiplizierer)
- Übung (Werkstatt Summe)
- Übung (Zeitmessung)
- Übung (Random Number)


# Erklärung Arithmetik

https://www.franzmatejka.at/htl/doc/SYTB_3/09_arithmetic.html

### Zusammenfassung

- Möglichkeiten für Berechnungen in Bash: ```let```, ```expr``` und bash Doppelklammer-Arithmetik

#### ```let```

Wichtig keine Leerzeichen erlaubt!

```bash
let a=5+4
let b=100-$a
```

geht auch mit Quotes

```bash
let "a = 5 + 4"
```

#### ```expr```

- ```expr``` gibt das Ergebnis sofort aus anstelle es in einer Variable zu speicher

```bash
expr 5 + 4
```

oder mit Command Substitution

```bash
echo $(expr 5 + 4)
```

#### Doppelklammer-Arithmetik

- am meisten genutzte Methode 
- man kann zwischen Zeichen Leerzeichen machen im gegensatz zu ```let``` 
- bekannte C Operationen wie ```+ - ++ -- * / % **``` sind möglich

#### Beispiel

```bash
b=$(( a + 3 ))
echo $b # 11
```

```bash
echo "Es sind $(( a + 5)) Wochen"
```

geht auch ohne return indem man das $ weglässt

```bash
((a=2*a)) 
((a++))
((a=a+4))
```

# Übung (Multiplizierer)

### Angabe:

Erstelle ein Skript das 2 Zahlen als Kommandozeilenargumente übernimmt. Multipliziere diese Zahlen und gib das Ergebnis aus, verwende jede der 3 besprochenen Methoden.

### Lösung:

```bash
#!/bin/bash

let erg=$1*$2

echo $erg

# * muss mit \ escaped werden, da es von expr als Wildcard interpretiert wird
echo $(expr $1 \* $2)

echo $(($1*$2))
```

### Erklärung:

- mit let wird in eigene Variable gespeichert (keine Leerzeichen)
- bei expr muss man ```*``` mit ``` \*``` escapen sonst gehts nicht
- ```#!/bin/bash``` ganz oben sonst gehts nicht

### Output:

```
┌──(kali㉿kali)-[~/SYTB/260421]
└─$ ./multiplier.sh 3 9
27
27
27
```

# Übung (Werkstatt Summe)

### Angabe:

Schreibe ein shell Script dass die Summe aller Beträge in klassenkassa.csv mit dem Text Werkstatt in ermittelt.

Anleitung:

- Verwende ```grep``` und ```cut``` zum filtern.
- Die Beträge stehen nun auf einzelnen Zeilen. Verwende ```paste``` um diese zu einer Zeile zusammenzufassen – mit ```paste``` kann ein Ausdruck der Form ```15+13+42+23``` erstellt werden.
- Verwende command substitution um den Berechnungs-Ausdruck in einer Variable zu speichern
- Verwende bash Arithmetik ```$(( expr ))``` um das Ergebnis auszurechnen

### Lösung:

```bash
if ! test -f klassenkassa.csv; then
   wget "https://www.franzmatejka.at/htl/doc/SYTB_3/testdata/klassenkassa.csv"
fi

rechnung=$(cat klassenkassa.csv | grep Werkstatt | cut -d, -f3 | paste -s -d '+')

echo "$rechnung" | bc
```

### Erklärung:

- das if prüft ob klassenkassa.csv schon heruntergeladen ist sonst lädt er es herunter mit wget
- der Inhalt von klassenkassa.csv wird in grep gepipped
- grep sucht nach dem Wort Werkstatt 
- cut teilt bei dem Zeichen ```,``` und ```-f3``` sorgt dafür, dass die 3. Spalte verwendet wird
- ```paste -s``` fügt horizontal zusammen und ```-d '+'``` fügt ```+``` dazwischen ein
- zum Schluss muss man den Inhalt der Variable in ```bc``` Pipen da Bash nicht mit Floating Point Numbers rechnen kann 

### Output:

```
┌──(kali㉿kali)-[~/SYTB/260421]
└─$ ./werkstattSumme.sh   
411.09
```

# Übung (Zeitmessung)

### Angabe:

Schreibe 2 Skripts: ```time_start.sh``` und ```time_stop.sh```. Bei Aufruf von ```time_stop.sh``` wird die Anzahl der Sekunden ausgegeben die seit dem letzten Aufruf von ```time_start.sh``` vergangen sind.

- Hinweis 1: verwende ```date``` um die Anzahl der Sekunden seit 01.01.1970 herauszufinden (die UNIX Zeit bezieht sich immer auf diesen Referenzpunkt).

- Hinweis 2: Speichere die Zeit in ```time_start.sh``` in einer, mit ```mktemp``` erzeugten, temporären Datei.

```
┌──(kali㉿kali)-[~/SYTB/260421]
└─$ cat time_stop.sh
oldTime=$(cat uhrzeit.*)
newTime=$(date +%s%N)
echo $((newTime-oldTime))

rm -rf uhrzeit.*

┌──(kali㉿kali)-[~/SYTB/260421]
└─$ cat time_start.sh 
mktemp uhrzeit.XXXXX
date +%s%N > uhrzeit.txt
```

### Lösung:

### Erklärung:

### Output:

# Übung (Random Number)

### Angabe:

```$RANDOM``` erzeugt Zahlen zwischen 0 und 32767. Das ist nicht immer hilfreich. Schreibe ein Skript random.sh wo über 2 Grenzen (Argumente des Skripts) der gewünschte Wertebereich vorgegeben werden kann. Zum Beispiel generiert ```./random.sh 10 45``` eine zufällige Zahl im Bereich von 10 bis 45 (jeweils inklusive).

### Lösung:

### Erklärung:

### Output:
