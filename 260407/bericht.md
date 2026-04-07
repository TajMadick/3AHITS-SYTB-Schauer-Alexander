# Arbeitsbericht

- Datum: 7.4.2026
- Thema: [Shell Scripts - Command Line Arguments und Loops](https://www.franzmatejka.at/htl/doc/SYTB_3/05_scripts_ue.html)
- Name: Alexander Schauer
- Klasse: 3AHITS
- Fach: SYTB

# Übersicht

- Erklärung Shell Script Command Line Arguments
- Übung (Directory Struktur)
- Übung (Skript Generator)
- Übung (Headline Cat)
- Übung (RANDOM)

# Erklärung Shell Script

### Command Line Arguments

wenn man nach dem Script-Namen auch noch Argumente schreibt: ```./script.sh abc cdf``` sind das Command Line Arguments.  
Man kann auf sie im Script mit spezielen Varibalen zugreifen: 
- ```$0``` für den Script-Name: ```./script.sh```
- ```$1``` für das erste Argument ```abc```
- ```$2``` für das Zweite ```cdf``` und so weiter

mit ```$@``` bekommt man alle Argumente ab ```$1```  
damit kann man zum Beispiel ein Schleife machen:

```bash
for arg in "$@"
do
    echo "$arg"
done
```

hier zu beachten ist doppelte Hochkomma ```"``` statt einfachen ```'``` herzunehmen da sonst der Variablen-Name nicht greift.

### Beispiel

```bash
# test.sh
for arg in "$@"
do
        echo "$arg"
done

echo "Script: $0"
echo "First Argument: $1"
```

### Output

```
┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ./test.sh abc def ghi jkl mno pqr stu vwx yz
abc
def
ghi
jkl
mno
pqr
stu
vwx
yz
Script: ./test.sh
First Argument: abc
```

# Übung (Directory Struktur)

### Angabe:
Schreibe ein Shell-Script das Unterverzeichnisse und Dateien anlegt, es wird ein Argument an das Script übergeben.

Aufruf: ./build_dirs.sh abcd

Dies führt zu folgender Directorystruktur:

```
./
└── abcd/
    ├── abcd_01/
    │   ├── abcd.01.1.txt
    │   ├── abcd.01.2.txt
    │   └── abcd.01.3.txt
    └── abcd_02/
        ├── abcd.02.1.txt
        ├── abcd.02.2.txt
        └── abcd.02.3.txt
```

Schreibe weiters ein Shell-Script clean_dir.sh das diese Verzeichnisstruktur wieder löscht.

Hinweis: Das Kommando tree kann verwendet werden um eine Directory Struktur in obiger Form darzustellen.

### Lösung:

```bash
#build_dirs.sh

#!/bin/bash

#wichtig da sonst nicht mit bash ausgeführ wird und schleife nicht funktionieren wuerde

mkdir "$1"
for i in {01..02}
do
        mkdir "$1/${1}_${i}"
        for j in {1..3}
        do
                touch "$1/${1}_${i}/${1}.${i}.${j}.txt"
        done
done

tree
```

### Output:

```
┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ./build_dirs.sh abcd
.
├── abcd
│   ├── abcd_01
│   │   ├── abcd.01.1.txt
│   │   ├── abcd.01.2.txt
│   │   └── abcd.01.3.txt
│   └── abcd_02
│       ├── abcd.02.1.txt
│       ├── abcd.02.2.txt
│       └── abcd.02.3.txt
├── build_dirs.sh
└── test.sh
```

### Erklärung

- 2 verschachtelte Schleifen für die Unterordner  
- Schleifen in Bash mit ```{1..3}``` für ranges  
- ganz wichtig oben ```#!/bin/bash``` sonst gehen diese Range-based for loops nicht

# Übung (Skript Generator)

### Angabe:

Schreibe ein Skript das

eine Skriptdatei erzeugt (Name wird als Argument übergeben),
die She-Bang Zeile einfügt,
einen echo Befehl einfügt und
das eXecution Flag für das Skript setzt.
Anwendung:

```
$ ./makescript.sh mytest
```

erzeugt die Datei mytest.sh :

```bash
#!/bin/env sh

echo "mytest Skript"

# write yor script here
```

Das erzeugte Skript kann sofort ausgeführt werden:

```
$ ./mytest.sh
```

### Lösung

```bash
echo "#!/bin/env sh\n\necho $1\" Script\"\n\n#write your script here" > "${1}.sh"

chmod +x mytest.sh
```

### Ausgabe

```
┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ./makescript.sh mytest
              
┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ./mytest.sh           
mytest Script

┌──(kali㉿kali)-[~/SYTB/260407]
└─$ cat mytest.sh        
#!/bin/env sh

echo mytest" Script"

#write your script here
```

# Übung (Headline Cat)

### Angabe: 
Verwende $@ zur Lösung dieser Aufgabenstellung.

Schreibe ein Skript das eine Art cat zur Verfügung stellt. Als Argumente werden eine beliebige Anzahl von Textdateien übergeben. Das Ergebnis (der Inhalt aller dieser Dateien) wird in die Datei result.txt (fixer Dateiname) geschrieben (ist die Datei vorhanden soll deren Inhalt überschrieben werden). Jedem Datei-Inhalt soll eine Überschrift vorangestellt werden.

Beispiel – der Aufruf

```
$ ./headline_cat.sh file1.txt file2.txt file3.txt
```

ergibt die Datei result.txt mit folgendem Inhalt:

```
== file1.txt ==========================================
Das ist der Inhalt
der ersten Textdatei

== file2.txt ==========================================
Das ist der Inhalt
der zweiten Textdatei

== file3.txt ==========================================
Das ist der Inhalt
der dritten Textdatei
```

### Lösung:

```bash
 > result.txt
for arg in "$@"
do
        echo "== $arg" >> result.txt
        echo "==========================================" >> result.txt
        echo "Das ist der Inhalt" >> result.txt
        echo "der ersten Textdatei\n" >> result.txt
done
```

### Erklärung

- ```> result.txt``` macht das File komplett leer
- wenn man ```>>``` bei ```echo``` hernimmt fügt es an das File an und macht automatisch Zeilenumbruch

### Ausgabe:

```
┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ./headline_cat.sh file1.txt file2.txt file3.txt
   
┌──(kali㉿kali)-[~/SYTB/260407]
└─$ cat result.txt                                 
== file1.txt
==========================================
Das ist der Inhalt
der ersten Textdatei

== file2.txt
==========================================
Das ist der Inhalt
der ersten Textdatei

== file3.txt
==========================================
Das ist der Inhalt
der ersten Textdatei
```

# Übung (RANDOM)

### Angabe:

Schreibe ein shellscript das eine beliebige Menge von Dateinamen als Parameter akzeptiert. Von jeder dieser Dateien soll eine Kopie im gleichen Verzeichnis angelegt werden. Die Kopie unterscheidet sich vom Original durch eine angefügte Zufallszahl, Beispiel:

```
test.txt --> test.txt.38573
```

Aufrufbeispiele:

```
$ ./randcp.sh test1.txt test2.txt
$ ./randcp.sh xyz1.md test3.txt abcd.dat
$ ./randcp.sh *.md
```

Hinweis: ```$RANDOM``` liefert bei jeder Verwendung eine zufällige Zahl.
Achtung: ```#!/bin/bash``` in der she-bang Zeile verwenden. ```sh``` unterstützt (in REPL) keine Zufallszahlen.

### Lösung

```bash
#!/bin/bash

for arg in "$@"
do
        cp "$arg" "${arg}.${RANDOM}" 
done
```

### Ausgabe

```
┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ls            
abcd  build_dirs.sh  headline_cat.sh  makescript.sh  mytest.sh  randcp.sh  result.txt  test.sh

┌──(kali㉿kali)-[~/SYTB/260407]
└─$ touch test1.txt test2.txt          

┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ls
abcd  build_dirs.sh  headline_cat.sh  makescript.sh  mytest.sh  randcp.sh  result.txt  test1.txt  test2.txt  test.sh

┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ./randcp.sh test1.txt test2.txt

┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ls
abcd  build_dirs.sh  headline_cat.sh  makescript.sh  mytest.sh  randcp.sh  result.txt  test1.txt  test1.txt.25488  test2.txt  test2.txt.27989  test.sh

┌──(kali㉿kali)-[~/SYTB/260407]
└─$ touch xyz1.md test3.txt abcd.dat 
  
┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ./randcp.sh xyz1.md test3.txt abcd.dat

┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ls
abcd      abcd.dat.17118  headline_cat.sh  mytest.sh  result.txt  test1.txt.25488  test2.txt.27989  test3.txt.3754  xyz1.md
abcd.dat  build_dirs.sh   makescript.sh    randcp.sh  test1.txt   test2.txt        test3.txt        test.sh         xyz1.md.10504

┌──(kali㉿kali)-[~/SYTB/260407]
└─$ touch one.md two.md three.md          
      
┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ./randcp.sh *.md            

┌──(kali㉿kali)-[~/SYTB/260407]
└─$ ls
abcd            build_dirs.sh    mytest.sh    randcp.sh   test1.txt.25488  test3.txt       three.md       two.md.16385   xyz1.md.15247
abcd.dat        headline_cat.sh  one.md       result.txt  test2.txt        test3.txt.3754  three.md.5725  xyz1.md
abcd.dat.17118  makescript.sh    one.md.4650  test1.txt   test2.txt.27989  test.sh         two.md         xyz1.md.10504
```