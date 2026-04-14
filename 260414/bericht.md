# Arbeitsbericht

- Datum: 7.4.2026
- Thema: [Command substitution](https://www.franzmatejka.at/htl/doc/SYTB_3/07_cmdsubst_ue.html)
- Name: Alexander Schauer
- Klasse: 3AHITS
- Fach: SYTB

# Übersicht

- Erklärung Command Substitution
- Übung (Anzahl Einträge in einem Verzeichnis)
- Übung (Tage bis zum Ball)
- Übung (Zufälliger Satz)
- Übung (dated copy V1)
- Übung (dated copy V2)
- Übung (dated copy V3)

# Erklärung Command Substitution

https://www.franzmatejka.at/htl/doc/SYTB_3/06_cmdsubst.html

### Zusammenfassung

- mit ```$(befehl)``` kann man den Output dieses Befehls als Variablen Wert verwenden
- Rechenoperationen sind auch möglich hierfür braucht man jedech doppelte Klammern: ```$((3+5))```. Außerdem muss man in Rechenoperationen vor Variablen kein ```$``` schreiben: ```$((Var1*10))```
- Bei Command Substitution ist es möglich ```"``` zu verschachteln, siehe Beispiel unten.


### Beispiele der Doc

Datum bekommt man mit dem Befehl ```date```.

```bash
$ echo "Das aktuelle Datum ist $(date)"
$ echo "Heute $(date -I) in einer Woche ist $(date --date='+1 week' -I)"
```

```-I``` steht für das ISO Format.

```bash
WEEKS=10
DATE2=$(date --date="+$WEEKS week" -I)
echo "Heute $(date -I) in $WEEKS Wochen ist der $DATE2"
```

Hier ist ein ```"``` innerhalb eines ```"``` möglich (Verschachtelt)

```bash
echo "Heute $(date -I) in $WEEKS Wochen ist der $(date --date="+$WEEKS week" -I)"
```

Erstellt ein temporäres File

```bash
TEMP=$(mktemp).txt
echo "Erstelle ein temporäres File $TEMP"
echo "lorem ipsum dolor sit amet" >$TEMP
```

Berechnungen Beispiel

```bash
# Berechnungen
X=99999
Y=88888
Z=$(( X - Y ))
echo $Z
```

# Übung (Anzahl Einträge in einem Verzeichnis)

### Angabe:
Schreibe ein shellscript das als Argument einen Pfad auf ein Verzeichnis erhält. Das Script soll die Anzahl der Einträge in diesem Verzeichnis als Zahl ausgeben. Dies soll aus der ls Ausgabe mit wc ermittelt werden.

```
$ ./nbrentries.sh ~/test
Es sind 12 Einträge im dir ~/test
```

Hinweis – Vergleiche die Ausgaben von

```
ls
ls | cat
echo "$(ls)"
```

Dokumentiere den Unterschied, was ist die Logik dahinter.

### Lösung:

```bash
echo "Es sind $(ls $1 | wc -w) Einträge im dir $1"
```

### Erklärung:

- ```$1``` ist das erste Command Line Argument
- In der Command Substitution wird das ls von den ersten Argument in ```wc```
- ```wc -w``` zählt die Wörter und gibt die Anzahl zurück 

### Output:

```
┌──(kali㉿kali)-[~/SYTB/260414]
└─$ ./nbrentries.sh . 
Es sind 1 Einträge im dir .
                                   
┌──(kali㉿kali)-[~/SYTB/260414]
└─$ ./nbrentries.sh ..
Es sind 4 Einträge im dir ..
                                   
┌──(kali㉿kali)-[~/SYTB/260414]
└─$ ls .              
nbrentries.sh

┌──(kali㉿kali)-[~/SYTB/260414]
└─$ ls ..             
260324  260407  260414  3AHITS-SYTB-Schauer-Alexander
```

# Übung (Tage bis zum Ball)

### Angabe:
Schreibe ein Shell-Skript das die Anzahl der Tage bis zum HTL Ball ermittelt. Die Ausgabe soll in der folgenden Form sein.

```
Es sind noch 42 Tage bis zum HTL Ball (2027-01-16)
```

Hinweise:

Verwende das ```date``` Format für ```seconds since the Epoch (1970-01-01 00:00 UTC)```


### Lösung:

```bash
htlBallDate="2027-01-16"

currentDateSec=$(date +%s)
htlBallDateSec=$(date +%s --date=$htlBallDate)

diff=$((htlBallDateSec - currentDateSec))

echo "Es sind noch $((diff/86400)) Tage bis zum HTL Ball ($htlBallDate)"
```

### Erklärung:

- ```date +%s``` gibt aktuelles Datum in Sekunden zurück
- mit ```--date``` kann man das Datum zu einem gewünschten Datum setzen
- dann rechnet man sich die Differenz mit ```$((...))``` aus Wichtig bei ```=``` keine Leerzeichen
- Zum Schluss rechnet man die Sekunden durch 86400 (die Anzahl der Sekunden in einem Tag)

### Output:

```
┌──(kali㉿kali)-[~/SYTB/260414]
└─$ ./htlBall.sh
Es sind noch 276 Tage bis zum HTL Ball (2027-01-16)
```

# Übung (Zufälliger Satz)

### Angabe:
### Lösung:
### Erklärung:
### Output:

The test command (written as [ here) has a "not" logical operator, ! (exclamation mark):

if [ ! -f /tmp/foo.txt ]; then
    echo "File not found!"
fi

if ! test -f wortliste1000.txt; then
   wget "https://www.franzmatejka.at/htl/doc/SYTB_3/testdata/wortliste1000.txt"
fi

lines=$(wc -l wortliste1000.txt)

echo $lines


### Angabe:
### Lösung:
### Erklärung:
### Output:

### Angabe:
### Lösung:
### Erklärung:
### Output: