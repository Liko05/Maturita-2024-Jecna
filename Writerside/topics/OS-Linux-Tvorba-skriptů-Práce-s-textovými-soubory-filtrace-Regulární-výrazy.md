# OS Linux - Tvorba skriptů. Práce s textovými soubory, filtrace, Regulární výrazy.

![pipes.png](pipes.png)

## Tvorba scriptu

Bash script je serie prikazu napsana v souboru. Ty jsou nasledne provadeny bashem. Program bezi radek po radce.
Vyuzivame jej casto kdyz si chceme ulehcit praci s nejakou opakujici se operaci.
Bash je primo v command line.

- `#!/bin/bash`: it used bash as a interpreter (you can use all commands that you are using in bash)
- `#!/bin/sh`: it used to execute the file using sh, which is a Bourne shell or a compatible shell
- `#!/bin/csh`: It is used to execute the file using csh, the C shell, or a compatible shell.
- `#!/usr/bin/perl -T`: It is used to execute using Perl with the option for taint checks.
- `#!/usr/bin/php`: It is used to execute the file using PHP command-line interpreter.
- `#!/usr/bin/python -O`: It is used to execute Python with optimizations to code.
- `#!/usr/bin/ruby`: It is used to execute using Ruby.
  Na zacatek skriptu je potreba definovat interpretera daneho kodu. Nejcasteji pokud budeme psat script. #! ... se
  nazyva shabang a pouziva se uplne na zacatku skriptu

### Promenne

```Bash
#!/bin/bash
# A simple variable example
greeting=Hello
name=Tux
echo $greeting $name
```

### Input

```Bash
#!/bin/bash
echo "Enter a number"
read a
echo "enter a number"
read b
var=$((a+b))
echo $var
```

### Conditions

```Bash
read x
read y
if [$x -gt $y]
then
echo "X is greater than Y"
elif [$x -lt $y]
then
echo "X is less than Y"
elif [$x -eq $y]
then
echo "X is equal to Y"
fi
```

### Loops

```Bash
for i in {1..5}
do
echo $i
done

i=1
while [[ $i -le 10]] ; do
echo "$i"
(( i+= 1 ))
done
```

## Prace s textovymi soubory

mkdir, rmdir pro praci se slozkami

### Vytvoreni

- `touch [filename]`
- `nano [filename]`
- `cat > [filename]`
- `vi [filename]`

### Ostatni

- Smazani: `rm [filename]`
- Kopirovani: `cp [source file/dir] [destination file/dir]`
- Presun: `mv [source file/dir] [destination file/dir]`
- Najit: `find [path to search] -name [file/dir]`
- Zobrazeni obsahu:
    - `cat [filename]` all the content of the file
    - `head [filename]` first 10 lines
    - `tail [filename]` last 10 lines

### Presmerovani

![presmerovani.png](presmerovani.png)

- (0) stdin (standard input) device is the keyboard .. <
- (1) stdout (standard output) device is the screen .. >
- (2) stderr (standard error)

#### 1. Overwrite

- ">" - standard input
- "<" - standard output

#### 2. Appends

- ">>" - standard output
- "<<" - standard output

#### 3. Merge

- "p>&q" - merge output from stream p with stream q
- "p>&q" - merge input from stream p with stream q

![redirecting.png](redirecting.png)

## Pipe

Pipe redirektuje vystup jednoho prikazu do vstupu jineho. Pipes muzeme retezit do nekonecna

- Grep .. patern a expresion vyhledavajici komand
- Sort .. seradi radky
    - `-d` dictionary order sort
    - `-n` arithmetic/numeric order
    - `-r` reverse order
    - `-b` ignore leading blanks
    - `-m` Merge (not sort)
- Unique .. pokud se prvky opakuji vybere je jen jednou
    - `-c`: count = it tells how many times a line was repeated by displaying a number as a prefix with the line.
    - `-u`: unique = It allows you to print only unique lines.
    - `-i`: ignore case = By default, comparisons done are case sensitive but with this option case insensitive
      comparisons can be made.
- Tr ... maze nebo prepisuje charaktery v souboru
    - `-d` Deletes each character from standard input that is contained in the string specified by String1
    - `tr '{}' '()' <textfile> newfile`
- More .. zobrazi content s paging control
- Less .. zobrazeni kde je mozne scrolovat
- Nl .. line numbering
- Wc .. number of lines, word count, byt and characters count

```Bash
cat /etc/group | egrep -i "[0-9]+:.+" | sort | nl
cat /etc/group | nl | egrep -i "[0-9]+:.+" | sort -d -r
```

## Grep

`grep -i (ignore case sensitive) -E 'regex' [file]`
`egrep -i 'regex' [file]`
`egrep == grep -E (extended)`

Muzeme spusit process na pozadi za pomoci ampersantu .. gedit &

![cheat-sheet-regex.png](cheat-sheet-regex.png)