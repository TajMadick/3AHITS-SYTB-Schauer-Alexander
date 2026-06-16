# Arbeitsbericht

- Datum: 2.6.2026
- Thema: [Schleifen](https://www.franzmatejka.at/htl/doc/SYTB_3/24_schleifen_ue.html)
- Name: Alexander Schauer
- Klasse: 3AHITS
- Fach: SYTB

# Übersicht

- Erklärung Schleifen
- Übung (Even/Odd)
- Übung (Summe und Maximum)
- Übung (Min)
- Übung (Durchschnitt)

# Erklärung Schleifen

Beispiel Programm:

```bash
#!/usr/bin/env bash
 
# while
counter=1
while ((counter<=10)) # <= 10
do
    echo $counter 
    ((counter++))
done
 
 
# for
 
# Liste = durch white spaces getrennter string
 
data="1 2 3 4 5 6 7"
for i in $data
do
    echo $d
done
 
echo "---Kommandozeilenargumente---"
for arg in $@
do  
    echo $arg
done
 
for value in {20..25}
do
    echo $value
done
 
mylist="hallo welt, hello world, guten tag; hi hao"
IFS=",;" # internal field seperator
for el in $mylist
do
    echo $el
done
```

# Übung (Even/Odd)

### Angabe:

Create a simple script which will print the numbers 1–42 (each on a separate line) and whether they are even or odd.

### Lösung:

```bash
#!/usr/bin/env bash
for v in {1..42}
do
        if ((v%2 == 0))
        then
                echo "Even: $v"
        else
                echo "Odd: $v"
        fi
done
```

### Erklärung:

- mit ```{1..42}``` legt man die range fest
- beim if wird ein arithmetischer Test verwendet

### Output:

```
Odd: 1
Even: 2
Odd: 3
Even: 4
Odd: 5
Even: 6
Odd: 7
Even: 8
Odd: 9
Even: 10
Odd: 11
Even: 12
Odd: 13
Even: 14
Odd: 15
Even: 16
Odd: 17
Even: 18
Odd: 19
Even: 20
Odd: 21
Even: 22
Odd: 23
Even: 24
Odd: 25
Even: 26
Odd: 27
Even: 28
Odd: 29
Even: 30
Odd: 31
Even: 32
Odd: 33
Even: 34
Odd: 35
Even: 36
Odd: 37
Even: 38
Odd: 39
Even: 40
Odd: 41
Even: 42
```

# Übung (Summe und Maximum)

### Angabe:

Schreibe ein bash Skript das eine beliebige Menge von positiven Zahlen als Argumente aus der Kommandozeile übernimmt. Es soll die Summe und die größte Zahl ausgegeben werden. Hinweis: Verwende ```#@```.

### Lösung:

```bash
#!/usr/bin/env bash
max=0
sum=0
for el in $@
do
        if ((el > max))
        then
                max=$el
        fi
        ((sum+=el))
done

echo "Sum: $sum"
echo "Max: $max"
```

### Erklärung:

- es wird durch alle CLI Argumente durchgegangen in der Schleife
- es wird geprüft ob ein Element größer wie max ist und zur Summe dazugezählt

### Output:

```
┌──(kali㉿kali)-[~/SYTB/260616]
└─$ ./sumMax.sh 9 0 11 100 6 -15
Sum: 111
Max: 100
```

# Übung (Min)

### Angabe:

Schreibe ein bash Skript das den Namen einer Datei als Argument akzeptiert:

```
$ ./min.sh input.txt
```

Die Input Datei enthält positive Zahlen die durch white spaces getrennt sind:

```
42
21 57
68 33 1
1
```


Das Skript soll die kleinste Zahl ermitteln und ausgeben.

Hinweis:

Der größte mögliche Wert in bash scripting ist 64 Bit signed

```
$ ((MAXINT=2**63-1))
$ echo $MAXINT
9223372036854775807
```

### Lösung:

```bash
#!/usr/bin/env bash
myList=$(cat $1)
min=$((2**63-1))
for el in $myList
do
        if ((el < min))
        then
                min=$el
        fi
done

echo $min
```

### Erklärung:

- die Schleife geht durch alle Elemente der Datei durch
- Prüft ob das Element kleiner ist
- Gibt das Kleinste aus

### Output:

```
┌──(kali㉿kali)-[~/SYTB/260616]
└─$ ./min.sh input.txt
1
```