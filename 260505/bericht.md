# Arbeitsbericht

- Datum: 5.5.2026
- Thema: [if statement](https://www.franzmatejka.at/htl/doc/SYTB_3/15_if_ue.html)
- Name: Alexander Schauer
- Klasse: 3AHITS
- Fach: SYTB

# Übersicht

- Erklärung if statement
- Übung (Maximum)
- Übung (Un-/Gerade)
- Übung (Directory)
- Übung (number lines script)
- Übung (Stundenplan V2)


# Erklärung if statement

https://www.franzmatejka.at/htl/doc/SYTB_3/14_if.html

### Zusammenfassung

Struktur:

```bash
if [ $1 -gt 100 ]
then
  echo "Hey that's a large number."
  pwd
fi
```

- keyword if gefolgt auf einen Boolian Wert zB: ```test``` bzw eckige Klammern oder mit Shell Arithmetik:

```bash
if (( x > y )) 
then
  echo "x > y"
fi
```

- auszuführener Code startet bei ```then``` und endet bei ```fi```
- geht auch mit ```else``` -> dann muss ```else``` zwischen ```then``` und ```fi```

```bash
if [ -n "$3" ]
then
  echo "Parameter #3 is $3"
else
  echo "Parameter #3 fehlt"
fi
```

- man kann auch logische Operationen machen zB mit UND oder ODER:

```bash
if [ -r $1 ] && [ -s $1 ]
then
    # wenn beide stimmen
fi
```

```bash
if [ $USER = 'bob' ] || [ $USER = 'andy' ]
then
    # wenn eines der Beiden stimmt
fi
```


# Übung (Maximum)

### Angabe:

Schreibe ein bash Skript das 2 Zahlen als Argumente aus der Kommandozeile übernimmt. Die größere der beiden Zahlen soll ausgegeben werden.

### Lösung:

```bash
#!/bin/bash

if (( $1 > $2 ))
then
        echo $1
fi

if (( $2 > $1 ))
then
        echo $2
fi
```

### Erklärung:

- da Shell Arithmetik nur mit Bash geht muss man oben ```#!/bin/bash``` schreiben

### Output:

```
┌──(kali㉿kali)-[~/SYTB/260505]
└─$ ./maximum.sh 100000000 1000
100000000
                                   
┌──(kali㉿kali)-[~/SYTB/260505]
└─$ ./maximum.sh 10 1000       
1000
           
┌──(kali㉿kali)-[~/SYTB/260505]
└─$ ./maximum.sh 10 10  
```

# Übung (Un-/Gerade)

### Angabe:

Schreibe ein Script das von einer als Argument übergebenen Zahl prüft ob sie gerade oder ungerade ist.

### Lösung:

```
#!/bin/bash

if (( $1 % 2 == 0)) 
then
        echo "gerade"
else
        echo "ungerade"
fi
```

### Erklärung:

- in der Bash Arithmetik wird erst die Zahl durch 2 und wenn der Rest 0 ist ist die Zahl gerade
- ansonsten Ungerade

### Output:

```
┌──(kali㉿kali)-[~/SYTB/260505]
└─$ ./gerUng.sh 2 
gerade
                           
┌──(kali㉿kali)-[~/SYTB/260505]
└─$ ./gerUng.sh 1 
ungerade
```

# Übung (Directory)

### Angabe:

Schreibe ein Skript ```makedir.sh``` das mit einem Argument aufgerufen wird.

```$ ./makedir.sh xyz```

Ein Directory mit dem Namen ```xyz``` soll angelegt werden falls es nicht existiert. Im Directory lege eine Datei mit dem Namen ```xyz.txt``` und Inhalt ```xyz``` an.

Existiert das Directory bereits so soll gefragt werden ob das Directory gelöscht werden darf. Bei dieser Abfrage soll angegeben werden wie viele Files sich im Directory befinden.

```Soll das Directory "xyz" (mit 5 Files) gelöscht werden? [j|n]:```

- Auswahl ```j```: Das Directory wird gelöscht und wieder wie oben angelegt.
- Auswahl ```n```: Das Skript wird beendet.


### Lösung:

```bash
#!/bin/bash

DIR=$1

if [ -d $DIR ]
then
        NumberFiles=$(ls $DIR | wc -l)
        echo "Soll das Directory \"xyz\" (mit $NumberFiles Files) gelöscht werden? [j|n]: "
        read answer
        if [ $answer = "j" ] || [ $answer = "J" ]
        then
                rm -rf $DIR
                mkdir $DIR
                echo $DIR > $DIR/$DIR.txt
        fi
else
        mkdir $DIR
        echo $DIR > $DIR/$DIR.txt
fi
```

### Erklärung:

- im ersten if wird geprüft ob das übergebene Dir existiert
- wenn ja wird mit ```ls``` und ```wc``` geschaut wie viele Elemnte es hat (die ```-l``` Option von ```wc``` zählt die Zeilen)
- mit ```read``` wird die user antwort in der Variable ```answer``` gespeichert
- wenn die Antwort ja ist wird das alte Dir gelöscht und das neue mit dem Inhalt erstellt
- sollte das Dir nicht exisitieren wird ein Dir mit Inhalt erstellt

### Output:

```
┌──(kali㉿kali)-[~/SYTB/260505]
└─$ ls    
1  2  gerUng.sh  makedir.sh  maximum.sh  zahl1  zahl2

┌──(kali㉿kali)-[~/SYTB/260505]
└─$ ./makedir.sh xyz

┌──(kali㉿kali)-[~/SYTB/260505]
└─$ ls             
1  2  gerUng.sh  makedir.sh  maximum.sh  xyz  zahl1  zahl2

┌──(kali㉿kali)-[~/SYTB/260505]
└─$ touch xyz/abc.txt

┌──(kali㉿kali)-[~/SYTB/260505]
└─$ ./makedir.sh xyz 
Soll das Directory "xyz" (mit 2 Files) gelöscht werden? [j|n]: 
j

┌──(kali㉿kali)-[~/SYTB/260505]
└─$ ls xyz           
xyz.txt
```

# Übung (number lines script)

### Angabe:

Schreibe ein Skript ```number.sh``` das von der Kommandozeile aus aufgerufen werden kann.

Angenommen es gibt die Datei ```test.txt``` mit Inhalt:

```
bbb eins
ccc zwei
aaa drei
```

Grundsätzlich kann das Skript mit einer Datei als **Argument** ausgeführt werden:

```
$ ./number test.txt
$ cat test.txt
```

```
1 bbb eins
2 ccc zwei
3 aaa drei
```

Es werden die einzelnen Zeilen **nummeriert** (dafür kann das Tool ```nl``` verwendet werden). Achtung: das Skript soll die Datei verändern nicht ausgeben.

Sollte die Datei nicht exisitieren, nicht lesbar sein oder leer sein soll ein entsprechender **Fehlertext** ausgegeben werden.

Es soll weiters auch möglich sein dem Tool Daten über **stdin** zu übergeben (wenn keine Datei angegeben wurde):

```
$ sort test.txt | ./number.sh
```

```
1 aaa drei
2 bbb eins
3 ccc zwei
```

Hinweis: ```/dev/stdin``` kann in der Kommandozeile wie ein Dateiname verwendet werden und liefert die Daten von stdin.

Die Verwendung der Option ```-?``` soll dann noch zur Ausgabe eines Hilfetexts führen:

```
number.sh: number lines of input
usage: number.sh [FILE]
FILE ... path to readable file of nonzero length
if FILE is omitted data is read from standard input
```

Hinweis: der Befehl ```exit``` beendet sofort die Skriptabarbeitung.

### Lösung:

```
if [ "$1" = "-?" ]
then
        echo "number.sh: number lines of input"
        echo "usage: number.sh [FILE]"
        echo "FILE ... path to readable file of nonzero length"
        echo "if FILE is omitted data is read from standard input"
        exit
fi

if [ -t 0 ]
then
        echo "Keine Datei angegeben"
        exit
else
        nl /dev/stdin
fi


if [ ! -e $1 ] || [ ! -r $1 ] || [ ! -s $1 ]
then

else
        tmpfile=$(mktemp)
        nl $1 > $tmpfile
        mv $tmpfile $1
fi

```

### Erklärung:

### Output:

# Übung (Stundenplan V2)

### Angabe:

### Lösung:

### Erklärung:

### Output:

