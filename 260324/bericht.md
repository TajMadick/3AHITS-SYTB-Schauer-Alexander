# Arbeitsbericht

- Datum: 24.3.2026
- Thema: [Variablen und Shell Scripts](https://www.franzmatejka.at/htl/doc/SYTB_3/02_variablen_ue.html)
- Name: Alexander Schauer
- Klasse: 3AHITS
- Fach: SYTB

# Übersicht

- Erklärung Shell Script
- Übung (Variablen)
- Übung (Begrüßung)
- Übung (Zeilenumbruch)
- Übung (admin)
- Übung (log file names)
- Übung (backup)
- Quellen

# Erklärung Shell Script

### Beispiel Script:
```
# !/bin/env bash
 
# Hallo Welt
 
# Shell Script = Textdatei mit shell Befehlen
# Befehle ergeben das gleiche Ergebnis wie wenn in der shell ausgeführt

echo Guten Morgen
ABC=abc
echo $ABC
 
FILE_NAME=test.txt
DIR_NAME=mydir
mkdir $DIR_NAME
echo "Irgendein Text" > $DIR_NAME/$FILE_NAME
 
# double quotes
NAME=ELIA
TEXT="Hallo $NAME"
echo $TEXT
 
#single quotes
TEXT2='Hallo $NAME'
echo $TEXT2
 
# curly braces {}
 
FILE=myname
echo "$FILE_001.txt"
echo "$FILE_002.txt"
 
echo "${FILE}_001.txt"
echo "${FILE}_002.txt"
```

### Erklärung einzelner Befehle
- ```# !/bin/env bash``` definiert die Standardshell mit der das Programm ausgeführt werden soll
- ```# Hallo Welt``` wenn ein ```#``` davorsteht ist es ein Kommentar
- ```echo Guten Morgen``` Ausgabe von Text mit echo
- ```ABC=abc``` so kann man Variablen anlegen. Normalerweise schreibt man Variablen Namen in Großbuchstaben und bei dem Leerzeichen darf kein Abstand sein
- ```echo $ABC``` mit $VARIABLEN_NAME kann man auf den Inhalt einer Variable zugreifen
- Beispiel: hier werden zwei Variablen angelegt: ein Ordner Name und ein File Name dann wird der Ordner erstellt und ein File mit dem Inhalt Irgendein Text wird in dem Ordner erstellt
```
FILE_NAME=test.txt
DIR_NAME=mydir
mkdir $DIR_NAME
echo "Irgendein Text" > $DIR_NAME/$FILE_NAME
```
- Wenn man einen Text in Double Quotes hat ```TEXT="Hallo $NAME"``` wird der Inhalt der Variable $NAME hergenommen
- Wenn man einen Text in Single Quotes hat ```TEXT2='Hallo $NAME'``` steht im Output auch $NAME wenn man das auch mit Double Quotes ereichen will kann man ```TEXT="Hallo \$NAME"``` schreiben
- um der Bash zu sagen was genau der Variablenname ist kann man den Variablennamen in Curly Braces einwickeln: ```echo "${FILE}_001.txt"```

### Vor ausführen:
- Datei mit chmod ausführbar machen und mit ls -l schauen ob bei der Datei die x gesetzt sind  

```
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ chmod 755 hello2.sh

┌──(kali㉿kali)-[~/SYTB/260324]
└─$ ls -l 
total 12
-rwxr-xr-x 1 kali kali  435 Mar 24 08:27 hello.sh
```

### Output:
- ./ vor Dateinamen weil Linux nach Scripts im sogenannten Path schaut und damit sagt man Linux das er nach dem Dateinamen im aktuellen Directory schauen soll
- man kann auch sh hello.sh schreiben  

```              
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ ./hello.sh        
Welt
Guten Morgen
Hallo Aleksander
Hallo $NAME
.txt
.txt
myname_001.txt
myname_002.txt
```

## Übung (Variablen)
### Angabe
Löse diese Aufgabe ohne ein shell-script zu schreiben.

Lege 2 Variablen für Directories an, eine Variable für den Filenamen und eine Variable für die Dateiendung (Extension).

Verwende nur die Variablen anstatt der Directory und Filenamen um folgendes zu lösen:

Erzeuge die Directories (das zweite befindet sich in dem ersten).
Lege in dem zweiten Directory eine Text-Datei mit Inhalt an, verwende Filenamen und Extension (getrennt mit .).
Gib den Inhalt der Datei (unter Verwendung der Variablen) aus.

### Lösung

```
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ DATEINAME=testdatei            
                                   
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ ENDUNG=.txt     
                                   
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ DIR1=dir1          
                                   
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ DIR2=dir2
                                   
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ mkdir $DIR1 
                                   
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ mkdir $DIR2
                                   
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ echo "abc" > ./$DIR2/${DATEINAME}${ENDUNG}

┌──(kali㉿kali)-[~/SYTB/260324]
└─$ cat $DIR2/${DATEINAME}${ENDUNG}
abc
```

## Übung (Begrüßung)
### Angabe
Schreibe ein Shell-Script mit dem Namen begruessung.sh, dieses soll:

den Benutzer nach seinem Namen fragen
den Namen einlesen und in einer Variable speichern
danach ausgeben:  
Hallo NAME  
Schön, dass du da bist.

Starte das Script auf alle besprochene Arten.

Hinweis: Verwende den read Befehl – recherchiere wie dieser zu verwenden ist.

### Lösung

```
begruessung.sh:

read NAME
echo Hallo $NAME
echo Schön, dass du da bist.

┌──(kali㉿kali)-[~/SYTB/260324]
└─$ chmod 755 begruessung.sh      

┌──(kali㉿kali)-[~/SYTB/260324]
└─$ ./begruessung.sh
Elia
Hallo Elia
Schön, dass du da bist.
```

## Übung (Zeilenumbruch)
### Angabe
Erzeuge eine Variable MSG, die mit echo $MSG folgende Ausgabe erzeugt:

Name: Dein Name  
Klasse: 3AHITS  
Raum: ...  

Vorgaben/Hinweise:

Es darf nur eine Variable verwendet werden.
Der Zeilenumbruch muss in der Variablen mit \n definiert sein.

### Lösung

```
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ MSG="Name: Alexander Schauer\nKlasse: 3AHITS\nRaum: ..."
                          
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ echo $MSG                                 
Name: Alexander Schauer
Klasse: 3AHITS
Raum: ...
```

## Übung (admin)
### Angabe
Gegeben ist:

USER="admin"

Gib folgende Strings mit echo korrekt aus:  
admin_backup  
admin_2026  
Erkläre, warum folgende Zeile nicht das gewünschte Ergebnis liefert:  
echo "$USER_backup"

Warum geht echo ```"$USER_backup"``` nicht? Weil Bash denkt die Variable heißt USER_backup

### Lösung
```
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ USER="admin"

┌──(kali㉿kali)-[~/SYTB/260324]
└─$ echo "${USER}_backup"                     
admin_backup
                          
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ echo "${USER}_2026"  
admin_2026
```

## Übung (log file names)
### Angabe
Gegeben ist:

DIR="/var/log/"

Erzeuge mit echo folgende Ausgaben unter Verwendung der Variabelen DIR:

- /var/log/nginx  
- /var/log/apache

### Lösung

```
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ DIR="/var/log/"

┌──(kali㉿kali)-[~/SYTB/260324]
└─$ echo "${DIR}nginx"
/var/log/nginx
                             
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ echo "${DIR}apache"
/var/log/apache
```

## Übung (backup)
### Angabe
Gegeben ist:

BASE="backup"  
DATE="2026-01-16"

Erzeuge folgende Dateinamen mit echo:

backup_2026-01-16.tar  
backup_2026-01-16.tar.gz

### Lösung
```
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ BASE="backup"      
                                   
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ DATE="2026-01-16"
                                   
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ echo "${BASE}_${DATE}.tar"
backup_2026-01-16.tar
                        
┌──(kali㉿kali)-[~/SYTB/260324]
└─$ echo "${BASE}_${DATE}.tar.gz"
backup_2026-01-16.tar.gz
```

## Quellen
- https://www.howtoforge.de/anleitung/der-linux-read-command/
- https://ryanstutorials.net/bash-scripting-tutorial/bash-variables.php